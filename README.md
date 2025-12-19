<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>تقرير تربوي رسمي</title>

<style>
/* ===== تضمين الخط الكوفي محليًا ===== */
@font-face {
    font-family: 'KufamLocal';
    src: url('static/Kufam-Regular.ttf') format('truetype');
    font-weight: 400;
}
@font-face {
    font-family: 'KufamLocal';
    src: url('static/Kufam-Bold.ttf') format('truetype');
    font-weight: 700;
}

/* ===== إعدادات الطباعة A4 ===== */
@page {
    size: A4;
    margin: 20mm;
}

/* ===== عام ===== */
body {
    font-family: 'KufamLocal', sans-serif;
    margin: 0;
    background: #eceff1;
    direction: rtl;
    color: #1f1f1f;
}

/* ===== الحاوية ===== */
.wrapper {
    max-width: 900px;
    margin: auto;
    padding: 15px;
}

/* ===== نموذج الإدخال ===== */
.form {
    background: #ffffff;
    padding: 22px;
    border-radius: 14px;
    box-shadow: 0 8px 25px rgba(0,0,0,0.08);
}

.form h2 {
    text-align: center;
    color: #0b3c5d;
}

.form label {
    display: block;
    margin-top: 15px;
    font-weight: 700;
}

.form input,
.form textarea {
    width: 100%;
    padding: 12px;
    margin-top: 6px;
    font-size: 16px;
    font-family: 'KufamLocal', sans-serif;
}

textarea { min-height: 120px; }

button {
    margin-top: 25px;
    width: 100%;
    padding: 14px;
    font-size: 18px;
    font-family: 'KufamLocal', sans-serif;
    background: linear-gradient(135deg, #0b3c5d, #1c5d99);
    color: white;
    border: none;
    border-radius: 10px;
    cursor: pointer;
}

/* ===== التقرير ===== */
.report {
    background: white;
    margin-top: 25px;
    padding: 25mm;
}

/* ===== الترويسة ===== */
.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 3px solid #0b3c5d;
    padding-bottom: 12px;
}

.header img {
    width: 95px;
}

.header-text h1 {
    margin: 0;
    font-size: 20px;
    font-weight: 700;
}

.header-text h2 {
    margin: 4px 0 0;
    font-size: 15px;
    font-weight: 400;
}

/* ===== عنوان التقرير ===== */
.report-title {
    text-align: center;
    margin: 30px 0;
    font-size: 24px;
    font-weight: 700;
    color: #0b3c5d;
}

/* ===== جدول البيانات ===== */
table {
    width: 100%;
    border-collapse: collapse;
    margin-bottom: 25px;
}

td {
    border: 1px solid #444;
    padding: 11px;
    font-size: 14px;
}

.label {
    background: #f0f4f8;
    font-weight: 700;
    width: 30%;
}

/* ===== العناوين ===== */
.section-title {
    margin: 28px 0 10px;
    font-size: 18px;
    font-weight: 700;
    color: #0b3c5d;
    border-right: 6px solid #0b3c5d;
    padding-right: 12px;
}

/* ===== النص ===== */
p {
    font-size: 15px;
    line-height: 2;
}

/* ===== الصور ===== */
.images {
    display: flex;
    flex-wrap: wrap;
    gap: 14px;
}

.images img {
    width: 48%;
    border-radius: 8px;
    border: 1px solid #999;
    page-break-inside: avoid;
}

/* ===== الطباعة ===== */
@media print {
    body { background: white; }
    .form { display: none; }
    .wrapper { padding: 0; }
    .report { margin: 0; }
}
</style>
</head>

<body>

<div class="wrapper">

<!-- ===== نموذج الإدخال ===== -->
<div class="form">
<h2>إدخال بيانات التقرير</h2>

<label>اسم المدرسة</label>
<input oninput="school.textContent=this.value" value="مدرسة النموذجية الثانوية">

<label>اسم المدير</label>
<input oninput="principal.textContent=this.value" value="محمد أحمد السعيد">

<label>معد التقرير</label>
<input oninput="reporter.textContent=this.value" value="خالد سعيد العتيبي">

<label>عنوان التقرير</label>
<input oninput="titleH.textContent=this.value" value="تقرير فعالية اليوم الوطني">

<label>وصف التقرير</label>
<textarea oninput="description.textContent=this.value">
تم تنفيذ فعالية بمناسبة اليوم الوطني تضمنت أنشطة ثقافية وتربوية متنوعة.
</textarea>

<label>التاريخ</label>
<input oninput="date.textContent=this.value" value="1445/06/12 هـ">

<label>المكان</label>
<input oninput="location.textContent=this.value" value="ساحة المدرسة">

<label>إدراج الصور</label>
<input type="file" multiple accept="image/*" onchange="loadImages(this.files)">

<button onclick="window.print()">تصدير PDF</button>
</div>

<!-- ===== التقرير ===== -->
<div class="report">

<div class="header">
    <img src="https://i.ibb.co/2037zjqy/IMG-2102.jpg" alt="الشعار">
    <div class="header-text">
        <h1>وزارة التعليم</h1>
        <h2>إدارة تعليم منطقة مكة المكرمة</h2>
    </div>
</div>

<div class="report-title" id="titleH">تقرير فعالية اليوم الوطني</div>

<table>
<tr><td class="label">اسم المدرسة</td><td id="school">مدرسة النموذجية الثانوية</td></tr>
<tr><td class="label">اسم المدير</td><td id="principal">محمد أحمد السعيد</td></tr>
<tr><td class="label">معد التقرير</td><td id="reporter">خالد سعيد العتيبي</td></tr>
<tr><td class="label">التاريخ</td><td id="date">1445/06/12 هـ</td></tr>
<tr><td class="label">المكان</td><td id="location">ساحة المدرسة</td></tr>
</table>

<div class="section-title">وصف التقرير</div>
<p id="description">
تم تنفيذ فعالية بمناسبة اليوم الوطني تضمنت أنشطة ثقافية وتربوية متنوعة.
</p>

<div class="section-title">الصور التوثيقية</div>
<div class="images" id="imagesContainer"></div>

</div>
</div>

<script>
function loadImages(files) {
    const container = document.getElementById("imagesContainer");
    container.innerHTML = "";
    Array.from(files).forEach(file => {
        if (!file.type.startsWith("image/")) return;
        const reader = new FileReader();
        reader.onload = e => {
            const img = document.createElement("img");
            img.src = e.target.result;
            container.appendChild(img);
        };
        reader.readAsDataURL(file);
    });
}
</script>

</body>
</html>