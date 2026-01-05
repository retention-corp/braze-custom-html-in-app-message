# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## PROJECT PURPOSE

Build **self-contained HTML in-app message templates** for Braze mobile campaigns. Each file is a complete, standalone HTML document uploaded directly to Braze's Custom Code message editor.

**Core Constraint**: Everything (HTML, CSS, JS) in one file. No external dependencies except CDN libraries and image URLs.

## CRITICAL: Braze Bridge API Migration

⚠️ **EXISTING TEMPLATES USE DEPRECATED API** ⚠️

Current templates use `appboyBridge` (deprecated). **ALL NEW CODE** must use `brazeBridge` with proper event listener:

```javascript
// ❌ WRONG (deprecated, current templates use this)
if (window.appboyBridge) {
    appboyBridge.logClick();
    appboyBridge.closeMessage();
}

// ✅ CORRECT (required for new templates)
window.addEventListener("ab.BridgeReady", function() {
    brazeBridge.logClick();
    brazeBridge.closeMessage();
}, false);
```

**When modifying existing templates**: Ask user whether to migrate to `brazeBridge` or keep `appboyBridge` for consistency.

## Essential Braze Bridge Methods

**Message Control:**
- `brazeBridge.closeMessage()` - Dismiss message
- `brazeBridge.requestImmediateDataFlush()` - Send analytics immediately

**Analytics:**
- `brazeBridge.logClick(button_id)` - Track clicks (alphanumeric + spaces/dashes/underscores ONLY)
- `brazeBridge.logCustomEvent(name, properties)` - Custom events
- `brazeBridge.logPurchase(productId, price, currency, quantity, properties)` - Track purchases

**User Attributes:**
- `brazeBridge.getUser().setCustomUserAttribute(key, value, merge)` - Set custom attribute
- `brazeBridge.getUser().setEmail(email)` - Update email
- `brazeBridge.getUser().addToCustomAttributeArray(key, value)` - Add to array attribute

**Push Permissions:**
- `brazeBridge.requestPushPermission(successCallback, deniedCallback)` - Request push (cross-platform)

**Full API**: https://www.braze.com/docs/user_guide/message_building_by_channel/in-app_messages/traditional/customize/html_in-app_messages

## File Structure Pattern

```
iam-[placement]_[type].md
├── <head>
│   ├── <meta viewport="...viewport-fit=cover">  ← Required for iOS safe area
│   ├── <link> CDN libraries (Swiper, etc.)
│   └── <style> All CSS inline
└── <body>
    ├── HTML markup
    └── <script>
        ├── Data (hardcoded OR Liquid variables)
        ├── ab.BridgeReady event listener
        ├── Braze Bridge interactions
        └── Component initialization
```

## Mobile Safe Area Handling (CRITICAL)

iOS devices with notches/home indicators require safe area compensation:

```css
/* Bottom-positioned elements */
.footer {
    padding-bottom: calc(20px + env(safe-area-inset-bottom, 20px));
}
```

```javascript
// Android fallback (env() support varies)
if (/Android/i.test(navigator.userAgent)) {
    document.querySelector(".footer").style.paddingBottom = "56px";
}
```

**Viewport meta tag required:**
```html
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
```

## Braze-Specific Constraints

| Constraint | Detail |
|------------|--------|
| **File size** | <100 KB (Braze rejects larger files) |
| **CSS** | Must be inline in `<style>` tags (no `<link rel="stylesheet">`) |
| **Images** | External URLs only (GCS, S3, CDN) |
| **API calls** | Client-side only, no server requests |
| **Liquid in JS** | **CANNOT** use Liquid in `brazeBridge` method calls |
| **Button IDs** | Alphanumeric, spaces, dashes, underscores ONLY (no accents: ö, â, ê) |

## Common Development Patterns

### Data Injection

**Hardcoded (static campaigns):**
```javascript
var data = [
    {"img": "https://...", "link": "athlerab://product/123"},
    {"img": "https://...", "link": "athlerab://product/456"}
];
```

