
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>حاسبة العمر وعدّاد الميلاد</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background: #f0f2f5;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
        }

        .container {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            width: 100%;
            max-width: 500px;
        }

        h1 {
            color: #2d3436;
            text-align: center;
            margin-bottom: 25px;
        }

        input[type="date"] {
            width: 100%;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 8px;
            margin: 15px 0;
            font-size: 16px;
        }

        button {
            background: #0984e3;
            color: white;
            padding: 12px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            width: 100%;
            font-size: 18px;
            transition: background 0.3s;
        }

        button:hover {
            background: #0873c4;
        }

        .result {
            margin-top: 25px;
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
        }

        .age-item {
            display: flex;
            justify-content: space-between;
            padding: 12px;
            margin: 8px 0;
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05);
        }

        .countdown {
            margin-top: 25px;
            background: #fff3e0;
            padding: 20px;
            border-radius: 10px;
        }

        .countdown-header {
            color: #e65100;
            text-align: center;
            margin-bottom: 15px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>حاسبة العمر 🎂</h1>
        <input type="date" id="birthDate">
        <button onclick="calculateAge()">احسب الآن</button>
        
        <div class="result">
            <div class="age-item">
                <span>العمر الحالي:</span>
                <span id="years">0 سنة</span>
            </div>
            <div class="age-item">
                <span>الشهور:</span>
                <span id="months">0</span>
            </div>
            <div class="age-item">
                <span>الأيام:</span>
                <span id="days">0</span>
            </div>
        </div>

        <div class="countdown">
            <h3 class="countdown-header">  عيد ميلادك القادم ⏳</h3>
            <div class="age-item">
                <span>الشهور المتبقية:</span>
                <span id="countdown-months">0</span>
            </div>
            <div class="age-item">
                <span>الأيام المتبقية:</span>
                <span id="countdown-days">0</span>
            </div>
            <div class="age-item">
                <span>الساعات المتبقية:</span>
                <span id="countdown-hours">0</span>
            </div>
            <div class="age-item">
                <span>الدقائق المتبقية:</span>
                <span id="countdown-minutes">0</span>
            </div>
        </div>
    </div>

    <script>
        function calculateAge() {
            const birthDate = new Date(document.getElementById('birthDate').value);
            const now = new Date();

            // حساب العمر الحالي
            let years = now.getFullYear() - birthDate.getFullYear();
            let months = now.getMonth() - birthDate.getMonth();
            let days = now.getDate() - birthDate.getDate();

            if (days < 0) {
                months--;
                days += new Date(now.getFullYear(), now.getMonth(), 0).getDate();
            }
            if (months < 0) {
                years--;
                months += 12;
            }

            // تحديث نتائج العمر
            document.getElementById('years').textContent = years + ' سنة';
            document.getElementById('months').textContent = months;
            document.getElementById('days').textContent = days;

            // حساب الوقت المتبقي لعيد الميلاد
            let nextBirthday = new Date(birthDate);
            nextBirthday.setFullYear(now.getFullYear());
            
            if (nextBirthday < now) {
                nextBirthday.setFullYear(now.getFullYear() + 1);
            }

            const diff = nextBirthday - now;
            
            let monthsRemaining = nextBirthday.getMonth() - now.getMonth();
            let daysRemaining = nextBirthday.getDate() - now.getDate();
            let hoursRemaining = nextBirthday.getHours() - now.getHours();
            let minutesRemaining = nextBirthday.getMinutes() - now.getMinutes();

            // تصحيح القيم السالبة
            if (minutesRemaining < 0) {
                hoursRemaining--;
                minutesRemaining += 60;
            }
            if (hoursRemaining < 0) {
                daysRemaining--;
                hoursRemaining += 24;
            }
            if (daysRemaining < 0) {
                monthsRemaining--;
                daysRemaining += new Date(now.getFullYear(), now.getMonth() + 1, 0).getDate();
            }
            if (monthsRemaining < 0) {
                monthsRemaining += 12;
            }

            // تحديث نتائج العد التنازلي
            document.getElementById('countdown-months').textContent = monthsRemaining;
            document.getElementById('countdown-days').textContent = daysRemaining;
            document.getElementById('countdown-hours').textContent = hoursRemaining;
            document.getElementById('countdown-minutes').textContent = minutesRemaining;

            // إذا كان اليوم هو عيد الميلاد
            if (monthsRemaining === 0 && daysRemaining === 0) {
                document.querySelector('.countdown').innerHTML = `
                    <h3 style="color: #d32f2f; text-align:center">🎉🎂 كل عام وأنت بخير! اليوم هو عيد ميلادك! 🎂🎉</h3>
                `;
            }
        }
    </script>
</body>
</html>
