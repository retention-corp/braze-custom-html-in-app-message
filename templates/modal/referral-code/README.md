# Referral Code Generator Modal Template

### 개요

사용자의 추천 코드를 표시하고 원클릭 복사 기능을 제공하는 모달 인앱 메시지입니다. 추천 프로그램 활성화와 바이럴 성장을 위한 최적의 템플릿입니다.

### 주요 기능

- ✅ 추천 코드 표시 (정적 또는 Liquid 동적 코드)
- ✅ 원클릭 복사 기능 (Clipboard API + 폴백)
- ✅ 복사 성공 시각적 피드백
- ✅ 추천 통계 표시 (초대한 친구 수, 받은 리워드)
- ✅ 네이티브 공유 시트 통합 (Web Share API)
- ✅ 커스텀 이벤트 로깅 (조회, 복사, 공유)
- ✅ 모바일 최적화 그라데이션 디자인

### 미리보기

```
┌──────────────────────────────┐
│                         ✕    │
│          🎁                  │
│   친구 초대하고              │
│   리워드 받기!               │
│ 친구에게 추천 코드를 공유하고│
│ 함께 혜택을 받으세요         │
│                              │
│ ┌──────────────────────────┐ │
│ │   내 추천 코드           │ │
│ │   FRIEND2026             │ │
│ │ [ 📋 코드 복사하기 ]     │ │
│ └──────────────────────────┘ │
│                              │
│   3         15,000₩          │
│ 초대한 친구   받은 리워드    │
│                              │
│ [ 친구에게 공유하기 ]        │
│                              │
│ 친구가 가입하면 5,000₩ 적립! │
└──────────────────────────────┘
```

### 커스터마이징 옵션

#### 기본 설정
```javascript
var config = {
    icon: "🎁",
    title: "친구 초대하고<br>리워드 받기!",
    description: "친구에게 추천 코드를 공유하고<br>함께 혜택을 받으세요",
    copyButtonText: "📋 코드 복사하기",
    copiedButtonText: "✅ 복사 완료!",
    shareButtonText: "친구에게 공유하기",
    rewardText: "친구가 가입하면 <strong>5,000₩</strong> 적립!"
};
```

#### 추천 코드 설정
```javascript
// 정적 코드
var referralCode = "FRIEND2026";

// Liquid 동적 코드 (사용자별 고유 코드)
var referralCode = "{{custom_attribute.${referral_code}}}";
```

#### 통계 표시 설정
```javascript
var statsConfig = {
    showStats: true,           // 통계 표시 여부
    friendsCount: 3,           // 정적 값
    // friendsCount: "{{custom_attribute.${referral_count}}}", // Liquid
    rewardsEarned: "15,000₩"   // 정적 값
    // rewardsEarned: "{{custom_attribute.${referral_rewards}}}₩" // Liquid
};
```

#### 공유 버튼 설정
```javascript
var shareConfig = {
    shareUrl: "athlerab://invite",
    linkType: "deeplink",  // "deeplink" 또는 "web"
    shareMessage: "나의 추천 코드로 가입하고 5,000₩ 받으세요! 코드: " + referralCode
};
```

### 작동 방식

1. **코드 표시**: 사용자별 추천 코드 표시 (정적 또는 Liquid)
2. **복사 기능**:
   - 최신 Clipboard API 사용
   - 미지원 브라우저는 폴백 방식 (execCommand)
   - 복사 성공 시 버튼 색상 변경 + 텍스트 변경
3. **통계 표시**: 초대한 친구 수, 받은 리워드 표시
4. **공유 기능**:
   - Web Share API 지원 시: 네이티브 공유 시트
   - 미지원 시: URL 직접 열기
5. **이벤트 추적**: 조회, 복사, 공유 모두 Braze 이벤트 로깅

### 커스텀 이벤트

| 이벤트명 | 트리거 시점 | 속성 |
|----------|-------------|------|
| `referral_code_viewed` | 코드 표시됨 | 없음 |
| `referral_code_copied` | 코드 복사됨 | `referral_code`: 복사된 코드 |
| `referral_share_click` | 공유 버튼 클릭 | `referral_code`: 공유할 코드 |

### 클릭 추적 버튼 ID

| 버튼 ID | 설명 |
|---------|------|
| `close_button` | 닫기 버튼 클릭 |
| `close_overlay` | 오버레이 배경 클릭 |
| `copy_button` | 코드 복사 버튼 클릭 |
| `share_button` | 공유 버튼 클릭 |

### 사용 사례

- **추천 프로그램**: 사용자가 친구 초대 시 리워드 제공
- **바이럴 성장**: 코드 공유로 신규 유저 유입
- **앱 초대**: 앱 다운로드 및 회원가입 유도
- **프로모션 공유**: 특별 할인 코드 배포
- **이벤트 참여**: 이벤트 초대 코드 생성
- **커뮤니티 빌딩**: 사용자 간 연결 강화

### AI 커스터마이징 예시

AI에게 추천 코드 템플릿 수정 요청:

