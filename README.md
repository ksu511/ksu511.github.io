<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حاسبة معدل التخصيص - ملء الشاشة</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #007bff; --primary-hover: #0056b3; --danger-color: #dc3545; --danger-hover: #c82333;
            --success-color: #28a745; --bg-color: #f7f9fc; --card-bg: #ffffff; --text-color: #2c3e50;
            --label-color: #34495e; --border-color: #dee2e6; --input-bg: #fdfdfd;
        }
        body.dark-mode {
            --bg-color: #121212; --card-bg: #1e1e1e; --text-color: #e0e0e0; --label-color: #adadad;
            --border-color: #444444; --input-bg: #2a2a2a;
        }
        html, body { height: 100%; margin: 0; padding: 0; }
        body {
            font-family: 'Tajawal', sans-serif; background-color: var(--bg-color); color: var(--text-color);
            display: flex; justify-content: center; align-items: center;
        }
        .container {
            background-color: var(--card-bg);
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 2rem;
            box-sizing: border-box;
            overflow-y: auto;
        }
        .calculator-content { width: 100%; max-width: 700px; }
        #theme-toggle { position: absolute; top: 20px; left: 20px; z-index: 10; width: 45px; height: 45px; font-size: 22px; border-radius: 50%; cursor: pointer; background-color: var(--input-bg); border: 1px solid var(--border-color); }
        #theme-toggle::after { content: '🌙'; }
        body.dark-mode #theme-toggle::after { content: '☀️'; }
        
        .header { text-align: center; margin-bottom: 2.5rem; }
        h1 { font-size: 2.5rem; margin: 0.5rem 0; }
        h2 { font-size: 1.7rem; color: var(--label-color); margin: 0; }

        #form-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 1.5rem; margin-bottom: 2rem; }
        label { font-size: 1rem; margin-bottom: 0.5rem; display: block; text-align: right; }
        input { font-size: 1.1rem; width: 100%; padding: 0.8rem; border-radius: 8px; border: 1px solid var(--border-color); background-color: var(--input-bg); color: var(--text-color); box-sizing: border-box; }
        
        .bottom-section { display: flex; justify-content: space-between; align-items: center; margin-top: 2rem; }
        .weights-total { font-size: 1.2rem; font-weight: bold; }
        .button-group { display: flex; gap: 1rem; }
        button { font-size: 1.1rem; padding: 0.8rem 1.8rem; border-radius: 8px; border: none; cursor: pointer; color: white; font-weight: bold; }
        #calculateBtn { background-color: var(--primary-color); }
        #clearBtn { background-color: var(--danger-color); }
        #result { text-align: center; font-size: 2.5rem; font-weight: 700; color: var(--success-color); margin-top: 2rem; min-height: 50px; }
        .footer { text-align: center; margin-top: 2rem; color: var(--label-color); }
    </style>
</head>
<body>
<div class="container">
    <button id="theme-toggle"></button>
    <div class="calculator-content">
        <div class="header"><h2>جامعة الملك سعود</h2><h1>حاسبة معدل التخصيص</h1></div>
        <form id="calculatorForm" onsubmit="return false;">
            <div id="form-grid">
                <div><label for="gpa">المعدل التراكمي (من 5)</label><input type="text" id="gpa"></div>
                <div><label for="gpa-weight">وزن المعدل %</label><input type="text" id="gpa-weight" value="50"></div>
                <div><label for="qudrat">درجة القدرات</label><input type="text" id="qudrat"></div>
                <div><label for="qudrat-weight">وزن القدرات %</label><input type="text" id="qudrat-weight" value="25"></div>
                <div><label for="tahsili">درجة التحصيلي</label><input type="text" id="tahsili"></div>
                <div><label for="tahsili-weight">وزن التحصيلي %</label><input type="text" id="tahsili-weight" value="25"></div>
            </div>
            <div class="bottom-section">
                <div id="weights-total-text" class="weights-total">مجموع الأوزان: 100%</div>
                <div class="button-group">
                    <button id="calculateBtn" type="button" onclick="calculate()">احسب</button>
                    <button id="clearBtn" type="button" onclick="clearData()">مسح الكل</button>
                </div>
            </div>
        </form>
        <div id="result"></div>
        <div class="footer"><p>دعواتكم لي ولوالدي وجميع المسلمين</p></div>
    </div>
</div>
<script>
    // JavaScript code remains the same
</script>
</body>
</html>
