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
            background: rgba(0, 0, 0, 0.05);
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
            background: rgba(0, 0, 0, 0.1);
        }
        .icon {
            font-size: 48px;
            margin-bottom: 10px;
        }
        .title {
            font-size: 22px;
            font-weight: 700;
            color: #222;
            margin-bottom: 8px;
        }
        .description {
            font-size: 14px;
            color: #666;
            margin-bottom: 20px;
        }
        .streak-container {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: #ffffff;
            padding: 15px;
            border-radius: 12px;
            margin-bottom: 20px;
        }
        .streak-text {
            font-size: 14px;
            opacity: 0.9;
            margin-bottom: 5px;
        }
        .streak-value {
            font-size: 32px;
            font-weight: 700;
        }
        .streak-unit {
            font-size: 16px;
            margin-left: 5px;
        }
        .calendar-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 8px;
            margin-bottom: 20px;
        }
        .day-cell {
            aspect-ratio: 1;
            border-radius: 8px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-size: 11px;
            position: relative;
            transition: all 0.2s;
        }
        .day-cell.completed {
            background: #e8f5e9;
            border: 2px solid #4caf50;
        }
        .day-cell.today {
            background: #fff3e0;
            border: 2px solid #ff9800;
        }
        .day-cell.locked {
            background: #f5f5f5;
            border: 2px solid #e0e0e0;
            opacity: 0.5;
        }
        .day-label {
            font-size: 10px;
            color: #999;
            margin-bottom: 4px;
        }
        .day-cell.completed .day-label,
        .day-cell.today .day-label {
            color: #666;
        }
        .day-reward {
            font-size: 18px;
            margin-bottom: 2px;
        }
        .day-points {
            font-size: 9px;
            font-weight: 600;
            color: #667eea;
        }
        .day-cell.completed .check-mark {
            position: absolute;
            top: 2px;
            right: 2px;
            width: 16px;
            height: 16px;
            background: #4caf50;
            border-radius: 50%;
            color: #ffffff;
            font-size: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .checkin-button {
            width: 100%;
            padding: 16px 24px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: #ffffff;
            font-size: 16px;
            font-weight: 600;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.2s;
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
            margin-bottom: 15px;
        }
        .checkin-button:active {
            transform: scale(0.98);
        }
        .checkin-button.completed {
            background: #4caf50;
            box-shadow: 0 4px 15px rgba(76, 175, 80, 0.4);
        }
        .checkin-button.disabled {
            background: #e0e0e0;
            color: #999;
            box-shadow: none;
            cursor: not-allowed;
        }
        .progress-container {
            margin-bottom: 15px;
        }
        .progress-label {
            font-size: 13px;
            color: #666;
            margin-bottom: 8px;
            display: flex;
            justify-content: space-between;
        }
        .progress-bar {
            width: 100%;
            height: 8px;
            background: #f0f0f0;
            border-radius: 4px;
            overflow: hidden;
        }
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
            border-radius: 4px;
            transition: width 0.5s ease;
        }
        .reward-preview {
            font-size: 13px;
            color: #999;
            line-height: 1.5;
        }
        .reward-preview strong {
            color: #667eea;
            font-weight: 600;
        }
    </style>
