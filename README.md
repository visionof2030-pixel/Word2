<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>أداة إعداد التقارير</title>

<style>
/* ===== الخط الكوفي ===== */
@font-face {
  font-family: 'KufamLocal';
  src: url('static/Kufam-Regular.ttf') format('truetype');
}
@font-face {
  font-family: 'KufamLocal';
  src: url('static/Kufam-Bold.ttf') format('truetype');
  font-weight: 700;
}

/* ===== عام ===== */
body {
  font-family: 'KufamLocal', sans-serif;
  background: #f2f2f2;
  margin: 0;
}

/* ===== الأداة (الشاشة) ===== */
.tool {
  max-width: 900px;
  margin: auto;
  padding: 20px;
  background: white;
}

.tool h2 {
  text-align: center;
}

.tool label {
  display: block;
  margin-top: 12px;
  font-weight: 700;
}

.tool input,
.tool textarea {
  width: 100%;
  padding: 10px;
  margin-top: 5px;
}

.tool textarea {
  min-height: 90px;
}

.tool button {
  margin-top: 20px;
  width: 100%;
  padding: 14px;
  font-size: 18px;
  background: #0a3b40;
  color: white;
  border: none;
  border-radius: 8px;
}

/* ===== قالب التقرير (مخفي على الشاشة) ===== */
.report {
  display: none;
}

/* =================== الطباعة =================== */
@page {
  size: A4;
  margin: 16mm;
}

@media print {

  body { background: white; }

  .tool { display: none; }

  .report {
    display: block;
    font-family: 'KufamLocal', sans-serif;
  }

  .header {
    background: #0a3b40;
    color: white;
    padding: 18px;
    border-radius: 18px;
    display: grid;
    grid-template-columns: auto 1fr;
    gap: 15px;
    align-items: center;
  }

  .header img {
    width: 85px;
    background: white;
    padding: 6px;
    border-radius: 10px;
  }

  .school-name {
    background: #0a3b40;
    color: white;
    width: fit-content;
    margin: 12px auto 18px;
    padding: 8px 25px;
    border-radius: 14px;
  }

  .grid-top {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
  }

  .cell {
    border: 2px solid #cfd8dc;
    border-radius: 14px;
    padding: 10px;
    font-size: 14px;
  }

  .cell .label {
    display: block;
    background: #e0e0e0;
    border-radius: 10px;
    padding: 4px;
    text-align: center;
    font-weight: 700;
    margin-bottom: 6px;
  }

  .grid-desc {
    display: grid;
    grid-template-columns: 1fr 80px 1fr;
    gap: 10px;
    margin-top: 18px;
  }

  .desc-box {
    border: 2px solid #cfd8dc;
    border-radius: 16px;
    padding: 12px;
  }

  .vertical {
    background: #e0e0e0;
    border-radius: 16px;
    writing-mode: vertical-rl;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 700;
  }

  .images {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin-top: 18px;
  }

  .images img {
    width: 100%;
    border-radius: 12px;
    border: 1px solid #999;
  }

  .footer {
    margin-top: 25px;
    background: linear-gradient(to left, #0a3b40, #138f8f);
    color: white;
    padding: 14px;
    border-radius: 14px;
    display: grid;
    grid-template-columns: 1fr 1fr;
  }
}
</style>
</head>

<body>

<!-- ========== الأداة ========== -->
<div class="tool">
<h2>إعداد التقرير</h2>

<label>اسم المدرسة</label>
<input oninput="school.textContent=this.value" value="ثانوية الرابعة">

<label>اسم البند</label>
<input oninput="item.textContent=this.value" value="تحسين نواتج المتعلمين">

<label>عنوان التقرير</label>
<input oninput="title.textContent=this.value" value="تقرير نشاط إثرائي">

<label>تاريخ التنفيذ</label>
<input oninput="date.textContent=this.value" value="1447-06-12">

<label>المستفيدون</label>
<input oninput="benef.textContent=this.value" value="طلاب المرحلة الثانوية">

<label>الوصف المختصر</label>
<textarea oninput="desc1.textContent=this.value">وصف مختصر لما تم تنفيذه</textarea>

<label>إجراءات التنفيذ</label>
<textarea oninput="desc2.textContent=this.value">آلية التنفيذ</textarea>

<label>النتائج</label>
<textarea oninput="desc3.textContent=this.value">نتائج النشاط</textarea>

<label>التوصيات</label>
<textarea oninput="desc4.textContent=this.value">التوصيات المستقبلية</textarea>

<label>معد التقرير</label>
<input oninput="writer.textContent=this.value">

<label>مدير المدرسة</label>
<input oninput="principal.textContent=this.value">

<button onclick="window.print()">تصدير PDF</button>
</div>

<!-- ========== التقرير المطبوع ========== -->
<div class="report">

<div class="header">
  <img src="https://i.ibb.co/2037zjqy/IMG-2102.jpg">
  <div>
    <strong>الإدارة العامة للتعليم</strong><br>
    وزارة التعليم
  </div>
</div>

<div class="school-name" id="school">ثانوية الرابعة</div>

<div class="grid-top">
  <div class="cell"><span class="label">اسم البند</span><span id="item"></span></div>
  <div class="cell"><span class="label">عنوان التقرير</span><span id="title"></span></div>
  <div class="cell"><span class="label">تاريخ التنفيذ</span><span id="date"></span></div>
  <div class="cell"><span class="label">المستفيدون</span><span id="benef"></span></div>
</div>

<div class="grid-desc">
  <div class="desc-box"><strong>وصف مختصر</strong><p id="desc1"></p></div>
  <div class="vertical">إجراءات<br>التنفيذ</div>
  <div class="desc-box"><p id="desc2"></p></div>
</div>

<div class="grid-desc">
  <div class="desc-box"><strong>النتائج</strong><p id="desc3"></p></div>
  <div class="vertical">التوصيات</div>
  <div class="desc-box"><p id="desc4"></p></div>
</div>

<div class="images">
  <img src="https://via.placeholder.com/600x400">
  <img src="https://via.placeholder.com/600x400">
</div>

<div class="footer">
  <div>معد التقرير: <span id="writer"></span></div>
  <div style="text-align:left">مدير المدرسة: <span id="principal"></span></div>
</div>

</div>

</body>
</html>