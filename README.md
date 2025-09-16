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
            background-color: #eef2f5; /* لون خلفية أفتح */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh; /* استخدام min-height بدلاً من height لتجنب مشاكل المحتوى الطويل */
            margin: 0;
            padding: 20px; /* إضافة padding لتحسين المظهر على الجوال */
            box-sizing: border-box; /* للتأكد من أن padding لا يزيد من عرض العنصر */
        }
        .container {
            background-color: #ffffff;
            padding: 35px;
            border-radius: 12px; /* حواف أكثر دائرية */
            box-shadow: 0 8px 20px rgba(0,0,0,0.1); /* ظل أوضح */
            text-align: center;
            width: 95%;
            max-width: 450px; /* عرض أكبر قليلاً */
        }
        .header {
            margin-bottom: 25px;
        }
        .logo {
            max-width: 100px; /* حجم الشعار */
            height: auto;
            margin-bottom: 15px;
        }
        h2 {
            color: #2c3e50; /* لون عنوان أغمق */
            margin-bottom: 25px;
            font-weight: 700; /* خط أعرض */
        }
        .input-group {
            margin-bottom: 20px;
            text-align: right;
        }
        label {
            display: block;
            margin-bottom: 8px;
            color: #34495e; /* لون نص التسمية */
            font-weight: bold;
            font-size: 15px;
        }
        input {
            width: 100%;
            padding: 12px;
            border: 1px solid #ced4da; /* لون حدود أوضح */
            border-radius: 6px;
            box-sizing: border-box;
            font-size: 16px;
            color: #333;
        }
        input:focus {
            border-color: #007bff; /* حدود زرقاء عند التركيز */
            outline: none;
            box-shadow: 0 0 0 0.2rem rgba(0,123,255,.25); /* ظل خفيف عند التركيز */
        }
        .button-group {
            margin-top: 30px;
            display: flex;
            gap: 10px; /* مسافة بين الأزرار */
        }
        button {
            flex: 1; /* لجعل الأزرار تأخذ نفس المساحة */
            padding: 12px;
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 17px;
            font-weight: bold;
            transition: background-color 0.3s ease; /* تأثير انتقال سلس */
        }
        #calculateBtn {
            background-color: #007bff; /* أزرق أساسي */
        }
        #calculateBtn:hover {
            background-color: #0056b3;
        }
        #clearBtn {
            background-color: #dc3545; /* أحمر للخيار السلبي */
        }
        #clearBtn:hover {
            background-color: #c82333;
        }
        #result {
            margin-top: 25px;
            font-size: 24px; /* حجم خط أكبر للنتيجة */
            font-weight: bold;
            color: #28a745; /* لون أخضر للنتيجة الإيجابية */
            min-height: 30px; /* للحفاظ على مساحة حتى لو لا يوجد نص */
        }
    </style>
</head>
<body>

<div class="container">
    <div class="header">
        <img src="https://upload.wikimedia.org/wikipedia/ar/2/22/King_Saud_University_logo.svg" alt="شعار جامعة الملك سعود" class="logo">
        <h2>حاسبة النسبة الموزونة</h2>
    </div>

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

    <div class="button-group">
        <button id="calculateBtn" onclick="calculate()">احسب</button>
        <button id="clearBtn" onclick="clearData()">مسح البيانات</button>
    </div>

    <div id="result"></div>
</div>

<script>
    function calculate() {
        const gpa = parseFloat(document.getElementById('gpa').value);
        const qudrat = parseFloat(document.getElementById('qudrat').value);
        const tahsili = parseFloat(document.getElementById('tahsili').value);

        if (isNaN(gpa) || isNaN(qudrat) || isNaN(tahsili)) {
            document.getElementById('result').innerText = 'الرجاء إدخال جميع القيم بشكل صحيح.';
            document.getElementById('result').style.color = '#dc3545'; // لون أحمر للخطأ
            return;
        }
        
        if (gpa > 5 || gpa < 0 || qudrat > 100 || qudrat < 0 || tahsili > 100 || tahsili < 0) {
            document.getElementById('result').innerText = 'الرجاء التأكد من أن القيم المدخلة ضمن النطاق المسموح به.';
            document.getElementById('result').style.color = '#dc3545'; // لون أحمر للخطأ
            return;
        }

        const gpaPercentage = (gpa / 5) * 100;
        const weightedScore = (gpaPercentage * 0.50) + (qudrat * 0.25) + (tahsili * 0.25);

        document.getElementById('result').innerText = `نسبتك الموزونة هي: ${weightedScore.toFixed(2)}%`;
        document.getElementById('result').style.color = '#28a745'; // لون أخضر للنتيجة
    }

    function clearData() {
        document.getElementById('gpa').value = ''; // مسح خانة المعدل
        document.getElementById('qudrat').value = ''; // مسح خانة القدرات
        document.getElementById('tahsili').value = ''; // مسح خانة التحصيلي
        document.getElementById('result').innerText = ''; // مسح النتيجة المعروضة
        document.getElementById('result').style.color = '#2c3e50'; // إعادة لون النتيجة للأصلي
    }
</script>

</body>
</html>
