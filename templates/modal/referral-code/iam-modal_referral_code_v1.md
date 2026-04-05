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
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 20px;
            max-width: 400px;
            width: 90%;
            padding: 40px 25px;
            text-align: center;
            transform: scale(0.9);
            transition: transform 0.3s ease;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
            color: #ffffff;
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
            background: rgba(255, 255, 255, 0.2);
            border: none;
            border-radius: 50%;
            cursor: pointer;
            font-size: 20px;
            color: #ffffff;
            line-height: 1;
            padding: 0;
            transition: background 0.2s;
        }
        .close-button:hover {
            background: rgba(255, 255, 255, 0.3);
        }
        .icon {
            font-size: 48px;
            margin-bottom: 15px;
        }
        .title {
            font-size: 24px;
            font-weight: 700;
            margin-bottom: 10px;
        }
        .description {
            font-size: 15px;
            opacity: 0.9;
            margin-bottom: 25px;
            line-height: 1.5;
        }
        .code-container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 20px;
        }
        .code-label {
            font-size: 12px;
            color: #999;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 10px;
        }
        .code-display {
            font-size: 32px;
            font-weight: 700;
            color: #667eea;
            letter-spacing: 4px;
            margin-bottom: 15px;
            user-select: all;
            -webkit-user-select: all;
        }
        .copy-button {
            width: 100%;
            padding: 14px 20px;
            background: #667eea;
            color: #ffffff;
            font-size: 15px;
            font-weight: 600;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
        }
        .copy-button:active {
            transform: scale(0.98);
        }
        .copy-button.copied {
            background: #4caf50;
        }
        .copy-button .copy-text {
            display: inline-block;
            transition: all 0.3s;
        }
        .copy-button .copied-text {
            position: absolute;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);
            opacity: 0;
            transition: all 0.3s;
        }
        .copy-button.copied .copy-text {
            opacity: 0;
        }
        .copy-button.copied .copied-text {
            opacity: 1;
        }
        .stats-container {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-bottom: 20px;
        }
        .stat-item {
            text-align: center;
        }
        .stat-value {
            font-size: 28px;
            font-weight: 700;
            margin-bottom: 5px;
        }
        .stat-label {
            font-size: 13px;
            opacity: 0.8;
        }
        .share-button {
            display: block;
            width: 100%;
            padding: 16px 24px;
            background: rgba(255, 255, 255, 0.2);
            color: #ffffff;
            font-size: 16px;
            font-weight: 600;
            border: 2px solid rgba(255, 255, 255, 0.5);
            border-radius: 8px;
            cursor: pointer;
            text-decoration: none;
            transition: all 0.2s;
        }
        .share-button:active {
            transform: scale(0.98);
            background: rgba(255, 255, 255, 0.3);
        }
        .reward-text {
            font-size: 14px;
            opacity: 0.9;
            margin-top: 15px;
            line-height: 1.5;
        }
        .reward-text strong {
            font-weight: 700;
            font-size: 16px;
        }
    </style>
