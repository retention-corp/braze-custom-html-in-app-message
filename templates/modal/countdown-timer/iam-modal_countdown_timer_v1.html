<!doctype html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
            overflow: hidden;
        }
        #overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.75);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 9999;
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        #overlay.show {
            opacity: 1;
        }
        .modal {
            position: relative;
            background: #ffffff;
            border-radius: 16px;
            max-width: 450px;
            width: 90%;
            padding: 30px 20px;
            text-align: center;
            transform: scale(0.9);
            transition: transform 0.3s ease;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
        }
        #overlay.show .modal {
            transform: scale(1);
        }
        .close-button {
            position: absolute;
            top: 12px;
            right: 12px;
            width: 28px;
            height: 28px;
            background: transparent;
            border: none;
            cursor: pointer;
            font-size: 24px;
            color: #999;
            line-height: 1;
            padding: 0;
            transition: color 0.2s;
        }
        .close-button:hover {
            color: #333;
        }
        .title {
            font-size: 22px;
            font-weight: 700;
            color: #222;
            margin-bottom: 10px;
        }
        .description {
            font-size: 15px;
            color: #666;
            margin-bottom: 25px;
            line-height: 1.5;
        }
        .countdown-container {
            background: #f8f8f8;
            border-radius: 12px;
            padding: 20px 15px;
            margin-bottom: 25px;
            transition: background 0.5s ease;
        }
        .countdown-container.urgent-medium {
            background: #fff9e6;
        }
        .countdown-container.urgent-high {
            background: #ffe6e6;
        }
        .countdown-label {
            font-size: 13px;
            color: #999;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 12px;
        }
        .countdown-units {
            display: flex;
            justify-content: center;
            gap: 12px;
        }
        .countdown-unit {
            flex: 1;
            max-width: 70px;
        }
        .countdown-value {
            font-size: 32px;
            font-weight: 700;
            color: #222;
            line-height: 1;
            transition: color 0.5s ease;
        }
        .countdown-container.urgent-medium .countdown-value {
            color: #ff9800;
        }
        .countdown-container.urgent-high .countdown-value {
            color: #f44336;
        }
        .countdown-text {
            font-size: 11px;
            color: #999;
            text-transform: uppercase;
            margin-top: 6px;
            letter-spacing: 0.5px;
        }
        .cta-button {
            display: block;
            width: 100%;
            padding: 16px 24px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: #ffffff;
            font-size: 16px;
            font-weight: 600;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            text-decoration: none;
            transition: transform 0.2s, box-shadow 0.2s;
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
        }
        .cta-button:active {
            transform: scale(0.98);
        }
        .expired-message {
            display: none;
            font-size: 18px;
            font-weight: 600;
            color: #f44336;
            padding: 20px;
        }
        .expired-message.show {
            display: block;
        }
        .countdown-container.expired {
            display: none;
        }
    </style>
