<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>أداة إعداد التقارير</title>

<style>
/* ===== الخط ===== */
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

/* ===== عام ===== */
body {
  font-family: 'KufamLocal', sans-serif;
  background: linear-gradient(135deg, #f2f7f6 0%, #e8eff0 100%);
  margin: 0;
  padding: 20px;
  color: #333;
}

/* ===== الأداة ===== */
.tool {
  max-width: 900px;
  margin: 30px auto;
  padding: 30px;
  background: white;
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(10, 59, 64, 0.08);
  border: 1px solid #e0e6e5;
}

.tool-header {
  text-align: center;
  margin-bottom: 30px;
  padding-bottom: 20px;
  border-bottom: 2px solid #0a3b40;
}

.tool-header h1 {
  color: #0a3b40;
  margin: 0;
  font-size: 26px;
  font-weight: 700;
}

.tool-header p {
  color: #4f6f68;
  margin-top: 8px;
  font-size: 16px;
}

/* ===== حقول الإدخال ===== */
.input-group {
  margin-bottom: 25px;
}

.tool label {
  display: block;
  margin-bottom: 8px;
  font-weight: 700;
  color: #1b5e52;
  font-size: 15px;
}

.tool input,
.tool textarea,
.tool select {
  width: 100%;
  padding: 14px;
  border: 2px solid #cfd8dc;
  border-radius: 12px;
  font-family: 'KufamLocal', sans-serif;
  font-size: 15px;
  transition: all 0.3s ease;
  box-sizing: border-box;
  background: #f9fbfb;
}

.tool input:focus,
.tool textarea:focus,
.tool select:focus {
  outline: none;
  border-color: #0a3b40;
  background: white;
  box-shadow: 0 0 0 3px rgba(10, 59, 64, 0.1);
}

.tool textarea {
  min-height: 100px;
  resize: vertical;
  line-height: 1.6;
}

.tool select {
  cursor: pointer;
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' viewBox='0 0 24 24' fill='none' stroke='%230a3b40' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpolyline points='6 9 12 15 18 9'%3E%3C/polyline%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: left 15px center;
  padding-right: 15px;
}

/* ===== معاينة الصور ===== */
.preview-container {
  margin-top: 10px;
}

.preview-container h4 {
  margin: 15px 0 10px;
  color: #1b5e52;
  font-size: 14px;
}

.preview {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
  gap: 12px;
  margin-top: 10px;
}

.preview img {
  width: 100%;
  height: 120px;
  object-fit: cover;
  border-radius: 10px;
  border: 2px solid #e0e6e5;
  transition: transform 0.3s ease;
}

.preview img:hover {
  transform: scale(1.03);
  border-color: #0a3b40;
}

/* ===== الأزرار ===== */
.button-container {
  display: flex;
  gap: 15px;
  margin-top: 30px;
}

button {
  flex: 1;
  padding: 16px;
  font-size: 17px;
  font-weight: 700;
  border: none;
  border-radius: 12px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-family: 'KufamLocal', sans-serif;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

#printBtn {
  background: linear-gradient(135deg, #0a3b40 0%, #1b5e52 100%);
  color: white;
}

#printBtn:hover {
  background: linear-gradient(135deg, #083136 0%, #164d44 100%);
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(10, 59, 64, 0.2);
}

#resetBtn {
  background: #f0f4f3;
  color: #4f6f68;
  border: 2px solid #cfd8dc;
}

#resetBtn:hover {
  background: #e8eff0;
  border-color: #8fbfb3;
}

/* ===== قالب التقرير ===== */
.report { display: none; }

/* =================== الطباعة =================== */
@page {
  size: A4;
  margin: 14mm;
}

