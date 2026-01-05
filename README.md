# Braze Custom HTML In-App Message Templates

### 📱 개요

Braze용 프로덕션 레디 커스텀 HTML 인앱 메시지 템플릿입니다. 최신 브리지 통합(`brazeBridge` + `ab.BridgeReady`), 반응형 디자인, 쉬운 커스터마이징 등 모범 사례를 적용했습니다.

### ⚠️ 중요 안내사항

**프로덕션 사용 전 반드시 테스트하세요!** 다음 요인에 따라 템플릿 조정이 필요할 수 있습니다:
- 앱의 WebView 구현 방식
- 웹사이트 보안 정책 (CSP, CORS)
- 모바일 OS 버전 및 브라우저 기능
- Braze SDK 버전 및 설정

캠페인 런칭 전, 반드시 Braze 테스트 모드에서 실제 기기(iOS/Android)로 테스트할 것을 강력히 권장합니다.

### 🤖 AI로 커스터마이징하기 (Claude Code)

이 템플릿들은 Claude Code 같은 AI 어시스턴트로 쉽게 커스터마이징할 수 있도록 설계되었습니다. 모든 커스터마이징 가능한 섹션은 AI가 이해하기 쉽도록 한국어 `/* CUSTOMIZABLE */` 주석으로 표시되어 있습니다.

**사용 가능한 프롬프트 예시:**

```
"버튼 텍스트를 '시작하기'로 바꾸고 URL 업데이트해줘"
"확률이 다른 프라이즈 등급 3개 더 추가해줘"
"스크래치 임계값을 50% 대신 60%로 만들어줘"
"모든 색상을 우리 브랜드 컬러(#FF6B6B)로 바꿔줘"
"24시간 남은 카운트다운 타이머 추가해줘"
```

**AI 활용 커스터마이징 팁:**
1. **구체적으로 요청** - 정확한 값(색상, URL, 텍스트) 제공
2. **점진적 테스트** - 한 번에 하나씩 변경하고 테스트
3. **맥락 제공** - 브랜드 가이드라인이나 디자인 요구사항 공유
4. **설명 요청** - AI에게 각 변경사항이 무엇을 하는지 설명 요청
5. **검증 요청** - AI에게 잠재적 문제 검토 요청

### 🏢 소개

이 템플릿은 모바일 마케팅 및 리텐션 전략 전문 그로스 컨설팅 스타트업 **[리텐션 주식회사](https://retn.kr/)**에서 제작 및 관리합니다.

**제작자**: 심규섭, 리텐션 주식회사 대표
- 2016년부터 Braze를 사용해온 비개발자
- 실제 캠페인 경험을 바탕으로 템플릿 제작
- 마케터를 위한 실용적이고 프로덕션 레디 솔루션에 집중

**🇰🇷 Braze 한국 클라이언트 환영합니다!**

Braze를 사용하는 한국 기업과의 협업을 항상 환영합니다. 다음 분야에 도움이 필요하시면 연락주세요:
- Braze 구현 및 최적화
- 커스텀 인앱 메시지 개발
- 그로스 마케팅 전략
- 리텐션 및 인게이지먼트 캠페인

**연락처:**
- 🌐 웹사이트: [retn.kr](https://retn.kr/)
- 📅 미팅 예약: [30분 무료 상담](https://tidycal.com/simgyusup/30m)

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