</head>
<body>
    <div id="overlay">
        <div class="modal">
            <button class="close-button" id="close-button">&times;</button>

            <div class="title" id="title">⏰ 타임 세일 진행중!</div>
            <div class="description" id="description">지금 바로 혜택을 받으세요!</div>

            <div class="countdown-container" id="countdown-container">
                <div class="countdown-label">남은 시간</div>
                <div class="countdown-units">
                    <div class="countdown-unit">
                        <div class="countdown-value" id="days">00</div>
                        <div class="countdown-text">일</div>
                    </div>
                    <div class="countdown-unit">
                        <div class="countdown-value" id="hours">00</div>
                        <div class="countdown-text">시간</div>
                    </div>
                    <div class="countdown-unit">
                        <div class="countdown-value" id="minutes">00</div>
                        <div class="countdown-text">분</div>
                    </div>
                    <div class="countdown-unit">
                        <div class="countdown-value" id="seconds">00</div>
                        <div class="countdown-text">초</div>
                    </div>
                </div>
            </div>

            <div class="expired-message" id="expired-message">
                ⏰ 이벤트가 종료되었습니다
            </div>

            <button class="cta-button" id="cta-button">지금 확인하기</button>
        </div>
    </div>

    <script>
        /* ============================================
           CUSTOMIZABLE: 기본 설정
           ============================================
           AI 요청 예시:
           - "타이틀을 '플래시 세일!'로 바꿔줘"
           - "설명 텍스트를 '오늘만 특가'로 바꿔줘"
           - "버튼 텍스트를 '혜택 받기'로 바꿔줘"
        */
        var config = {
            title: "⏰ 타임 세일 진행중!",
            description: "지금 바로 혜택을 받으세요!",
            ctaButtonText: "지금 확인하기",
            expiredMessage: "⏰ 이벤트가 종료되었습니다"
        };

        /* ============================================
           CUSTOMIZABLE: 카운트다운 설정
           ============================================
           AI 요청 예시:
           - "종료 시간을 2026년 1월 10일 23:59로 설정해줘"
           - "자동 닫기 기능을 켜줘"
           - "긴급 상태 임계값을 12시간으로 바꿔줘"

           targetDate: 카운트다운 종료 날짜/시간
           - 형식: "YYYY-MM-DD HH:MM:SS" (24시간 형식)
           - 예: "2026-01-10 23:59:59"

           autoCloseOnExpiry: 종료 시 자동으로 메시지 닫기
           - true = 자동 닫기
           - false = 열린 상태 유지

           urgencyThresholds: 긴급도 색상 변경 임계값
           - medium: 중간 긴급 상태 (노란색) - 초 단위
           - high: 높은 긴급 상태 (빨간색) - 초 단위
        */
        var countdownConfig = {
            targetDate: "2026-01-10 23:59:59",  // 종료 날짜/시간
            autoCloseOnExpiry: false,            // 종료 시 자동 닫기
            urgencyThresholds: {
                medium: 24 * 60 * 60,  // 24시간 (86400초)
                high: 6 * 60 * 60      // 6시간 (21600초)
            }
        };

        /* ============================================
           CUSTOMIZABLE: CTA 버튼 링크 설정
           ============================================
           AI 요청 예시:
           - "딥링크를 athlerab://sale/winter로 바꿔줘"
           - "웹 링크로 변경해줘: https://example.com/sale"

           ctaUrl: 클릭 시 이동할 URL
           linkType: 링크 타입
           - "deeplink" = 앱 내부 딥링크
           - "web" = 브라우저에서 열기
        */
        var ctaUrl = "athlerab://promotion/timesale";
        var linkType = "deeplink";  // "deeplink" 또는 "web"

        /* ============================================
           CUSTOMIZABLE: Braze 이벤트 설정
           ============================================
           AI 요청 예시:
           - "이벤트명을 'flash_sale_viewed'로 바꿔줘"
           - "만료 이벤트명을 'timer_expired'로 바꿔줘"
        */
        var eventNames = {
            timerView: "countdown_timer_viewed",
            timerExpire: "countdown_timer_expired",
            ctaClick: "countdown_cta_click"
        };

        // ============================================
        // 내부 로직 (수정 불필요)
        // ============================================

        var overlay = document.getElementById("overlay");
        var modal = overlay.querySelector(".modal");
        var closeButton = document.getElementById("close-button");
        var ctaButton = document.getElementById("cta-button");
        var countdownContainer = document.getElementById("countdown-container");
        var expiredMessageEl = document.getElementById("expired-message");

        var daysEl = document.getElementById("days");
        var hoursEl = document.getElementById("hours");
        var minutesEl = document.getElementById("minutes");
        var secondsEl = document.getElementById("seconds");

        var countdownInterval;
        var isExpired = false;

        // 설정 적용
        document.getElementById("title").textContent = config.title;
        document.getElementById("description").textContent = config.description;
        ctaButton.textContent = config.ctaButtonText;
        expiredMessageEl.textContent = config.expiredMessage;

        // Braze Bridge 초기화
        window.addEventListener("ab.BridgeReady", function() {
            try {
                brazeBridge.logCustomEvent(eventNames.timerView);
            } catch(e) {
                console.error("Braze error:", e);
            }
        }, false);

        // 카운트다운 계산 함수
        function updateCountdown() {
            var now = new Date().getTime();
            var target = new Date(countdownConfig.targetDate).getTime();
            var distance = target - now;

            if (distance < 0) {
                clearInterval(countdownInterval);
                handleExpiry();
                return;
            }

            var days = Math.floor(distance / (1000 * 60 * 60 * 24));
            var hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            var minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
            var seconds = Math.floor((distance % (1000 * 60)) / 1000);

            daysEl.textContent = String(days).padStart(2, "0");
            hoursEl.textContent = String(hours).padStart(2, "0");
            minutesEl.textContent = String(minutes).padStart(2, "0");
            secondsEl.textContent = String(seconds).padStart(2, "0");

            // 긴급도에 따른 색상 변경
            var totalSeconds = distance / 1000;
            countdownContainer.classList.remove("urgent-medium", "urgent-high");

            if (totalSeconds <= countdownConfig.urgencyThresholds.high) {
                countdownContainer.classList.add("urgent-high");
            } else if (totalSeconds <= countdownConfig.urgencyThresholds.medium) {
                countdownContainer.classList.add("urgent-medium");
            }
        }

        // 만료 처리
        function handleExpiry() {
            isExpired = true;
            countdownContainer.classList.add("expired");
            expiredMessageEl.classList.add("show");
            ctaButton.style.display = "none";

            window.addEventListener("ab.BridgeReady", function() {
                try {
                    brazeBridge.logCustomEvent(eventNames.timerExpire);
                } catch(e) {}
            }, false);

            if (countdownConfig.autoCloseOnExpiry) {
                setTimeout(function() {
                    closeMessage();
                }, 2000);
            }
        }

        // 메시지 닫기
        function closeMessage() {
            overlay.classList.remove("show");
            setTimeout(function() {
                window.addEventListener("ab.BridgeReady", function() {
                    try {
                        brazeBridge.closeMessage();
                    } catch(e) {}
                }, false);
            }, 300);
        }

        // 닫기 버튼
        closeButton.onclick = function() {
            window.addEventListener("ab.BridgeReady", function() {
                try {
                    brazeBridge.logClick("close_button");
                } catch(e) {}
            }, false);
            closeMessage();
        };

        // 오버레이 클릭
        overlay.onclick = function(e) {
            if (e.target === overlay) {
                window.addEventListener("ab.BridgeReady", function() {
                    try {
                        brazeBridge.logClick("close_overlay");
                    } catch(e) {}
                }, false);
                closeMessage();
            }
        };

        // CTA 버튼
        ctaButton.onclick = function() {
            if (isExpired) return;

            window.addEventListener("ab.BridgeReady", function() {
                try {
                    brazeBridge.logClick("cta_button");
                    brazeBridge.logCustomEvent(eventNames.ctaClick);

                    if (linkType === "web") {
                        window.open(ctaUrl, "_blank");
                    } else {
                        window.location.href = ctaUrl;
                    }
                } catch(e) {}
            }, false);
        };

        // 초기화
        setTimeout(function() {
            overlay.classList.add("show");
            updateCountdown();
            countdownInterval = setInterval(updateCountdown, 1000);
        }, 300);
    </script>
</body>
</html>
