<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حساب النسبة الموزونة</title>
    <style>
        body {
            font-family: 'Tahoma', sans-serif;
            background-color: #f4f4f9;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .container {
            background-color: #fff;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            text-align: center;
            width: 90%;
            max-width: 400px;
        }
        h2 {
            color: #333;
            margin-bottom: 25px;
        }
        .input-group {
            margin-bottom: 20px;
            text-align: right;
        }
        label {
            display: block;
            margin-bottom: 8px;
            color: #555;
            font-weight: bold;
        }
        input {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            box-sizing: border-box;
            font-size: 16px;
        }
        button {
            width: 100%;
            padding: 12px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 18px;
            font-weight: bold;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #0056b3;
        }
        #result {
            margin-top: 25px;
            font-size: 22px;
            font-weight: bold;
            color: #2c3e50;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>حاسبة النسبة الموزونة</h2>

    <div class="input-group">
        <label for="gpa">المعدل التراكمي (من 5)</label>
        <input type="number" id="gpa" placeholder="أدخل المعدل من 5" max="5" step="0.01">
    </div>

    <div class="input-group">
        <label for="qudrat">درجة القدرات (من 100)</label>
        <input type="number" id="qudrat" placeholder="أدخل درجة القدرات" max="100">
    </div>

    <div class="input-group">
        <label for="tahsili">درجة التحصيلي (من 100)</label>
        <input type="number" id="tahsili" placeholder="أدخل درجة التحصيلي" max="100">
    </div>

    <button onclick="calculate()">احسب</button>

    <div id="result"></div>
</div>

<script>
    function calculate() {
        // الحصول على القيم من الخانات
        const gpa = parseFloat(document.getElementById('gpa').value);
        const qudrat = parseFloat(document.getElementById('qudrat').value);
        const tahsili = parseFloat(document.getElementById('tahsili').value);

        // التحقق من أن المدخلات أرقام
        if (isNaN(gpa) || isNaN(qudrat) || isNaN(tahsili)) {
            document.getElementById('result').innerText = 'الرجاء إدخال جميع القيم بشكل صحيح.';
            return;
        }

        // التحقق من أن القيم ضمن النطاق الصحيح
        if (gpa > 5 || gpa < 0 || qudrat > 100 || qudrat < 0 || tahsili > 100 || tahsili < 0) {
            document.getElementById('result').innerText = 'الرجاء التأكد من أن القيم المدخلة ضمن النطاق المسموح به.';
            return;
        }

        // المعادلة الحسابية
        // 1. تحويل المعدل من 5 إلى نسبة مئوية (المعدل / 5) * 100
        const gpaPercentage = (gpa / 5) * 100;
        // 2. حساب النسبة الموزونة النهائية
        const weightedScore = (gpaPercentage * 0.50) + (qudrat * 0.25) + (tahsili * 0.25);

        // عرض النتيجة
        document.getElementById('result').innerText = `نسبتك الموزونة هي: ${weightedScore.toFixed(2)}%`;
    }
</script>

</body>
</html>
