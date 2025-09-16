<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حاسبة النسبة الموزونة | جامعة الملك سعود</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Tajawal', sans-serif;
            background-color: #eef2f5;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
            box-sizing: border-box;
        }
        .container {
            background-color: #ffffff;
            padding: 35px;
            border-radius: 12px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.1);
            text-align: center;
            width: 95%;
            max-width: 450px;
        }
        .header {
            margin-bottom: 25px;
        }
        .logo {
            max-width: 85px; /* تم تعديل حجم الشعار ليتناسب مع التصميم الجديد */
            height: auto;
            margin-bottom: 15px;
        }
        h2 {
            color: #2c3e50;
            margin-bottom: 25px;
            font-weight: 700;
        }
        .input-group {
            margin-bottom: 20px;
            text-align: right;
        }
        label {
            display: block;
            margin-bottom: 8px;
            color: #34495e;
            font-weight: bold;
            font-size: 15px;
        }
        input {
            width: 100%;
            padding: 12px;
            border: 1px solid #ced4da;
            border-radius: 6px;
            box-sizing: border-box;
            font-size: 18px; /* حجم خط أكبر لرؤية الأرقام العربية بوضوح */
            font-family: 'Tajawal', sans-serif; /* تطبيق الخط على خانات الإدخال */
            color: #333;
        }
        input:focus {
            border-color: #007bff;
            outline: none;
            box-shadow: 0 0 0 0.2rem rgba(0,123,255,.25);
        }
        .button-group {
            margin-top: 30px;
            display: flex;
            gap: 10px;
        }
        button {
            flex: 1;
            padding: 12px;
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 17px;
            font-family: 'Tajawal', sans-serif; /* تطبيق الخط على الأزرار */
            font-weight: bold;
            transition: background-color 0.3s ease;
        }
        #calculateBtn {
            background-color: #007bff;
        }
        #calculateBtn:hover {
            background-color: #0056b3;
        }
        #clearBtn {
            background-color: #dc3545;
        }
        #clearBtn:hover {
            background-color: #c82333;
        }
        #result {
            margin-top: 25px;
            font-size: 24px;
            font-weight: bold;
            color: #28a745;
            min-height: 30px;
        }
    </style>
</head>
<body>

<div class="container">
    <div class="header">
        <img src="https://i.ibb.co/LQr5p5X/image.png" alt="شعار جامعة الملك سعود" class="logo">
        <h2>حاسبة النسبة الموزونة</h2>
    </div>

    <form id="calculatorForm">
        <div class="input-group">
            <label for="gpa">المعدل التراكمي (من 5)</label>
            <input type="text" inputmode="decimal" id="gpa" placeholder="أدخل المعدل من ٥" max="5">
        </div>

        <div class="input-group">
            <label for="qudrat">درجة القدرات (من 100)</label>
            <input type="text" inputmode="numeric" id="qudrat" placeholder="أدخل درجة القدرات" max="100">
        </div>

        <div class="input-group">
            <label for="tahsili">درجة التحصيلي (من 100)</label>
            <input type="text" inputmode="numeric" id="tahsili" placeholder="أدخل درجة التحصيلي" max="100">
        </div>

        <div class="button-group">
            <button id="calculateBtn" type="button" onclick="calculate()">احسب</button>
            <button id="clearBtn" type="button" onclick="clearData()">مسح البيانات</button>
        </div>
    </form>

    <div id="result"></div>
</div>

<script>
    // دالة لتحويل الأرقام العربية (١٢٣) والهندية (123) إلى أرقام إنجليزية للعمليات الحسابية
    function convertToArabicNumerals(str) {
        if (str === null || str === undefined) return NaN;
        const arabic = '٠١٢٣٤٥٦٧٨٩.';
        const english = '0123456789.';
        let newStr = String(str);
        for (let i = 0; i < english.length; i++) {
            newStr = newStr.replace(new RegExp(arabic[i], 'g'), english[i]);
        }
        return parseFloat(newStr);
    }

    function calculate() {
        // قراءة القيم وتحويلها باستخدام الدالة الجديدة
        const gpa = convertToArabicNumerals(document.getElementById('gpa').value);
        const qudrat = convertToArabicNumerals(document.getElementById('qudrat').value);
        const tahsili = convertToArabicNumerals(document.getElementById('tahsili').value);

        if (isNaN(gpa) || isNaN(qudrat) || isNaN(tahsili)) {
            document.getElementById('result').innerText = 'الرجاء إدخال جميع القيم بشكل صحيح.';
            document.getElementById('result').style.color = '#dc3545';
            return;
        }
        
        if (gpa > 5 || gpa < 0 || qudrat > 100 || qudrat < 0 || tahsili > 100 || tahsili < 0) {
            document.getElementById('result').innerText = 'الرجاء التأكد من أن القيم المدخلة ضمن النطاق المسموح به.';
            document.getElementById('result').style.color = '#dc3545';
            return;
        }

        const gpaPercentage = (gpa / 5) * 100;
        const weightedScore = (gpaPercentage * 0.50) + (qudrat * 0.25) + (tahsili * 0.25);

        // تحويل النتيجة النهائية إلى أرقام عربية للعرض
        const arabicResult = new Intl.NumberFormat('ar-SA', { minimumFractionDigits: 2, maximumFractionDigits: 2 }).format(weightedScore);
        document.getElementById('result').innerText = `نسبتك الموزونة هي: ${arabicResult}٪`;
        document.getElementById('result').style.color = '#28a745';
    }

    function clearData() {
        document.getElementById('calculatorForm').reset();
        document.getElementById('result').innerText = '';
        document.getElementById('result').style.color = '#2c3e50';
    }
</script>

</body>
</html>
