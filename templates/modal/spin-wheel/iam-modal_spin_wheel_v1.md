<!doctype html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; overflow: hidden; }
        #overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.75); display: flex; align-items: center; justify-content: center; z-index: 9999; opacity: 0; transition: opacity 0.3s; }
        #overlay.show { opacity: 1; }
        .modal { position: relative; background: #fff; border-radius: 20px; max-width: 400px; width: 90%; padding: 30px 20px; text-align: center; transform: scale(0.9); transition: transform 0.3s; box-shadow: 0 10px 40px rgba(0,0,0,0.3); }
        #overlay.show .modal { transform: scale(1); }
        .close-button { position: absolute; top: 12px; right: 12px; width: 28px; height: 28px; background: rgba(0,0,0,0.05); border: none; border-radius: 50%; cursor: pointer; font-size: 20px; color: #666; }
        .title { font-size: 22px; font-weight: 700; color: #222; margin-bottom: 8px; }
        .description { font-size: 14px; color: #666; margin-bottom: 20px; }
        .wheel-container { position: relative; width: 280px; height: 280px; margin: 0 auto 20px; }
        .wheel { width: 100%; height: 100%; border-radius: 50%; position: relative; transition: transform 3s cubic-bezier(0.17, 0.67, 0.12, 0.99); box-shadow: 0 5px 20px rgba(0,0,0,0.2); }
        .wheel-segment { position: absolute; width: 50%; height: 50%; transform-origin: 100% 100%; clip-path: polygon(0 0, 100% 0, 100% 100%); display: flex; align-items: center; justify-content: center; }
        .segment-content { position: absolute; top: 30%; left: 60%; font-size: 24px; transform: rotate(-22.5deg); }
        .arrow { position: absolute; top: -10px; left: 50%; transform: translateX(-50%); width: 0; height: 0; border-left: 15px solid transparent; border-right: 15px solid transparent; border-top: 25px solid #f44336; z-index: 10; filter: drop-shadow(0 2px 5px rgba(0,0,0,0.3)); }
        .spin-button { width: 100%; padding: 16px; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: #fff; font-size: 16px; font-weight: 600; border: none; border-radius: 10px; cursor: pointer; transition: all 0.2s; box-shadow: 0 4px 15px rgba(102,126,234,0.4); }
        .spin-button:disabled { background: #ccc; cursor: not-allowed; }
        .result { display: none; margin-top: 15px; padding: 15px; background: #f0f0f0; border-radius: 10px; }
        .result.show { display: block; }
        .result-prize { font-size: 32px; margin-bottom: 8px; }
        .result-text { font-size: 18px; font-weight: 600; color: #222; margin-bottom: 5px; }
        .result-desc { font-size: 14px; color: #666; }
        .claim-button { width: 100%; padding: 14px; background: #4caf50; color: #fff; font-size: 15px; font-weight: 600; border: none; border-radius: 8px; cursor: pointer; margin-top: 10px; }
    </style>
</head>
<body>
    <div id="overlay">
        <div class="modal">
            <button class="close-button" id="close-button">&times;</button>
            <div class="title">🎡 행운의 룰렛!</div>
            <div class="description">룰렛을 돌려서 푸짐한 경품을 받으세요</div>
            <div class="wheel-container">
                <div class="arrow"></div>
                <div class="wheel" id="wheel"></div>
            </div>
            <button class="spin-button" id="spin-button">룰렛 돌리기!</button>
            <div class="result" id="result">
                <div class="result-prize" id="result-prize">🎁</div>
                <div class="result-text" id="result-text">축하합니다!</div>
                <div class="result-desc" id="result-desc">5,000P를 받으셨습니다</div>
                <button class="claim-button" id="claim-button">받기</button>
            </div>
        </div>
    </div>
    <script>
        /* CUSTOMIZABLE: 룰렛 프라이즈 설정 */
        var prizes = [
            { emoji: "🎁", name: "5,000P", probability: 0.3, eventName: "spin_win_5000p", claimUrl: "athlerab://prize/5000p" },
            { emoji: "💎", name: "10,000P", probability: 0.2, eventName: "spin_win_10000p", claimUrl: "athlerab://prize/10000p" },
            { emoji: "🏆", name: "20,000P", probability: 0.15, eventName: "spin_win_20000p", claimUrl: "athlerab://prize/20000p" },
            { emoji: "👑", name: "50,000P", probability: 0.1, eventName: "spin_win_50000p", claimUrl: "athlerab://prize/50000p" },
            { emoji: "💰", name: "100,000P", probability: 0.05, eventName: "spin_win_100000p", claimUrl: "athlerab://prize/100000p" },
            { emoji: "🎉", name: "다시 도전", probability: 0.2, eventName: "spin_try_again", claimUrl: "athlerab://spin/retry" }
        ];
        var linkType = "deeplink";
        var colors = ["#FF6B6B", "#4ECDC4", "#45B7D1", "#FFA07A", "#98D8C8", "#F7DC6F"];

        var overlay = document.getElementById("overlay");
        var wheel = document.getElementById("wheel");
        var spinButton = document.getElementById("spin-button");
        var resultDiv = document.getElementById("result");
        var resultPrize = document.getElementById("result-prize");
        var resultText = document.getElementById("result-text");
        var resultDesc = document.getElementById("result-desc");
        var claimButton = document.getElementById("claim-button");
        var isSpinning = false;
        var selectedPrize = null;

        // 휠 생성
        var segmentAngle = 360 / prizes.length;
        prizes.forEach(function(prize, i) {
            var segment = document.createElement("div");
            segment.className = "wheel-segment";
            segment.style.transform = "rotate(" + (i * segmentAngle) + "deg)";
            segment.style.background = colors[i % colors.length];
            var content = document.createElement("div");
            content.className = "segment-content";
            content.innerHTML = prize.emoji + "<br><small>" + prize.name + "</small>";
            segment.appendChild(content);
            wheel.appendChild(segment);
        });

        // 확률 기반 프라이즈 선택
        function selectPrize() {
            var cumulative = [];
            var sum = 0;
            prizes.forEach(function(p) {
                sum += p.probability;
                cumulative.push(sum);
            });
            var rand = Math.random() * sum;
            for (var i = 0; i < cumulative.length; i++) {
                if (rand <= cumulative[i]) return i;
            }
            return 0;
        }

        // 스핀
        spinButton.onclick = function() {
            if (isSpinning) return;
            isSpinning = true;
            spinButton.disabled = true;
            resultDiv.classList.remove("show");

            var prizeIndex = selectPrize();
            selectedPrize = prizes[prizeIndex];
            var targetAngle = 360 * 5 + (360 - (prizeIndex * segmentAngle + segmentAngle / 2));
            wheel.style.transform = "rotate(" + targetAngle + "deg)";

            window.addEventListener("ab.BridgeReady", function() {
                try {
                    brazeBridge.logCustomEvent("spin_wheel_start");
                } catch(e) {}
            }, false);

            setTimeout(function() {
                isSpinning = false;
                resultPrize.textContent = selectedPrize.emoji;
                resultText.textContent = "축하합니다!";
                resultDesc.textContent = selectedPrize.name + "를 받으셨습니다";
                resultDiv.classList.add("show");

                window.addEventListener("ab.BridgeReady", function() {
                    try {
                        brazeBridge.logCustomEvent(selectedPrize.eventName);
                        brazeBridge.getUser().setCustomUserAttribute("last_spin_prize", selectedPrize.name);
                    } catch(e) {}
                }, false);
            }, 3000);
        };

        // 받기 버튼
        claimButton.onclick = function() {
            window.addEventListener("ab.BridgeReady", function() {
                try {
                    brazeBridge.logClick("claim_button");
                    if (linkType === "web") {
                        window.open(selectedPrize.claimUrl, "_blank");
                    } else {
                        window.location.href = selectedPrize.claimUrl;
                    }
                } catch(e) {}
            }, false);
        };

        // 닫기
        document.getElementById("close-button").onclick = function() {
            window.addEventListener("ab.BridgeReady", function() {
                try {
                    brazeBridge.logClick("close_button");
                    brazeBridge.closeMessage();
                } catch(e) {}
            }, false);
        };

        overlay.onclick = function(e) {
            if (e.target === overlay) {
                window.addEventListener("ab.BridgeReady", function() {
                    try {
                        brazeBridge.logClick("close_overlay");
                        brazeBridge.closeMessage();
                    } catch(e) {}
                }, false);
            }
        };

        window.addEventListener("ab.BridgeReady", function() {
            try {
                brazeBridge.logCustomEvent("spin_wheel_viewed");
            } catch(e) {}
        }, false);

        setTimeout(function() { overlay.classList.add("show"); }, 300);
    </script>
</body>
</html>
