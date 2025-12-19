<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام إعداد التقارير التربوية - إدارة تعليم منطقة مكة المكرمة</title>
    
    <!-- خطوط -->
    <link href="https://fonts.googleapis.com/css2?family=Kufam:wght@400;600;700&family=Cairo:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

<style>
/* ===== إعدادات الطباعة A4 ===== */
@page {
    size: A4;
    margin: 20mm;
}

/* ===== عام ===== */
body {
    font-family: 'Cairo', 'Kufam', sans-serif;
    margin: 0;
    background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
    direction: rtl;
    color: #1f1f1f;
    line-height: 1.8;
    padding: 0;
    min-height: 100vh;
}

/* ===== حاوية عامة ===== */
.wrapper {
    max-width: 1200px;
    margin: auto;
    padding: 15px;
}

/* ===== الترويسة الثابتة ===== */
.header {
    background: linear-gradient(135deg, #2c3e50 0%, #1a252f 100%);
    color: white;
    padding: 25px 20px;
    text-align: center;
    position: fixed;
    top: 0;
    width: 100%;
    z-index: 1000;
    box-shadow: 0 5px 25px rgba(0,0,0,0.2);
    border-bottom: 4px solid #e74c3c;
    font-family: 'Cairo', sans-serif;
}

.header h1 {
    font-size: 28px;
    margin-bottom: 8px;
    font-weight: 800;
    text-shadow: 0 2px 4px rgba(0,0,0,0.2);
}

.header-subtitle {
    font-size: 16px;
    opacity: 0.9;
    font-weight: 400;
}

/* ===== تعليمات ===== */
.instruction-box {
    background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
    border-right: 4px solid #e74c3c;
    padding: 25px;
    border-radius: 8px;
    margin-bottom: 30px;
    box-shadow: 0 2px 15px rgba(0,0,0,0.08);
    position: relative;
    overflow: hidden;
    margin-top: 130px;
}

.instruction-box h3 {
    color: #2c3e50;
    margin-bottom: 15px;
    display: flex;
    align-items: center;
    gap: 12px;
    font-size: 22px;
}

.instruction-box p {
    color: #1f1f1f;
    font-size: 16px;
    line-height: 1.8;
}

/* ===== نموذج الإدخال ===== */
.form {
    background: #ffffff;
    padding: 40px;
    border-radius: 8px;
    box-shadow: 0 5px 25px rgba(0,0,0,0.1);
    margin-bottom: 40px;
    position: relative;
    overflow: hidden;
}

.form::before {
    content: '';
    position: absolute;
    top: 0;
    right: 0;
    width: 100%;
    height: 5px;
    background: linear-gradient(90deg, #2c3e50 0%, #3498db 100%);
}

.form-section {
    margin-bottom: 40px;
    padding-bottom: 30px;
    border-bottom: 2px dashed #bdc3c7;
}

.form-section:last-child {
    border-bottom: none;
}

.section-header {
    color: #2c3e50;
    border-right: 4px solid #e74c3c;
    padding-right: 20px;
    margin: 40px 0 25px;
    font-size: 24px;
    font-weight: 700;
    display: flex;
    align-items: center;
    gap: 12px;
    position: relative;
}

.section-header i {
    font-size: 22px;
    background: rgba(44, 62, 80, 0.1);
    padding: 12px;
    border-radius: 8px;
    width: 55px;
    height: 55px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.section-subtitle {
    color: #7f8c8d;
    font-size: 16px;
    margin-bottom: 30px;
    padding-right: 25px;
    line-height: 1.7;
}

.form-group {
    margin-bottom: 30px;
}

.form-label {
    display: block;
    margin-bottom: 12px;
    font-weight: 600;
    color: #2c3e50;
    font-size: 16px;
    display: flex;
    align-items: center;
    gap: 8px;
}

.form-label i {
    color: #2c3e50;
    font-size: 18px;
}

.form-label.required::after {
    content: " *";
    color: #c0392b;
    font-weight: bold;
}

.form-input, .form-select, .form-textarea {
    width: 100%;
    padding: 16px;
    border: 2px solid #bdc3c7;
    border-radius: 8px;
    font-size: 16px;
    font-family: 'Cairo', sans-serif;
    transition: all 0.3s ease;
    background-color: white;
    box-shadow: inset 0 2px 4px rgba(0,0,0,0.05);
}

.form-input:focus, .form-select:focus, .form-textarea:focus {
    outline: none;
    border-color: #2c3e50;
    box-shadow: 0 0 0 4px rgba(44, 62, 80, 0.15);
}

.form-textarea {
    min-height: 140px;
    resize: vertical;
    line-height: 1.8;
}

.form-row {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 30px;
}

.form-example {
    font-size: 14px;
    color: #7f8c8d;
    margin-top: 8px;
    font-style: italic;
    padding-right: 5px;
}

/* ===== تحميل الصور ===== */
.upload-section {
    margin-top: 40px;
    border-top: 2px dashed #bdc3c7;
    padding-top: 40px;
}

.upload-area {
    border: 3px dashed #bdc3c7;
    border-radius: 8px;
    padding: 50px 30px;
    text-align: center;
    background-color: #f9f9f9;
    cursor: pointer;
    transition: all 0.3s ease;
    margin-bottom: 25px;
    position: relative;
    overflow: hidden;
}

.upload-area:hover {
    border-color: #2c3e50;
    background-color: rgba(44, 62, 80, 0.02);
    transform: translateY(-2px);
}

.upload-area.dragover {
    border-color: #2c3e50;
    background-color: rgba(44, 62, 80, 0.05);
    animation: pulse 1.5s infinite;
}

@keyframes pulse {
    0% { box-shadow: 0 0 0 0 rgba(44, 62, 80, 0.2); }
    70% { box-shadow: 0 0 0 15px rgba(44, 62, 80, 0); }
    100% { box-shadow: 0 0 0 0 rgba(44, 62, 80, 0); }
}

.upload-icon {
    font-size: 56px;
    color: #2c3e50;
    margin-bottom: 20px;
    opacity: 0.8;
}

.upload-text {
    font-size: 18px;
    color: #2c3e50;
    margin-bottom: 12px;
    font-weight: 500;
}

.upload-hint {
    font-size: 15px;
    color: #7f8c8d;
    max-width: 500px;
    margin: 0 auto;
}

.image-preview {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
    gap: 20px;
    margin-top: 30px;
}

.preview-item {
    position: relative;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 15px rgba(0,0,0,0.08);
    border: 1px solid #bdc3c7;
    transition: all 0.3s ease;
}

.preview-item:hover {
    transform: translateY(-5px);
    box-shadow: 0 5px 25px rgba(0,0,0,0.1);
}

.preview-img {
    width: 100%;
    height: 200px;
    object-fit: cover;
    display: block;
    transition: all 0.3s ease;
}

.preview-item:hover .preview-img {
    transform: scale(1.05);
}

.preview-remove {
    position: absolute;
    top: 15px;
    left: 15px;
    background: rgba(192, 57, 43, 0.9);
    color: white;
    border: none;
    width: 35px;
    height: 35px;
    border-radius: 50%;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
    transition: all 0.3s ease;
    box-shadow: 0 2px 8px rgba(0,0,0,0.2);
}

.preview-remove:hover {
    background: #c0392b;
    transform: scale(1.1);
}

/* ===== أزرار ===== */
.action-buttons {
    display: flex;
    justify-content: space-between;
    margin-top: 60px;
    padding-top: 40px;
    border-top: 2px solid #bdc3c7;
    gap: 20px;
    flex-wrap: wrap;
}

.btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    background-color: #2c3e50;
    color: white;
    border: none;
    padding: 16px 32px;
    border-radius: 8px;
    cursor: pointer;
    font-size: 16px;
    font-weight: 600;
    transition: all 0.3s ease;
    text-decoration: none;
    min-height: 55px;
    box-shadow: 0 4px 12px rgba(44, 62, 80, 0.2);
    position: relative;
    overflow: hidden;
    font-family: 'Cairo', sans-serif;
}

.btn:hover {
    background-color: #1a252f;
    transform: translateY(-3px);
    box-shadow: 0 6px 18px rgba(44, 62, 80, 0.3);
}

.btn-success {
    background-color: #27ae60;
}

.btn-success:hover {
    background-color: #219653;
}

.btn-outline {
    background-color: transparent;
    border: 2px solid #2c3e50;
    color: #2c3e50;
    box-shadow: none;
}

.btn-outline:hover {
    background-color: #2c3e50;
    color: white;
}

/* ===== منطقة التعبئة التلقائية ===== */
.auto-fill-section {
    background: #f8f9fa;
    border-radius: 8px;
    padding: 20px;
    margin: 20px 0;
    border-right: 4px solid #2980b9;
}

.auto-fill-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 15px;
}

.auto-fill-title {
    color: #2980b9;
    font-weight: 600;
    font-size: 18px;
    display: flex;
    align-items: center;
    gap: 10px;
}

.btn-sm {
    padding: 8px 16px;
    font-size: 14px;
    min-height: 40px;
}

/* ===== معاينة التقرير ===== */
.report {
    background: white;
    margin-top: 25px;
    padding: 25mm;
    display: none;
    box-shadow: 0 8px 25px rgba(0,0,0,0.1);
    border-radius: 8px;
}

.report.show {
    display: block;
}

.report-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 3px solid #2c3e50;
    padding-bottom: 12px;
}

