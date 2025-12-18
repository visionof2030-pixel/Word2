<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أداة متقدمة لقراءة ملفات Word مع الجداول</title>
    
    <!-- المكتبات المطلوبة -->
    <script src="https://unpkg.com/mammoth@1.4.8/mammoth.browser.min.js"></script>
    <script src="https://unpkg.com/xlsx@0.18.5/dist/xlsx.full.min.js"></script>
    
    <style>
        :root {
            --primary: #4361ee;
            --secondary: #3a0ca3;
            --success: #4cc9f0;
            --warning: #f72585;
            --light: #f8f9fa;
            --dark: #212529;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Segoe UI', 'Cairo', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
            color: var(--dark);
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            overflow: hidden;
        }
        
        /* رأس التطبيق */
        .app-header {
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            color: white;
            padding: 30px;
            text-align: center;
        }
        
        .app-header h1 {
            font-size: 2.8rem;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
        }
        
        .app-header p {
            font-size: 1.2rem;
            opacity: 0.9;
            max-width: 800px;
            margin: 0 auto;
        }
        
        /* لوحة التحميل */
        .upload-panel {
            padding: 40px;
            background: var(--light);
            border-bottom: 1px solid #dee2e6;
        }
        
        .file-upload-area {
            border: 3px dashed var(--primary);
            border-radius: 15px;
            padding: 40px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            background: white;
        }
        
        .file-upload-area:hover {
            border-color: var(--warning);
            background: #f8f9ff;
            transform: translateY(-5px);
        }
        
        .upload-icon {
            font-size: 4rem;
            color: var(--primary);
            margin-bottom: 20px;
        }
        
        .upload-text h3 {
            color: var(--secondary);
            margin-bottom: 10px;
            font-size: 1.8rem;
        }
        
        .upload-text p {
            color: #6c757d;
            margin-bottom: 20px;
        }
        
        .file-input {
            display: none;
        }
        
        .btn {
            padding: 15px 30px;
            border: none;
            border-radius: 10px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            gap: 10px;
            margin: 5px;
        }
        
        .btn-primary {
            background: var(--primary);
            color: white;
        }
        
        .btn-primary:hover {
            background: var(--secondary);
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(67, 97, 238, 0.3);
        }
        
        .btn-success {
            background: var(--success);
            color: white;
        }
        
        /* معلومات الملف */
        .file-info {
            margin-top: 30px;
            padding: 25px;
            background: white;
            border-radius: 15px;
            border: 2px solid #e9ecef;
            display: none;
        }
        
        .file-info-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .info-card {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
            border-left: 5px solid var(--primary);
        }
        
        /* لوحة العرض */
        .content-panel {
            padding: 30px;
            display: none;
        }
        
        .content-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }
        
        .tab-btn {
            padding: 15px 30px;
            background: #e9ecef;
            border: none;
            border-radius: 10px 10px 0 0;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .tab-btn.active {
            background: var(--primary);
            color: white;
        }
        
        .tab-content {
            display: none;
            animation: fadeIn 0.5s;
        }
        
        .tab-content.active {
            display: block;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* الجداول */
        .table-container {
            overflow-x: auto;
            margin: 20px 0;
            border-radius: 10px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            border: 1px solid #dee2e6;
        }
        
        .data-table {
            width: 100%;
            border-collapse: collapse;
            min-width: 800px;
        }
        
        .data-table th {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            padding: 18px 15px;
            text-align: center;
            font-weight: bold;
            border: 1px solid #dee2e6;
            position: sticky;
            top: 0;
            font-size: 1.1rem;
        }
        
        .data-table td {
            padding: 15px;
            border: 1px solid #dee2e6;
            text-align: center;
            vertical-align: middle;
            background: white;
            transition: background 0.3s;
            font-size: 1rem;
        }
        
        .data-table tr:nth-child(even) td {
            background-color: #f8f9fa;
        }
        
        .data-table tr:hover td {
            background-color: #e3f2fd;
        }
        
        /* الفقرات */
        .paragraph-section {
            margin-bottom: 30px;
        }
        
        .paragraph-block {
            background: white;
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 20px;
            border: 2px solid #e9ecef;
            transition: all 0.3s;
            position: relative;
        }
        
        .paragraph-block:hover {
            border-color: var(--primary);
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            transform: translateY(-5px);
        }
        
        .paragraph-number {
            position: absolute;
            top: -15px;
            right: -15px;
            background: var(--warning);
            color: white;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 1.2rem;
            box-shadow: 0 5px 15px rgba(247, 37, 133, 0.4);
        }
        
        .paragraph-content {
            font-size: 1.1rem;
            line-height: 1.8;
            color: #333;
            margin-bottom: 20px;
            min-height: 60px;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 10px;
        }
        
        /* أزرار التعديل */
        .action-buttons {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }
        
        .btn-edit {
            background: var(--primary);
            color: white;
            padding: 12px 25px;
        }
        
        .btn-save {
            background: #28a745;
            color: white;
            padding: 12px 25px;
        }
        
        .btn-cancel {
            background: #dc3545;
            color: white;
            padding: 12px 25px;
        }
        
        .edit-textarea {
            width: 100%;
            min-height: 150px;
            padding: 20px;
            border: 3px solid var(--primary);
            border-radius: 10px;
            font-size: 1.1rem;
            font-family: inherit;
            margin-bottom: 15px;
            resize: vertical;
            background: #f8f9ff;
            line-height: 1.6;
        }
        
        /* الرسائل */
        .message {
            position: fixed;
            top: 30px;
            right: 30px;
            padding: 20px 30px;
            border-radius: 10px;
            color: white;
            font-weight: bold;
            z-index: 1000;
            animation: slideIn 0.5s, fadeOut 0.5s 4.5s;
            max-width: 400px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .message-success {
            background: linear-gradient(135deg, #28a745, #20c997);
        }
        
        .message-error {
            background: linear-gradient(135deg, #dc3545, #fd7e14);
        }
        
        .message-info {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
        }
        
        @keyframes slideIn {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }
        
        @keyframes fadeOut {
            to { opacity: 0; }
        }
        
        /* التحميل */
        .loading {
            text-align: center;
            padding: 50px;
            display: none;
        }
        
        .spinner {
            border: 5px solid #f3f3f3;
            border-top: 5px solid var(--primary);
            border-radius: 50%;
            width: 60px;
            height: 60px;
            animation: spin 1s linear infinite;
            margin: 0 auto 20px;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        /* التصدير */
        .export-panel {
            background: #f8f9fa;
            padding: 30px;
            border-radius: 15px;
            margin-top: 40px;
            text-align: center;
            border: 2px dashed #dee2e6;
        }
        
        /* تفاعلية للجوال */
        @media (max-width: 768px) {
            .container {
                border-radius: 10px;
            }
            
            .app-header h1 {
                font-size: 2rem;
                flex-direction: column;
            }
            
            .upload-panel {
                padding: 20px;
            }
            
            .file-upload-area {
                padding: 20px;
            }
            
            .content-tabs {
                flex-direction: column;
            }
            
            .tab-btn {
                width: 100%;
                justify-content: center;
            }
            
            .btn {
                width: 100%;
                justify-content: center;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- رأس التطبيق -->
        <header class="app-header">
            <h1>
                <span>📊</span>
                أداة قراءة ملفات Word المتقدمة
                <span>📄</span>
            </h1>
            <p>أداة متكاملة لقراءة وعرض وتعديل ملفات Word مع دعم كامل للجداول والفقرات</p>
        </header>
        
        <!-- لوحة التحميل -->
        <section class="upload-panel">
            <div class="file-upload-area" id="uploadArea">
                <div class="upload-icon">
                    📁
                </div>
                <div class="upload-text">
                    <h3>اسحب وأفلت ملف Word هنا</h3>
                    <p>أو انقر لاختيار ملف (يدعم DOCX, DOC, TXT)</p>
                    <p style="color: var(--warning); font-size: 0.9rem; margin-top: 10px;">
                        ⚡ يدعم الجداول المعقدة والنصوص والتنسيقات
                    </p>
                </div>
                <input type="file" id="fileInput" class="file-input" accept=".docx,.doc,.txt">
                <div style="margin-top: 30px;">
                    <button class="btn btn-primary" onclick="document.getElementById('fileInput').click()">
                        <span>📂</span>
                        اختيار ملف
                    </button>
                    <button class="btn btn-primary" id="processBtn" style="display: none;">
                        <span>⚡</span>
                        معالجة الملف
                    </button>
                </div>
            </div>
            
            <div class="file-info" id="fileInfo">
                <h3>📋 معلومات الملف</h3>
                <div class="file-info-grid" id="fileInfoGrid"></div>
            </div>
            
            <div class="loading" id="loading">
                <div class="spinner"></div>
                <h3>جاري معالجة الملف...</h3>
                <p>يرجى الانتظار، هذا قد يستغرق بضع ثوانٍ</p>
            </div>
        </section>
        
        <!-- لوحة العرض -->
        <section class="content-panel" id="contentPanel">
            <!-- علامات التبويب -->
            <div class="content-tabs">
                <button class="tab-btn active" data-tab="tables">
                    <span>📊</span>
                    الجداول
                    <span id="tablesCount" class="badge">0</span>
                </button>
                <button class="tab-btn" data-tab="paragraphs">
                    <span>📝</span>
                    الفقرات
                    <span id="paragraphsCount" class="badge">0</span>
                </button>
                <button class="tab-btn" data-tab="raw">
                    <span>🔍</span>
                    عرض كامل
                </button>
            </div>
            
            <!-- محتوى الجداول -->
            <div class="tab-content active" id="tablesContent">
                <div id="tablesContainer"></div>
            </div>
            
            <!-- محتوى الفقرات -->
            <div class="tab-content" id="paragraphsContent">
                <div id="paragraphsContainer"></div>
            </div>
            
            <!-- العرض الكامل -->
            <div class="tab-content" id="rawContent">
                <div id="rawContainer"></div>
            </div>
            
            <!-- لوحة التصدير -->
            <div class="export-panel">
                <h3>📤 تصدير المحتوى</h3>
                <p>يمكنك تصدير المحتوى المعدل بعدة صيغ</p>
                <div style="margin-top: 20px;">
                    <button class="btn btn-success" id="exportTxt">
                        <span>📄</span>
                        تصدير كملف نصي
                    </button>
                    <button class="btn btn-success" id="exportExcel">
                        <span>📊</span>
                        تصدير كـ Excel
                    </button>
                    <button class="btn btn-success" id="exportHtml">
                        <span>🌐</span>
                        تصدير كـ HTML
                    </button>
                </div>
            </div>
        </section>
    </div>
    
    <!-- منطقة الرسائل -->
    <div id="messageContainer"></div>

    <script>
        // متغيرات التطبيق
        const app = {
            file: null,
            content: {
                tables: [],
                paragraphs: [],
                rawText: '',
                metadata: {}
            },
            currentTab: 'tables'
        };

        // تهيئة التطبيق
        document.addEventListener('DOMContentLoaded', function() {
            initApp();
        });

        function initApp() {
            // أحداث سحب وإفلات الملف
            const uploadArea = document.getElementById('uploadArea');
            uploadArea.addEventListener('dragover', handleDragOver);
            uploadArea.addEventListener('drop', handleFileDrop);
            
            // أحداث اختيار الملف
            document.getElementById('fileInput').addEventListener('change', handleFileSelect);
            document.getElementById('processBtn').addEventListener('click', processFile);
            
            // أحداث علامات التبويب
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    switchTab(this.dataset.tab);
                });
            });
            
            // أحداث التصدير
            document.getElementById('exportTxt').addEventListener('click', exportAsTxt);
            document.getElementById('exportExcel').addEventListener('click', exportAsExcel);
            document.getElementById('exportHtml').addEventListener('click', exportAsHtml);
            
            showMessage('مرحباً! قم بتحميل ملف Word لبدء الاستخدام', 'info');
        }

        // معالجة سحب وإفلات الملف
        function handleDragOver(e) {
            e.preventDefault();
            e.stopPropagation();
            e.dataTransfer.dropEffect = 'copy';
            document.getElementById('uploadArea').style.borderColor = '#f72585';
            document.getElementById('uploadArea').style.backgroundColor = '#f8f9ff';
        }

        function handleFileDrop(e) {
            e.preventDefault();
            e.stopPropagation();
            
            const file = e.dataTransfer.files[0];
            if (file) {
                loadFile(file);
            }
            
            document.getElementById('uploadArea').style.borderColor = '#4361ee';
            document.getElementById('uploadArea').style.backgroundColor = 'white';
        }

        // معالجة اختيار الملف
        function handleFileSelect(e) {
            const file = e.target.files[0];
            if (file) {
                loadFile(file);
            }
        }

        function loadFile(file) {
            app.file = file;
            
            // عرض معلومات الملف
            document.getElementById('processBtn').style.display = 'inline-flex';
            document.getElementById('fileInfo').style.display = 'block';
            
            const infoGrid = document.getElementById('fileInfoGrid');
            infoGrid.innerHTML = `
                <div class="info-card">
                    <strong>📄 اسم الملف:</strong><br>
                    ${file.name}
                </div>
                <div class="info-card">
                    <strong>📊 حجم الملف:</strong><br>
                    ${(file.size / 1024).toFixed(2)} كيلوبايت
                </div>
                <div class="info-card">
                    <strong>📅 آخر تعديل:</strong><br>
                    ${new Date(file.lastModified).toLocaleDateString('ar-SA')}
                </div>
                <div class="info-card">
                    <strong>📝 نوع الملف:</strong><br>
                    ${file.type || 'غير معروف'}
                </div>
            `;
            
            showMessage(`تم تحميل الملف: ${file.name}`, 'success');
        }

        // معالجة الملف
        async function processFile() {
            if (!app.file) {
                showMessage('يرجى اختيار ملف أولاً', 'error');
                return;
            }
            
            showLoading(true);
            
            try {
                if (app.file.name.endsWith('.docx')) {
                    await processDocxFile();
                } else if (app.file.name.endsWith('.txt')) {
                    await processTextFile();
                } else if (app.file.name.endsWith('.doc')) {
                    // ملفات DOC القديمة
                    showMessage('ملفات DOC تحتاج معالجة خاصة. يفضل تحويلها إلى DOCX', 'error');
                    showLoading(false);
                    return;
                } else {
                    showMessage('نوع الملف غير مدعوم', 'error');
                    showLoading(false);
                    return;
                }
                
                // عرض المحتوى
                displayContent();
                showLoading(false);
                document.getElementById('contentPanel').style.display = 'block';
                showMessage('تم معالجة الملف بنجاح!', 'success');
                
            } catch (error) {
                console.error('Error processing file:', error);
                showMessage('حدث خطأ أثناء معالجة الملف', 'error');
                showLoading(false);
            }
        }

        // معالجة ملفات DOCX
        async function processDocxFile() {
            return new Promise((resolve, reject) => {
                const reader = new FileReader();
                
                reader.onload = async function(e) {
                    try {
                        const arrayBuffer = e.target.result;
                        
                        // استخدام Mammoth.js لاستخراج النص
                        const result = await mammoth.convertToHtml({arrayBuffer: arrayBuffer});
                        
                        // استخراج الجداول من HTML
                        const tempDiv = document.createElement('div');
                        tempDiv.innerHTML = result.value;
                        
                        // استخراج الجداول
                        const tables = tempDiv.querySelectorAll('table');
                        app.content.tables = [];
                        
                        tables.forEach((table, index) => {
                            const tableData = extractTableData(table);
                            app.content.tables.push({
                                id: index + 1,
                                data: tableData,
                                html: table.outerHTML
                            });
                        });
                        
                        // استخراج الفقرات
                        const paragraphs = [];
                        tempDiv.querySelectorAll('p, h1, h2, h3, h4, h5, h6, div, li').forEach(el => {
                            const text = el.textContent.trim();
                            if (text && !el.closest('table')) {
                                paragraphs.push({
                                    text: text,
                                    type: el.tagName.toLowerCase(),
                                    html: el.outerHTML
                                });
                            }
                        });
                        
                        app.content.paragraphs = paragraphs;
                        app.content.rawText = tempDiv.textContent;
                        
                        resolve();
                    } catch (error) {
                        reject(error);
                    }
                };
                
                reader.onerror = reject;
                reader.readAsArrayBuffer(app.file);
            });
        }

        // استخراج بيانات الجدول
        function extractTableData(tableElement) {
            const data = [];
            const rows = tableElement.querySelectorAll('tr');
            
            rows.forEach(row => {
                const rowData = [];
                const cells = row.querySelectorAll('th, td');
                
                cells.forEach(cell => {
                    rowData.push({
                        text: cell.textContent.trim(),
                        colspan: cell.colSpan || 1,
                        rowspan: cell.rowSpan || 1,
                        isHeader: cell.tagName === 'TH'
                    });
                });
                
                if (rowData.length > 0) {
                    data.push(rowData);
                }
            });
            
            return data;
        }

        // معالجة الملفات النصية
        async function processTextFile() {
            return new Promise((resolve, reject) => {
                const reader = new FileReader();
                
                reader.onload = function(e) {
                    const text = e.target.result;
                    
                    // تقسيم النص إلى فقرات
                    const paragraphs = text.split(/\n\s*\n/).filter(p => p.trim());
                    
                    app.content.paragraphs = paragraphs.map((text, index) => ({
                        id: index + 1,
                        text: text,
                        type: 'p'
                    }));
                    
                    app.content.tables = [];
                    app.content.rawText = text;
                    
                    resolve();
                };
                
                reader.onerror = reject;
                reader.readAsText(app.file, 'UTF-8');
            });
        }

        // عرض المحتوى
        function displayContent() {
            // تحديث العداد
            document.getElementById('tablesCount').textContent = app.content.tables.length;
            document.getElementById('paragraphsCount').textContent = app.content.paragraphs.length;
            
            // عرض الجداول
            displayTables();
            
            // عرض الفقرات
            displayParagraphs();
            
            // العرض الكامل
            displayRawContent();
        }

        // عرض الجداول
        function displayTables() {
            const container = document.getElementById('tablesContainer');
            container.innerHTML = '';
            
            if (app.content.tables.length === 0) {
                container.innerHTML = `
                    <div style="text-align: center; padding: 50px; color: #6c757d;">
                        <div style="font-size: 4rem; margin-bottom: 20px;">📊</div>
                        <h3>لا توجد جداول في الملف</h3>
                        <p>الملف لا يحتوي على جداول لعرضها</p>
                    </div>
                `;
                return;
            }
            
            app.content.tables.forEach((table, tableIndex) => {
                const tableSection = document.createElement('div');
                tableSection.className = 'table-section';
                tableSection.innerHTML = `
                    <div style="margin: 30px 0 20px 0; display: flex; justify-content: space-between; align-items: center;">
                        <h3 style="color: var(--secondary);">
                            <span>📋</span>
                            الجدول ${tableIndex + 1}
                        </h3>
                        <button class="btn btn-edit" onclick="editTable(${tableIndex})">
                            <span>✏️</span>
                            تعديل الجدول
                        </button>
                    </div>
                    <div class="table-container">
                        <table class="data-table" id="table-${tableIndex}">
                            ${generateTableHTML(table.data)}
                        </table>
                    </div>
                    <div id="tableEditor-${tableIndex}" style="display: none; margin-top: 20px;">
                        <textarea class="edit-textarea" id="tableText-${tableIndex}">${JSON.stringify(table.data, null, 2)}</textarea>
                        <div class="action-buttons">
                            <button class="btn btn-save" onclick="saveTable(${tableIndex})">💾 حفظ</button>
                            <button class="btn btn-cancel" onclick="cancelTableEdit(${tableIndex})">❌ إلغاء</button>
                        </div>
                    </div>
                `;
                container.appendChild(tableSection);
            });
        }

        // توليد HTML للجدول
        function generateTableHTML(tableData) {
            let html = '<tbody>';
            
            tableData.forEach((row, rowIndex) => {
                html += '<tr>';
                row.forEach((cell, cellIndex) => {
                    const tag = cell.isHeader ? 'th' : 'td';
                    const attrs = [];
                    
                    if (cell.colspan > 1) attrs.push(`colspan="${cell.colspan}"`);
                    if (cell.rowspan > 1) attrs.push(`rowspan="${cell.rowspan}"`);
                    
                    html += `<${tag} ${attrs.join(' ')} data-row="${rowIndex}" data-col="${cellIndex}">
                        ${cell.text}
                    </${tag}>`;
                });
                html += '</tr>';
            });
            
            html += '</tbody>';
            return html;
        }

        // عرض الفقرات
        function displayParagraphs() {
            const container = document.getElementById('paragraphsContainer');
            container.innerHTML = '';
            
            if (app.content.paragraphs.length === 0) {
                container.innerHTML = `
                    <div style="text-align: center; padding: 50px; color: #6c757d;">
                        <div style="font-size: 4rem; margin-bottom: 20px;">📝</div>
                        <h3>لا توجد فقرات في الملف</h3>
                        <p>الملف لا يحتوي على نصوص لعرضها</p>
                    </div>
                `;
                return;
            }
            
            app.content.paragraphs.forEach((para, index) => {
                const paraBlock = document.createElement('div');
                paraBlock.className = 'paragraph-block';
                paraBlock.innerHTML = `
                    <div class="paragraph-number">${index + 1}</div>
                    <div class="paragraph-content" id="paraContent-${index}">
                        ${para.text}
                    </div>
                    <div class="action-buttons">
                        <button class="btn btn-edit" onclick="editParagraph(${index})">
                            <span>✏️</span>
                            تعديل
                        </button>
                    </div>
                    <div id="paraEditor-${index}" style="display: none;">
                        <textarea class="edit-textarea" id="paraText-${index}">${para.text}</textarea>
                        <div class="action-buttons">
                            <button class="btn btn-save" onclick="saveParagraph(${index})">💾 حفظ</button>
                            <button class="btn btn-cancel" onclick="cancelParagraphEdit(${index})">❌ إلغاء</button>
                        </div>
                    </div>
                `;
                container.appendChild(paraBlock);
            });
        }

        // عرض المحتوى الكامل
        function displayRawContent() {
            const container = document.getElementById('rawContainer');
            container.innerHTML = `
                <div style="background: #f8f9fa; padding: 25px; border-radius: 15px; margin: 20px 0;">
                    <h3 style="color: var(--secondary); margin-bottom: 20px;">
                        <span>📊</span>
                        ملخص المحتوى
                    </h3>
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px;">
                        <div style="background: white; padding: 20px; border-radius: 10px; text-align: center;">
                            <div style="font-size: 2.5rem; color: var(--primary);">${app.content.tables.length}</div>
                            <div style="color: #6c757d;">عدد الجداول</div>
                        </div>
                        <div style="background: white; padding: 20px; border-radius: 10px; text-align: center;">
                            <div style="font-size: 2.5rem; color: var(--success);">${app.content.paragraphs.length}</div>
                            <div style="color: #6c757d;">عدد الفقرات</div>
                        </div>
                        <div style="background: white; padding: 20px; border-radius: 10px; text-align: center;">
                            <div style="font-size: 2.5rem; color: var(--warning);">${app.content.rawText.length}</div>
                            <div style="color: #6c757d;">عدد الأحرف</div>
                        </div>
                        <div style="background: white; padding: 20px; border-radius: 10px; text-align: center;">
                            <div style="font-size: 2.5rem; color: #9b59b6;">${app.content.rawText.split(/\s+/).length}</div>
                            <div style="color: #6c757d;">عدد الكلمات</div>
                        </div>
                    </div>
                </div>
                
                <div style="background: white; padding: 30px; border-radius: 15px; margin: 20px 0; border: 2px solid #e9ecef;">
                    <h3 style="color: var(--secondary); margin-bottom: 20px;">
                        <span>📝</span>
                        النص الكامل
                    </h3>
                    <div style="background: #f8f9fa; padding: 20px; border-radius: 10px; max-height: 500px; overflow-y: auto;">
                        <pre style="white-space: pre-wrap; font-family: inherit; line-height: 1.6;">${app.content.rawText}</pre>
                    </div>
                </div>
            `;
        }

        // تبديل علامات التبويب
        function switchTab(tabName) {
            // تحديث الأزرار النشطة
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.toggle('active', btn.dataset.tab === tabName);
            });
            
            // تحديث المحتوى النشط
            document.querySelectorAll('.tab-content').forEach(content => {
                content.classList.toggle('active', content.id === `${tabName}Content`);
            });
            
            app.currentTab = tabName;
        }

        // وظائف التعديل
        function editTable(index) {
            document.getElementById(`table-${index}`).style.display = 'none';
            document.getElementById(`tableEditor-${index}`).style.display = 'block';
        }

        function saveTable(index) {
            try {
                const newData = JSON.parse(document.getElementById(`tableText-${index}`).value);
                app.content.tables[index].data = newData;
                
                // إعادة توليد الجدول
                const tableElement = document.getElementById(`table-${index}`);
                tableElement.innerHTML = generateTableHTML(newData);
                
                document.getElementById(`table-${index}`).style.display = 'table';
                document.getElementById(`tableEditor-${index}`).style.display = 'none';
                
                showMessage('تم حفظ الجدول بنجاح', 'success');
            } catch (error) {
                showMessage('خطأ في تنسيق JSON', 'error');
            }
        }

        function cancelTableEdit(index) {
            document.getElementById(`table-${index}`).style.display = 'table';
            document.getElementById(`tableEditor-${index}`).style.display = 'none';
        }

        function editParagraph(index) {
            document.getElementById(`paraContent-${index}`).style.display = 'none';
            document.getElementById(`paraEditor-${index}`).style.display = 'block';
        }

        function saveParagraph(index) {
            const newText = document.getElementById(`paraText-${index}`).value;
            app.content.paragraphs[index].text = newText;
            
            document.getElementById(`paraContent-${index}`).textContent = newText;
            document.getElementById(`paraContent-${index}`).style.display = 'block';
            document.getElementById(`paraEditor-${index}`).style.display = 'none';
            
            showMessage('تم حفظ الفقرة بنجاح', 'success');
        }

        function cancelParagraphEdit(index) {
            document.getElementById(`paraContent-${index}`).style.display = 'block';
            document.getElementById(`paraEditor-${index}`).style.display = 'none';
        }

        // وظائف التصدير
        function exportAsTxt() {
            let content = '';
            
            content += '=== الجداول ===\n\n';
            app.content.tables.forEach((table, index) => {
                content += `الجدول ${index + 1}:\n\n`;
                table.data.forEach(row => {
                    const rowText = row.map(cell => cell.text).join('\t');
                    content += rowText + '\n';
                });
                content += '\n'.repeat(2);
            });
            
            content += '=== الفقرات ===\n\n';
            app.content.paragraphs.forEach((para, index) => {
                content += `الفقرة ${index + 1}:\n${para.text}\n\n`;
            });
            
            const blob = new Blob([content], { type: 'text/plain;charset=utf-8' });
            const url = URL.createObjectURL(blob);
            
            const a = document.createElement('a');
            a.href = url;
            a.download = `ملف_مستخرج_${new Date().toISOString().slice(0,10)}.txt`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            
            showMessage('تم التصدير كملف نصي بنجاح!', 'success');
        }

        function exportAsExcel() {
            try {
                // إنشاء مصنف Excel جديد
                const wb = XLSX.utils.book_new();
                
                // ورقة للجداول
                if (app.content.tables.length > 0) {
                    app.content.tables.forEach((table, tableIndex) => {
                        // تحويل بيانات الجدول إلى صيغة Excel
                        const excelData = [];
                        table.data.forEach(row => {
                            const excelRow = row.map(cell => cell.text);
                            excelData.push(excelRow);
                        });
                        
                        const ws = XLSX.utils.aoa_to_sheet(excelData);
                        XLSX.utils.book_append_sheet(wb, ws, `جدول_${tableIndex + 1}`);
                    });
                }
                
                // ورقة للفقرات
                if (app.content.paragraphs.length > 0) {
                    const paragraphsData = [
                        ['رقم الفقرة', 'النص'],
                        ...app.content.paragraphs.map((para, index) => [index + 1, para.text])
                    ];
                    
                    const ws = XLSX.utils.aoa_to_sheet(paragraphsData);
                    XLSX.utils.book_append_sheet(wb, ws, 'الفقرات');
                }
                
                // تصدير الملف
                XLSX.writeFile(wb, `ملف_مستخرج_${new Date().toISOString().slice(0,10)}.xlsx`);
                
                showMessage('تم التصدير كملف Excel بنجاح!', 'success');
            } catch (error) {
                console.error('Export error:', error);
                showMessage('حدث خطأ أثناء التصدير إلى Excel', 'error');
            }
        }

        function exportAsHtml() {
            let html = `
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ملف مستخرج - ${app.file.name}</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Segoe UI', 'Cairo', sans-serif;
            line-height: 1.6;
            color: #333;
            background: #f5f5f5;
            padding: 20px;
            max-width: 1200px;
            margin: 0 auto;
        }
        
        .header {
            text-align: center;
            margin-bottom: 40px;
            padding: 30px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border-radius: 15px;
        }
        
        .header h1 {
            margin-bottom: 10px;
            font-size: 2.5em;
        }
        
        .file-info {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
            margin-top: 20px;
        }
        
        .info-item {
            background: rgba(255,255,255,0.2);
            padding: 10px 20px;
            border-radius: 10px;
        }
        
        .section {
            background: white;
            margin-bottom: 30px;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .section-title {
            color: #4361ee;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 3px solid #4361ee;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        
        table th {
            background: #4361ee;
            color: white;
            padding: 15px;
            text-align: center;
            border: 1px solid #ddd;
        }
        
        table td {
            padding: 12px 15px;
            border: 1px solid #ddd;
            text-align: center;
        }
        
        table tr:nth-child(even) {
            background-color: #f9f9f9;
        }
        
        .paragraph-block {
            background: #f8f9fa;
            padding: 20px;
            margin-bottom: 20px;
            border-radius: 10px;
            border-right: 5px solid #4361ee;
        }
        
        .paragraph-number {
            display: inline-block;
            background: #f72585;
            color: white;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            text-align: center;
            line-height: 30px;
            margin-left: 10px;
            font-weight: bold;
        }
        
        @media print {
            body {
                background: white;
                padding: 0;
            }
            
            .header {
                background: #4361ee !important;
                -webkit-print-color-adjust: exact;
            }
            
            .section {
                box-shadow: none;
                border: 1px solid #ddd;
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>📄 ملف مستخرج</h1>
        <p>${app.file.name}</p>
        <div class="file-info">
            <div class="info-item">📅 ${new Date().toLocaleDateString('ar-SA')}</div>
            <div class="info-item">📊 ${app.content.tables.length} جدول</div>
            <div class="info-item">📝 ${app.content.paragraphs.length} فقرة</div>
        </div>
    </div>
`;
            
            // إضافة الجداول
            if (app.content.tables.length > 0) {
                html += `
    <div class="section">
        <h2 class="section-title">
            <span>📊</span>
            الجداول
        </h2>`;
                
                app.content.tables.forEach((table, tableIndex) => {
                    html += `
        <h3 style="margin: 25px 0 15px 0; color: #3a0ca3;">الجدول ${tableIndex + 1}</h3>
        <table>
            <thead>
                <tr>`;
                    
                    // العناوين
                    if (table.data[0]) {
                        table.data[0].forEach(cell => {
                            html += `<th>${cell.text}</th>`;
                        });
                    }
                    
                    html += `
                </tr>
            </thead>
            <tbody>`;
                    
                    // الصفوف
                    table.data.slice(1).forEach((row, rowIndex) => {
                        html += '<tr>';
                        row.forEach(cell => {
                            html += `<td>${cell.text}</td>`;
                        });
                        html += '</tr>';
                    });
                    
                    html += `
            </tbody>
        </table>`;
                });
                
                html += `</div>`;
            }
            
            // إضافة الفقرات
            if (app.content.paragraphs.length > 0) {
                html += `
    <div class="section">
        <h2 class="section-title">
            <span>📝</span>
            الفقرات
        </h2>`;
                
                app.content.paragraphs.forEach((para, index) => {
                    html += `
        <div class="paragraph-block">
            <span class="paragraph-number">${index + 1}</span>
            <div style="margin-top: 10px;">${para.text}</div>
        </div>`;
                });
                
                html += `</div>`;
            }
            
            html += `
</body>
</html>`;
            
            const blob = new Blob([html], { type: 'text/html;charset=utf-8' });
            const url = URL.createObjectURL(blob);
            
            const a = document.createElement('a');
            a.href = url;
            a.download = `ملف_مستخرج_${new Date().toISOString().slice(0,10)}.html`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            
            showMessage('تم التصدير كملف HTML بنجاح!', 'success');
        }

        // وظائف المساعدة
        function showLoading(show) {
            document.getElementById('loading').style.display = show ? 'block' : 'none';
            document.getElementById('processBtn').style.display = show ? 'none' : 'inline-flex';
        }

        function showMessage(text, type) {
            const messageContainer = document.getElementById('messageContainer');
            
            const messageDiv = document.createElement('div');
            messageDiv.className = `message message-${type}`;
            messageDiv.innerHTML = `
                <span>${type === 'success' ? '✅' : type === 'error' ? '❌' : 'ℹ️'}</span>
                <span>${text}</span>
            `;
            
            messageContainer.appendChild(messageDiv);
            
            // إزالة الرسالة بعد 5 ثوان
            setTimeout(() => {
                if (messageDiv.parentNode) {
                    messageDiv.style.animation = 'fadeOut 0.5s';
                    setTimeout(() => {
                        if (messageDiv.parentNode) {
                            messageDiv.parentNode.removeChild(messageDiv);
                        }
                    }, 500);
                }
            }, 5000);
        }

        // إضافة إمكانية تحرير الخلايا مباشرة
        function makeCellsEditable() {
            document.querySelectorAll('.data-table td').forEach(cell => {
                cell.addEventListener('dblclick', function() {
                    const originalText = this.textContent;
                    const row = this.getAttribute('data-row');
                    const col = this.getAttribute('data-col');
                    const tableIndex = this.closest('[id^="table-"]').id.split('-')[1];
                    
                    this.innerHTML = `<input type="text" value="${originalText}" 
                        style="width: 100%; border: none; padding: 5px;"
                        onblur="updateCell(${tableIndex}, ${row}, ${col}, this.value)"
                        onkeypress="if(event.key === 'Enter') this.blur()">`;
                    
                    this.querySelector('input').focus();
                });
            });
        }

        function updateCell(tableIndex, row, col, newValue) {
            // تحديث البيانات في الذاكرة
            if (app.content.tables[tableIndex] && 
                app.content.tables[tableIndex].data[row] && 
                app.content.tables[tableIndex].data[row][col]) {
                app.content.tables[tableIndex].data[row][col].text = newValue;
            }
            
            // تحديث العرض
            const cell = document.querySelector(`#table-${tableIndex} td[data-row="${row}"][data-col="${col}"]`);
            if (cell) {
                cell.textContent = newValue;
            }
            
            showMessage('تم تحديث الخلية', 'success');
        }

        // إضافة زر لتنزيل جميع الصور (إذا كانت موجودة)
        function extractImagesFromDocx() {
            // هذه الوظيفة يمكن توسيعها لاستخراج الصور من DOCX
            console.log('وظيفة استخراج الصور تحت التطوير...');
        }

        // وظائف إضافية للتحسين
        function addTableRow(tableIndex) {
            const table = app.content.tables[tableIndex];
            if (table && table.data.length > 0) {
                const cols = table.data[0].length;
                const newRow = Array(cols).fill().map(() => ({ text: '', colspan: 1, rowspan: 1, isHeader: false }));
                table.data.push(newRow);
                displayTables();
                showMessage('تم إضافة صف جديد', 'success');
            }
        }

        function removeTableRow(tableIndex, rowIndex) {
            const table = app.content.tables[tableIndex];
            if (table && table.data[rowIndex]) {
                table.data.splice(rowIndex, 1);
                displayTables();
                showMessage('تم حذف الصف', 'success');
            }
        }

        // تهيئة الخلايا القابلة للتحرير عند تحميل الجداول
        document.addEventListener('click', function() {
            setTimeout(() => {
                makeCellsEditable();
            }, 1000);
        });
    </script>
</body>
</html>