**Liquid (dynamic campaigns):**
```javascript
var data = {{custom_attribute.${product_carousel}}};
```

⚠️ Liquid renders server-side before JS execution. Output must be valid JSON.

### Deep Link Click Tracking

```javascript
element.onclick = function() {
    window.addEventListener("ab.BridgeReady", function() {
        brazeBridge.logClick();
        window.location.href = deeplink_url;
    }, false);
};
```

**Supported schemas**: `athlerab://`, `https://`, `intent://`

### "Don't Show Today" Suppression

```javascript
function suppressToday() {
    try {
        localStorage.setItem("suppress_key", new Date().toDateString());
    } catch(e) {}
    brazeBridge.closeMessage();
}
```

Check suppression before showing message.

## File Size Optimization

Templates must stay under 100 KB. Use these techniques:

1. **Minify variable names**: `data` → `D`, `closeMessage` → `c`
2. **Remove whitespace**: Minify CSS/JS before deployment
3. **Use CDN libraries**: Don't inline Swiper.js, load from CDN
4. **Compress images externally**: Host optimized images on GCS/CDN
5. **Remove comments**: Delete all comments before deployment

**Current template example**: `iam-bottom_sheet_carousel.md` uses single-letter function names (`c()`, `k()`) to save bytes.

## Template Files Format

Each template exists in **two file formats** for different workflows:

| Format | Extension | Purpose | How to Use |
|--------|-----------|---------|------------|
| **Markdown** | `.md` | GitHub preview, code editing | Open in IDE/text editor for editing |
| **HTML** | `.html` | Direct browser preview | Double-click to open in Chrome for visual testing |

**Example:**
- `iam-slide_up_v5.md` - Edit this file
- `iam-slide_up_v5.html` - Click to preview in browser

Both files contain **identical HTML code**. The `.md` files are for code readability and GitHub display, while `.html` files allow instant visual testing without any setup.

## Testing Workflow

**Quick Visual Testing (Recommended):**
1. **Double-click any `.html` file** to open in Chrome
2. Chrome DevTools → Toggle Device Toolbar (Cmd+Shift+M / Ctrl+Shift+M)
3. Select mobile device viewport (e.g., iPhone 12 Pro, Galaxy S21)
4. Simulate Braze Bridge in Console:
   ```javascript
   window.dispatchEvent(new Event("ab.BridgeReady"));
   window.brazeBridge = {
       logClick: (id) => console.log("Click:", id),
       closeMessage: () => console.log("Closed")
   };
   ```

**Code Editing:**
1. Open corresponding `.md` file in IDE
2. Make changes
3. Save changes to both `.md` and `.html` files (keep them in sync)
4. Refresh browser to see updates

**Braze Dashboard testing:**
1. Messaging → In-App Messages → Create Campaign
2. Custom Code → Paste HTML from either file
3. Preview → Select platform/device
4. Test → Send to your device

**Pre-deployment checklist:**
- [ ] Using `brazeBridge` with `ab.BridgeReady` listener (new templates)
- [ ] All CSS inline (no external stylesheets)
- [ ] Image URLs absolute (no relative paths)
- [ ] Safe area padding for iOS/Android
- [ ] File size <100 KB
- [ ] Button IDs alphanumeric only
- [ ] Deep links tested on iOS + Android
- [ ] Debug tag included with version identifier
- [ ] `.md` and `.html` files are in sync

## Existing Templates: Slide Up

### v5 (Current): `iam-slide_up_v5.md` / `.html`

Slide-up notification from bottom or top of screen

**Tech stack:**
- Pure CSS animations (no dependencies)
- Dark mode support
- Web link + deep link support with auto-detection
- iOS and Android slide animations

**Key Features:**
- ✅ brazeBridge with ab.BridgeReady
- ✅ Extensive Korean CUSTOMIZABLE comments
- ✅ AI-friendly customization points
- ✅ Web link opens in new tab, deep link opens in app
- ✅ Auto-detection of link type from URL

