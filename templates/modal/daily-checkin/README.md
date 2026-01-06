# Daily Check-in Calendar Modal Template

### 개요

7일 출석 체크 캘린더가 있는 모달 인앱 메시지입니다. 매일 출석을 유도하여 사용자 참여도와 리텐션을 높이는 게임화 전략에 최적화된 템플릿입니다.

### 주요 기능

- ✅ 7일 캘린더 그리드 UI
- ✅ 출석 현황 시각화 (완료, 오늘, 잠김)
- ✅ 연속 출석 스트릭 카운터
- ✅ 일별 리워드 표시
- ✅ 진행률 바
- ✅ 출석 완료 시 커스텀 이벤트 및 속성 업데이트
- ✅ 동적 상태 관리 (Liquid 지원)
- ✅ 모바일 최적화 반응형 디자인

### 미리보기

```
┌──────────────────────────────┐
│                         ✕    │
│          📅                  │
│   데일리 출석 체크!          │
│ 매일 출석하고 리워드를 받으세요 │
│                              │
│ ┌──────────────────────────┐ │
│ │     연속 출석             │ │
│ │        3일               │ │
│ └──────────────────────────┘ │
│                              │
│ 월 화 수 목 금 토 일         │
│ ✓  ✓  ⭐ 🎁 🏆 👑 🎉     │
│ 100 200 300 400 500 700 1000│
│                              │
│ 주간 진행률        3/7일    │
│ ██████░░░░░░░░░              │
│                              │
│ [ 오늘 출석하기 🎁 ]        │
│                              │
│ 오늘 출석 시 300P 리워드!   │
└──────────────────────────────┘
```

### 커스터마이징 옵션

#### 기본 설정
```javascript
var config = {
    icon: "📅",
    title: "데일리 출석 체크!",
    description: "매일 출석하고 리워드를 받으세요",
    checkinButtonText: "오늘 출석하기 🎁",
    alreadyCheckedText: "✅ 오늘 출석 완료!",
    tooEarlyText: "내일 다시 출석하세요",
    streakText: "연속 출석",
    progressLabel: "주간 진행률"
};
```

#### 캘린더 설정
```javascript
var calendarConfig = {
    dayLabels: ["월", "화", "수", "목", "금", "토", "일"],
    rewards: [
        { emoji: "💎", points: "100P" },
        { emoji: "⭐", points: "200P" },
        { emoji: "🎁", points: "300P" },
        { emoji: "💰", points: "400P" },
        { emoji: "🏆", points: "500P" },
        { emoji: "👑", points: "700P" },
        { emoji: "🎉", points: "1000P" }
    ]
};
```

#### 출석 현황 설정
```javascript
// 정적 값
var checkinStatus = {
    currentDay: 3,         // 0-7 (현재 연속 출석 일수)
    todayChecked: false    // 오늘 출석 완료 여부
};

// Liquid 동적 값
var checkinStatus = {
    currentDay: "{{custom_attribute.${checkin_streak}}}",
    todayChecked: "{{custom_attribute.${today_checked}}}"
};
```

### 작동 방식

1. **캘린더 렌더링**: 7일 그리드 생성, 현재 출석 일수에 따라 상태 표시
2. **출석 상태**:
   - **완료** (초록): 과거 출석한 날짜, 체크 마크 표시
   - **오늘** (주황): 오늘 출석 가능한 날짜, 하이라이트
   - **잠김** (회색): 미래 날짜, 비활성화
3. **출석 버튼 클릭**:
   - `currentDay` 증가
   - `todayChecked` = true
   - UI 업데이트 (캘린더, 진행률, 스트릭)
   - Braze 이벤트 로깅
   - 사용자 속성 업데이트
4. **진행률 바**: 7일 중 완료된 일수 비율 표시
5. **리워드 미리보기**: 다음 출석 시 받을 리워드 안내

### 커스텀 이벤트

| 이벤트명 | 트리거 시점 | 속성 |
|----------|-------------|------|
| `daily_checkin_viewed` | 캘린더 표시됨 | `current_streak`, `today_checked` |
| `daily_checkin_complete` | 출석 완료 | `day`, `reward` |

### 커스텀 속성