.report-header img {
    width: 95px;
}

.report-header-text {
    text-align: left;
}

.report-header-text h1 {
    font-size: 20px;
    margin: 0;
    font-weight: 700;
    color: #2c3e50;
}

.report-header-text h2 {
    font-size: 15px;
    margin: 4px 0 0;
    font-weight: 400;
    color: #7f8c8d;
}

.report-title {
    text-align: center;
    margin: 30px 0 25px;
    font-size: 24px;
    color: #2c3e50;
    font-weight: 700;
    letter-spacing: 0.5px;
}

.report-table {
    width: 100%;
    border-collapse: collapse;
    margin-bottom: 25px;
}

.report-table td {
    border: 1px solid #444;
    padding: 11px;
    font-size: 14px;
}

.report-label {
    background: #f0f4f8;
    font-weight: 700;
    width: 30%;
}

.section-title {
    margin: 28px 0 10px;
    font-size: 18px;
    color: #2c3e50;
    border-right: 6px solid #2c3e50;
    padding-right: 12px;
    font-weight: 700;
}

.report-content {
    font-size: 15px;
    line-height: 2;
    margin: 0;
}

.report-images {
    display: flex;
    flex-wrap: wrap;
    gap: 14px;
    margin-top: 20px;
}

.report-images img {
    width: 48%;
    border-radius: 8px;
    border: 1px solid #999;
    page-break-inside: avoid;
}