**Customization points:**
- Line 79: Slide height (80px)
- Line 102: Background color (#000000)
- Line 112: Border radius (4px)
- Line 124: Icon size (50px)
- Line 156: Text size (0.9375rem)
- Line 178: Text color (#ffffff)
- Line 276-280: Icon image URL
- Line 288-290: Message text
- Line 318: Slide direction ("up" or "down")
- Line 327: Click URL (web or deep link)
- Line 373: Dark mode support (true/false)

**Click tracking button IDs:**
- `message_body` - Message content click
- `close_button` - Close icon click
- `background_close` - Background overlay click

## Existing Templates: Bottom Sheet Single

### v1 (Current): `iam-bottom_sheet_single_v1.md` / `.html`

Single image bottom sheet (no carousel)

**Tech stack:**
- Pure HTML/CSS (no dependencies)
- Single image with click tracking
- Web link + deep link support with auto-detection

**Key Features:**
- ✅ brazeBridge with ab.BridgeReady
- ✅ Korean CUSTOMIZABLE comments
- ✅ Simpler than carousel (smaller file size)
- ✅ Web link opens in new tab, deep link opens in app
- ✅ Auto-detection of link type

**Customization points:**
- Line 34: Overlay background (rgba)
- Line 55: Modal border radius (20px)
- Line 73: Image height (400px)
- Line 156-161: Image URL
- Line 168-169: Button text
- Line 187: Image link URL
- Line 188: Link type ("deeplink" or "web")
- Line 231: Modal delay (500ms)

**Click tracking button IDs:**
- `image_click` - Image click
- `suppress_today` - Don't show today button
- `suppress_today_close` - Close after suppression
- `close_button` - Close button
- `close_overlay` - Overlay click

## Existing Templates: Bottom Sheet Carousel

### v1 (Legacy): `iam-bottom_sheet_carousel.md`

Product carousel in bottom sheet modal

**Tech stack:**
- Swiper.js 11 (CDN)
- Bottom sheet with slide-up animation
- localStorage "don't show today" suppression
- Safe area padding

**⚠️ Uses deprecated `appboyBridge`** - kept for backward compatibility with deployed campaigns.

**Customization points:**
- Line 121-125: Data array `D`
- Line 48: Carousel height (`.swiper { height: 400px }`)
- Line 166: Auto-play delay (`autoplay: { delay: 3000 }`)
- Line 113-114: Button text/actions

### v2: `iam-bottom_sheet_carousel_v2.md` / `.html`

**Optimizations over v1:**
- ✅ Uses `brazeBridge` with `ab.BridgeReady` event listener
- ✅ Backward compatible fallback to `appboyBridge` for older SDKs
- ✅ Specific button IDs for click tracking: `close_overlay`, `close_button`, `suppress_today`, `slide_1`-`slide_4`
- ✅ All interactions tracked (overlay click, suppress button, each slide)
- ✅ Bridge ready state management

**Customization points:** Same as v1

### v3: `iam-bottom_sheet_carousel_v3.md` / `.html`

**Optimizations over v2:**
- ✅ Proper rounded corners on modal top (20px radius)
- ✅ Swiper container respects modal border radius
- ✅ Added `overflow: hidden` to `.modal` and `.swiper` for clean corner clipping
- ✅ Images no longer cover rounded corners

**CSS Changes:**
```css
.modal {
    overflow: hidden;  /* Added */
}
.swiper {
    border-radius: 20px 20px 0 0;  /* Added */
    overflow: hidden;  /* Added */
}
```

**Customization points:** Same as v1

### v4: `iam-bottom_sheet_carousel_v4.md` / `.html`

**Optimizations over v3:**
- ✅ Removed bottom safe area padding for tighter Android GNB fit
- ✅ Buttons now sit flush with Android navigation bar
- ✅ Commented safe area code with Korean instructions for re-enabling if needed

**When to use v3 vs v4:**
- **v4**: Default for Android apps with visible GNB (tighter fit)
- **v3**: Use if buttons are covered by Android navigation bar (add safe area padding)

**Customization points:** Same as v1

### v5 (Current - Easy Customization): `iam-bottom_sheet_carousel_v5.md` / `.html`

**Optimizations over v4:**
- ✅ **Extensive Korean comments** for non-developer customization
- ✅ **AI-friendly comment blocks** with example requests
- ✅ **Web link support** with automatic type detection (`deeplink` vs `web`)
- ✅ **Clear customization sections** for common changes

**Key Features for Non-Developers:**

**1. Data Array with Examples (Line 140-181)**
```javascript
var D = [
    {
        "i": "image_url",           // 이미지 URL
        "u": "athlerab://product/123", // 링크 URL
        "t": "deeplink"             // 링크 타입: "deeplink" 또는 "web"
    }
];
```

**2. Link Type Auto-Detection**
- `"t": "deeplink"` → Opens in app
- `"t": "web"` → Opens in new browser tab
- No type specified → Auto-detects from URL (http = web, else = deeplink)

**3. Customizable Elements with AI Request Examples:**

| Element | AI Request Example (Korean) | Location |
|---------|----------------------------|----------|
| **이미지 URL** | "이미지 URL을 바꿔줘" | Line 140-181 |
| **딥링크** | "딥링크를 athlerab://product/999로 바꿔줘" | Line 140-181 |
| **웹링크 추가** | "세 번째 슬라이드를 웹 링크로 바꿔줘" | Line 140-181 |
| **슬라이드 개수** | "슬라이드를 5개로 늘려줘" | Line 140-181 |
| **버튼 텍스트** | "버튼 텍스트를 '다시 보지 않기'로 바꿔줘" | Line 158-159 |
| **캐러셀 높이** | "캐러셀을 더 높게/낮게 만들어줘" | Line 61 (400px) |
| **자동재생 속도** | "자동재생 속도를 더 빠르게/느리게 해줘" | Line 311 (3000ms) |
| **오버레이 색상** | "오버레이를 더 어둡게/밝게 만들어줘" | Line 33 (rgba) |
| **둥근 모서리** | "모서리를 더 둥글게/덜 둥글게 만들어줘" | Line 49 (20px) |
| **모달 딜레이** | "모달을 더 빨리/천천히 나타나게 해줘" | Line 326 (500ms) |

**How to Use with AI Coding Agents:**

Non-developers can simply say (in Korean or English):
- "슬라이드 3개를 웹 링크로 바꾸고, 이미지는 [URL]로 변경해줘"
- "자동재생을 끄고 캐러셀을 더 높게 만들어줘"
- "버튼 색깔을 파란색으로 바꿔줘"

All customization points have Korean comment blocks that AI agents can easily identify.

## Existing Templates: Fullscreen Single

### v1 (Current): `iam-fullscreen_single_v1.md` / `.html`

Full screen single image template (covers entire screen)

**Tech stack:**
- Pure HTML/CSS (no dependencies)
- Full screen overlay with object-fit: contain
- Web link + deep link support with auto-detection

**Key Features:**
- ✅ brazeBridge with ab.BridgeReady
- ✅ Full viewport coverage (100% width/height)
- ✅ Image scales to fit screen while maintaining aspect ratio
- ✅ Close button top-right corner
- ✅ Web link opens in new tab, deep link opens in app

**Customization points:**
- Line 10: Fullscreen background color (#000)
- Line 14: Image object-fit (contain)
- Line 36-37: Image URL
- Line 42: Image link URL
- Line 43: Link type ("deeplink" or "web")

**Click tracking button IDs:**
- `image_click` - Image click
- `close_button` - Close button

## Existing Templates: Fullscreen Carousel

### v1 (Current): `iam-fullscreen_carousel_v1.md` / `.html`

Full screen carousel template (covers entire screen)

**Tech stack:**
- Swiper.js 11 (CDN)
- Full screen overlay
- Page indicator at bottom center
- Auto-play support

**Key Features:**
- ✅ brazeBridge with ab.BridgeReady
- ✅ Full viewport coverage with carousel
- ✅ Image object-fit: contain for full visibility
- ✅ Loop and auto-play enabled
- ✅ Web/deeplink support per slide

**Customization points:**
- Line 36-41: Data array `D` with image URLs and links
- Line 70: Auto-play delay (3000ms)
- Line 73: Swiper height (100%)
- Line 17: Page indicator style

**Click tracking button IDs:**
- `close_button` - Close button
- `slide_1`, `slide_2`, `slide_3`, `slide_4` - Individual slide clicks

## Existing Templates: Modal Single

### v1 (Current): `iam-modal_single_v1.md` / `.html`

Centered modal single image (max-width constrained)

**Tech stack:**
- Pure HTML/CSS (no dependencies)
- Centered modal with scale animation
- Dark overlay background
- Web link + deep link support with auto-detection

**Key Features:**
- ✅ brazeBridge with ab.BridgeReady
- ✅ Extensive Korean CUSTOMIZABLE comments
- ✅ Centered modal with 500px max-width
- ✅ Scale animation (0.9 → 1.0)
- ✅ Dark overlay (rgba(0,0,0,0.7))
- ✅ Web link opens in new tab, deep link opens in app

**Customization points:**
- Line 33: Overlay background color (rgba)
- Line 54: Modal max-width (500px)
- Line 64: Modal background color (#000000)
- Line 74: Modal border radius (16px)
- Line 149: Image URL
- Line 175: Click URL
- Line 176: Link type ("deeplink" or "web")
- Line 240: Modal display delay (300ms)

**Click tracking button IDs:**
- `image_click` - Image click
- `close_button` - Close button
- `close_overlay` - Overlay click

## Existing Templates: Modal Carousel

### v1 (Current): `iam-modal_carousel_v1.md` / `.html`

Centered modal carousel (max-width constrained)

**Tech stack:**
- Swiper.js 11 (CDN)
- Centered modal with scale animation
- 400px height carousel
- Dark overlay background

**Key Features:**
- ✅ brazeBridge with ab.BridgeReady
- ✅ Centered modal (max-width: 500px)
- ✅ Scale animation
- ✅ Page indicator bottom-right
- ✅ Auto-play with loop
- ✅ Minified code for file size

**Customization points:**
- Line 40-45: Data array `D` with image URLs and links
- Line 14: Carousel height (400px)
- Line 74: Auto-play delay (3000ms)
- Line 12: Modal max-width (500px)

**Click tracking button IDs:**
- `close_button` - Close button
- `close_overlay` - Overlay click
- `slide_1`, `slide_2`, `slide_3`, `slide_4` - Individual slide clicks

## Existing Templates: Modal Scratch Card

### v1 (Current): `iam-modal_scratch_card_v1.md` / `.html`

Scratch card promotion modal with **real Canvas-based scratch effect** and probability-based prize system

**Tech stack:**
- HTML Canvas API for real scratch effect
- Pure HTML/CSS (no dependencies)
- Centered modal with scale animation
- Dark overlay background
- Touch and mouse event support

**Key Features:**
- ✅ brazeBridge with ab.BridgeReady
- ✅ **Real Canvas scratch effect** with `destination-out` composite operation
- ✅ Touch/mouse scratch interaction (mobile + desktop)
- ✅ **Probability-based prize selection** (n prizes with x probability)
- ✅ **Custom event logging** on prize reveal (`logCustomEvent`)
- ✅ **Custom attribute setting** on prize reveal (`setCustomAttribute`)
- ✅ Silver scratch layer with texture effect
- ✅ Scratch completion detection (configurable threshold)
- ✅ Disabled claim button until scratch complete
- ✅ Web link + deep link support

**Customization points:**
- Line 205-238: **Prize configuration array** (n prizes with probability)
  - `image`: Prize image URL
  - `eventName`: Custom event name to log on reveal
  - `attributeKey`: Custom attribute key to set
  - `attributeValue`: Custom attribute value to set
  - `claimUrl`: URL for claim button
  - `probability`: Prize probability (0.0-1.0, must sum to 1.0)
- Line 245: Scratch brush size (30px default)
- Line 246: Scratch completion threshold (50% default)
- Line 247: Link type ("deeplink" or "web")
- Line 16: Overlay background (rgba)
- Line 28: Modal max-width (450px)
- Line 40: Title font size (20px)
- Line 47: Description text (15px)
- Line 58: Scratch container max-width (300px)
- Line 180: Title text
- Line 181: Description text

**Click tracking button IDs:**
- `scratch_start` - User starts scratching
- `scratch_complete` - Scratch threshold reached (50%+)
- `claim_prize` - Claim button click
- `close_button` - Close button
- `close_overlay` - Overlay click

**Prize Selection Algorithm:**
```javascript
// Cumulative probability selection
// Example: [5%, 15%, 30%, 50%] = [0.05, 0.20, 0.50, 1.00]
var random = Math.random(); // 0.0-1.0
if (random <= 0.05) return prize1;  // 5% chance
if (random <= 0.20) return prize2;  // 15% chance
if (random <= 0.50) return prize3;  // 30% chance
return prize4;  // 50% chance
```

**Braze Integration:**
- Custom event logged when prize revealed: `scratch_win_grand_prize`, `scratch_win_second_prize`, etc.
- Custom attribute set when prize revealed: `last_scratch_result` = `"grand_prize"`, `"second_prize"`, etc.
- Use these for retargeting, segmentation, or analytics

**Use Case:**
- Gamified promotions with real scratch interaction
- Mystery prize reveals with probability control
- Lucky draw campaigns with weighted outcomes
- Scratch-to-win events with Braze event tracking
- Replacement for Braze DnD scratch card templates

## Existing Templates: Modal Two Cards

### v1: `iam-modal_two_cards_v1.md` / `.html`

Two-card layout modal (card front + card back with CTA) - Side-by-side display

**Tech stack:**
- Pure HTML/CSS (no dependencies)
- Flexbox two-column card layout
- Centered modal with scale animation
- Dark semi-transparent overlay

**Key Features:**
- ✅ brazeBridge with ab.BridgeReady
- ✅ Two-card horizontal layout (CARD FRONT + CARD BACK)
- ✅ "Learn More" button with tracking
- ✅ Responsive layout (wraps on mobile)
- ✅ White cards on dark modal background
- ✅ Clean replacement for Braze DnD templates

**Customization points:**
- Line 28: Modal max-width (800px)
- Line 30: Modal background (rgba)
- Line 32: Modal padding (50px 20px)
- Line 40: Card gap (30px)
- Line 47: Card max-width (350px)
- Line 152: Card front image URL
- Line 159: Card back text
- Line 216: Learn More button URL

**Click tracking button IDs:**
- `close_button` - Close button
- `close_overlay` - Overlay click
- `learn_more` - Learn More button

**Use Case:**
- Replacement for Braze drag-and-drop editor templates
- Product showcase with CTA
- Two-sided information display (front/back pattern)

## Existing Templates: Modal Card Flip

### v1 (Current): `iam-modal_card_flip_v1.md` / `.html`

Card flip modal - Front card flips to reveal back card with 3D animation (optimized, no white space)

**Tech stack:**
- Pure HTML/CSS (no dependencies)
- CSS 3D transforms for flip animation
- Two content types for back card: image OR text
- Centered modal with scale animation
- Optimized layout with dynamic height

**Key Features:**
- ✅ brazeBridge with ab.BridgeReady
- ✅ **3D card flip animation** (perspective + rotateY)
- ✅ Front card: Single image (click to flip)
- ✅ Back card: Either image OR text (title + description + button)
- ✅ Back button to return to front card
- ✅ **No white space issues** - optimized padding and min-height
- ✅ Korean CUSTOMIZABLE comments for easy AI editing

**Customization points:**
- Line 220: Front card image URL
- Line 230: Back card type ("image" or "text")
- Line 238: Back card image URL (if type = "image")
- Line 248-254: Back card text content (if type = "text")
  - `title`: 제목
  - `description`: 설명
  - `buttonText`: 버튼 텍스트
  - `buttonUrl`: 버튼 링크 URL
  - `linkType`: "deeplink" 또는 "web"

**Click tracking button IDs:**
- `close_button` - Close button
- `close_overlay` - Overlay click
- `front_card_click` - Front card click (flip to back)
- `back_button` - Back button click (flip to front)
- `back_card_button` - Back card button click (text type only)

**Optimizations (vs previous version):**
- ✅ Removed fixed `min-height: 400px` from card container
- ✅ Reduced back card padding: `30px 25px` (was `40px 30px`)
- ✅ Optimized back card `min-height: 250px` (was implicit 400px)
- ✅ Added flexbox centering for back card content
- ✅ Mobile optimized: `min-height: 220px` on small screens

**Use Case:**
- Interactive product reveal
- Before/after comparisons
- Mystery offer reveals
- Gamified promotions
- Two-step information flow

## Existing Templates: Modal Survey

### v1 (Current): `iam-modal_survey_v1.md` / `.html`

Survey modal with title, description, and customizable options (single or multiple choice)

**Tech stack:**
- Pure HTML/CSS/JavaScript (no dependencies)
- Centered modal with scale animation
- Radio buttons (single choice) or checkboxes (multiple choice)
- Dark overlay background

**Key Features:**
- ✅ brazeBridge with ab.BridgeReady
- ✅ **Title and description support** for survey context
- ✅ **Single or multiple choice** (radio or checkbox)
- ✅ **Randomize options** (optional)
- ✅ **Custom event logging** on submission with response data
- ✅ **Custom attribute setting** to store last response
- ✅ Thank you message after submission
- ✅ Korean CUSTOMIZABLE comments for easy AI editing
- ✅ Clean replacement for Braze DnD survey templates

**Customization points:**
- Line 129: Survey title
- Line 130: Survey description
- Line 141-147: Survey options array (add/remove/edit options)
- Line 156: Multiple choice setting (true = checkbox, false = radio)
- Line 157: Randomize options (true/false)
- Line 158: Submit button text
- Line 159: Custom event name for submission tracking
- Line 160: Custom attribute key to store response
- Line 168: Thank you title
- Line 169: Thank you message

**Click tracking button IDs:**
- `close_button` - Close button
- `close_overlay` - Overlay click
- `survey_submit` - Submit button click

**Braze Integration:**
- Custom event logged on submission: `survey_submitted` (default, customizable)
- Event properties include full response: `{ response: "Selected Option" }`
- Custom attribute set: `last_survey_response` (default, customizable)
- For multiple choice: responses joined with ", " (e.g., "Option 1, Option 2")

**Use Case:**
- Customer satisfaction surveys (CSAT, NPS)
- Product feedback collection
- Feature preference surveys
- Event feedback forms
- Quick polls and questionnaires
- Replacement for Braze DnD survey templates

## AI Customization Guide (For Non-Developers)

v5 is designed for easy customization using AI coding agents like Claude Code. Non-developers can modify templates using natural language requests.

### How to Customize with AI

**1. Open the template file:**
```bash
# Open v5 in your IDE or Claude Code
open iam-bottom_sheet_carousel_v5.md
```

**2. Tell the AI what you want to change using natural language:**

**Examples in Korean:**
```
"첫 번째 슬라이드 이미지를 https://example.com/image.jpg로 바꿔줘"
"두 번째 슬라이드를 웹 링크 https://example.com으로 바꿔줘"
"슬라이드를 3개로 줄여줘"
"자동재생을 5초로 늘려줘"
"캐러셀 높이를 500px로 올려줘"
"닫기 버튼을 '확인'으로 바꿔줘"
"버튼에 파란색 배경을 추가해줘"
"오버레이를 더 어둡게 만들어줘"
```

**Examples in English:**
```
"Change the first slide image to https://example.com/image.jpg"
"Change the second slide to web link https://example.com"
"Reduce to 3 slides"
"Increase autoplay to 5 seconds"
"Make carousel height 500px"
"Change close button to 'Confirm'"
"Add blue background to buttons"
"Make overlay darker"
```

### Common Customization Patterns

**Pattern 1: Update Product Images and Links**
```
"슬라이드 4개 모두 업데이트:
1. 이미지: [URL1], 딥링크: athlerab://product/111
2. 이미지: [URL2], 딥링크: athlerab://product/222
3. 이미지: [URL3], 딥링크: athlerab://product/333
4. 이미지: [URL4], 딥링크: athlerab://product/444"
```

**Pattern 2: Mix Deep Links and Web Links**
```
"슬라이드 1-2는 앱 딥링크, 슬라이드 3은 웹 링크로:
1. athlerab://product/100
2. athlerab://product/200
3. https://promotion.example.com (웹 링크)"
```

**Pattern 3: Add More Slides**
```
"슬라이드를 6개로 늘리고, 마지막 2개는 더미 데이터로 채워줘"
```

**Pattern 4: Visual Adjustments**
```
"캐러셀 높이 450px, 자동재생 4초, 모서리 30px로 더 둥글게"
```

### What AI Can Find Easily in v5

All customization sections have this format:
```
/* ============================================
   CUSTOMIZABLE: [섹션 이름]
   ============================================
   AI 요청 예시: "[요청 예시]"
   설명 및 옵션
*/
```

AI agents can:
1. Search for `CUSTOMIZABLE:` comments
2. Read the Korean instructions
3. Understand what can be changed
4. Make the changes safely

### Testing After Customization

**Local test:**
```bash
# Open in browser to verify
open iam-bottom_sheet_carousel_v5.md
```

**Braze test:**
1. Copy entire HTML content
2. Paste into Braze Custom Code editor
3. Use Preview to test on device

## Common Commands

**No build process** - these are static HTML files.

**Validate file size:**
```bash
du -h iam-*.md
```

**Minify for deployment** (if >100 KB):
```bash
# Install minifier if needed
npm install -g html-minifier

# Minify
html-minifier --collapse-whitespace --remove-comments \
  --minify-css --minify-js iam-template.md > iam-template.min.html
```

## Version Control Strategy

Braze has no built-in version control. Use these patterns:

1. **Debug tags**: Add `<div class="debug-tag">V2_LIQUID</div>` to identify deployed versions
2. **File suffixes**: Save variants as `iam-carousel_v1.md`, `iam-carousel_v2.md`
3. **Git commit messages**: Document what changed and why
4. **Keep working versions**: Don't delete old variants (needed for rollback)

### ⚠️ CRITICAL RULE: Never Override Existing Templates

**When optimizing or modifying templates, ALWAYS create a new version file.**

❌ **WRONG**: Edit `iam-bottom_sheet_carousel.md` directly
✅ **CORRECT**: Create `iam-bottom_sheet_carousel_v2.md`

**Why**: Deployed campaigns reference specific template versions. Overwriting files breaks deployed campaigns and eliminates rollback capability.

## Project-Specific Quirks

- **`.md` extension**: GitHub renders HTML in markdown files for easier preview
- **Korean button text**: Common in templates (e.g., "오늘 하루 보지 않기" = "Don't show today")
- **`athlerab://` deep links**: Custom app scheme for client's app
- **Google Cloud Storage URLs**: Images hosted on `storage.googleapis.com`
- **Debug tags**: All templates should include version identifier in top-right corner

## When to Ask User

- **API migration**: "Should I migrate this template from `appboyBridge` to `brazeBridge`?"
- **Data source**: "Should this use hardcoded data or Liquid variables from custom attributes?"
- **File size trade-off**: "Template is 105 KB. Minify variable names or reduce features?"
- **Safe area padding**: "iOS safe area padding adds complexity. Is this template mobile-only?"

## References

**Official Docs:**
- Braze HTML IAM Guide: https://www.braze.com/docs/user_guide/message_building_by_channel/in-app_messages/traditional/customize/html_in-app_messages
- Braze Customization: https://www.braze.com/docs/user_guide/message_building_by_channel/in-app_messages/traditional/customize

**Important Notes:**
- Braze's official templates repo (github.com/braze-inc/in-app-message-templates) is **ARCHIVED** as of Feb 2024
- Braze now recommends "drag-and-drop editor" over custom HTML for new users
- Custom HTML still fully supported for advanced use cases (like this project)