</head>
<body>
    <div id="overlay">
        <div class="modal">
            <button class="close-button" id="close-button">&times;</button>

            <div class="icon">📅</div>
            <div class="title" id="title">데일리 출석 체크!</div>
            <div class="description" id="description">매일 출석하고 리워드를 받으세요</div>

            <div class="streak-container">
                <div class="streak-text">연속 출석</div>
                <div>
                    <span class="streak-value" id="streak-value">3</span>
                    <span class="streak-unit">일</span>
                </div>
            </div>

            <div class="calendar-grid" id="calendar-grid">
                <!-- 동적으로 생성됨 -->
            </div>

            <div class="progress-container">
                <div class="progress-label">
                    <span>주간 진행률</span>
                    <span id="progress-text">3/7일</span>
                </div>
                <div class="progress-bar">
                    <div class="progress-fill" id="progress-fill" style="width: 0%"></div>
                </div>
            </div>

            <button class="checkin-button" id="checkin-button">오늘 출석하기 🎁</button>

            <div class="reward-preview" id="reward-preview">
                내일 출석 시 <strong>500P</strong> 리워드!
            </div>
        </div>
    </div>

    <script>
        /* ============================================
           CUSTOMIZABLE: 기본 설정
           ============================================
           AI 요청 예시:
           - "타이틀을 '7일 챌린지!'로 바꿔줘"
           - "아이콘을 🎁로 바꿔줘"
        */
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

        /* ============================================
           CUSTOMIZABLE: 캘린더 설정
           ============================================
           AI 요청 예시:
           - "리워드를 모두 1000P로 바꿔줘"
           - "Day 7 리워드를 10,000P로 높여줘"
           - "요일 라벨을 영문으로 바꿔줘"

           dayLabels: 요일 라벨 (7개)
           rewards: 각 날짜별 리워드 (아이콘, 포인트)
        */
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

        /* ============================================
           CUSTOMIZABLE: 출석 현황 설정
           ============================================
           AI 요청 예시:
           - "현재 출석일을 5일로 바꿔줘"
           - "Liquid 변수로 동적 출석일 사용하게 바꿔줘"

           currentDay: 현재 출석 완료 일수 (0-7)
           - 정적 값: 3 (3일째 출석)
           - Liquid 변수: "{{custom_attribute.${checkin_streak}}}"

           todayChecked: 오늘 이미 출석했는지 여부
           - true = 오늘 출석 완료
           - false = 오늘 출석 가능
        */
        var checkinStatus = {
            currentDay: 3,         // 0-7 (0 = 시작 전, 7 = 완료)
            todayChecked: false    // 오늘 출석 완료 여부
        };

        /* ============================================
           CUSTOMIZABLE: Braze 이벤트 설정
           ============================================
           AI 요청 예시:
           - "이벤트명을 'daily_checkin'으로 바꿔줘"
        */
        var eventNames = {
            calendarView: "daily_checkin_viewed",
            checkinComplete: "daily_checkin_complete"
        };

        // ============================================
        // 내부 로직 (수정 불필요)
        // ============================================

        var overlay = document.getElementById("overlay");
        var modal = overlay.querySelector(".modal");
        var closeButton = document.getElementById("close-button");
        var checkinButton = document.getElementById("checkin-button");
        var calendarGrid = document.getElementById("calendar-grid");
        var streakValue = document.getElementById("streak-value");
        var progressFill = document.getElementById("progress-fill");
        var progressText = document.getElementById("progress-text");
        var rewardPreview = document.getElementById("reward-preview");

        // 설정 적용
        document.querySelector(".icon").textContent = config.icon;
        document.getElementById("title").textContent = config.title;
        document.getElementById("description").textContent = config.description;
        document.querySelector(".streak-text").textContent = config.streakText;

        // 출석 현황을 숫자로 변환 (Liquid 대응)
        var currentDayNum = parseInt(checkinStatus.currentDay) || 0;
        var todayChecked = checkinStatus.todayChecked;

        // 연속 출석일 표시
        streakValue.textContent = currentDayNum;

        // 캘린더 그리드 생성
        function renderCalendar() {
            calendarGrid.innerHTML = "";

            for (var i = 0; i < 7; i++) {
                var dayCell = document.createElement("div");
                dayCell.className = "day-cell";

                var dayLabel = document.createElement("div");
                dayLabel.className = "day-label";
                dayLabel.textContent = calendarConfig.dayLabels[i];

                var dayReward = document.createElement("div");
                dayReward.className = "day-reward";
                dayReward.textContent = calendarConfig.rewards[i].emoji;

                var dayPoints = document.createElement("div");
                dayPoints.className = "day-points";
                dayPoints.textContent = calendarConfig.rewards[i].points;

                dayCell.appendChild(dayLabel);
                dayCell.appendChild(dayReward);
                dayCell.appendChild(dayPoints);

                // 상태 결정
                if (i < currentDayNum) {
                    // 과거 완료된 날짜
                    dayCell.classList.add("completed");
                    var checkMark = document.createElement("div");
                    checkMark.className = "check-mark";
                    checkMark.textContent = "✓";
                    dayCell.appendChild(checkMark);
                } else if (i === currentDayNum && !todayChecked) {
                    // 오늘 (출석 가능)
                    dayCell.classList.add("today");
                } else {
                    // 미래 잠긴 날짜
                    dayCell.classList.add("locked");
                }

                calendarGrid.appendChild(dayCell);
            }
        }

        // 진행률 업데이트
        function updateProgress() {
            var progress = (currentDayNum / 7) * 100;
            progressFill.style.width = progress + "%";
            progressText.textContent = currentDayNum + "/7일";
        }

        // 리워드 미리보기 업데이트
        function updateRewardPreview() {
            if (currentDayNum >= 7) {
                rewardPreview.innerHTML = "🎉 7일 챌린지 완료!";
            } else if (todayChecked) {
                var nextDay = currentDayNum;
                if (nextDay < 7) {
                    var nextReward = calendarConfig.rewards[nextDay].points;
                    rewardPreview.innerHTML = "내일 출석 시 <strong>" + nextReward + "</strong> 리워드!";
                }
            } else {
                var todayReward = calendarConfig.rewards[currentDayNum].points;
                rewardPreview.innerHTML = "오늘 출석 시 <strong>" + todayReward + "</strong> 리워드!";
            }
        }

        // 출석 버튼 상태 업데이트
        function updateCheckinButton() {
            if (todayChecked) {
                checkinButton.textContent = config.alreadyCheckedText;
                checkinButton.classList.add("completed");
                checkinButton.disabled = true;
            } else if (currentDayNum >= 7) {
                checkinButton.textContent = "챌린지 완료!";
                checkinButton.classList.add("disabled");
                checkinButton.disabled = true;
            } else {
                checkinButton.textContent = config.checkinButtonText;
            }
        }

        // Braze Bridge 초기화
        window.addEventListener("ab.BridgeReady", function() {
            try {
                brazeBridge.logCustomEvent(eventNames.calendarView, {
                    current_streak: currentDayNum,
                    today_checked: todayChecked
                });
            } catch(e) {
                console.error("Braze error:", e);
            }
        }, false);

        // 출석 처리
        function handleCheckin() {
            if (todayChecked || currentDayNum >= 7) {
                return;
            }

            // 출석 완료 처리
            currentDayNum++;
            todayChecked = true;

            // UI 업데이트
            renderCalendar();
            updateProgress();
            updateRewardPreview();
            updateCheckinButton();
            streakValue.textContent = currentDayNum;

            // Braze 이벤트 로깅
            window.addEventListener("ab.BridgeReady", function() {
                try {
                    brazeBridge.logClick("checkin_button");
                    brazeBridge.logCustomEvent(eventNames.checkinComplete, {
                        day: currentDayNum,
                        reward: calendarConfig.rewards[currentDayNum - 1].points
                    });

                    // 사용자 속성 업데이트 (연속 출석일)
                    brazeBridge.getUser().setCustomUserAttribute("checkin_streak", currentDayNum);
                    brazeBridge.getUser().setCustomUserAttribute("last_checkin_date", new Date().toISOString().split("T")[0]);

                    brazeBridge.requestImmediateDataFlush();
                } catch(e) {
                    console.error("Braze checkin error:", e);
                }
            }, false);
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

        // 출석 버튼
        checkinButton.onclick = function() {
            if (!todayChecked && currentDayNum < 7) {
                handleCheckin();
            }
        };

        // 초기화
        renderCalendar();
        updateProgress();
        updateRewardPreview();
        updateCheckinButton();

        setTimeout(function() {
            overlay.classList.add("show");
        }, 300);
    </script>
</body>
</html>
