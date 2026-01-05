# Scratch Card Modal Template

[English](#english) | [한국어](#korean)

---

<a name="english"></a>
## 🇬🇧 English

### Overview

Interactive scratch card in-app message with probability-based prize selection. Users scratch to reveal their prize, creating an engaging gamified experience.

### Features

- ✅ Real Canvas-based scratch effect
- ✅ Probability-based prize selection
- ✅ Multiple prize tiers support
- ✅ Custom event logging for each prize tier
- ✅ Custom attribute tracking for user prizes
- ✅ Configurable scratch threshold and brush size
- ✅ Mobile-optimized touch interactions

### Preview

```
┌──────────────────────────────┐
│ Scratch Here to Reveal!      │
│                              │
│ ┌─────────────────────────┐  │
│ │  [Silver Scratch Layer] │  │
│ │   SCRATCH HERE!         │  │
│ │                         │  │
│ └─────────────────────────┘  │
│                              │
│   [ CLAIM YOUR PRIZE ]       │
└──────────────────────────────┘
```

### Customizable Options

#### Prize Configuration
```javascript
var prizes = [
    {
        image: "https://picsum.photos/seed/Prize1/300/200",
        eventName: "scratch_win_grand_prize",
        attributeKey: "last_scratch_result",
        attributeValue: "grand_prize",
        claimUrl: "https://www.example.com/grand-prize",
        probability: 0.05 // 5%
    },
    // Add more prize tiers...
];
```

#### Scratch Settings
```javascript
var scratchBrushSize = 30; // Brush size in pixels
var scratchThreshold = 50; // Completion percentage (0-100)
var linkType = "web"; // "web" or "deeplink"
```

### How It Works

1. **Prize Selection**: Random prize selected based on probability weights
2. **Scratch Interaction**: User scratches canvas to reveal prize image
3. **Threshold Check**: When X% scratched, prize is fully revealed
4. **Button Activation**: Claim button becomes enabled
5. **Event Logging**: Custom event logged for prize tier
6. **Attribute Setting**: User attribute set for segmentation

### Custom Events

| Event Name | When Triggered | Properties |
|------------|----------------|------------|
| `scratch_win_grand_prize` | Grand prize revealed | None |
| `scratch_win_second_prize` | Second prize revealed | None |
| `scratch_no_prize` | No prize (try again) | None |
| `scratch_start` | User starts scratching | None |
| `scratch_complete` | Scratch reaches threshold | None |
| `claim_prize` | User clicks claim button | None |

### Custom Attributes

| Attribute Key | Value | Purpose |
|---------------|-------|---------|
| `last_scratch_result` | `grand_prize`, `second_prize`, etc. | Track user's last prize for segmentation |

### AI Customization Examples

Ask AI to modify your scratch card:

```
"Add a 5th prize tier with 10% probability"
"Change brush size to 40 pixels"
"Update grand prize image to [URL]"
"Change scratch threshold to 60%"
"Rename custom event to 'winter_scratch_complete'"
```

### Browser Support

- ✅ iOS Safari 12+
- ✅ Android Chrome 80+
- ✅ Modern mobile browsers with Canvas support

### Known Limitations

- Requires JavaScript enabled
- Canvas API required (no IE11 support)
- Performance may vary on older devices with large canvas sizes

### Tips

1. **Image Optimization**: Use compressed images (< 200KB) for fast loading
2. **Probability Tuning**: Test different probability distributions for engagement
3. **Threshold Setting**: 50% is optimal - too low feels incomplete, too high is frustrating
4. **Prize Variety**: Include both high-value and consolation prizes
5. **Clear CTAs**: Make claim URLs lead to relevant landing pages

---

<a name="korean"></a>
## 🇰🇷 한국어

### 개요

확률 기반 프라이즈 선택이 가능한 인터랙티브 스크래치 카드 인앱 메시지입니다. 사용자가 스크래치하여 프라이즈를 드러내는 게임화된 경험을 제공합니다.

### 주요 기능

- ✅ 실제 Canvas 기반 스크래치 효과
- ✅ 확률 기반 프라이즈 선택
- ✅ 다중 프라이즈 등급 지원
- ✅ 각 프라이즈 등급별 커스텀 이벤트 로깅
- ✅ 사용자 프라이즈 커스텀 속성 추적
- ✅ 설정 가능한 스크래치 임계값 및 브러시 크기
- ✅ 모바일 최적화 터치 인터랙션

### 미리보기

```
┌──────────────────────────────┐
│ 스크래치해서 프라이즈 확인!  │
│                              │
│ ┌─────────────────────────┐  │
│ │  [은색 스크래치 레이어] │  │
│ │   여기를 긁으세요!      │  │
│ │                         │  │
│ └─────────────────────────┘  │
│                              │
│   [ 프라이즈 받기 ]          │
└──────────────────────────────┘
```

### 커스터마이징 옵션

#### 프라이즈 설정
```javascript
var prizes = [
    {
        image: "https://picsum.photos/seed/Prize1/300/200",
        eventName: "scratch_win_grand_prize",
        attributeKey: "last_scratch_result",
        attributeValue: "grand_prize",
        claimUrl: "https://www.example.com/grand-prize",
        probability: 0.05 // 5%
    },
    // 프라이즈 등급 추가...
];
```

#### 스크래치 설정
```javascript
var scratchBrushSize = 30; // 브러시 크기 (픽셀)
var scratchThreshold = 50; // 완료 비율 (0-100)
var linkType = "web"; // "web" 또는 "deeplink"
```

### 작동 방식

1. **프라이즈 선택**: 확률 가중치에 따라 무작위 프라이즈 선택
2. **스크래치 인터랙션**: 사용자가 캔버스를 긁어 프라이즈 이미지 드러냄
3. **임계값 체크**: X% 긁으면 프라이즈 완전히 드러남
4. **버튼 활성화**: 받기 버튼 활성화
5. **이벤트 로깅**: 프라이즈 등급별 커스텀 이벤트 로그
6. **속성 설정**: 세그멘테이션을 위한 사용자 속성 설정

### 커스텀 이벤트

| 이벤트명 | 트리거 시점 | 속성 |
|----------|-------------|------|
| `scratch_win_grand_prize` | 대상 드러남 | 없음 |
| `scratch_win_second_prize` | 2등 드러남 | 없음 |
| `scratch_no_prize` | 꽝 (다시 시도) | 없음 |
| `scratch_start` | 사용자가 긁기 시작 | 없음 |
| `scratch_complete` | 스크래치 임계값 도달 | 없음 |
| `claim_prize` | 사용자가 받기 버튼 클릭 | 없음 |

### 커스텀 속성

| 속성 키 | 값 | 목적 |
|---------|-------|------|
| `last_scratch_result` | `grand_prize`, `second_prize` 등 | 세그멘테이션을 위한 사용자 마지막 프라이즈 추적 |

### AI 커스터마이징 예시

AI에게 스크래치 카드 수정 요청:

```
"10% 확률로 5번째 프라이즈 등급 추가해줘"
"브러시 크기를 40픽셀로 변경해줘"
"대상 이미지를 [URL]로 업데이트해줘"
"스크래치 임계값을 60%로 변경해줘"
"커스텀 이벤트명을 'winter_scratch_complete'로 바꿔줘"
```

### 브라우저 지원

- ✅ iOS Safari 12+
- ✅ Android Chrome 80+
- ✅ Canvas를 지원하는 최신 모바일 브라우저

### 알려진 제한사항

- JavaScript 활성화 필요
- Canvas API 필요 (IE11 미지원)
- 큰 캔버스 크기의 경우 구형 기기에서 성능 저하 가능

### 팁

1. **이미지 최적화**: 빠른 로딩을 위해 압축된 이미지 사용 (< 200KB)
2. **확률 조정**: 참여도를 위해 다양한 확률 분포 테스트
3. **임계값 설정**: 50%가 최적 - 너무 낮으면 불완전하고, 너무 높으면 답답함
4. **프라이즈 다양성**: 고가치 및 위로 프라이즈 모두 포함
5. **명확한 CTA**: 받기 URL이 관련 랜딩 페이지로 연결되도록 설정
