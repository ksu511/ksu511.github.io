<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حاسبة معدل التخصيص - جامعة الملك سعود</title>
    
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --primary-color: #007bff;
            --primary-hover: #0056b3;
            --danger-color: #dc3545;
            --danger-hover: #c82333;
            --success-color: #28a745;
            --bg-color: #f7f9fc;
            --card-bg: #ffffff;
            --text-color: #2c3e50;
            --label-color: #34495e;
            --border-color: #dee2e6;
            --input-bg: #ffffff;
            --shadow-color: rgba(0, 0, 0, 0.08);
            --mode-icon: '🌙';
        }

        body.dark-mode {
            --bg-color: #121212;
            --card-bg: #1e1e1e;
            --text-color: #e0e0e0;
            --label-color: #adadad;
            --border-color: #444444;
            --input-bg: #2a2a2a;
            --shadow-color: rgba(0, 0, 0, 0.2);
            --mode-icon: '☀️';
        }

        body {
            font-family: 'Tajawal', sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
            box-sizing: border-box;
            transition: background-color 0.3s, color 0.3s;
        }
        .container {
            position: relative;
            background-color: var(--card-bg);
            padding: 25px; /* تم تقليل الحشوة الداخلية */
            border-radius: 15px;
            box-shadow: 0 10px 25px var(--shadow-color);
            text-align: center;
            width: 100%;
            max-width: 400px; /* عرض مناسب للجوال */
            border-top: 5px solid var(--primary-color);
            transition: background-color 0.3s;
            margin-bottom: 20px;
        }
        #theme-toggle {
            position: absolute;
            top: 15px;
            left: 15px;
            background: transparent;
            border: 1px solid var(--border-color);
            border-radius: 50%;
            width: 40px;
            height: 40px;
            cursor: pointer;
            font-size: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: background-color 0.3s, border-color 0.3s;
        }
        #theme-toggle::after { content: var(--mode-icon); }
        #theme-toggle:hover { background-color: rgba(128, 128, 128, 0.1); }
        
        .header { margin-bottom: 25px; }
        h1 {
            font-size: 20px; /* تم تصغير الخط ليناسب العنوان */
            font-weight: 700;
            color: var(--text-color);
            margin: 0;
            line-height: 1.4;
        }
        h2 {
            color: var(--label-color);
            margin: 0 0 10px 0;
            font-weight: 500;
            font-size: 18px;
        }
        .score-input-row {
            display: flex;
            gap: 10px;
            align-items: center;
            margin-bottom: 20px;
        }
        .input-group { 
            flex: 3.5; /* زيادة المساحة لخانة الإدخال الرئيسية */
            text-align: right; 
            position: relative;
        }
        .weight-group { flex: 1; text-align: right; }
        
        label {
            display: block;
            margin-bottom: 8px;
            color: var(--label-color);
            font-weight: 500;
            font-size: 14px; /* تم تصغير الخط ليناسب الخانات */
        }
        input {
            width: 100%;
            padding: 12px 15px;
            padding-left: 35px; 
            border: 1px solid var(--border-color);
            background-color: var(--input-bg);
            color: var(--text-color);
            border-radius: 8px;
            box-sizing: border-box;
            font-size: 16px;
            font-family: 'Tajawal', sans-serif;
            transition: border-color 0.3s, box-shadow 0.3s, background-color 0.3s;
        }
        input:focus {
            border-color: var(--primary-color);
            outline: none;
            box-shadow: 0 0 0 4px rgba(0, 123, 255, 0.1);
        }
        .clear-btn {
            position: absolute;
            left: 1px;
            top: 50%;
            transform: translateY(-50%);
            background: transparent;
            border: none;
            color: var(--label-color);
            cursor: pointer;
            font-size: 22px;
            font-weight: bold;
            width: 35px;
            height: 100%;
            line-height: 1;
            opacity: 0.6;
            transition: opacity 0.2s;
        }
        .clear-btn:hover {
            opacity: 1;
        }

        .weights-total {
            margin-bottom: 20px;
            font-weight: bold;
        }
        .button-group {
            margin-top: 20px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }
        button {
            padding: 13px;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            font-family: 'Tajawal', sans-serif;
            font-weight: 700;
            transition: all 0.3s ease;
        }
        button:active { transform: scale(0.98); }
        #calculateBtn { background-color: var(--primary-color); }
        #calculateBtn:hover { background-color: var(--primary-hover); }
        #clearBtn { background-color: var(--danger-color); }
        #clearBtn:hover { background-color: var(--danger-hover); }
        #result {
            margin-top: 25px;
            font-size: 24px;
            font-weight: 700;
            color: var(--success-color);
            min-height: 35px;
            line-height: 1.5;
        }
        .footer {
            font-size: 16px;
            color: var(--label-color);
            text-align: center;
        }
        .prayer-text {
            margin-top: 20px;
            font-size: 14px;
            color: var(--label-color);
        }
    </style>
</head>
<body>

