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
            border-radius: 20px;
            max-width: 420px;
            width: 90%;
            padding: 0;
            text-align: center;
            transform: scale(0.9);
            transition: transform 0.3s ease;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
            overflow: hidden;
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
            background: rgba(0, 0, 0, 0.1);
            border: none;
            border-radius: 50%;
            cursor: pointer;
            font-size: 20px;
            color: #666;
            line-height: 1;
            padding: 0;
            transition: background 0.2s;
            z-index: 10;
        }
        .close-button:hover {
            background: rgba(0, 0, 0, 0.2);
        }
        .header {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            padding: 40px 25px 30px;
            color: #ffffff;
        }
        .discount-badge {
            display: inline-block;
            background: rgba(255, 255, 255, 0.3);
            border: 2px solid #ffffff;
            border-radius: 50%;
            width: 100px;
            height: 100px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            margin-bottom: 15px;
        }
        .discount-value {
            font-size: 36px;
            font-weight: 700;
            line-height: 1;
        }
        .discount-unit {
            font-size: 14px;
            margin-top: 4px;
            opacity: 0.9;
        }
        .title {
            font-size: 22px;
            font-weight: 700;
            margin-bottom: 8px;
        }
        .description {
            font-size: 15px;
            opacity: 0.95;
            line-height: 1.5;
        }
        .content {
            padding: 30px 25px;
        }
        .coupon-container {
            background: #f8f9fa;
            border: 2px dashed #dee2e6;
            border-radius: 12px;
            padding: 20px 15px;
            margin-bottom: 20px;
        }
        .coupon-label {
            font-size: 12px;
            color: #999;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 10px;
        }
        .coupon-display {
            font-size: 28px;
            font-weight: 700;
            color: #f5576c;
            letter-spacing: 3px;
            margin-bottom: 15px;
            user-select: all;
            -webkit-user-select: all;
        }
        .copy-button {
            width: 100%;
            padding: 14px 20px;
            background: #f5576c;
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
        .info-section {
            margin-bottom: 20px;
        }
        .info-row {
            display: flex;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px solid #f0f0f0;
        }
        .info-row:last-child {
            border-bottom: none;
        }
        .info-label {
            font-size: 14px;
            color: #666;
        }
        .info-value {
            font-size: 14px;
            font-weight: 600;
            color: #222;
        }
        .info-value.expiry {
            color: #f5576c;
        }
        .redeem-button {
            display: block;
            width: 100%;
            padding: 16px 24px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: #ffffff;
            font-size: 16px;
            font-weight: 600;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            text-decoration: none;
            transition: transform 0.2s, box-shadow 0.2s;
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
        }
        .redeem-button:active {
            transform: scale(0.98);
        }
        .terms {
            font-size: 12px;
            color: #999;
            margin-top: 15px;
            line-height: 1.5;
        }
    </style>
</head>
<body>
    <div id="overlay">
        <div class="modal">
            <button class="close-button" id="close-button">&times;</button>

            <div class="header">
                <div class="discount-badge" style="margin: 0 auto;">
                    <div class="discount-value" id="discount-value">30%</div>
                    <div class="discount-unit" id="discount-unit">할인</div>
                </div>
                <div class="title" id="title">특별 할인 쿠폰!</div>
                <div class="description" id="description">지금 바로 사용하세요</div>
            </div>

            <div class="content">
                <div class="coupon-container">
                    <div class="coupon-label">쿠폰 코드</div>
                    <div class="coupon-display" id="coupon-display">SAVE30</div>
                    <button class="copy-button" id="copy-button">
                        <span class="copy-text">📋 코드 복사하기</span>
                        <span class="copied-text">✅ 복사 완료!</span>
                    </button>
                </div>

                <div class="info-section" id="info-section">
                    <div class="info-row">
                        <span class="info-label">최소 주문 금액</span>
                        <span class="info-value" id="min-purchase">50,000₩</span>
                    </div>
                    <div class="info-row">
                        <span class="info-label">최대 할인 금액</span>
                        <span class="info-value" id="max-discount">15,000₩</span>
                    </div>
                    <div class="info-row">
                        <span class="info-label">유효 기간</span>
                        <span class="info-value expiry" id="expiry-date">2026.01.31까지</span>
                    </div>
                </div>

                <button class="redeem-button" id="redeem-button">지금 사용하기</button>

                <div class="terms" id="terms">
                    * 일부 상품 제외<br>
                    * 다른 쿠폰과 중복 사용 불가
                </div>
            </div>
        </div>
    </div>

    <script>
        /* ============================================
           CUSTOMIZABLE: 기본 설정
           ============================================
           AI 요청 예시:
           - "타이틀을 '윈터 세일 쿠폰!'로 바꿔줘"
           - "설명을 '오늘만 사용 가능'으로 바꿔줘"
        */
        var config = {
            title: "특별 할인 쿠폰!",
            description: "지금 바로 사용하세요",
            copyButtonText: "📋 코드 복사하기",
            copiedButtonText: "✅ 복사 완료!",
            redeemButtonText: "지금 사용하기",
            terms: "* 일부 상품 제외<br>* 다른 쿠폰과 중복 사용 불가"
        };

        /* ============================================
           CUSTOMIZABLE: 쿠폰 설정
           ============================================
           AI 요청 예시:
           - "쿠폰 코드를 WINTER2026으로 바꿔줘"
           - "Liquid 변수로 동적 쿠폰 사용하게 바꿔줘"

           couponCode: 쿠폰 코드
           - 정적 코드: "SAVE30"
           - Liquid 변수: "{{custom_attribute.${coupon_code}}}"
        */
        var couponCode = "SAVE30";  // 또는 Liquid: "{{custom_attribute.${coupon_code}}}"

        /* ============================================
           CUSTOMIZABLE: 할인 정보
           ============================================
           AI 요청 예시:
           - "할인율을 50%로 바꿔줘"
           - "할인 단위를 '₩' (금액)로 바꿔줘"
           - "할인 금액을 10,000₩로 설정해줘"

           discountType: 할인 타입
           - "percentage" = 퍼센트 할인 (30%)
           - "amount" = 금액 할인 (10,000₩)

           discountValue: 할인 값
           - percentage인 경우: 30 (숫자만)
           - amount인 경우: "10,000₩" (문자열)
        */
        var discountInfo = {
            type: "percentage",  // "percentage" 또는 "amount"
            value: 30,           // percentage: 숫자, amount: 문자열
            unit: "할인"         // "할인" 또는 "적립" 등
        };

        /* ============================================
           CUSTOMIZABLE: 쿠폰 조건 정보
           ============================================
           AI 요청 예시:
           - "최소 주문 금액을 100,000₩로 바꿔줘"
           - "유효 기간을 2026년 2월 28일까지로 바꿔줘"
           - "정보 섹션을 숨겨줘"

           showInfo: 쿠폰 조건 정보 표시 여부
           - true = 표시
           - false = 숨김
        */
        var couponInfo = {
            showInfo: true,
            minPurchase: "50,000₩",
            maxDiscount: "15,000₩",
            expiryDate: "2026.01.31까지"
        };

        /* ============================================
           CUSTOMIZABLE: 사용하기 버튼 설정
           ============================================
           AI 요청 예시:
           - "사용 URL을 https://shop.example.com/cart로 바꿔줘"
           - "딥링크로 변경: athlerab://checkout"

           redeemUrl: 사용하기 버튼 클릭 시 이동할 URL
           linkType: 링크 타입
           - "deeplink" = 앱 내부 딥링크
           - "web" = 브라우저에서 열기
        */
        var redeemUrl = "athlerab://checkout";
        var linkType = "deeplink";  // "deeplink" 또는 "web"

        /* ============================================
           CUSTOMIZABLE: Braze 이벤트 설정
           ============================================
           AI 요청 예시:
           - "이벤트명을 'coupon_viewed'로 바꿔줘"
        */
        var eventNames = {
            couponView: "coupon_code_viewed",
            couponCopy: "coupon_code_copied",
            couponRedeem: "coupon_redeem_click"
        };

        // ============================================
        // 내부 로직 (수정 불필요)
        // ============================================

        var overlay = document.getElementById("overlay");
        var modal = overlay.querySelector(".modal");
        var closeButton = document.getElementById("close-button");
        var copyButton = document.getElementById("copy-button");
        var redeemButton = document.getElementById("redeem-button");
        var couponDisplay = document.getElementById("coupon-display");
        var infoSection = document.getElementById("info-section");

        // 설정 적용
        document.getElementById("title").textContent = config.title;
        document.getElementById("description").textContent = config.description;
        document.querySelector(".copy-text").textContent = config.copyButtonText;
        document.querySelector(".copied-text").textContent = config.copiedButtonText;
        redeemButton.textContent = config.redeemButtonText;
        document.getElementById("terms").innerHTML = config.terms;
        couponDisplay.textContent = couponCode;

        // 할인 정보 적용
        if (discountInfo.type === "percentage") {
            document.getElementById("discount-value").textContent = discountInfo.value + "%";
        } else {
            document.getElementById("discount-value").textContent = discountInfo.value;
        }
        document.getElementById("discount-unit").textContent = discountInfo.unit;

        // 쿠폰 조건 정보 적용
        if (couponInfo.showInfo) {
            document.getElementById("min-purchase").textContent = couponInfo.minPurchase;
            document.getElementById("max-discount").textContent = couponInfo.maxDiscount;
            document.getElementById("expiry-date").textContent = couponInfo.expiryDate;
        } else {
            infoSection.style.display = "none";
        }

        // Braze Bridge 초기화
        window.addEventListener("ab.BridgeReady", function() {
            try {
                brazeBridge.logCustomEvent(eventNames.couponView, {
                    coupon_code: couponCode,
                    discount_type: discountInfo.type,
                    discount_value: discountInfo.value
                });
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
            copyToClipboard(couponCode)
                .then(function() {
                    copyButton.classList.add("copied");

                    window.addEventListener("ab.BridgeReady", function() {
                        try {
                            brazeBridge.logClick("copy_button");
                            brazeBridge.logCustomEvent(eventNames.couponCopy, {
                                coupon_code: couponCode
                            });
                        } catch(e) {}
                    }, false);

                    setTimeout(function() {
                        copyButton.classList.remove("copied");
                    }, 2000);
                })
                .catch(function(err) {
                    console.error("Copy failed:", err);
                    alert("쿠폰 코드 복사에 실패했습니다. 수동으로 복사해주세요.");
                });
        };

        // 사용하기 버튼
        redeemButton.onclick = function() {
            window.addEventListener("ab.BridgeReady", function() {
                try {
                    brazeBridge.logClick("redeem_button");
                    brazeBridge.logCustomEvent(eventNames.couponRedeem, {
                        coupon_code: couponCode
                    });

                    if (linkType === "web") {
                        window.open(redeemUrl, "_blank");
                    } else {
                        window.location.href = redeemUrl;
                    }
                } catch(e) {
                    console.error("Redeem error:", e);
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