/* ===== التمرير للأعلى ===== */
.scroll-indicator {
    position: fixed;
    bottom: 40px;
    left: 40px;
    background: linear-gradient(135deg, #2c3e50 0%, #3498db 100%);
    color: white;
    width: 55px;
    height: 55px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 22px;
    cursor: pointer;
    box-shadow: 0 6px 20px rgba(44, 62, 80, 0.3);
    transition: all 0.3s ease;
    z-index: 100;
    opacity: 0;
    transform: translateY(20px);
}

.scroll-indicator.visible {
    opacity: 1;
    transform: translateY(0);
}

.scroll-indicator:hover {
    background: #1a252f;
    transform: translateY(-5px) scale(1.05);
}

/* ===== رسائل التنبيه ===== */
.alert {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: white;
    padding: 30px 40px;
    border-radius: 8px;
    box-shadow: 0 15px 40px rgba(0,0,0,0.2);
    text-align: center;
    z-index: 3000;
    display: none;
    max-width: 500px;
    width: 90%;
}

.alert.show {
    display: block;
    animation: fadeIn 0.3s ease;
}

@keyframes fadeIn {
    from { opacity: 0; transform: translate(-50%, -50%) scale(0.9); }
    to { opacity: 1; transform: translate(-50%, -50%) scale(1); }
}

.alert-icon {
    font-size: 70px;
    margin-bottom: 25px;
}

.alert-icon.success {
    color: #27ae60;
}

.alert-icon.error {
    color: #c0392b;
}

.alert-title {
    font-size: 26px;
    color: #2c3e50;
    margin-bottom: 15px;
    font-weight: 700;
}

.alert-details {
    color: #7f8c8d;
    font-size: 16px;
    margin-bottom: 25px;
    line-height: 1.8;
}

/* ===== الطباعة ===== */
@media print {
    body {
        background: white;
    }

    .header,
    .instruction-box,
    .form,
    .action-buttons,
    .scroll-indicator {
        display: none !important;
    }

    .wrapper {
        padding: 0;
    }

    .report {
        margin: 0;
        box-shadow: none;
        padding: 20mm;
        display: block !important;
    }
    
    .report.show {
        display: block !important;
    }
}

@media (max-width: 992px) {
    .form-row {
        grid-template-columns: 1fr;
    }
    
    .wrapper {
        padding: 10px;
    }
    
    .form {
        padding: 30px 20px;
    }
}

@media (max-width: 768px) {
    .header h1 {
        font-size: 20px;
    }
    
    .instruction-box {
        margin-top: 120px;
        padding: 20px;
    }
    
    .action-buttons {
        flex-direction: column;
    }
    
    .action-buttons .btn {
        width: 100%;
    }
    
    .scroll-indicator {
        bottom: 20px;
        left: 20px;
        width: 50px;
        height: 50px;
    }
}
</style>
</head>

<body>

<!-- الترويسة الثابتة -->
<div class="header">
    <h1>نظام إعداد التقارير التربوية</h1>
    <div class="header-subtitle">إدارة تعليم منطقة مكة المكرمة</div>
</div>

<!-- تعليمات -->
<div class="wrapper">
<div class="instruction-box">
    <h3><i class="fas fa-info-circle"></i> تعليمات إعداد التقرير</h3>
    <p>يرجى تعبئة جميع الحقول المطلوبة (*) بدقة. يمكنك استخدام زر "تعبئة تلقائية" لملء الحقول بالنصوص المناسبة حسب نوع التقرير، ثم تعديلها حسب الحاجة.</p>
</div>

<!-- ===== نموذج الإدخال ===== -->
<div class="form">
    
    <div class="form-section">
        <h2 class="section-header"><i class="fas fa-file-signature"></i> اختيار نوع التقرير</h2>
        <p class="section-subtitle">اختر نوع التقرير المناسب لهذا البند من القائمة التالية</p>
        
        <div class="form-group">
            <label class="form-label required"><i class="fas fa-tasks"></i> أداء الواجبات الوظيفية (البند رقم 1)</label>
            <select class="form-select" id="reportType">
                <option value="">اختر نوع التقرير...</option>
                <option value="strategy" selected>تقرير تنفيذ استراتيجية تدريس</option>
                <option value="activity-session">تقرير حصة النشاط الطلابي</option>
                <option value="class-activities">تقرير الأنشطة الصفية</option>
                <option value="educational-trip">تقرير رحلة تربوية</option>
                <option value="workshop">تقرير ورشة عمل تربوية</option>
                <option value="competition">تقرير مسابقة مدرسية</option>
                <option value="parent-meeting">تقرير اجتماع أولياء الأمور</option>
                <option value="training-program">تقرير برنامج تدريبي</option>
                <option value="educational-project">تقرير مشروع تربوي</option>
                <option value="scientific-club">تقرير النادي العلمي</option>
                <option value="cultural-activity">تقرير نشاط ثقافي</option>
                <option value="sports-activity">تقرير نشاط رياضي</option>
                <option value="art-activity">تقرير نشاط فني</option>
                <option value="technology-activity">تقرير نشاط تقني</option>
                <option value="learning-communities">تقرير مجتمعات التعلم</option>
                <option value="practical-lesson">تقرير تنفيذ درس تطبيقي</option>
                <option value="training-courses">تقرير حضور دورات وورش تدريبية</option>
                <option value="parent-communication">تقرير التواصل مع ولي الأمر</option>
                <option value="parent-notification">تقرير إشعار ولي الأمر عن مستوى ابنه</option>
                <option value="parent-attendance">تقرير حضور اجتماع أولياء الأمور</option>
                <option value="weekly-plan">تقرير تفعيل الخطة الاسبوعية</option>
                <option value="results-analysis">تقرير تحليل نتائج الطلاب</option>
                <option value="student-diagnosis">تقرير تشخيص الطلاب حسب مستوياتهم</option>
                <option value="improvement-test">تقرير تنفيذ اختبار تحسن</option>
                <option value="student-participation">تقرير المشاركات بين الطلاب</option>
            </select>
        </div>
        
        <div class="auto-fill-section">
            <div class="auto-fill-header">
                <div class="auto-fill-title">
                    <i class="fas fa-magic"></i> تعبئة تلقائية للحقول
                </div>
                <button class="btn btn-sm" id="autoFillBtn" style="background-color: #2980b9;">
                    <i class="fas fa-bolt"></i> تعبئة تلقائية
                </button>
            </div>
            <p style="color: #7f8c8d; font-size: 14px; line-height: 1.6;">
                سيتم تعبئة الحقول التالية تلقائياً بناءً على نوع التقرير المحدد. يمكنك تعديل النصوص بعد ذلك حسب الحاجة.
            </p>
        </div>
    </div>

    <div class="form-section">
        <h2 class="section-header"><i class="fas fa-database"></i> البيانات الرئيسية</h2>
        <p class="section-subtitle">البيانات الرئيسية التي ستظهر في رأس التقرير النهائي</p>
        
        <div class="form-row">
            <div class="form-group">
                <label class="form-label required"><i class="fas fa-map-marker-alt"></i> اسم المنطقة</label>
                <input type="text" class="form-input" id="region" placeholder="مكة المكرمة" value="مكة المكرمة">
                <div class="form-example">مثال: مكة المكرمة، المدينة المنورة، الرياض</div>
            </div>
            
            <div class="form-group">
                <label class="form-label required"><i class="fas fa-school"></i> اسم المدرسة</label>
                <input type="text" class="form-input" id="school" placeholder="اسم المدرسة" value="سعيد بن العاص المتوسطة">
            </div>
        </div>
        
        <div class="form-row">
            <div class="form-group">
                <label class="form-label required"><i class="fas fa-user-tie"></i> مدير المدرسة</label>
                <input type="text" class="form-input" id="principal" placeholder="مدير المدرسة" value="نايف عوض اللحياني">
                <div class="form-example">مثال: نايف عوض اللحياني</div>
            </div>
            
            <div class="form-group">
                <label class="form-label required"><i class="fas fa-user-edit"></i> معد التقرير</label>
                <input type="text" class="form-input" id="reporter" placeholder="معد التقرير" value="فهد نغيمش الخالدي">
                <div class="form-example">مثال: فهد نغيمش الخالدي</div>
            </div>
        </div>
        
        <div class="form-group">
            <label class="form-label required"><i class="fas fa-heading"></i> عنوان التقرير</label>
            <input type="text" class="form-input" id="reportTitle" placeholder="عنوان التقرير" value="تقرير تنفيذ استراتيجية تدريس">
        </div>
        
        <div class="form-group">
            <label class="form-label required"><i class="fas fa-book"></i> تابع للمناهج (نعم/لا)</label>
            <select class="form-select" id="curriculumRelated">
                <option value="نعم" selected>نعم</option>
                <option value="لا">لا</option>
            </select>
        </div>
    </div>

    <div class="form-section">
        <h2 class="section-header"><i class="fas fa-calendar-alt"></i> تفاصيل البرنامج</h2>
        <p class="section-subtitle">التفاصيل الزمنية والمكانية للبرنامج المنفذ</p>
        
        <div class="form-row">
            <div class="form-group">
                <label class="form-label required"><i class="fas fa-calendar"></i> تاريخ البرنامج (هجري)</label>
                <input type="text" class="form-input" id="programDate" placeholder="1447-06-12" value="1447-06-12">
                <div class="form-example">التاريخ الهجري بالصيغة: 1447-06-12</div>
            </div>
            
            <div class="form-group">
                <label class="form-label required"><i class="fas fa-map-marker"></i> مكان التنفيذ</label>
                <input type="text" class="form-input" id="location" placeholder="مثال: قاعة المصادر" value="قاعة المصادر">
                <div class="form-example">مثال: قاعة المصادر، الفصل الدراسي، الساحة المدرسية</div>
            </div>
        </div>
        
        <div class="form-row">
            <div class="form-group">
                <label class="form-label required"><i class="fas fa-users"></i> المستهدفون</label>
                <input type="text" class="form-input" id="target" placeholder="مثال: طلاب الصف الثالث متوسط" value="طلاب الصف الثالث متوسط">
                <div class="form-example">مثال: طلاب الصف الثالث متوسط، معلمو المرحلة</div>
            </div>
            
            <div class="form-group">
                <label class="form-label required"><i class="fas fa-user-check"></i> عدد المستفيدين</label>
                <input type="number" class="form-input" id="beneficiaries" placeholder="مثال: 30" value="30" min="1">
                <div class="form-example">أدخل عدد المستفيدين من البرنامج (رقم فقط)</div>
            </div>
        </div>
    </div>

    <div class="form-section">
        <h2 class="section-header"><i class="fas fa-align-left"></i> وصف النشاط</h2>
        <p class="section-subtitle">وصف شامل وواضح للنشاط الذي تم تنفيذه</p>
        
        <div class="form-group">
            <label class="form-label required"><i class="fas fa-clipboard-list"></i> وصف مختصر لما تم تنفيذه</label>
            <textarea class="form-textarea" id="description" placeholder="وصف مختصر لما تم تنفيذه في النشاط">تم تنفيذ استراتيجية التدريس وفق الخطة المعتمدة، مع توزيع الطلاب على مجموعات عمل تعاونية وتنويع الأنشطة بما يناسب ميولهم واحتياجاتهم. تم تطبيق استراتيجية التعلم النشط من خلال أنشطة عملية وتفاعلية.</textarea>
            <div class="form-example">يجب أن يتضمن الوصف ملخصاً واضحاً وشاملاً للنشاط المنفذ</div>
        </div>
    </div>

    <div class="form-section">
        <h2 class="section-header"><i class="fas fa-tasks"></i> إجراءات التنفيذ</h2>
        <p class="section-subtitle">الخطوات والإجراءات التي تم اتباعها لتنفيذ النشاط</p>
        
        <div class="form-group">
            <label class="form-label required"><i class="fas fa-list-ol"></i> إجراءات التنفيذ (افصل بين النقاط بفاصلة)</label>
            <textarea class="form-textarea" id="procedures" placeholder="أدخل إجراءات التنفيذ">إعداد خطة حصة النشاط وتحديد الأهداف والأنشطة المناسبة, توزيع الطلاب إلى مجموعات عمل وتوضيح المهام لكل مجموعة, توفير المواد والأدوات اللازمة للنشاط, متابعة تنفيذ الطلاب للنشاط وتقديم التوجيه اللازم, تقييم مخرجات النشاط من قبل الطلاب والمعلم</textarea>
            <div class="form-example">أدخل كل إجراء في سطر جديد أو افصل بين النقاط بفاصلة (,) كل إجراء يجب أن يكون جملة كاملة</div>
        </div>
    </div>

    <div class="form-section">
        <h2 class="section-header"><i class="fas fa-chart-line"></i> النتائج</h2>
        <p class="section-subtitle">النتائج المتحققة والأثر الإيجابي للنشاط</p>
        
        <div class="form-group">
            <label class="form-label required"><i class="fas fa-chart-bar"></i> النتائج (افصل بين النقاط بفاصلة)</label>
            <textarea class="form-textarea" id="results" placeholder="أدخل النتائج المتحققة">تفاعل إيجابي من الطلاب أثناء تنفيذ استراتيجية التدريس, تنمية روح التعاون والعمل الجماعي بين الطلاب, اكتشاف مواهب الطلاب في مجالات متنوعة, تطبيق المعرفة النظرية في أنشطة عملية, زيادة دافعية الطلاب للتعلم والمشاركة</textarea>
            <div class="form-example">اذكر النتائج الإيجابية التي تحققت من تنفيذ النشاط بشكل واضح ومفصل</div>
        </div>
    </div>

    <div class="form-section">
        <h2 class="section-header"><i class="fas fa-lightbulb"></i> التوصيات</h2>
        <p class="section-subtitle">توصيات للتحسين والتطوير في المستقبل</p>
        
        <div class="form-group">
            <label class="form-label required"><i class="fas fa-comments"></i> التوصيات</label>
            <textarea class="form-textarea" id="recommendations" placeholder="أدخل التوصيات">الاستمرار في تنويع استراتيجيات التدريس وتوثيق الممارسات المميزة لإثراء التجارب المستقبلية. توفير المزيد من الموارد والأدوات اللازمة للأنشطة العملية. تشجيع الطلاب المبدعين للمشاركة في المسابقات والمنافسات الخارجية. عقد ورش عمل للمعلمين لتبادل الخبرات في مجال استراتيجيات التدريس الحديثة.</textarea>
            <div class="form-example">قدم توصيات واضحة وعملية للتحسين والتطوير في المستقبل</div>
        </div>
    </div>

    <div class="form-section upload-section">
        <h2 class="section-header"><i class="fas fa-images"></i> الصور المرفقة بالتقرير</h2>
        <p class="section-subtitle">صور توثيقية للنشاط المنفذ (صورتان كحد أقصى)</p>
        
        <div class="upload-area" id="uploadArea">
            <div class="upload-icon">
                <i class="fas fa-cloud-upload-alt"></i>
            </div>
            <div class="upload-text">انقر لرفع الصور أو اسحبها إلى هنا</div>
            <div class="upload-hint">الحجم الأقصى: 5MB لكل صورة | الصيغ المدعومة: JPG, PNG, GIF | الحد الأقصى: 4 صور</div>
            <input type="file" id="imageUpload" accept="image/*" multiple style="display: none;">
        </div>
        
        <div class="image-preview" id="imagePreview"></div>
        
        <div class="form-group" style="margin-top: 20px;">
            <label class="form-label"><i class="fas fa-tips"></i> نصائح للصور المرفقة:</label>
            <ul style="padding-right: 20px; color: #7f8c8d; font-size: 14px; line-height: 1.8;">
                <li>صورة توثيق تنفيذ النشاط داخل الصف أو ساحة المدرسة</li>
                <li>صورة لأعمال أو منتجات الطلاب الناتجة عن النشاط</li>
                <li>صورة لعرض الطلاب لمخرجاتهم أو مشاركتهم في النشاط</li>
                <li>يفضل إرفاق صور واضحة توثق التنفيذ أو النماذج أو أعمال الطلاب</li>
            </ul>
        </div>
    </div>

    <div class="action-buttons">
        <button class="btn btn-outline" id="previewReport">
            <i class="fas fa-eye"></i> معاينة التقرير
        </button>
        <button class="btn btn-success" id="createReport">
            <i class="fas fa-file-alt"></i> إنشاء وطباعة التقرير
        </button>
    </div>
</div>

<!-- ===== التقرير النهائي ===== -->
<div class="report" id="finalReport">

<div class="report-header">
    <img src="https://i.ibb.co/2037zjqy/IMG-2102.jpg" alt="شعار الجهة">
    <div class="report-header-text">
        <h1>وزارة التعليم</h1>
        <h2>إدارة تعليم منطقة مكة المكرمة</h2>
    </div>
</div>

<div class="report-title" id="reportTitlePreview">تقرير فعالية اليوم الوطني</div>

<table class="report-table">
<tr><td class="report-label">اسم المدرسة</td><td id="schoolPreview">مدرسة النموذجية الثانوية</td></tr>
<tr><td class="report-label">اسم المدير</td><td id="principalPreview">محمد أحمد السعيد</td></tr>
<tr><td class="report-label">معد التقرير</td><td id="reporterPreview">خالد سعيد العتيبي</td></tr>
<tr><td class="report-label">التاريخ</td><td id="datePreview">1445/06/12 هـ</td></tr>
<tr><td class="report-label">المكان</td><td id="locationPreview">ساحة المدرسة</td></tr>
<tr><td class="report-label">المستهدفون</td><td id="targetPreview">طلاب الصف الثالث متوسط</td></tr>
<tr><td class="report-label">عدد المستفيدين</td><td id="beneficiariesPreview">30</td></tr>
<tr><td class="report-label">تابع للمناهج</td><td id="curriculumRelatedPreview">نعم</td></tr>
</table>

<div class="section-title">وصف التقرير</div>
<p class="report-content" id="descriptionPreview">
تم تنفيذ فعالية بمناسبة اليوم الوطني تضمنت أنشطة ثقافية وتربوية متنوعة هدفت إلى تعزيز الانتماء الوطني والهوية السعودية.
</p>

<div class="section-title">إجراءات التنفيذ</div>
<p class="report-content" id="proceduresPreview">
إعداد خطة حصة النشاط وتحديد الأهداف والأنشطة المناسبة، توزيع الطلاب إلى مجموعات عمل وتوضيح المهام لكل مجموعة، توفير المواد والأدوات اللازمة للنشاط، متابعة تنفيذ الطلاب للنشاط وتقديم التوجيه اللازم، تقييم مخرجات النشاط من قبل الطلاب والمعلم.
</p>

<div class="section-title">النتائج</div>
<p class="report-content" id="resultsPreview">
تفاعل إيجابي من الطلاب أثناء تنفيذ استراتيجية التدريس، تنمية روح التعاون والعمل الجماعي بين الطلاب، اكتشاف مواهب الطلاب في مجالات متنوعة، تطبيق المعرفة النظرية في أنشطة عملية، زيادة دافعية الطلاب للتعلم والمشاركة.
</p>

<div class="section-title">التوصيات</div>
<p class="report-content" id="recommendationsPreview">
الاستمرار في تنويع استراتيجيات التدريس وتوثيق الممارسات المميزة لإثراء التجارب المستقبلية. توفير المزيد من الموارد والأدوات اللازمة للأنشطة العملية. تشجيع الطلاب المبدعين للمشاركة في المسابقات والمنافسات الخارجية. عقد ورش عمل للمعلمين لتبادل الخبرات في مجال استراتيجيات التدريس الحديثة.
</p>

<div class="section-title">الصور التوثيقية</div>
<div class="report-images" id="reportImagesPreview"></div>

</div>

</div>

<!-- زر التمرير للأعلى -->
<div class="scroll-indicator" id="scrollToTop">
    <i class="fas fa-arrow-up"></i>
</div>

<!-- رسالة تنبيه -->
<div class="alert" id="successAlert">
    <div class="alert-icon success">
        <i class="fas fa-check-circle"></i>
    </div>
    <h3 class="alert-title">تم إنشاء التقرير بنجاح!</h3>
    <p class="alert-details">يمكنك الآن معاينة التقرير وطباعته كملف PDF</p>
    <button class="btn btn-success" onclick="hideAlert()">
        <i class="fas fa-check"></i> موافق
    </button>
</div>

<script>
document.addEventListener('DOMContentLoaded', function() {
    const uploadArea = document.getElementById('uploadArea');
    const imageUpload = document.getElementById('imageUpload');
    const imagePreview = document.getElementById('imagePreview');
    const previewReportBtn = document.getElementById('previewReport');
    const createReportBtn = document.getElementById('createReport');
    const autoFillBtn = document.getElementById('autoFillBtn');
    const scrollToTopBtn = document.getElementById('scrollToTop');
    const finalReport = document.getElementById('finalReport');
    const successAlert = document.getElementById('successAlert');
    
    let uploadedImages = [];
    
    // نصوص تلقائية لأنواع التقارير المختلفة
    const reportTemplates = {
        'strategy': {
            description: 'تم تنفيذ استراتيجية تدريس حديثة تعتمد على التعلم النشط والتعاوني، حيث تم تصميم الأنشطة لتتناسب مع قدرات الطلاب المختلفة وتنمي مهارات التفكير العليا لديهم. ركزت الاستراتيجية على جعل الطالب محور العملية التعليمية.',
            procedures: 'تحليل المحتوى التعليمي وتحديد الأهداف, تصميم أنشطة تعليمية متنوعة, تقسيم الطلاب إلى مجموعات عمل, توفير الأدوات والمواد التعليمية, تقديم التوجيه والإرشاد, تقييم الأداء وتقديم التغذية الراجعة',
            results: 'تحسن ملحوظ في مستوى الفهم والاستيعاب, زيادة مشاركة الطلاب في الأنشطة الصفية, تنمية مهارات العمل الجماعي, ارتفاع مستوى التحصيل الدراسي, تعزيز الثقة بالنفس لدى الطلاب',
            recommendations: 'الاستمرار في تطبيق استراتيجيات التعلم النشط, تنظيم ورش عمل للمعلمين حول استراتيجيات التدريس, توفير المزيد من الموارد التعليمية, توثيق التجارب الناجحة ونشرها'
        },
        'activity-session': {
            description: 'تم تنفيذ حصة نشاط طلابي هادفة تهدف إلى تنمية المهارات الحياتية والاجتماعية للطلاب، حيث اشتملت على أنشطة عملية وتفاعلية تعزز القيم والمبادئ التربوية.',
            procedures: 'تحديد أهداف حصة النشاط, إعداد المواد والأدوات اللازمة, تنظيم المكان وتجهيزه, شرح النشاط وتوزيع المهام, متابعة تنفيذ الطلاب, تقييم النتائج وتلخيصها',
            results: 'تفاعل إيجابي من جميع الطلاب, اكتشاف مواهب وقدرات جديدة, تنمية روح التعاون والمسؤولية, تحسين المهارات الاجتماعية, زيادة الحماس للأنشطة المدرسية',
            recommendations: 'تنويع أنشطة الحصص النشاطية, تخصيص مساحة أكبر للأنشطة, إشراك أولياء الأمور في بعض الأنشطة, تنظيم مسابقات بين الفصول'
        },
        'learning-communities': {
            description: 'تم تنفيذ برنامج مجتمعات التعلم المهنية بهدف تطوير الممارسات التعليمية وتبادل الخبرات بين المعلمين، حيث تم التركيز على العمل الجماعي والتفكير النقدي.',
            procedures: 'تحديد موضوع مجتمع التعلم, تشكيل فريق العمل, إعداد خطة الجلسات, تنفيذ جلسات النقاش والتحليل, توثيق المخرجات والتوصيات, متابعة تنفيذ التوصيات',
            results: 'تحسين الممارسات التعليمية, تبادل الخبرات بين المعلمين, تطوير أساليب تقييم الطلاب, تعزيز العمل الجماعي, رفع مستوى الكفاءة المهنية',
            recommendations: 'استمرار عقد جلسات مجتمعات التعلم, توسيع نطاق المشاركة, تخصيص وقت كاف للجلسات, توثيق أفضل الممارسات ونشرها'
        },
        'practical-lesson': {
            description: 'تم تنفيذ درس تطبيقي عملي يهدف إلى ربط المعرفة النظرية بالتطبيق العملي، حيث تم استخدام أساليب تدريس تفاعلية وتطبيقية.',
            procedures: 'تحضير الوسائل والأدوات العملية, تصميم الأنشطة التطبيقية, شرح المفهوم النظري, تنفيذ التطبيق العملي, مناقشة النتائج والتطبيقات, تقييم مستوى الفهم',
            results: 'تحسين الفهم العملي للمفاهيم, تنمية المهارات التطبيقية, زيادة تفاعل الطلاب مع المادة العلمية, ربط المعرفة بالحياة العملية, تحسين مستوى الاحتفاظ بالمعلومات',
            recommendations: 'زيادة عدد الدروس التطبيقية, توفير الأدوات والمواد اللازمة, تدريب المعلمين على تصميم الدروس التطبيقية, توثيق الدروس الناجحة'
        },
        'training-courses': {
            description: 'تم حضور دورات وورش تدريبية متخصصة تهدف إلى تطوير المهارات المهنية والمعرفية في مجال التخصص.',
            procedures: 'التسجيل في البرنامج التدريبي, حضور الجلسات التدريبية, المشاركة في الأنشطة والتطبيقات العملية, تنفيذ المهام والتكليفات التدريبية, المشاركة في المناقشات وتبادل الخبرات',
            results: 'اكتساب معارف ومهارات جديدة, تطوير الممارسات المهنية, زيادة الوعي بأحدث المستجدات في التخصص, تحسين الكفاءة المهنية, توسيع الشبكة المهنية',
            recommendations: 'الاستمرار في المشاركة في البرامج التدريبية, تطبيق ما تم تعلمه في الميدان, نقل المعرفة للزملاء, المشاركة في تصميم برامج تدريبية'
        },
        'parent-communication': {
            description: 'تم التواصل مع أولياء الأمور بهدف متابعة مستوى الطلاب ودراسة احتياجاتهم وتقديم الدعم اللازم لهم.',
            procedures: 'تحديد أولويات التواصل, إعداد تقارير عن مستوى الطلاب, التواصل عبر الوسائل المتاحة (هاتف، زيارة، رسالة), مناقشة التحديات والمشكلات, تقديم التوصيات والمقترحات, متابعة تنفيذ التوصيات',
            results: 'تحسين مستوى التواصل مع الأسر, التعرف على احتياجات الطلاب بشكل أفضل, زيادة وعي أولياء الأمور بمستوى أبنائهم, تحسين دعم الطلاب دراسياً, تعزيز الشراكة بين المدرسة والأسرة',
            recommendations: 'تنويع وسائل التواصل مع الأسر, زيادة وتيرة التواصل, إشراك أولياء الأمور في خطط التحسين, توثيق عمليات التواصل'
        }
    };
    
    // إعداد مستمعي الأحداث
    function setupEventListeners() {
        uploadArea.addEventListener('click', function() {
            imageUpload.click();
        });
        
        uploadArea.addEventListener('dragover', function(e) {
            e.preventDefault();
            this.classList.add('dragover');
        });
        
        uploadArea.addEventListener('dragleave', function() {
            this.classList.remove('dragover');
        });
        
        uploadArea.addEventListener('drop', function(e) {
            e.preventDefault();
            this.classList.remove('dragover');
            const files = e.dataTransfer.files;
            handleImageUpload(files);
        });
        
        imageUpload.addEventListener('change', function(e) {
            const files = e.target.files;
            handleImageUpload(files);
        });
        
        scrollToTopBtn.addEventListener('click', function() {
            window.scrollTo({ top: 0, behavior: 'smooth' });
        });
        
        window.addEventListener('scroll', function() {
            if (window.scrollY > 300) {
                scrollToTopBtn.classList.add('visible');
            } else {
                scrollToTopBtn.classList.remove('visible');
            }
        });
        
        previewReportBtn.addEventListener('click', previewReport);
        createReportBtn.addEventListener('click', createReport);
        autoFillBtn.addEventListener('click', autoFillFields);
    }
    
    function handleImageUpload(files) {
        if (uploadedImages.length + files.length > 4) {
            showError('يمكنك رفع 4 صور كحد أقصى فقط');
            return;
        }
        
        for (let i = 0; i < files.length; i++) {
            const file = files[i];
            
            if (!file.type.startsWith('image/')) {
                showError('الرجاء رفع ملفات صور فقط (JPG, PNG, GIF)');
                continue;
            }
            
            if (file.size > 5 * 1024 * 1024) {
                showError('حجم الصورة يجب أن يكون أقل من 5MB');
                continue;
            }
            
            const reader = new FileReader();
            
            reader.onload = function(e) {
                uploadedImages.push({
                    data: e.target.result,
                    name: file.name,
                    type: file.type
                });
                updateImagePreview();
            };
            
            reader.readAsDataURL(file);
        }
        
        imageUpload.value = '';
    }
    
    function updateImagePreview() {
        imagePreview.innerHTML = '';
        
        uploadedImages.forEach((imgData, index) => {
            const item = document.createElement('div');
            item.className = 'preview-item';
            
            item.innerHTML = `
                <img src="${imgData.data}" class="preview-img" alt="صورة ${index + 1}">
                <button class="preview-remove" data-index="${index}">
                    <i class="fas fa-times"></i>
                </button>
            `;
            
            imagePreview.appendChild(item);
        });
        
        document.querySelectorAll('.preview-remove').forEach(btn => {
            btn.addEventListener('click', function() {
                const index = parseInt(this.dataset.index);
                uploadedImages.splice(index, 1);
                updateImagePreview();
            });
        });
    }
    
    function autoFillFields() {
        const reportType = document.getElementById('reportType').value;
        const reportTitle = document.getElementById('reportTitle').value;
        
        if (!reportType) {
            showError('يرجى اختيار نوع التقرير أولاً');
            return;
        }
        
        const template = reportTemplates[reportType];
        if (template) {
            // تعبئة الحقول بالنصوص التلقائية
            document.getElementById('description').value = template.description;
            document.getElementById('procedures').value = template.procedures;
            document.getElementById('results').value = template.results;
            document.getElementById('recommendations').value = template.recommendations;
            
            // تحديث عنوان التقرير إذا لم يتم تعديله
            if (!reportTitle || reportTitle === 'تقرير تنفيذ استراتيجية تدريس') {
                const reportTypeText = document.getElementById('reportType').options[document.getElementById('reportType').selectedIndex].text;
                document.getElementById('reportTitle').value = reportTypeText;
            }
            
            showSuccess('تم تعبئة الحقول تلقائياً بنجاح. يمكنك تعديل النصوص حسب الحاجة.');
        } else {
            showError('لا يوجد قالب لهذا النوع من التقارير');
        }
    }
    
    function previewReport() {
        // تحديث معاينة التقرير
        updateReportPreview();
        
        // إظهار قسم التقرير
        finalReport.classList.add('show');
        
        // التمرير إلى قسم التقرير
        finalReport.scrollIntoView({ behavior: 'smooth' });
        
        showSuccess('تم تحديث معاينة التقرير بنجاح');
    }
    
    function createReport() {
        // تحديث معاينة التقرير
        updateReportPreview();
        
        // إظهار قسم التقرير
        finalReport.classList.add('show');
        
        // إظهار رسالة النجاح
        showAlert();
        
        // التمرير إلى قسم التقرير
        finalReport.scrollIntoView({ behavior: 'smooth' });
    }
    
    function updateReportPreview() {
        // تحديث بيانات التقرير
        document.getElementById('reportTitlePreview').textContent = document.getElementById('reportTitle').value;
        document.getElementById('schoolPreview').textContent = document.getElementById('school').value;
        document.getElementById('principalPreview').textContent = document.getElementById('principal').value;
        document.getElementById('reporterPreview').textContent = document.getElementById('reporter').value;
        document.getElementById('datePreview').textContent = document.getElementById('programDate').value;
        document.getElementById('locationPreview').textContent = document.getElementById('location').value;
        document.getElementById('targetPreview').textContent = document.getElementById('target').value;
        document.getElementById('beneficiariesPreview').textContent = document.getElementById('beneficiaries').value;
        document.getElementById('curriculumRelatedPreview').textContent = document.getElementById('curriculumRelated').value;
        document.getElementById('descriptionPreview').textContent = document.getElementById('description').value;
        
        // تحديث إجراءات التنفيذ (بدون ترقيم)
        const procedures = document.getElementById('procedures').value.split(',').map(p => p.trim()).filter(p => p);
        document.getElementById('proceduresPreview').textContent = procedures.join('، ');
        
        // تحديث النتائج (بدون ترقيم)
        const results = document.getElementById('results').value.split(',').map(r => r.trim()).filter(r => r);
        document.getElementById('resultsPreview').textContent = results.join('، ');
        
        // تحديث التوصيات
        document.getElementById('recommendationsPreview').textContent = document.getElementById('recommendations').value;
        
        // تحديث الصور
        const reportImagesContainer = document.getElementById('reportImagesPreview');
        reportImagesContainer.innerHTML = '';
        
        uploadedImages.forEach((imgData) => {
            const img = document.createElement('img');
            img.src = imgData.data;
            img.alt = 'صورة توثيقية';
            reportImagesContainer.appendChild(img);
        });
    }
    
    function showAlert() {
        successAlert.classList.add('show');
    }
    
    function hideAlert() {
        successAlert.classList.remove('show');
    }
    
    function showError(message) {
        alert(`❌ ${message}`);
    }
    
    function showSuccess(message) {
        alert(`✅ ${message}`);
    }
    
    // بدء التشغيل
    setupEventListeners();
    
    // تحميل المسودة المحفوظة
    loadDraft();
    
    // الحفظ التلقائي كل 30 ثانية
    setInterval(saveDraft, 30000);
    
    function saveDraft() {
        const reportData = {
            type: document.getElementById('reportType').value,
            school: document.getElementById('school').value,
            principal: document.getElementById('principal').value,
            reporter: document.getElementById('reporter').value,
            title: document.getElementById('reportTitle').value,
            curriculumRelated: document.getElementById('curriculumRelated').value,
            programDate: document.getElementById('programDate').value,
            location: document.getElementById('location').value,
            target: document.getElementById('target').value,
            beneficiaries: document.getElementById('beneficiaries').value,
            description: document.getElementById('description').value,
            procedures: document.getElementById('procedures').value,
            results: document.getElementById('results').value,
            recommendations: document.getElementById('recommendations').value,
            images: uploadedImages,
            savedAt: new Date().toLocaleTimeString('ar-SA')
        };
        
        localStorage.setItem('reportDraft', JSON.stringify(reportData));
    }
    
    function loadDraft() {
        const savedDraft = localStorage.getItem('reportDraft');
        if (savedDraft) {
            try {
                const draftData = JSON.parse(savedDraft);
                if (confirm('يوجد تقرير محفوظ كمسودة. هل تريد استكماله؟')) {
                    document.getElementById('reportType').value = draftData.type || 'strategy';
                    document.getElementById('school').value = draftData.school || 'سعيد بن العاص المتوسطة';
                    document.getElementById('principal').value = draftData.principal || 'نايف عوض اللحياني';
                    document.getElementById('reporter').value = draftData.reporter || 'فهد نغيمش الخالدي';
                    document.getElementById('reportTitle').value = draftData.title || 'تقرير تنفيذ استراتيجية تدريس';
                    document.getElementById('curriculumRelated').value = draftData.curriculumRelated || 'نعم';
                    document.getElementById('programDate').value = draftData.programDate || '1447-06-12';
                    document.getElementById('location').value = draftData.location || 'قاعة المصادر';
                    document.getElementById('target').value = draftData.target || 'طلاب الصف الثالث متوسط';
                    document.getElementById('beneficiaries').value = draftData.beneficiaries || '30';
                    document.getElementById('description').value = draftData.description || '';
                    document.getElementById('procedures').value = draftData.procedures || '';
                    document.getElementById('results').value = draftData.results || '';
                    document.getElementById('recommendations').value = draftData.recommendations || '';
                    
                    if (draftData.images && draftData.images.length > 0) {
                        uploadedImages = [...draftData.images];
                        updateImagePreview();
                    }
                    
                    showSuccess('تم تحميل بيانات المسودة بنجاح');
                }
            } catch (e) {
                console.error('Error loading draft:', e);
            }
        }
    }
    
    // دالة للطباعة
    window.printReport = function() {
        window.print();
    };
    
    // إضافة زر الطباعة إلى زر إنشاء التقرير
    createReportBtn.addEventListener('click', function() {
        setTimeout(() => {
            createReportBtn.innerHTML = '<i class="fas fa-print"></i> طباعة التقرير';
            createReportBtn.onclick = window.printReport;
        }, 100);
    });
});
</script>
</body>
</html>