<div class="container">
    <button id="theme-toggle" title="تبديل الوضع"></button>
    
    <div class="header">
        <h2>جامعة الملك سعود</h2>
        <h1>حاسبة معدل التخصيص للمسارين العلمي والصحي</h1>
    </div>

    <form id="calculatorForm" onsubmit="return false;">
        <div class="score-input-row">
            <div class="input-group">
                <label for="gpa">المعدل التراكمي (من 5)</label>
                <input type="text" inputmode="decimal" id="gpa">
                <button type="button" class="clear-btn" onclick="clearInput('gpa')">&times;</button>
            </div>
            <div class="weight-group">
                <label for="gpa-weight">الوزن %</label>
                <input type="text" inputmode="numeric" id="gpa-weight" value="50" class="weight-input">
            </div>
        </div>
        <div class="score-input-row">
            <div class="input-group">
                <label for="qudrat">درجة القدرات</label>
                <input type="text" inputmode="numeric" id="qudrat">
                 <button type="button" class="clear-btn" onclick="clearInput('qudrat')">&times;</button>
            </div>
            <div class="weight-group">
                <label for="qudrat-weight">الوزن %</label>
                <input type="text" inputmode="numeric" id="qudrat-weight" value="25" class="weight-input">
            </div>
        </div>
        <div class="score-input-row">
            <div class="input-group">
                <label for="tahsili">درجة التحصيلي</label>
                <input type="text" inputmode="numeric" id="tahsili">
                 <button type="button" class="clear-btn" onclick="clearInput('tahsili')">&times;</button>
            </div>
            <div class="weight-group">
                <label for="tahsili-weight">الوزن %</label>
                <input type="text" inputmode="numeric" id="tahsili-weight" value="25" class="weight-input">
            </div>
        </div>
        
        <div class="weights-total" id="weights-total-text">
            مجموع الأوزان: 100%
        </div>

        <div class="button-group">
            <button id="calculateBtn" type="button" onclick="calculate()">احسب</button>
            <button id="clearBtn" type="button" onclick="clearData()">مسح الكل</button>
        </div>
    </form>

    <div id="result"></div>
</div>

<div class="footer">
    <p class="prayer-text">دعواتكم لي ولوالدي وجميع المسلمين</p>
</div>

<script>
    // --- GENERAL ELEMENTS ---
    const resultDiv = document.getElementById('result');
    const dangerColor = getComputedStyle(document.documentElement).getPropertyValue('--danger-color').trim();
    const successColor = getComputedStyle(document.documentElement).getPropertyValue('--success-color').trim();

    // --- DARK MODE LOGIC ---
    const themeToggle = document.getElementById('theme-toggle');
    const body = document.body;
    themeToggle.addEventListener('click', () => {
        body.classList.toggle('dark-mode');
        // Save the user's preference
        if (body.classList.contains('dark-mode')) {
            localStorage.setItem('theme', 'dark');
        } else {
            localStorage.setItem('theme', 'light');
        }
    });

    // --- WEIGHTS VALIDATION LOGIC ---
    const weightInputs = document.querySelectorAll('.weight-input');
    const weightsTotalText = document.getElementById('weights-total-text');
    function updateWeightsTotal() {
        let total = 0;
        weightInputs.forEach(input => {
            total += convertToEnglishNumerals(input.value) || 0;
        });
        weightsTotalText.textContent = `مجموع الأوزان: ${total}%`;
        if (total !== 100) {
            weightsTotalText.style.color = dangerColor;
        } else {
            weightsTotalText.style.color = successColor;
        }
    }
    weightInputs.forEach(input => input.addEventListener('input', updateWeightsTotal));

    // --- PAGE LOAD INITIALIZATION ---
    document.addEventListener('DOMContentLoaded', () => {
        // Default to dark mode unless the user has explicitly chosen light mode
        if (localStorage.getItem('theme') !== 'light') {
            body.classList.add('dark-mode');
        }
        updateWeightsTotal();
    });

    // --- CALCULATOR LOGIC ---
    function convertToEnglishNumerals(str) {
        if (str === null || str === undefined || String(str).trim() === '') return NaN;
        const arabicEastern = /[\u0660-\u0669]/g;
        const arabicIndic = /[\u06F0-\u06F9]/g;
        let newStr = String(str)
            .replace(arabicEastern, d => d.charCodeAt(0) - 0x0660)
            .replace(arabicIndic, d => d.charCodeAt(0) - 0x06F0)
            .replace(/٫/g, '.');
        return parseFloat(newStr);
    }

    function calculate() {
        const gpa = convertToEnglishNumerals(document.getElementById('gpa').value);
        const qudrat = convertToEnglishNumerals(document.getElementById('qudrat').value);
        const tahsili = convertToEnglishNumerals(document.getElementById('tahsili').value);

        const gpaWeight = convertToEnglishNumerals(document.getElementById('gpa-weight').value);
        const qudratWeight = convertToEnglishNumerals(document.getElementById('qudrat-weight').value);
        const tahsiliWeight = convertToEnglishNumerals(document.getElementById('tahsili-weight').value);

        if (isNaN(gpa) || isNaN(qudrat) || isNaN(tahsili) || isNaN(gpaWeight) || isNaN(qudratWeight) || isNaN(tahsiliWeight)) {
            resultDiv.innerText = 'الرجاء إدخال جميع القيم والأوزان.';
            resultDiv.style.color = dangerColor;
            return;
        }
        
        const totalWeight = gpaWeight + qudratWeight + tahsiliWeight;
        if (Math.round(totalWeight) !== 100) {
            resultDiv.innerText = 'مجموع الأوزان يجب أن يكون 100%.';
            resultDiv.style.color = dangerColor;
            return;
        }

        const gpaPercentage = (gpa / 5) * 100;
        const weightedScore = (gpaPercentage * (gpaWeight / 100)) + (qudrat * (qudratWeight / 100)) + (tahsili * (tahsiliWeight / 100));

        const arabicResult = new Intl.NumberFormat('ar-SA', { minimumFractionDigits: 2, maximumFractionDigits: 2 }).format(weightedScore);
        resultDiv.innerText = `النسبة الموزونة النهائية: ${arabicResult}٪`;
        resultDiv.style.color = successColor;
    }
    
    // Function to clear a single input field
    function clearInput(inputId) {
        document.getElementById(inputId).value = '';
        document.getElementById(inputId).focus();
    }

    // Function to clear all form fields
    function clearData() {
        document.getElementById('calculatorForm').reset();
        resultDiv.innerText = '';
        updateWeightsTotal();
    }
</script>

</body>
</html>