@media print {
  body {
    background: white;
    padding: 0;
  }
  
  .tool { display: none; }
  .report { display: block; }

  .page {
    page-break-after: always;
    padding-bottom: 20mm;
  }
  
  .page:last-child { page-break-after: auto; }

  /* ===== الهيدر ===== */
  .header-full {
    background: linear-gradient(135deg, #0a3b40 0%, #1b5e52 100%);
    color: white;
    border-radius: 18px;
    padding: 22px;
    text-align: center;
    margin-bottom: 25px;
  }

  .header-full img {
    width: 110px;
    margin-bottom: 12px;
  }

  .header-full h1 {
    margin: 0;
    font-size: 20px;
    font-weight: 700;
    letter-spacing: 0.5px;
  }

  .header-full h2 {
    margin: 8px 0 0;
    font-size: 15px;
    font-weight: 400;
    opacity: 0.9;
  }

  .school-name {
    background: #0a3b40;
    color: white;
    width: fit-content;
    margin: 15px auto 25px;
    padding: 10px 35px;
    border-radius: 14px;
    font-size: 16px;
    font-weight: 700;
    text-align: center;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  /* ===== شبكة المعلومات ===== */
  .info-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 12px;
    margin-bottom: 25px;
  }

  .info-box {
    border: 2px solid #cfd8dc;
    border-radius: 14px;
    padding: 12px;
    font-size: 14px;
    background: #f9fbfb;
  }

  .info-box span {
    display: block;
    background: #e0e0e0;
    border-radius: 10px;
    padding: 6px;
    text-align: center;
    font-weight: 700;
    margin-bottom: 8px;
    font-size: 13px;
    color: #333;
  }

  /* ===== محتوى ===== */
  .grid-desc {
    display: grid;
    grid-template-columns: 1fr 90px 1fr;
    gap: 15px;
    margin-top: 25px;
  }

  .desc-box {
    border: 2px solid #cfd8dc;
    border-radius: 16px;
    padding: 18px;
    background: #f9fbfb;
  }

  .desc-box strong {
    display: block;
    color: #0a3b40;
    margin-bottom: 10px;
    font-size: 16px;
    border-bottom: 1px dashed #cfd8dc;
    padding-bottom: 8px;
  }

  /* ===== المربع النصفي المعدل ===== */
  .vertical {
    background: #eef3f1;
    border-radius: 16px;
    display: grid;
    grid-template-columns: 1fr 1px 1fr;
    align-items: center;
    padding: 15px 8px;
    font-weight: 600;
    height: 100%;
  }

  .vertical .right {
    writing-mode: vertical-rl;
    font-size: 13px;
    color: #1b5e52;
    text-align: center;
    font-weight: 700;
  }

  .vertical .left {
    writing-mode: vertical-lr;
    transform: rotate(180deg);
    font-size: 13px;
    color: #4f6f68;
    text-align: center;
    font-weight: 700;
  }

  .vertical .divider {
    width: 1px;
    height: 85%;
    background: #8fbfb3;
    margin: auto;
  }

  /* ===== الصور ===== */
  .images-page {
    margin-top: 20px;
  }
  
  .images-page h3 {
    text-align: center;
    color: #0a3b40;
    font-size: 20px;
    margin-bottom: 25px;
    padding-bottom: 10px;
    border-bottom: 2px solid #cfd8dc;
  }

  .images {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 15px;
    margin-top: 15px;
  }

  .images img {
    width: 100%;
    height: 180px;
    object-fit: cover;
    border-radius: 12px;
    border: 2px solid #b0bec5;
  }
  
  /* ===== فوتر الصفحة ===== */
  .page-footer {
    position: absolute;
    bottom: 10mm;
    left: 14mm;
    right: 14mm;
    text-align: center;
    color: #666;
    font-size: 12px;
    border-top: 1px solid #ddd;
    padding-top: 10px;
  }
}
</style>
</head>

<body>

<!-- ========= الأداة ========= -->
<div class="tool">
  <div class="tool-header">
    <h1>🖋️ أداة إعداد التقارير المدرسية</h1>
    <p>املأ النموذج أدناه لإنشاء تقرير احترافي جاهز للطباعة</p>
  </div>

  <div class="input-group">
    <label>🏫 اسم المدرسة</label>
    <input type="text" id="schoolInput" placeholder="أدخل اسم المدرسة">
  </div>

  <div class="input-group">
    <label>📄 عنوان التقرير</label>
    <select id="reportType">
      <option value="">اختر نوع التقرير</option>
      <option value="تقرير تنفيذ استراتيجية">تقرير تنفيذ استراتيجية</option>
      <option value="تقرير تنفيذ أنشطة داخل الفصل">تقرير تنفيذ أنشطة داخل الفصل</option>
      <option value="تقرير نشاط إثرائي">تقرير نشاط إثرائي</option>
      <option value="تقرير خطة علاجية">تقرير خطة علاجية</option>
      <option value="تقرير تكريم المتميزين">تقرير تكريم المتميزين</option>
    </select>
  </div>

  <div class="input-group">
    <label>📅 تاريخ التنفيذ</label>
    <input type="text" id="dateInput" placeholder="يوم / شهر / سنة">
  </div>

  <div class="input-group">
    <label>👥 المستهدفون</label>
    <input type="text" id="targetInput" placeholder="الفئة المستهدفة">
  </div>

  <div class="input-group">
    <label>🔢 عدد المستفيدين</label>
    <input type="text" id="countInput" placeholder="عدد المشاركين">
  </div>

  <div class="input-group">
    <label>📝 الوصف المختصر</label>
    <textarea id="desc1Input" placeholder="وصف مختصر للنشاط أو البرنامج"></textarea>
  </div>

  <div class="input-group">
    <label>⚙️ إجراءات التنفيذ</label>
    <textarea id="desc2Input" placeholder="الخطوات والإجراءات التنفيذية"></textarea>
  </div>

  <div class="input-group">
    <label>📊 النتائج</label>
    <textarea id="desc3Input" placeholder="النتائج المتحققة من التنفيذ"></textarea>
  </div>

  <div class="input-group">
    <label>💡 التوصيات</label>
    <textarea id="desc4Input" placeholder="التوصيات والمقترحات"></textarea>
  </div>

  <div class="input-group">
    <label>🖼️ إرفاق الصور (اختياري)</label>
    <input type="file" id="imageInput" multiple accept="image/*">
    <div class="preview-container">
      <h4>معاينة الصور المرفوعة:</h4>
      <div class="preview" id="preview"></div>
    </div>
  </div>

  <div class="button-container">
    <button id="resetBtn" onclick="resetForm()">🔄 مسح النموذج</button>
    <button id="printBtn" onclick="generateReport()">📥 تصدير PDF</button>
  </div>
</div>

<!-- ========= التقرير ========= -->
<div class="report">

<!-- الصفحة الأولى -->
<div class="page">
  <div class="header-full">
    <img src="https://i.ibb.co/2037zjqy/IMG-2102.jpg" alt="شعار الوزارة">
    <h1>الإدارة العامة للتعليم</h1>
    <h2>وزارة التعليم</h2>
  </div>

  <div class="school-name" id="school"></div>

  <div class="info-grid">
    <div class="info-box"><span>عنوان التقرير</span><div id="title"></div></div>
    <div class="info-box"><span>تاريخ التنفيذ</span><div id="date"></div></div>
    <div class="info-box"><span>المستهدفون</span><div id="target"></div></div>
    <div class="info-box"><span>عدد المستفيدين</span><div id="count"></div></div>
  </div>

  <div class="grid-desc">
    <div class="desc-box">
      <strong>وصف مختصر</strong>
      <p id="desc1"></p>
    </div>

    <div class="vertical">
      <div class="right">وصف مختصر</div>
      <div class="divider"></div>
      <div class="left">إجراءات التنفيذ</div>
    </div>

    <div class="desc-box">
      <strong>إجراءات التنفيذ</strong>
      <p id="desc2"></p>
    </div>
  </div>
  
  <div class="page-footer">صفحة 1 من 3</div>
</div>

<!-- الصفحة الثانية -->
<div class="page">
  <div class="grid-desc">
    <div class="desc-box">
      <strong>النتائج</strong>
      <p id="desc3"></p>
    </div>

    <div class="vertical">
      <div class="right">النتائج</div>
      <div class="divider"></div>
      <div class="left">التوصيات</div>
    </div>

    <div class="desc-box">
      <strong>التوصيات</strong>
      <p id="desc4"></p>
    </div>
  </div>
  
  <div class="page-footer">صفحة 2 من 3</div>
</div>

<!-- الصفحة الثالثة -->
<div class="page images-page" id="imagesPage">
  <h3>📸 شواهد الصور</h3>
  <div class="images" id="imagesContainer"></div>
  <div class="page-footer">صفحة 3 من 3</div>
</div>

</div>

<script>
// عناصر DOM
const schoolInput = document.getElementById('schoolInput');
const reportType = document.getElementById('reportType');
const dateInput = document.getElementById('dateInput');
const targetInput = document.getElementById('targetInput');
const countInput = document.getElementById('countInput');
const desc1Input = document.getElementById('desc1Input');
const desc2Input = document.getElementById('desc2Input');
const desc3Input = document.getElementById('desc3Input');
const desc4Input = document.getElementById('desc4Input');
const imageInput = document.getElementById('imageInput');

// عناصر التقرير
const schoolElement = document.getElementById('school');
const titleElement = document.getElementById('title');
const dateElement = document.getElementById('date');
const targetElement = document.getElementById('target');
const countElement = document.getElementById('count');
const desc1Element = document.getElementById('desc1');
const desc2Element = document.getElementById('desc2');
const desc3Element = document.getElementById('desc3');
const desc4Element = document.getElementById('desc4');

// تحديث التقرير في الوقت الحقيقي
schoolInput.addEventListener('input', () => schoolElement.textContent = schoolInput.value);
reportType.addEventListener('change', () => titleElement.textContent = reportType.value);
dateInput.addEventListener('input', () => dateElement.textContent = dateInput.value);
targetInput.addEventListener('input', () => targetElement.textContent = targetInput.value);
countInput.addEventListener('input', () => countElement.textContent = countInput.value);
desc1Input.addEventListener('input', () => desc1Element.textContent = desc1Input.value);
desc2Input.addEventListener('input', () => desc2Element.textContent = desc2Input.value);
desc3Input.addEventListener('input', () => desc3Element.textContent = desc3Input.value);
desc4Input.addEventListener('input', () => desc4Element.textContent = desc4Input.value);

// تحميل الصور
imageInput.addEventListener('change', function(e) {
  const preview = document.getElementById('preview');
  const container = document.getElementById('imagesContainer');
  const imagesPage = document.getElementById('imagesPage');
  
  preview.innerHTML = '';
  container.innerHTML = '';
  
  const files = Array.from(e.target.files);
  
  if (files.length === 0) {
    imagesPage.style.display = 'none';
    return;
  }
  
  imagesPage.style.display = 'block';
  
  files.forEach((file, index) => {
    if (!file.type.startsWith('image/')) return;
    
    const reader = new FileReader();
    reader.onload = function(e) {
      // صورة المعاينة
      const previewImg = document.createElement('img');
      previewImg.src = e.target.result;
      previewImg.title = `صورة ${index + 1}`;
      preview.appendChild(previewImg);
      
      // صورة التقرير
      const reportImg = document.createElement('img');
      reportImg.src = e.target.result;
      reportImg.alt = `شاهد ${index + 1}`;
      container.appendChild(reportImg);
    };
    reader.readAsDataURL(file);
  });
});

// توليد التقرير
function generateReport() {
  // التحقق من الحقول المطلوبة
  if (!schoolInput.value.trim()) {
    alert('⚠️ الرجاء إدخال اسم المدرسة');
    schoolInput.focus();
    return;
  }
  
  if (!reportType.value) {
    alert('⚠️ الرجاء اختيار نوع التقرير');
    reportType.focus();
    return;
  }
  
  if (!dateInput.value.trim()) {
    alert('⚠️ الرجاء إدخال تاريخ التنفيذ');
    dateInput.focus();
    return;
  }
  
  // تحديث التقرير النهائي
  schoolElement.textContent = schoolInput.value;
  titleElement.textContent = reportType.value;
  dateElement.textContent = dateInput.value;
  targetElement.textContent = targetInput.value || 'غير محدد';
  countElement.textContent = countInput.value || 'غير محدد';
  desc1Element.textContent = desc1Input.value || 'لا يوجد وصف';
  desc2Element.textContent = desc2Input.value || 'لا توجد إجراءات محددة';
  desc3Element.textContent = desc3Input.value || 'لا توجد نتائج مسجلة';
  desc4Element.textContent = desc4Input.value || 'لا توجد توصيات';
  
  // إظهار رسالة نجاح
  alert('✅ تم إنشاء التقرير بنجاح! جارٍ فتح نافذة الطباعة...');
  
  // تأخير بسيط لضمان تحديث العناصر
  setTimeout(() => {
    window.print();
  }, 500);
}

// مسح النموذج
function resetForm() {
  if (confirm('هل تريد مسح جميع الحقول؟')) {
    schoolInput.value = '';
    reportType.selectedIndex = 0;
    dateInput.value = '';
    targetInput.value = '';
    countInput.value = '';
    desc1Input.value = '';
    desc2Input.value = '';
    desc3Input.value = '';
    desc4Input.value = '';
    imageInput.value = '';
    
    // مسح المعاينة
    document.getElementById('preview').innerHTML = '';
    document.getElementById('imagesContainer').innerHTML = '';
    document.getElementById('imagesPage').style.display = 'block';
    
    // إعادة تعيين التقرير
    schoolElement.textContent = '';
    titleElement.textContent = '';
    dateElement.textContent = '';
    targetElement.textContent = '';
    countElement.textContent = '';
    desc1Element.textContent = '';
    desc2Element.textContent = '';
    desc3Element.textContent = '';
    desc4Element.textContent = '';
    
    alert('✅ تم مسح النموذج بنجاح');
  }
}

// تعيين تاريخ افتراضي
window.onload = function() {
  const today = new Date();
  const formattedDate = `${today.getDate()}/${today.getMonth() + 1}/${today.getFullYear()}`;
  dateInput.value = formattedDate;
  dateElement.textContent = formattedDate;
};
</script>

</body>
</html>