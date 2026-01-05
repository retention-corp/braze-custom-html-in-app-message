# Survey Modal Template

[English](#english) | [한국어](#korean)

---

<a name="english"></a>
## 🇬🇧 English

### Overview

Interactive survey modal with single or multiple choice options. Perfect for collecting user feedback, preferences, and satisfaction metrics.

### Features

- ✅ Single-choice (radio) or multiple-choice (checkbox) modes
- ✅ Configurable options with randomization support
- ✅ Custom event logging with response data
- ✅ Custom attribute tracking for user segmentation
- ✅ Thank you message after submission
- ✅ Validation for empty submissions

### Preview

```
┌──────────────────────────────┐
│ We'd Love Your Feedback!     │
│ Please answer this question  │
│                              │
│ ○ Very Satisfied             │
│ ○ Satisfied                  │
│ ○ Neutral                    │
│ ○ Dissatisfied               │
│ ○ Very Dissatisfied          │
│                              │
│     [ Submit ]               │
└──────────────────────────────┘
```

### Customizable Options

#### Survey Configuration
```javascript
var surveyTitle = "We'd Love Your Feedback!";
var surveyDescription = "Please take a moment to answer this quick question.";
var buttonText = "Submit";
```

#### Survey Options
```javascript
var surveyOptions = [
    "Very Satisfied",
    "Satisfied",
    "Neutral",
    "Dissatisfied",
    "Very Dissatisfied"
];
```

#### Survey Settings
```javascript
var multipleChoice = false; // true = checkbox, false = radio
var randomizeOptions = false; // true = randomize order
var customEventName = "survey_submitted";
var customAttributeKey = "last_survey_response";
```

### How It Works

1. **Display Options**: Show radio buttons (single) or checkboxes (multiple)
2. **User Selection**: User selects one or more options
3. **Validation**: Check that at least one option is selected
4. **Event Logging**: Log custom event with response data
5. **Attribute Setting**: Save response to user profile
6. **Thank You**: Show confirmation message

### Custom Events

| Event Name | When Triggered | Properties |
|------------|----------------|------------|
| `survey_submitted` | User submits survey | `response`: Selected option(s) |
| `survey_submit` | Submit button clicked | None |
| `close_overlay` | User closes modal | None |
| `close_button` | Close button clicked | None |

### Custom Attributes

| Attribute Key | Value | Purpose |
|---------------|-------|---------|
| `last_survey_response` | User's selected option(s) | Track user satisfaction for segmentation |

### Use Cases

- **Satisfaction Surveys**: NPS, CSAT, customer satisfaction
- **Preference Collection**: Feature requests, product preferences
- **Feedback Forms**: App experience, onboarding feedback
- **Market Research**: User demographics, interests
- **A/B Testing**: Feature preference validation

### AI Customization Examples

Ask AI to modify your survey:

```
"Change to multiple choice mode"
"Add 'Other' option"
"Randomize option order"
"Update survey title to 'Product Feedback'"
"Add 7 options for NPS scale (0-10)"
```

### Best Practices

1. **Keep It Short**: 3-7 options maximum for better completion rates
2. **Clear Labels**: Use simple, unambiguous option text
3. **Balanced Options**: Include positive, neutral, and negative choices
4. **Randomization**: Use for unbiased results (A/B testing)
5. **Follow-up**: Send thank you message or incentive after completion
6. **Segmentation**: Use responses to trigger personalized campaigns

### Browser Support

- ✅ iOS Safari 12+
- ✅ Android Chrome 80+
- ✅ All modern mobile browsers

---

<a name="korean"></a>
## 🇰🇷 한국어

### 개요

단일 또는 다중 선택 옵션이 있는 인터랙티브 설문조사 모달입니다. 사용자 피드백, 선호도, 만족도 메트릭 수집에 적합합니다.

### 주요 기능

- ✅ 단일 선택(라디오) 또는 다중 선택(체크박스) 모드
- ✅ 무작위화 지원이 있는 설정 가능한 옵션
- ✅ 응답 데이터와 함께 커스텀 이벤트 로깅
- ✅ 사용자 세그멘테이션을 위한 커스텀 속성 추적
- ✅ 제출 후 감사 메시지
- ✅ 빈 제출 검증

### 미리보기

```
┌──────────────────────────────┐
│ 피드백을 주세요!             │
│ 빠른 질문에 답해주세요       │
│                              │
│ ○ 매우 만족                  │
│ ○ 만족                       │
│ ○ 보통                       │
│ ○ 불만족                     │
│ ○ 매우 불만족                │
│                              │
│     [ 제출 ]                 │
└──────────────────────────────┘
```

### 커스터마이징 옵션

#### 설문 설정
```javascript
var surveyTitle = "피드백을 주세요!";
var surveyDescription = "간단한 질문에 답해주세요.";
var buttonText = "제출";
```

#### 설문 옵션
```javascript
var surveyOptions = [
    "매우 만족",
    "만족",
    "보통",
    "불만족",
    "매우 불만족"
];
```

#### 설문 설정
```javascript
var multipleChoice = false; // true = 체크박스, false = 라디오
var randomizeOptions = false; // true = 순서 무작위화
var customEventName = "survey_submitted";
var customAttributeKey = "last_survey_response";
```

### 작동 방식

1. **옵션 표시**: 라디오 버튼(단일) 또는 체크박스(다중) 표시
2. **사용자 선택**: 사용자가 하나 이상의 옵션 선택
3. **검증**: 최소 하나의 옵션이 선택되었는지 확인
4. **이벤트 로깅**: 응답 데이터와 함께 커스텀 이벤트 로그
5. **속성 설정**: 사용자 프로필에 응답 저장
6. **감사 메시지**: 확인 메시지 표시

### 커스텀 이벤트

| 이벤트명 | 트리거 시점 | 속성 |
|----------|-------------|------|
| `survey_submitted` | 사용자가 설문 제출 | `response`: 선택된 옵션 |
| `survey_submit` | 제출 버튼 클릭 | 없음 |
| `close_overlay` | 사용자가 모달 닫기 | 없음 |
| `close_button` | 닫기 버튼 클릭 | 없음 |

### 커스텀 속성

| 속성 키 | 값 | 목적 |
|---------|-------|------|
| `last_survey_response` | 사용자가 선택한 옵션 | 세그멘테이션을 위한 사용자 만족도 추적 |

### 사용 사례

- **만족도 조사**: NPS, CSAT, 고객 만족도
- **선호도 수집**: 기능 요청, 제품 선호도
- **피드백 양식**: 앱 경험, 온보딩 피드백
- **시장 조사**: 사용자 인구통계, 관심사
- **A/B 테스팅**: 기능 선호도 검증

### AI 커스터마이징 예시

AI에게 설문 수정 요청:

```
"다중 선택 모드로 변경해줘"
"'기타' 옵션 추가해줘"
"옵션 순서를 무작위로 섞어줘"
"설문 제목을 '제품 피드백'으로 업데이트해줘"
"NPS 척도를 위해 7개 옵션 추가해줘 (0-10)"
```

### 모범 사례

1. **짧게 유지**: 더 나은 완료율을 위해 3-7개 옵션 최대
2. **명확한 라벨**: 간단하고 명확한 옵션 텍스트 사용
3. **균형 잡힌 옵션**: 긍정적, 중립적, 부정적 선택지 포함
4. **무작위화**: 편향 없는 결과를 위해 사용 (A/B 테스팅)
5. **후속 조치**: 완료 후 감사 메시지 또는 인센티브 전송
6. **세그멘테이션**: 응답을 사용하여 개인화된 캠페인 트리거

### 브라우저 지원

- ✅ iOS Safari 12+
- ✅ Android Chrome 80+
- ✅ 모든 최신 모바일 브라우저