```
"추천 코드를 Liquid 변수 {{custom_attribute.${my_referral_code}}}로 바꿔줘"
"통계를 숨겨줘"
"친구 수와 리워드를 Liquid 변수로 동적으로 표시하게 바꿔줘"
"공유 메시지를 '같이 혜택받자! 내 코드: XXX'로 바꿔줘"
"아이콘을 🎉로 바꿔줘"
"그라데이션 색상을 파란색 계열로 바꿔줘"
"리워드 텍스트를 '친구 초대 시 10,000P 지급!'으로 바꿔줘"
```

### 클립보드 API 지원

템플릿은 두 가지 복사 방식을 지원합니다:

| 방식 | 지원 환경 | 우선순위 |
|------|-----------|----------|
| **Clipboard API** | 최신 브라우저 (iOS 13.4+, Chrome 63+) | 1순위 |
| **execCommand 폴백** | 레거시 브라우저 | 2순위 폴백 |

두 방식 모두 실패 시 사용자에게 수동 복사 안내 메시지 표시.

### Web Share API 통합

공유 버튼은 네이티브 공유 기능을 우선 사용:

**지원 환경:**
- iOS Safari 12+
- Android Chrome 61+
- 모바일 환경에서 네이티브 공유 시트 표시

**미지원 환경:**
- 데스크톱 브라우저 (일부 예외)
- 폴백: 직접 URL 열기

### Liquid 변수 활용

#### 동적 추천 코드
```javascript
var referralCode = "{{custom_attribute.${referral_code}}}";
```

#### 동적 통계
```javascript
var statsConfig = {
    showStats: true,
    friendsCount: "{{custom_attribute.${referral_count}}}",
    rewardsEarned: "{{custom_attribute.${referral_rewards}}}₩"
};
```

#### 동적 공유 URL
```javascript
var shareConfig = {
    shareUrl: "athlerab://invite?code={{custom_attribute.${referral_code}}}",
    linkType: "deeplink",
    shareMessage: "코드: {{custom_attribute.${referral_code}}}"
};
```

### 추천 프로그램 구현 팁

1. **고유 코드 생성**:
   - 백엔드에서 사용자별 고유 코드 생성
   - Braze 커스텀 속성에 저장
   - Liquid로 인앱 메시지에 주입

2. **통계 추적**:
   - 추천 성공 시 `referral_count` 속성 증가
   - 리워드 지급 시 `referral_rewards` 속성 업데이트
   - 통계를 인앱 메시지에 실시간 표시

3. **이벤트 기반 트리거**:
   - 첫 로그인 시: 추천 코드 안내
   - 친구 초대 성공 시: 축하 메시지 + 통계 업데이트
   - 리워드 도달 시: 리워드 사용 유도

4. **세그멘테이션**:
   - 추천 코드 복사한 사용자
   - 친구 초대 0명 vs 1명 이상 vs 3명 이상
   - 리워드 미사용 vs 사용

### 모범 사례

1. **명확한 혜택 제시**: "친구 초대 시 5,000₩" 같은 구체적 리워드
2. **복사 용이성**: 코드 자동 복사로 마찰 최소화
3. **즉각적 피드백**: 복사 성공 시 시각적 확인
4. **통계 표시**: 사용자 성과를 보여줘 동기 부여
5. **공유 간편화**: 네이티브 공유 시트로 다양한 채널 지원
6. **A/B 테스트**: 리워드 금액, 문구, 디자인 테스트

### 추천 프로그램 분석 지표

Braze에서 추적할 핵심 지표:

| 지표 | 설명 | Braze 활용 |
|------|------|-----------|
| **조회율** | `referral_code_viewed` 이벤트 수 | 캠페인 도달률 |
| **복사율** | `referral_code_copied` / 조회 | 참여도 측정 |
| **공유율** | `referral_share_click` / 조회 | 바이럴 잠재력 |
| **전환율** | 실제 친구 가입 / 코드 복사 | ROI 측정 |
| **리워드 효율** | 지급 리워드 / 신규 유저 | 프로그램 수익성 |

### 브라우저 지원

- ✅ iOS Safari 12+ (Clipboard API, Web Share API)
- ✅ Android Chrome 80+ (Clipboard API, Web Share API)
- ✅ 레거시 브라우저 (execCommand 폴백)
- ✅ 모든 최신 모바일 브라우저

### 알려진 제한사항

- Clipboard API는 HTTPS 필수 (로컬 테스트 시 제한)
- Web Share API는 사용자 제스처 필요 (버튼 클릭 등)
- 일부 구형 브라우저에서 복사 실패 가능 (수동 복사 안내)

### 팁

1. **초기 세팅**: Braze에서 `referral_code` 커스텀 속성 미리 생성
2. **테스트**: 다양한 기기에서 복사 및 공유 기능 테스트
3. **폴백 준비**: 복사 실패 시 코드를 수동 선택할 수 있도록 `user-select: all` 적용
4. **분석 활용**: 복사 후 실제 가입 전환율 추적으로 프로그램 최적화
5. **리워드 노출**: 받은 리워드를 눈에 띄게 표시하여 참여 동기 부여
6. **공유 독려**: 공유 시 추가 보너스 제공 등 인센티브 설계