</head>
<body>
    <div id="overlay">
        <div class="modal">
            <button class="close-button" id="close-button">&times;</button>

            <div class="icon" id="icon">🎁</div>
            <div class="title" id="title">친구 초대하고<br>리워드 받기!</div>
            <div class="description" id="description">
                친구에게 추천 코드를 공유하고<br>함께 혜택을 받으세요
            </div>

            <div class="code-container">
                <div class="code-label">내 추천 코드</div>
                <div class="code-display" id="code-display">FRIEND2026</div>
                <button class="copy-button" id="copy-button">
                    <span class="copy-text">📋 코드 복사하기</span>
                    <span class="copied-text">✅ 복사 완료!</span>
                </button>
            </div>

            <div class="stats-container" id="stats-container">
                <div class="stat-item">
                    <div class="stat-value" id="friends-count">3</div>
                    <div class="stat-label">초대한 친구</div>
                </div>
                <div class="stat-item">
                    <div class="stat-value" id="rewards-count">15,000₩</div>
                    <div class="stat-label">받은 리워드</div>
                </div>
            </div>

            <button class="share-button" id="share-button">친구에게 공유하기</button>

            <div class="reward-text" id="reward-text">
                친구가 가입하면 <strong>5,000₩</strong> 적립!
            </div>
        </div>
    </div>

    <script>
        /* ============================================
           CUSTOMIZABLE: 기본 설정
           ============================================
           AI 요청 예시:
           - "타이틀을 '추천하고 보상받기!'로 바꿔줘"
           - "아이콘을 🎉로 바꿔줘"
           - "설명 텍스트를 바꿔줘"
        */
        var config = {
            icon: "🎁",
            title: "친구 초대하고<br>리워드 받기!",
            description: "친구에게 추천 코드를 공유하고<br>함께 혜택을 받으세요",
            copyButtonText: "📋 코드 복사하기",
            copiedButtonText: "✅ 복사 완료!",
            shareButtonText: "친구에게 공유하기",
            rewardText: "친구가 가입하면 <strong>5,000₩</strong> 적립!"
        };

        /* ============================================
           CUSTOMIZABLE: 추천 코드 설정
           ============================================
           AI 요청 예시:
           - "추천 코드를 WELCOME2026으로 바꿔줘"
           - "Liquid 변수로 동적 코드 사용하게 바꿔줘"

           referralCode: 추천 코드
           - 정적 코드: "FRIEND2026"
           - Liquid 변수: "{{custom_attribute.${referral_code}}}"
        */
        var referralCode = "FRIEND2026";  // 또는 Liquid: "{{custom_attribute.${referral_code}}}"

        /* ============================================
           CUSTOMIZABLE: 통계 표시 설정
           ============================================
           AI 요청 예시:
           - "통계를 숨겨줘"
           - "친구 수를 10명으로 바꿔줘"
           - "리워드를 30,000₩로 바꿔줘"

           showStats: 통계 표시 여부
           - true = 통계 표시
           - false = 통계 숨김

           friendsCount: 초대한 친구 수
           - 정적 값: 3
           - Liquid 변수: "{{custom_attribute.${referral_count}}}"

           rewardsEarned: 받은 리워드
           - 정적 값: "15,000₩"
           - Liquid 변수: "{{custom_attribute.${referral_rewards}}}₩"
        */
        var statsConfig = {
            showStats: true,           // 통계 표시 여부
            friendsCount: 3,           // 초대한 친구 수
            rewardsEarned: "15,000₩"   // 받은 리워드
        };

        /* ============================================
           CUSTOMIZABLE: 공유 버튼 설정
           ============================================
           AI 요청 예시:
           - "공유 링크를 https://app.example.com/invite로 바꿔줘"
           - "딥링크로 변경: myapp://invite"
           - "공유 메시지를 바꿔줘"

           shareUrl: 공유 버튼 클릭 시 이동할 URL
           - 웹 링크: "https://..."
           - 딥링크: "myapp://..."
           - Liquid: "myapp://invite?code={{custom_attribute.${referral_code}}}"

           linkType: 링크 타입
           - "web" = 브라우저에서 열기
           - "deeplink" = 앱에서 열기

           shareMessage: 공유할 메시지 (Web Share API용)
           - iOS/Android의 네이티브 공유 시트에 사용
        */
        var shareConfig = {
            shareUrl: "myapp://invite",
            linkType: "deeplink",  // "deeplink" 또는 "web"
            shareMessage: "나의 추천 코드로 가입하고 5,000₩ 받으세요! 코드: " + referralCode
        };

        /* ============================================
           CUSTOMIZABLE: Braze 이벤트 설정
           ============================================
           AI 요청 예시:
           - "이벤트명을 'referral_viewed'로 바꿔줘"
           - "복사 이벤트명을 'code_copied'로 바꿔줘"
        */
        var eventNames = {
            referralView: "referral_code_viewed",
            codeCopy: "referral_code_copied",
            shareClick: "referral_share_click"
        };

        // ============================================
        // 내부 로직 (수정 불필요)
        // ============================================

        var overlay = document.getElementById("overlay");
        var modal = overlay.querySelector(".modal");
        var closeButton = document.getElementById("close-button");
        var copyButton = document.getElementById("copy-button");
        var shareButton = document.getElementById("share-button");
        var codeDisplay = document.getElementById("code-display");
        var statsContainer = document.getElementById("stats-container");

        // 설정 적용
        document.getElementById("icon").innerHTML = config.icon;
        document.getElementById("title").innerHTML = config.title;
        document.getElementById("description").innerHTML = config.description;
        document.querySelector(".copy-text").textContent = config.copyButtonText;
        document.querySelector(".copied-text").textContent = config.copiedButtonText;
        shareButton.textContent = config.shareButtonText;
        document.getElementById("reward-text").innerHTML = config.rewardText;
        codeDisplay.textContent = referralCode;

        if (statsConfig.showStats) {
            document.getElementById("friends-count").textContent = statsConfig.friendsCount;
            document.getElementById("rewards-count").textContent = statsConfig.rewardsEarned;
        } else {
            statsContainer.style.display = "none";
        }

        // Braze Bridge 초기화
        window.addEventListener("ab.BridgeReady", function() {
            try {
                brazeBridge.logCustomEvent(eventNames.referralView);
            } catch(e) {
                console.error("Braze error:", e);
            }
        }, false);

        // 클립보드 복사 함수
        function copyToClipboard(text) {
            // Modern Clipboard API
            if (navigator.clipboard && navigator.clipboard.writeText) {
                return navigator.clipboard.writeText(text);
            }

            // Fallback for older browsers
            return new Promise(function(resolve, reject) {
                var textArea = document.createElement("textarea");
                textArea.value = text;
                textArea.style.position = "fixed";
                textArea.style.left = "-9999px";
                document.body.appendChild(textArea);
                textArea.focus();
                textArea.select();

                try {
                    var successful = document.execCommand("copy");
                    document.body.removeChild(textArea);
                    if (successful) {
                        resolve();
                    } else {
                        reject();
                    }
                } catch (err) {
                    document.body.removeChild(textArea);
                    reject(err);
                }
            });
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

        // 코드 복사 버튼
        copyButton.onclick = function() {
            copyToClipboard(referralCode)
                .then(function() {
                    copyButton.classList.add("copied");

                    window.addEventListener("ab.BridgeReady", function() {
                        try {
                            brazeBridge.logClick("copy_button");
                            brazeBridge.logCustomEvent(eventNames.codeCopy, {
                                referral_code: referralCode
                            });
                        } catch(e) {}
                    }, false);

                    setTimeout(function() {
                        copyButton.classList.remove("copied");
                    }, 2000);
                })
                .catch(function(err) {
                    console.error("Copy failed:", err);
                    alert("코드 복사에 실패했습니다. 수동으로 복사해주세요.");
                });
        };

        // 공유 버튼
        shareButton.onclick = function() {
            window.addEventListener("ab.BridgeReady", function() {
                try {
                    brazeBridge.logClick("share_button");
                    brazeBridge.logCustomEvent(eventNames.shareClick, {
                        referral_code: referralCode
                    });

                    // Web Share API 시도 (모바일 네이티브 공유)
                    if (navigator.share) {
                        navigator.share({
                            title: "친구 초대 코드",
                            text: shareConfig.shareMessage,
                            url: shareConfig.shareUrl
                        }).catch(function(err) {
                            // 사용자가 공유 취소한 경우 무시
                        });
                    } else {
                        // Web Share API 미지원 시 링크 열기
                        if (shareConfig.linkType === "web") {
                            window.open(shareConfig.shareUrl, "_blank");
                        } else {
                            window.location.href = shareConfig.shareUrl;
                        }
                    }
                } catch(e) {
                    console.error("Share error:", e);
                }
            }, false);
        };

        // 초기화
        setTimeout(function() {
            overlay.classList.add("show");
        }, 300);
    </script>
</body>
</html>
