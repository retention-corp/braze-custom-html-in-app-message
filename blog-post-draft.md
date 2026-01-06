# 비개발자가 AI와 함께 Braze 템플릿을 오픈소스로 만들기까지

> "굳이 SaaS를 만들 필요 없이, 내가 직접 구현할 수 있는 시대가 왔다."

## 🎯 TL;DR

- 비개발자(CEO)가 Claude Code로 9개의 프로덕션 레디 Braze 템플릿 제작
- CLAUDE.md에 공식 문서를 넣어 best practice 자동 준수
- 워킹 코드 하나로 수십 개 배리에이션을 AI가 생성
- 1~2일만에 워킹 프로토타입 → 테스트 → 프로덕션 배포
- GitHub 오픈소스 공개: https://github.com/retention-corp/braze-custom-html-in-app-message

---

## 📖 이야기의 시작

2016년부터 Braze를 사용해왔지만, 나는 개발자가 아니다.

리텐션 주식회사 대표로서 수십 개의 클라이언트 캠페인을 운영하면서 항상 부딪혔던 문제가 있다:

> "이런 인앱 메시지 템플릿이 있으면 좋겠는데..."

Braze의 Drag & Drop 에디터는 편리하지만 제한적이고, Custom HTML은 자유롭지만 개발자가 필요하다. Hippo Tools 같은 서드파티 도구들은 비싸거나 내가 원하는 기능이 정확히 없었다.

그래서 결심했다: **"내가 직접 만들어보자."**

---

## 🤖 AI Coding Agent와의 협업

### Phase 1: 첫 번째 워킹 프로토타입

Claude Code를 열고 이렇게 시작했다:

```
"Braze용 스크래치 카드 인앱 메시지 만들어줘.
확률 기반으로 프라이즈를 선택하고,
각 프라이즈마다 다른 커스텀 이벤트를 로깅해야 해."
```

놀랍게도, **30분 만에 첫 프로토타입이 나왔다.**

물론 완벽하지 않았다. Canvas가 제대로 안 그려지고, 터치 이벤트가 작동하지 않았다. 하지만 중요한 건, **워킹 코드의 뼈대가 생겼다는 것**이다.

### Phase 2: 디버깅과 최적화

```
"스크래치가 작동 안 해. 직접 테스트해봐."
```

Claude는 Playwright를 사용해 실제로 브라우저를 열고 스크래치를 시도했다. 그리고 발견했다:

```javascript
// ❌ 작동 안 함
ctx.globalCompositeOperation = 'destination-out';
ctx.arc(x, y, 30, 0, Math.PI * 2);
ctx.fill();

// ✅ 작동함
ctx.fillStyle = 'rgba(0, 0, 0, 1)'; // 이 한 줄이 필요했다!
ctx.globalCompositeOperation = 'destination-out';
ctx.arc(x, y, 30, 0, Math.PI * 2);
ctx.fill();
```

이런 미묘한 Canvas API 버그는 검색해도 잘 안 나오는데, AI가 직접 테스트하면서 찾아냈다.

### Phase 3: 배리에이션 대량 생성

**워킹 코드 하나가 생기면, 거기서부터는 쉽다.**

```
"이거 카드 뒤집기 버전으로 바꿔줘"
"이거 설문조사로 만들어줘"
"이거 캐러셀 3개로 늘려줘"
"모바일 safe area 처리해줘"
```

하루 만에 9개의 템플릿이 완성되었다:
- Modal (Single, Carousel, Survey, Scratch Card, Card Flip)
- Fullscreen (Single, Carousel)
- Bottom Sheet (Single, Carousel)

---

## 📚 CLAUDE.md의 힘: Best Practice 자동 준수

프로젝트를 시작하면서 가장 먼저 한 일은 `CLAUDE.md` 파일을 작성한 것이다.

### CLAUDE.md에 넣은 것들:

1. **Braze Bridge API 공식 문서**
   ```markdown
   ## CRITICAL: Braze Bridge API Migration

   ❌ WRONG (deprecated):
   appboyBridge.logClick();

   ✅ CORRECT (required):
   window.addEventListener("ab.BridgeReady", function() {
       brazeBridge.logClick();
   }, false);
   ```

