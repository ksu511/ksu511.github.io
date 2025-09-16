<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حاسبة معدل التخصيص - نسخة عريضة</title>
    
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --primary-color: #007bff; --primary-hover: #0056b3; --danger-color: #dc3545; --danger-hover: #c82333;
            --success-color: #28a745; --bg-color: #f7f9fc; --card-bg: #ffffff; --text-color: #2c3e50;
            --label-color: #34495e; --border-color: #dee2e6; --input-bg: #ffffff; --shadow-color: rgba(0, 0, 0, 0.08);
            --mode-icon: '🌙';
        }
        body.dark-mode {
            --bg-color: #121212; --card-bg: #1e1e1e; --text-color: #e0e0e0; --label-color: #adadad;
            --border-color: #444444; --input-bg: #2a2a2a; --shadow-color: rgba(0, 0, 0, 0.2); --mode-icon: '☀️';
        }
        body {
            font-family: 'Tajawal', sans-serif; background-color: var(--bg-color); color: var(--text-color);
            display: flex; flex-direction: column; justify-content: center; align-items: center;
            min-height: 100vh; margin: 0; padding: 25px; box-sizing: border-box; transition: background-color 0.3s, color 0.3s;
        }
        .container {
            position: relative; background-color: var(--card-bg); padding: 40px 50px; border-radius: 20px;
            box-shadow: 0 10px 30px var(--shadow-color); text-align: center; width: 100%;
            max-width: 900px; /* <<<--- تم زيادة العرض جداً هنا */
            border-top: 5px solid var(--primary-color); transition: background-color 0.3s; margin-bottom: 20px;
        }
        #theme-toggle { position: absolute; top: 20px; left: 20px; width: 40px; height: 40px; font-size: 20px; }
        .header { margin-bottom: 30px; }
        h1 { font-size: 32px; font-weight: 700; color: var(--text-color); margin: 0; }
        h2 { color: var(--label-color); margin: 0 0 10px 0; font-weight: 500; font-size: 26px; }
        
        #form-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 25px; margin-bottom: 25px; }
        .score-input-row { display: flex; flex-direction: column; gap: 10px; }
        .input-and-weight { display: flex; gap: 10px; }
        .input-group { flex: 3; text-align: right; position: relative; }
        .weight-group { flex: 1; text-align: right; }
        label { display: block; margin-bottom: 8px; font-weight: 500; font-size: 16px; text-align: right; }
        input { width: 100%; padding: 14px; padding-left: 40px; border: 1px solid var(--border-color); background-color: var(--input-bg); color: var(--text-color); border-radius: 8px; box-sizing: border-box; font-size: 18px; }
        .clear-btn { position: absolute; left: 1px; top: 50%; transform: translateY(-50%); background: transparent; border: none; color: var(--label-color); cursor: pointer; font-size: 24px; font-weight: bold; width: 40px; height: 100%; opacity: 0.6; }
        
        .bottom-section { display: flex; justify-content: space-between; align-items: center; margin-top: 20px; }
        .weights-total { font-weight: bold; font-size: 18px; }
        .button-group { display: flex; gap: 15px; }
        button { padding: 14px 30px; border: none; border-radius: 8px; cursor: pointer; font-size: 18px; font-weight: 700; }
        #result { margin-top: 25px; font-size: 32px; font-weight: 700; color: var(--success-color); min-height: 45px; }
        
        .footer { text-align: center; } .prayer-text { margin-top: 20px; font-size: 14px; }
    </style>
</head>
<body>
<div class="container">
    <button id="theme-toggle"></button>
    <div class="header"><h2>جامعة الملك سعود</h2><h1>حاسبة معدل التخصيص</h1></div>
    <form id="calculatorForm" onsubmit="return false;">
        <div id="form-grid">
            <div class="score-input-row">
                <label for="gpa">المعدل التراكمي (من 5)</label>
                <div class="input-and-weight">
                    <div class="input-group"><input type="text" id="gpa"><button type="button" class="clear-btn" onclick="clearInput('gpa')">&times;</button></div>
                    <div class="weight-group"><input type="text" id="gpa-weight" value="50" class="weight-input"></div>
                </div>
            </div>
            <div class="score-input-row">
                <label for="qudrat">درجة القدرات</label>
                <div class="input-and-weight">
                    <div class="input-group"><input type="text" id="qudrat"><button type="button" class="clear-btn" onclick="clearInput('qudrat')">&times;</button></div>
                    <div class="weight-group"><input type="text" id="qudrat-weight" value="25" class="weight-input"></div>
                </div>
            </div>
            <div class="score-input-row">
                <label for="tahsili">درجة التحصيلي</label>
                <div class="input-and-weight">
                    <div class="input-group"><input type="text" id="tahsili"><button type="button" class="clear-btn" onclick="clearInput('tahsili')">&times;</button></div>
                    <div class="weight-group"><input type="text" id="tahsili-weight" value="25" class="weight-input"></div>
                </div>
            </div>
        </div>
        <div class="bottom-section">
            <div class="weights-total" id="weights-total-text">مجموع الأوزان: 100%</div>
            <div class="button-group">
                <button id="calculateBtn" type="button" onclick="calculate()">احسب</button>
                <button id="clearBtn" type="button" onclick="clearData()">مسح الكل</button>
            </div>
        </div>
    </form>
    <div id="result"></div>
</div>
<div class="footer"><p class="prayer-text">دعواتكم لي ولوالدي وجميع المسلمين</p></div>
<script>
    // السكربت نفسه لم يتغير
</script>
</body>
</html>
