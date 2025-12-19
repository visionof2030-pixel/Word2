<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>تقرير تربوي رسمي</title>

<!-- خط عربي احترافي -->
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">

<style>
/* ========== إعدادات الطباعة A4 ========== */
@page {
    size: A4;
    margin: 20mm;
}

/* ========== عام ========== */
body {
    font-family: 'Cairo', sans-serif;
    margin: 0;
    background: #eaeaea;
    direction: rtl;
    color: #222;
}

/* ========== واجهة الإدخال ========== */
.wrapper {
    max-width: 900px;
    margin: auto;
    padding: 15px;
}

.form {
    background: #ffffff;
    padding: 20px;
    border-radius: 12px;
}

.form h2 {
    text-align: center;
    color: #0d47a1;
}

.form label {
    display: block;
    margin-top: 15px;
    font-weight: 600;
}

.form input,
.form textarea {
    width: 100%;
    padding: 12px;
    margin-top: 6px;
    font-size: 16px;
}

textarea {
    min-height: 120px;
}

button {
    margin-top: 25px;
    width: 100%;
    padding: 14px;
    font-size: 18px;
    background: #0d47a1;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
}

/* ========== صفحة التقرير (A4) ========== */
.report {
    background: white;
    margin-top: 20px;
    padding: 25mm;
    border-radius: 0;
}

/* ===== الترويسة ===== */
.header {
    display: flex;
    align-items: center;
    gap: 15px;
    border-bottom: 3px solid #0d47a1;
    padding-bottom: 10px;
}

.header img {
    width: 90px;
}

.header-text h1 {
    font-size: 20px;
    margin: 0;
}

.header-text h2 {
    font-size: 16px;
    margin: 2px 0 0;
    font-weight: normal;
}

/* ===== عنوان التقرير ===== */
.report-title {
    text-align: center;
    margin: 25px 0;
    font-size: 22px;
    color: #0d47a1;
    font-weight: 700;
}

/* ===== جدول البيانات ===== */
table {
    width: 100%;
    border-collapse: collapse;
    margin-bottom: 20px;
}

td {
    border: 1px solid #444;
    padding: 10px;
    font-size: 14px;
}

.label {
    background: #f3f6fb;
    font-weight: 700;
    width: 30%;
}

/* ===== الوصف ===== */
.section-title {
    margin: 25px 0 10px;
    font-size: 18px;
    color: #0d47a1;
    border-right: 5px solid #0d47a1;
    padding-right: 10px;
}

p {
    font-size: 15px;
    line-height: 1.9;
}

/* ===== الصور ===== */
.images {
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
}

.images img {
    width: 48%;
    border: 1px solid #aaa;
    border-radius: 6px;
    page-break-inside: avoid;
}

/* ===== الطباعة ===== */
@media print {
    body {
        background: white;
    }

    .form {
        display: none;
    }

    .wrapper {
        padding: 0;
    }

    .report {
        margin: 0;
    }
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
تم تنفيذ فعالية بمناسبة اليوم الوطني تضمنت أنشطة ثقافية وتربوية متنوعة هدفت إلى تعزيز الانتماء الوطني.
</textarea>

<label>التاريخ</label>
<input oninput="date.textContent=this.value" value="1445/06/12 هـ">

<label>المكان</label>
<input oninput="location.textContent=this.value" value="ساحة المدرسة">

<label>إدراج الصور التوثيقية</label>
<input type="file" multiple accept="image/*" onchange="loadImages(this.files)">

<button onclick="window.print()">تصدير PDF</button>
</div>

<!-- ===== التقرير ===== -->
<div class="report">

<!-- الترويسة -->
<div class="header">
    <img src="https://i.ibb.co/YTXHP5GF/SVG-PNG.jpg" alt="شعار وزارة التعليم">
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
تم تنفيذ فعالية بمناسبة اليوم الوطني تضمنت أنشطة ثقافية وتربوية متنوعة هدفت إلى تعزيز الانتماء الوطني.
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