| 속성 키 | 값 | 목적 |
|---------|-------|---------|
| `checkin_streak` | 1-7 | 현재 연속 출석 일수 |
| `last_checkin_date` | "2026-01-05" | 마지막 출석 날짜 (ISO 날짜) |

### 클릭 추적 버튼 ID

| 버튼 ID | 설명 |
|---------|------|
| `close_button` | 닫기 버튼 클릭 |
| `close_overlay` | 오버레이 배경 클릭 |
| `checkin_button` | 출석 버튼 클릭 |

### 사용 사례

- **리텐션 향상**: 매일 앱 접속 유도
- **습관 형성**: 연속 출석을 통한 습관 만들기
- **포인트 적립**: 출석 리워드로 포인트 지급
- **커뮤니티 챌린지**: 7일 챌린지 완주 이벤트
- **신규 사용자 온보딩**: 첫 7일 출석 유도
- **이탈 방지**: 매일 출석 혜택으로 이탈 감소

### AI 커스터마이징 예시

AI에게 출석 캘린더 수정 요청:

```
"요일 라벨을 영어로 바꿔줘: Mon, Tue, Wed..."
"모든 리워드를 500P로 통일해줘"
"Day 7 리워드를 10,000P로 특별하게 올려줘"
"현재 출석일을 5일로 설정해줘"
"Liquid 변수로 동적 출석일 사용하게 바꿔줘"
"타이틀을 '7일 챌린지!'로 바꿔줘"
"출석 버튼 텍스트를 'Check In Today!'로 바꿔줘"
"리워드 아이콘을 전부 ⭐로 통일해줘"
```

### Liquid 변수 활용

#### 동적 출석 현황
```javascript
var checkinStatus = {
    currentDay: "{{custom_attribute.${checkin_streak}}}",
    todayChecked: "{{custom_attribute.${today_checked}}}"
};
```

#### 백엔드 로직 필요사항

출석 캘린더를 완전히 작동시키려면 백엔드에서 다음을 처리해야 합니다:

1. **날짜 검증**: 마지막 출석 날짜 확인
2. **스트릭 관리**: 연속 출석 끊김 감지 및 리셋
3. **리워드 지급**: 출석 시 포인트 지급
4. **속성 업데이트**: Braze 사용자 속성 동기화

**예시 플로우:**
```
1. 사용자 출석 버튼 클릭
2. Braze 이벤트: daily_checkin_complete (day: 3)
3. 백엔드 웹훅 수신
4. 날짜 검증 (오늘 이미 출석했는지 확인)
5. 스트릭 업데이트 (연속 출석 체크)
6. 리워드 지급 (300P 적립)
7. Braze 속성 업데이트 (checkin_streak, last_checkin_date)
```

### 스트릭 관리 전략

#### 연속 출석 리셋 조건
- **하루 건너뛴 경우**: 스트릭 0으로 리셋
- **7일 완료 후**: 스트릭 0으로 리셋, 새로운 챌린지 시작

#### 스트릭 유지 조건
- **매일 출석**: 스트릭 유지 및 증가
- **같은 날 중복 출석**: 스트릭 증가하지 않음

#### 백엔드 스트릭 검증 로직 (예시)
```javascript
function validateCheckin(userId, lastCheckinDate, currentStreak) {
    const today = new Date().toISOString().split("T")[0];
    const yesterday = new Date(Date.now() - 86400000).toISOString().split("T")[0];

    // 오늘 이미 출석한 경우
    if (lastCheckinDate === today) {
        return { success: false, reason: "already_checked_in" };
    }

    // 어제 출석한 경우 (스트릭 유지)
    if (lastCheckinDate === yesterday) {
        return { success: true, newStreak: currentStreak + 1 };
    }

    // 하루 이상 건너뛴 경우 (스트릭 리셋)
    return { success: true, newStreak: 1 };
}
```

### 리워드 구조 커스터마이징

#### 증가형 리워드 (추천)
```javascript
rewards: [
    { emoji: "💎", points: "100P" },
    { emoji: "⭐", points: "200P" },
    { emoji: "🎁", points: "300P" },
    { emoji: "💰", points: "500P" },
    { emoji: "🏆", points: "700P" },
    { emoji: "👑", points: "1000P" },
    { emoji: "🎉", points: "2000P" }  // Day 7 특별 리워드
]
```