2. **모바일 Safe Area 핸들링**
   ```markdown
   ## Mobile Safe Area Handling (CRITICAL)

   iOS devices with notches require:
   ```css
   padding-bottom: calc(20px + env(safe-area-inset-bottom, 20px));
   ```

3. **파일 크기 제약**
   ```markdown
   ## Braze-Specific Constraints

   | Constraint | Detail |
   |------------|--------|
   | File size  | <100 KB (Braze rejects larger files) |
   | CSS        | Must be inline |
   | Images     | External URLs only |
   ```

4. **Git 커밋 규칙**
   ```markdown
   ## Git Safety Protocol
   - NEVER force push to main/master
   - NEVER run git commit --amend unless...
   ```

### 결과: AI가 알아서 Best Practice 준수

놀라운 점은, **내가 일일이 지시하지 않아도 AI가 CLAUDE.md를 읽고 자동으로 베스트 프랙티스를 적용한다**는 것이다.

- 모든 템플릿에서 자동으로 `brazeBridge` + `ab.BridgeReady` 사용
- iOS safe area 자동 처리
- 파일 크기 초과하면 자동으로 최적화 제안
- Git 커밋 메시지도 컨벤션 준수

**CLAUDE.md는 나의 "리모트 개발팀 온보딩 문서"였다.**

---

## 💡 핵심 인사이트: SaaS vs. DIY

### 2024년 이전의 세상:

```
문제 발견 → 개발자 고용/외주 →
3~6개월 개발 → 비용 수천만원 →
유지보수 계속 필요
```

또는

```
문제 발견 → SaaS 구독 →
월 $99~$999 지불 →
내가 원하는 기능 없음 →
결국 다른 솔루션 찾기
```

### 2025년 AI 시대:

```
문제 발견 → Claude Code 열기 →
1~2일 만에 워킹 프로토타입 →
테스트 → 프로덕션 배포 →
필요하면 언제든 수정 가능
```

**굳이 SaaS를 만들거나 구독할 필요 없이, 내가 직접 구현 가능한 시대가 왔다.**

물론 한계는 있다:
- 모든 환경에서 완벽하게 작동할까? 모르겠다.
- 엣지 케이스는? 발견하면 그때그때 AI와 함께 고친다.
- 보안은? CLAUDE.md에 보안 가이드라인을 넣어두면 AI가 지킨다.

하지만 중요한 건, **내가 직접 코드를 소유하고, 원할 때마다 수정할 수 있다**는 것이다.

---

## 🚀 리텐션의 AI-Augmented 워크플로우

우리 회사는 이제 모든 개발을 이렇게 한다:

### 1. GCP + Vertex AI + Claude Code

```
내 머릿속 아이디어
→ Claude Code
→ Google Cloud Platform 배포
→ Vertex AI 통합
→ 바이브 코딩으로 빠른 프로토타입
```

### 2. 개발자 커뮤니케이션 시간 단축

**Before AI (2023년):**
- 요구사항 정리: 2일
- 개발자와 미팅: 1일
- 개발 대기: 1주일
- 피드백과 수정: 1주일
- **총 3~4주**

**After AI (2025년):**
- Claude와 대화: 30분
- 워킹 프로토타입: 1일
- 테스트와 수정: 1일
- 프로덕션 배포: 1일
- **총 2~3일**

### 3. 실제 프로젝트 타임라인

이번 Braze 템플릿 프로젝트:
- **Day 1**: Scratch card 첫 프로토타입 + Canvas 버그 수정
- **Day 2**: 9개 템플릿 완성 + GitHub 레포 구축
- **Day 3**: 문서화 (영어/한국어) + 오픈소스 공개

**개발자를 고용했다면? 최소 2~3주는 걸렸을 것이다.**

---

## 🎨 나의 사고 흐름 (Thesis)

### Thesis 1: "코드는 대화의 결과물이다"

더 이상 코드를 "작성"하지 않는다. 코드는 내가 AI와 나눈 **대화의 결과물**이다.

```
나: "스크래치 카드 만들어줘"
AI: [코드 생성]
나: "안 돼. 직접 테스트해봐"
AI: [테스트 후] "fillStyle 추가했어요"
나: "좋아. 이제 확률 기반으로 바꿔줘"
AI: [코드 수정]
```

이 과정에서 나는:
- 프로그래밍 언어를 몰라도 된다
- 알고리즘을 직접 짤 필요 없다
- 대신 **내가 원하는 것을 명확하게 설명**하면 된다

### Thesis 2: "CLAUDE.md는 나의 확장된 뇌"

CLAUDE.md에 적어둔 것들:
- Braze API 베스트 프랙티스
- 과거에 겪었던 버그와 해결책
- 회사의 코딩 컨벤션
- 보안 가이드라인

이것들이 **나의 암묵지(Tacit Knowledge)**였다. 이제는 CLAUDE.md에 명시지로 변환되어, AI가 나를 대신해 지킨다.

**마치 나의 뇌를 확장한 것 같다.**

### Thesis 3: "오픈소스는 레버리지다"

이번에 만든 템플릿을 오픈소스로 공개한 이유:

1. **내 회사의 전문성 증명**
   - "리텐션은 Braze를 이렇게 잘 다룹니다"
   - 코드가 곧 포트폴리오

2. **커뮤니티로부터의 피드백**
   - 버그 리포트
   - 새로운 아이디어
   - 무료 테스터들

3. **미래 고객 확보**
   - Braze 사용자들이 이 템플릿을 쓰다가
   - "더 복잡한 건 리텐션에 맡겨야겠네"
   - 인바운드 리드 생성

**오픈소스는 마케팅이고, 세일즈 퍼널이다.**

### Thesis 4: "80%의 완성도로 100%의 가치"

이 템플릿들이 완벽할까? 아니다.
- 모든 브라우저에서 테스트했나? 아니다.
- 엣지 케이스를 다 처리했나? 아니다.
- 프로덕션 그레이드인가? **충분히 그렇다.**

하지만 중요한 건:
- 80%의 완성도로 시작해서
- 실제 사용자 피드백을 받고
- AI와 함께 나머지 20%를 채워간다

**Perfect is the enemy of good.** AI 시대에는 더욱 그렇다.

---

## 📊 결과물

### GitHub 오픈소스 공개

**Repository**: https://github.com/retention-corp/braze-custom-html-in-app-message

**포함된 것들:**
- 9개의 프로덕션 레디 템플릿
- 완전한 한국어 문서화
- AI-Friendly 주석 (Claude Code 최적화)
- 실전에서 발견하고 수정한 버그 픽스
- CLAUDE.md (베스트 프랙티스 가이드)

### 독창적인 부분 (vs. 기존 솔루션)

| 기능 | 오픈소스 | Braze 공식 | Hippo Tools | **우리 템플릿** |
|------|----------|-----------|-------------|--------------|
| Scratch Card | ✅ | ❌ | ✅ (비공개) | ✅ |
| 확률 기반 프라이즈 | ❌ | ❌ | ❓ | ✅ |
| Braze 통합 | ❌ | 제한적 | ✅ | ✅ |
| AI 친화 주석 | ❌ | ❌ | ❌ | ✅ |
| 한국어 지원 | ❌ | ❌ | ❌ | ✅ |
| 오픈소스 | ✅ | 부분적 | ❌ | ✅ |

### 커뮤니티 반응 (예상)

아직 공개 직후지만, 기대하는 것들:
- Braze 한국 사용자들의 피드백
- 버그 리포트 및 개선 제안
- 새로운 템플릿 요청
- 협업 문의

---

## 🎯 핵심 교훈

### 1. 비개발자도 할 수 있다

나는 JSON이 뭔지는 알지만, JavaScript를 처음부터 끝까지 짤 수는 없다. 하지만 **AI와 대화하는 능력**만 있으면 충분하다.

### 2. CLAUDE.md는 필수다

공식 문서, 베스트 프랙티스, 회사 규칙을 CLAUDE.md에 넣어두면, AI가 자동으로 지킨다. **이것이 AI 시대의 온보딩 문서다.**

### 3. 워킹 코드 하나가 시작점

완벽한 템플릿 하나를 만들려고 하지 말자. 대충 작동하는 코드 하나를 만들고, 거기서 무한히 배리에이션을 만들면 된다.

### 4. 80%로 시작해서 피드백으로 완성

완벽을 추구하지 말고, 빠르게 공개하고, 사용자 피드백을 받고, AI와 함께 개선하자.

### 5. SaaS가 아니라 DIY

월 $999짜리 SaaS 구독하지 말고, 2일 만에 내가 원하는 대로 만들자. 코드는 내가 소유한다.

---

## 🚀 다음 단계

### 1. 커뮤니티 참여 유도

- GitHub Issues로 버그 리포트 받기
- Discussions로 새로운 아이디어 수집
- Pull Request 환영

### 2. 더 많은 템플릿 추가

유저들이 요청하는 템플릿들:
- Countdown Timer
- Video Embed
- Multi-Step Form
- NPS Survey

**하루면 만들 수 있다. AI와 함께.**

### 3. 라이브러리화

나중에는 npm 패키지로 만들어서, 다른 플랫폼에서도 사용할 수 있게 만들 수도 있다.

---

## 💬 리텐션과 함께하기

**Braze를 사용하는 한국 기업이신가요?**

우리는 이런 일을 합니다:
- Braze 구현 및 최적화
- 커스텀 인앱 메시지 개발
- 그로스 마케팅 전략
- AI-Augmented 워크플로우 컨설팅

**연락처:**
- 🌐 웹사이트: [retn.kr](https://retn.kr/)
- 📅 미팅 예약: [30분 무료 상담](https://tidycal.com/simgyusup/30m)
- 💻 GitHub: [retention-corp](https://github.com/retention-corp)

---

## 📝 마무리하며

2016년에 Braze를 처음 써보고, "이런 기능 있으면 좋겠는데" 하고 바랐던 것들을 2025년에 AI와 함께 직접 만들었다.

**개발자 없이.**
**2~3일 만에.**
**오픈소스로.**

이게 가능한 시대다.

당신도 할 수 있다. 아이디어만 있다면, AI가 코드를 짜준다. CLAUDE.md에 당신의 지식을 넣어두면, AI가 베스트 프랙티스를 지킨다.

**굳이 SaaS를 만들거나, 개발자를 고용하거나, 월 구독료를 낼 필요 없다.**

**그냥 만들면 된다. AI와 함께.**

---

**#Braze #AIAugmented #OpenSource #NoCode #ClaudeCode #RetentionMarketing**

---

> 이 포스트가 도움이 되었다면, GitHub에서 ⭐️ 눌러주세요!
> https://github.com/retention-corp/braze-custom-html-in-app-message
