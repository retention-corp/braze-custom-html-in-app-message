# Braze Custom HTML In-App Message Templates

[English](#english) | [한국어](#korean)

---

<a name="english"></a>
## 🇬🇧 English

### 📱 Overview

Production-ready custom HTML in-app message templates for Braze, built with best practices including proper bridge integration (`brazeBridge` + `ab.BridgeReady`), responsive design, and easy customization.

### ✨ Features

- ✅ **Modern Braze Bridge API** - Uses `brazeBridge` with proper `ab.BridgeReady` event handling
- ✅ **Mobile-First Design** - Fully responsive and touch-optimized
- ✅ **Easy Customization** - Clear sections marked with `/* CUSTOMIZABLE */` comments
- ✅ **Production Ready** - Tested and battle-hardened code
- ✅ **Zero Dependencies** - Pure HTML, CSS, and JavaScript
- ✅ **Analytics Ready** - Built-in event logging and custom attribute tracking

### 📦 Available Templates

#### Modal Templates
- **[Single Image/CTA](./templates/modal/single/)** - Simple modal with image and CTA button
- **[Carousel](./templates/modal/carousel/)** - Multi-slide carousel with navigation
- **[Survey](./templates/modal/survey/)** - Interactive survey with single/multiple choice options
- **[Scratch Card](./templates/modal/scratch-card/)** - Gamified scratch-to-reveal prize system with probability-based rewards
- **[Card Flip](./templates/modal/card-flip/)** - Flip card animation revealing offer/content

#### Fullscreen Templates
- **[Single Image/CTA](./templates/fullscreen/single/)** - Fullscreen takeover with image and CTA
- **[Carousel](./templates/fullscreen/carousel/)** - Fullscreen multi-slide carousel

#### Bottom Sheet Templates
- **[Single Image/CTA](./templates/bottom-sheet/single/)** - Mobile-native bottom sheet design
- **[Carousel](./templates/bottom-sheet/carousel/)** - Multi-card carousel in bottom sheet format

### 🚀 Quick Start

1. **Choose a template** from the directories above
2. **Copy the HTML** from the `.html` file
3. **Paste into Braze** Dashboard → Messaging → In-App Messages → Create Custom Code
4. **Customize** the variables in the `/* CUSTOMIZABLE */` sections
5. **Test** in Braze test mode
6. **Launch** your campaign

### 📖 Usage Example

```html
<!doctype html>
<html>
<head>
    <!-- Template code here -->
</head>
<body>
    <script>
        /* ============================================
           CUSTOMIZABLE: Your Configuration
           ============================================ */
        var buttonText = "Get Started";
        var buttonUrl = "https://your-app.com/offer";
        var linkType = "web"; // or "deeplink"

        // Rest of the template code...
    </script>
</body>
</html>
```

### 🎨 Customization Guide

Each template has clearly marked `CUSTOMIZABLE` sections where you can modify:

- **Images & URLs** - Replace placeholder images with your assets
- **Text & Copy** - Update titles, descriptions, button labels
- **Colors & Styles** - Modify CSS variables for brand consistency
- **Behavior** - Adjust timings, animations, and interactions
- **Analytics** - Configure custom event names and attributes

### 🔧 Braze Integration

#### Event Logging
```javascript
// Log custom events
logCustomEvent("button_clicked", {
    campaign_id: "winter_sale_2024",
    user_action: "cta_click"
});
```

#### Custom Attributes
```javascript
// Set user attributes
setCustomAttribute("last_survey_response", "satisfied");
setCustomAttribute("scratch_card_result", "grand_prize");
```

#### Link Handling
```javascript
// Web URLs (opens in browser)
var linkType = "web";
var buttonUrl = "https://example.com/offer";

// Deep Links (opens in app)
var linkType = "deeplink";
var buttonUrl = "myapp://promo/winter-sale";
```

### 📱 Testing Checklist

Before launching:
- [ ] Test on iOS devices (Safari)
- [ ] Test on Android devices (Chrome)
- [ ] Verify close button works
- [ ] Check CTA button clicks and URL opens correctly
- [ ] Confirm custom events are logged in Braze dashboard
- [ ] Test responsive behavior on various screen sizes
- [ ] Verify animations and transitions work smoothly

### 🎯 Best Practices

1. **Always use `brazeBridge`** - Modern API, better support
2. **Handle `ab.BridgeReady` event** - Ensures bridge is available
3. **Log meaningful events** - Track user interactions for optimization
4. **Set custom attributes** - Persist user preferences and responses
5. **Test in Braze test mode** - Catch issues before production
6. **Optimize images** - Use compressed images for fast loading
7. **Mobile-first design** - Prioritize mobile experience
8. **Clear CTAs** - Make primary actions obvious

### 🐛 Troubleshooting

**Issue**: Images not loading
- **Solution**: Use HTTPS URLs, check CORS settings

**Issue**: Bridge not available
- **Solution**: Ensure `ab.BridgeReady` event listener is set before other code

**Issue**: Links not opening
- **Solution**: Verify `linkType` matches URL format (web vs deeplink)

**Issue**: Custom events not showing in Braze
- **Solution**: Call `requestImmediateDataFlush()` before closing message

### 📄 License

MIT License - Free to use in commercial and personal projects.

### 🤝 Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Test your changes thoroughly
4. Submit a pull request with clear description

### 💬 Support

- **Issues**: [GitHub Issues](https://github.com/retention-corp/braze-custom-html-in-app-message/issues)
- **Discussions**: [GitHub Discussions](https://github.com/retention-corp/braze-custom-html-in-app-message/discussions)

---

<a name="korean"></a>
## 🇰🇷 한국어

### 📱 개요

Braze용 프로덕션 레디 커스텀 HTML 인앱 메시지 템플릿입니다. 최신 브리지 통합(`brazeBridge` + `ab.BridgeReady`), 반응형 디자인, 쉬운 커스터마이징 등 모범 사례를 적용했습니다.

### ✨ 주요 기능

- ✅ **최신 Braze Bridge API** - `ab.BridgeReady` 이벤트 처리를 포함한 `brazeBridge` 사용
- ✅ **모바일 우선 디자인** - 완전한 반응형 및 터치 최적화
- ✅ **쉬운 커스터마이징** - `/* CUSTOMIZABLE */` 주석으로 명확하게 표시된 섹션
- ✅ **프로덕션 레디** - 실전 테스트를 거친 안정적인 코드
- ✅ **의존성 제로** - 순수 HTML, CSS, JavaScript
- ✅ **분석 준비 완료** - 이벤트 로깅 및 커스텀 속성 추적 내장

### 📦 사용 가능한 템플릿

#### 모달 템플릿
- **[Single Image/CTA](./templates/modal/single/)** - 이미지와 CTA 버튼이 있는 간단한 모달
- **[Carousel](./templates/modal/carousel/)** - 네비게이션이 있는 멀티 슬라이드 캐러셀
- **[Survey](./templates/modal/survey/)** - 단일/다중 선택 옵션이 있는 인터랙티브 설문조사
- **[Scratch Card](./templates/modal/scratch-card/)** - 확률 기반 보상이 있는 게임화된 스크래치 카드
- **[Card Flip](./templates/modal/card-flip/)** - 오퍼/콘텐츠를 드러내는 카드 뒤집기 애니메이션

#### 풀스크린 템플릿
- **[Single Image/CTA](./templates/fullscreen/single/)** - 이미지와 CTA가 있는 풀스크린 테이크오버
- **[Carousel](./templates/fullscreen/carousel/)** - 풀스크린 멀티 슬라이드 캐러셀

#### 바텀 시트 템플릿
- **[Single Image/CTA](./templates/bottom-sheet/single/)** - 모바일 네이티브 바텀 시트 디자인
- **[Carousel](./templates/bottom-sheet/carousel/)** - 바텀 시트 형식의 멀티 카드 캐러셀

### 🚀 빠른 시작

1. **템플릿 선택** - 위 디렉토리에서 원하는 템플릿 선택
2. **HTML 복사** - `.html` 파일에서 코드 복사
3. **Braze에 붙여넣기** - Dashboard → Messaging → In-App Messages → Create Custom Code
4. **커스터마이징** - `/* CUSTOMIZABLE */` 섹션의 변수 수정
5. **테스트** - Braze 테스트 모드에서 확인
6. **런칭** - 캠페인 실행

### 📖 사용 예시

```html
<!doctype html>
<html>
<head>
    <!-- 템플릿 코드 -->
</head>
<body>
    <script>
        /* ============================================
           CUSTOMIZABLE: 설정
           ============================================ */
        var buttonText = "시작하기";
        var buttonUrl = "https://your-app.com/offer";
        var linkType = "web"; // 또는 "deeplink"

        // 나머지 템플릿 코드...
    </script>
</body>
</html>
```

### 🎨 커스터마이징 가이드

각 템플릿은 명확하게 표시된 `CUSTOMIZABLE` 섹션에서 다음을 수정할 수 있습니다:

- **이미지 & URL** - 플레이스홀더 이미지를 자신의 에셋으로 교체
- **텍스트 & 카피** - 제목, 설명, 버튼 라벨 업데이트
- **색상 & 스타일** - 브랜드 일관성을 위한 CSS 변수 수정
- **동작** - 타이밍, 애니메이션, 인터랙션 조정
- **분석** - 커스텀 이벤트명 및 속성 설정

### 🔧 Braze 통합

#### 이벤트 로깅
```javascript
// 커스텀 이벤트 로그
logCustomEvent("button_clicked", {
    campaign_id: "winter_sale_2024",
    user_action: "cta_click"
});
```

#### 커스텀 속성
```javascript
// 사용자 속성 설정
setCustomAttribute("last_survey_response", "satisfied");
setCustomAttribute("scratch_card_result", "grand_prize");
```

#### 링크 처리
```javascript
// 웹 URL (브라우저에서 열기)
var linkType = "web";
var buttonUrl = "https://example.com/offer";

// 딥링크 (앱에서 열기)
var linkType = "deeplink";
var buttonUrl = "myapp://promo/winter-sale";
```

### 📱 테스트 체크리스트

런칭 전 확인사항:
- [ ] iOS 기기 테스트 (Safari)
- [ ] Android 기기 테스트 (Chrome)
- [ ] 닫기 버튼 작동 확인
- [ ] CTA 버튼 클릭 및 URL 오픈 확인
- [ ] Braze 대시보드에서 커스텀 이벤트 로그 확인
- [ ] 다양한 화면 크기에서 반응형 동작 테스트
- [ ] 애니메이션 및 전환 효과 원활성 확인

### 🎯 모범 사례

1. **항상 `brazeBridge` 사용** - 최신 API, 더 나은 지원
2. **`ab.BridgeReady` 이벤트 처리** - 브리지 사용 가능 확인
3. **의미 있는 이벤트 로깅** - 최적화를 위한 사용자 인터랙션 추적
4. **커스텀 속성 설정** - 사용자 선호도 및 응답 지속
5. **Braze 테스트 모드에서 테스트** - 프로덕션 전 이슈 발견
6. **이미지 최적화** - 빠른 로딩을 위한 압축 이미지 사용
7. **모바일 우선 디자인** - 모바일 경험 우선순위
8. **명확한 CTA** - 주요 액션을 명확하게 표시

### 🐛 문제 해결

**문제**: 이미지가 로드되지 않음
- **해결책**: HTTPS URL 사용, CORS 설정 확인

**문제**: 브리지를 사용할 수 없음
- **해결책**: 다른 코드보다 먼저 `ab.BridgeReady` 이벤트 리스너 설정

**문제**: 링크가 열리지 않음
- **해결책**: `linkType`이 URL 형식과 일치하는지 확인 (web vs deeplink)

**문제**: 커스텀 이벤트가 Braze에 표시되지 않음
- **해결책**: 메시지를 닫기 전에 `requestImmediateDataFlush()` 호출

### 📄 라이선스

MIT 라이선스 - 상업적 및 개인 프로젝트에서 자유롭게 사용 가능

### 🤝 기여

기여를 환영합니다! 다음 단계를 따라주세요:
1. 리포지토리 포크
2. 기능 브랜치 생성
3. 변경 사항 철저히 테스트
4. 명확한 설명과 함께 풀 리퀘스트 제출

### 💬 지원

- **이슈**: [GitHub Issues](https://github.com/retention-corp/braze-custom-html-in-app-message/issues)
- **토론**: [GitHub Discussions](https://github.com/retention-corp/braze-custom-html-in-app-message/discussions)
