<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        /* تصميم انسيابي وهادئ */
        body {
            background-color: transparent;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
            overflow: hidden;
            color: #ffffff;
        }

        #timer-container {
            text-align: center;
            padding: 20px 40px;
            background: rgba(0, 0, 0, 0.2); /* خلفية سوداء شفافة جداً */
            backdrop-filter: blur(5px); /* تأثير زجاجي */
            border-radius: 100px; /* شكل بيضاوي أنيق */
            border: 1px solid rgba(255, 255, 255, 0.3);
            cursor: pointer;
            transition: all 0.3s ease;
        }

        #timer-container:active {
            transform: scale(0.95);
        }

        #timer {
            font-size: 80px;
            font-weight: 200; /* خط نحيف جداً ليعطي طابعاً سينمائياً */
            letter-spacing: -2px;
            margin: 0;
            line-height: 1;
        }

        #label {
            font-size: 14px;
            text-transform: uppercase;
            letter-spacing: 4px;
            margin-bottom: 5px;
            opacity: 0.7;
        }
    </style>
</head>
<body>

<div id="timer-container" onclick="toggleTimer()">
    <div id="label">Focus</div>
    <div id="timer">50:00</div>
</div>

<script>
    let timeLeft = 50 * 60;
    let isRunning = false; // لا يبدأ إلا عند الضغط
    let timerId = null;

    const timerDisplay = document.getElementById('timer');
    const labelDisplay = document.getElementById('label');

    function updateDisplay() {
        const mins = Math.floor(timeLeft / 60);
        const secs = timeLeft % 60;
        timerDisplay.textContent = 
            `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
    }

    function toggleTimer() {
        if (isRunning) {
            clearInterval(timerId);
            timerId = null;
            labelDisplay.textContent = "Paused";
        } else {
            labelDisplay.textContent = "Focus";
            timerId = setInterval(() => {
                if (timeLeft > 0) {
                    timeLeft--;
                    updateDisplay();
                } else {
                    clearInterval(timerId);
                    labelDisplay.textContent = "Done";
                }
            }, 1000);
        }
        isRunning = !isRunning;
    }

    // تحديث العرض الأولي
    updateDisplay();
</script>

</body>
</html>