#### 균일 리워드
```javascript
rewards: [
    { emoji: "⭐", points: "500P" },
    { emoji: "⭐", points: "500P" },
    { emoji: "⭐", points: "500P" },
    { emoji: "⭐", points: "500P" },
    { emoji: "⭐", points: "500P" },
    { emoji: "⭐", points: "500P" },
    { emoji: "🎉", points: "1000P" }  // Day 7만 특별
]
```

#### 아이템 리워드
```javascript
rewards: [
    { emoji: "🎁", points: "코인 10개" },
    { emoji: "💰", points: "골드 50" },
    { emoji: "💎", points: "다이아 1개" },
    { emoji: "🏆", points: "경험치 100" },
    { emoji: "🎫", points: "쿠폰 1장" },
    { emoji: "👑", points: "VIP 1일" },
    { emoji: "🎉", points: "레어 아이템" }
]
```

### 캠페인 전략

#### 1. 신규 사용자 온보딩
- **대상**: 가입 후 7일 이내 사용자
- **목표**: 초기 습관 형성
- **리워드**: 증가형 (100P → 2000P)

#### 2. 휴면 복귀 챌린지
- **대상**: 30일 이상 미접속 사용자
- **목표**: 재활성화
- **리워드**: 높은 포인트 (500P~5000P)

#### 3. 시즌 이벤트
- **대상**: 전체 사용자
- **목표**: 이벤트 기간 참여도 증대
- **리워드**: 특별 아이템 + 포인트

#### 4. VIP 전용 챌린지
- **대상**: VIP 등급 사용자
- **목표**: VIP 혜택 차별화
- **리워드**: 2배 포인트

### 분석 및 최적화

#### 추적 지표
| 지표 | 설명 | Braze 활용 |
|------|------|-----------|
| **출석률** | 전체 사용자 중 출석 비율 | 일별 `daily_checkin_complete` 이벤트 수 |
| **완주율** | 7일 완주한 사용자 비율 | `checkin_streak = 7` 속성 필터 |
| **평균 스트릭** | 사용자별 평균 연속 출석일 | `checkin_streak` 속성 평균 |
| **이탈일** | 출석 중단한 날짜 분포 | Day 1~7 중단 비율 분석 |

#### A/B 테스트 아이디어
1. **리워드 구조**: 증가형 vs 균일형 vs Day 7 특별 보상
2. **리워드 금액**: 100P vs 500P vs 1000P 시작
3. **요일 라벨**: 한글 vs 영문 vs 숫자
4. **디자인**: 그라데이션 vs 단색 vs 일러스트

### 모범 사례

1. **명확한 리워드**: 각 날짜별 리워드 명시
2. **진행률 시각화**: 진행 상황을 한눈에 확인 가능하게
3. **스트릭 강조**: 연속 출석일 수를 크게 표시
4. **백엔드 검증**: 프론트만 믿지 말고 서버에서 재검증
5. **스트릭 리셋 안내**: 하루 건너뛰면 리셋된다는 안내
6. **완주 리워드 차별화**: Day 7 리워드를 특별하게

### 브라우저 지원

- ✅ iOS Safari 12+
- ✅ Android Chrome 80+
- ✅ 모든 최신 모바일 브라우저
- ✅ JavaScript 필수

### 알려진 제한사항

- 프론트엔드만으로는 날짜 검증 불완전 (기기 시간 조작 가능)
- 백엔드 로직 필수 (스트릭 관리, 리워드 지급)
- Braze 속성 업데이트는 비동기 (즉시 반영 안 될 수 있음)

### 팁

1. **백엔드 필수**: 프론트는 UI만, 실제 검증은 백엔드에서
2. **타임존 고려**: 사용자 로컬 시간대 기준으로 날짜 판단
3. **스트릭 리셋 알림**: 출석 누락 시 푸시 알림 발송
4. **완주 축하**: 7일 완주 시 특별 메시지 + 보너스 리워드
5. **재참여 유도**: 스트릭 끊긴 사용자에게 재시작 독려
6. **데이터 시각화**: Braze 대시보드에서 일별 출석률 모니터링
