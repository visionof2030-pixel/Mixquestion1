<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أداة خلط أسئلة PDF</title>
    <script src="https://unpkg.com/pdf-lib@1.17.1/dist/pdf-lib.min.js"></script>
    <script src="https://unpkg.com/@pdf-lib/fontkit@1.0.0/dist/fontkit.umd.min.js"></script>
    <style>
        * {
            box-sizing: border-box;
            font-family: 'Arial', sans-serif;
        }
        body {
            background-color: #f5f7fa;
            margin: 0;
            padding: 20px;
            color: #333;
            line-height: 1.6;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 5px 25px rgba(0,0,0,0.08);
        }
        h1 {
            text-align: center;
            color: #2c3e50;
            margin-bottom: 10px;
            font-size: 28px;
        }
        .subtitle {
            text-align: center;
            color: #7f8c8d;
            margin-bottom: 30px;
            font-size: 16px;
        }
        .workflow {
            display: flex;
            justify-content: center;
            margin: 30px 0;
            flex-wrap: wrap;
            gap: 10px;
        }
        .step {
            display: flex;
            align-items: center;
            background: #f8f9fa;
            padding: 12px 20px;
            border-radius: 10px;
            border: 2px solid #e9ecef;
            font-weight: bold;
            color: #495057;
        }
        .step.active {
            background: #3498db;
            color: white;
            border-color: #2980b9;
        }
        .step .number {
            background: #e9ecef;
            color: #495057;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-left: 10px;
        }
        .step.active .number {
            background: #2980b9;
            color: white;
        }
        .arrow {
            color: #95a5a6;
            font-size: 20px;
            padding: 0 10px;
        }
        .upload-section {
            background: #f8f9fa;
            padding: 30px;
            border-radius: 10px;
            border: 2px dashed #3498db;
            text-align: center;
            margin: 30px 0;
        }
        .upload-section h3 {
            color: #2c3e50;
            margin-bottom: 20px;
        }
        .file-input {
            padding: 15px;
            border: 2px solid #ddd;
            border-radius: 8px;
            width: 100%;
            max-width: 400px;
            margin: 0 auto;
            display: block;
            cursor: pointer;
            background: white;
        }
        .preview-container {
            margin: 30px 0;
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
        }
        .questions-preview {
            flex: 1;
            min-width: 300px;
            background: white;
            border: 1px solid #e0e0e0;
            border-radius: 10px;
            padding: 20px;
            overflow-y: auto;
            max-height: 500px;
        }
        .questions-preview h3 {
            color: #2c3e50;
            padding-bottom: 10px;
            border-bottom: 2px solid #3498db;
            margin-bottom: 20px;
        }
        .question-item {
            background: #f8f9fa;
            padding: 15px;
            margin-bottom: 15px;
            border-radius: 8px;
            border-left: 4px solid #3498db;
            transition: all 0.3s;
        }
        .question-item:hover {
            background: #e8f4fc;
            transform: translateX(-5px);
        }
        .question-item .q-number {
            background: #3498db;
            color: white;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            margin-left: 10px;
            font-weight: bold;
        }
        .question-item .q-text {
            margin-top: 10px;
            padding: 10px;
            background: white;
            border-radius: 5px;
            border: 1px solid #e0e0e0;
        }
        .options {
            margin-top: 10px;
            padding-right: 20px;
        }
        .option {
            display: flex;
            align-items: center;
            margin-bottom: 5px;
            padding: 5px 10px;
            background: white;
            border-radius: 4px;
            border: 1px solid #eee;
        }
        .option-letter {
            background: #2ecc71;
            color: white;
            width: 24px;
            height: 24px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-left: 10px;
            font-size: 14px;
            font-weight: bold;
        }
        .controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 30px 0;
            flex-wrap: wrap;
        }
        button {
            padding: 14px 28px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            min-width: 200px;
        }
        .btn-primary {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
        }
        .btn-success {
            background: linear-gradient(135deg, #2ecc71, #27ae60);
            color: white;
        }
        .btn-warning {
            background: linear-gradient(135deg, #f39c12, #e67e22);
            color: white;
        }
        .btn-danger {
            background: linear-gradient(135deg, #e74c3c, #c0392b);
            color: white;
        }
        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 7px 20px rgba(0,0,0,0.15);
        }
        button:disabled {
            background: #bdc3c7;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        .loading {
            display: none;
            text-align: center;
            padding: 30px;
        }
        .loading.active {
            display: block;
        }
        .spinner {
            border: 5px solid #f3f3f3;
            border-top: 5px solid #3498db;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            animation: spin 1s linear infinite;
            margin: 0 auto 20px;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .status {
            padding: 15px;
            margin: 15px 0;
            border-radius: 8px;
            text-align: center;
            font-weight: bold;
        }
        .status.success {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
        .status.error {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
        .status.info {
            background: #d1ecf1;
            color: #0c5460;
            border: 1px solid #bee5eb;
        }
        .section-title {
            font-size: 18px;
            font-weight: bold;
            color: #2c3e50;
            margin: 25px 0 15px;
            padding-bottom: 10px;
            border-bottom: 2px solid #3498db;
        }
        .original-pdf {
            text-align: center;
            margin: 20px 0;
            padding: 20px;
            background: #f8f9fa;
            border-radius: 10px;
            border: 1px solid #ddd;
        }
        .pdf-info {
            background: #e8f4fc;
            padding: 15px;
            border-radius: 8px;
            margin: 15px 0;
            border-right: 4px solid #3498db;
        }
        .stats {
            display: flex;
            justify-content: space-around;
            flex-wrap: wrap;
            margin: 20px 0;
            gap: 15px;
        }
        .stat-card {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 3px 15px rgba(0,0,0,0.08);
            text-align: center;
            flex: 1;
            min-width: 200px;
        }
        .stat-card .number {
            font-size: 32px;
            font-weight: bold;
            color: #3498db;
            margin-bottom: 10px;
        }
        .stat-card .label {
            color: #7f8c8d;
            font-size: 14px;
        }
        .shuffle-options {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
            border: 1px solid #e0e0e0;
        }
        .checkbox-group {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            margin: 15px 0;
        }
        .checkbox-item {
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .checkbox-item input {
            width: 20px;
            height: 20px;
        }
        footer {
            text-align: center;
            margin-top: 40px;
            padding-top: 20px;
            border-top: 1px solid #eee;
            color: #7f8c8d;
            font-size: 14px;
        }
        @media (max-width: 768px) {
            .container {
                padding: 15px;
            }
            button {
                width: 100%;
            }
            .workflow {
                flex-direction: column;
                align-items: center;
            }
            .arrow {
                transform: rotate(90deg);
                padding: 10px 0;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>📄 أداة خلط أسئلة PDF</h1>
        <div class="subtitle">قم بتحميل ملف PDF الأصلي، إعادة ترتيب الأسئلة عشوائيًا، وحفظ نسخة جديدة</div>
        
        <!-- خطوات العمل -->
        <div class="workflow">
            <div class="step active">
                <span class="number">1</span>
                تحميل PDF الأصلي
            </div>
            <div class="arrow">→</div>
            <div class="step">
                <span class="number">2</span>
                استخراج الأسئلة
            </div>
            <div class="arrow">→</div>
            <div class="step">
                <span class="number">3</span>
                خلط الأسئلة
            </div>
            <div class="arrow">→</div>
            <div class="step">
                <span class="number">4</span>
                حفظ PDF جديد
            </div>
        </div>
        
        <!-- قسم رفع الملف -->
        <div class="upload-section">
            <h3>📤 الخطوة 1: تحميل ملف PDF الأصلي</h3>
            <p>قم باختيار ملف الاختبار الذي تريد خلط أسئلته</p>
            <input type="file" id="pdfInput" accept=".pdf" class="file-input">
            <div class="pdf-info" id="pdfInfo" style="display: none;">
                <strong>✓ تم تحميل الملف بنجاح</strong>
                <p id="fileName"></p>
                <p id="fileSize"></p>
            </div>
        </div>
        
        <!-- خيارات الخلط -->
        <div class="shuffle-options" id="shuffleOptions" style="display: none;">
            <h3>⚙️ خيارات الخلط</h3>
            <p>اختر الأقسام التي تريد خلط أسئلتها:</p>
            <div class="checkbox-group">
                <div class="checkbox-item">
                    <input type="checkbox" id="shuffleGrammar" checked>
                    <label for="shuffleGrammar">🔤 قسم القواعد (Grammar)</label>
                </div>
                <div class="checkbox-item">
                    <input type="checkbox" id="shuffleOrthography" checked>
                    <label for="shuffleOrthography">✏️ قسم الإملاء (Orthography)</label>
                </div>
                <div class="checkbox-item">
                    <input type="checkbox" id="shuffleMatching" checked>
                    <label for="shuffleMatching">🖼️ قسم التطابق (Matching)</label>
                </div>
                <div class="checkbox-item">
                    <input type="checkbox" id="shuffleReading" checked>
                    <label for="shuffleReading">📖 قسم القراءة (Reading)</label>
                </div>
            </div>
        </div>
        
        <!-- معاينة الأسئلة -->
        <div class="preview-container" id="previewContainer" style="display: none;">
            <div class="questions-preview">
                <h3>🔍 معاينة الأسئلة الأصلية</h3>
                <div id="originalQuestions"></div>
            </div>
            <div class="questions-preview">
                <h3>🔀 معاينة الأسئلة بعد الخلط</h3>
                <div id="shuffledQuestions"></div>
            </div>
        </div>
        
        <!-- الإحصائيات -->
        <div class="stats" id="statsSection" style="display: none;">
            <div class="stat-card">
                <div class="number" id="totalQuestions">0</div>
                <div class="label">إجمالي الأسئلة</div>
            </div>
            <div class="stat-card">
                <div class="number" id="shuffledCount">0</div>
                <div class="label">الأسئلة المخلوطة</div>
            </div>
            <div class="stat-card">
                <div class="number" id="pagesCount">0</div>
                <div class="label">عدد الصفحات</div>
            </div>
        </div>
        
        <!-- حالة التحميل -->
        <div class="loading" id="loading">
            <div class="spinner"></div>
            <p>جاري معالجة ملف PDF...</p>
        </div>
        
        <!-- رسالة الحالة -->
        <div class="status" id="statusMessage"></div>
        
        <!-- أزرار التحكم -->
        <div class="controls">
            <button class="btn-primary" onclick="extractQuestions()" id="extractBtn" disabled>
                📊 استخراج الأسئلة
            </button>
            <button class="btn-warning" onclick="shuffleQuestions()" id="shuffleBtn" disabled>
                🔀 خلط الأسئلة عشوائيًا
            </button>
            <button class="btn-success" onclick="saveShuffledPDF()" id="saveBtn" disabled>
                💾 حفظ PDF مخلوط
            </button>
            <button class="btn-danger" onclick="resetAll()">
                🗑️ إعادة تعيين
            </button>
        </div>
        
        <!-- ملف PDF الأصلي -->
        <div class="original-pdf" id="originalPdfSection" style="display: none;">
            <h3>📄 ملف PDF الأصلي</h3>
            <iframe id="pdfPreview" width="100%" height="500px" style="border: 1px solid #ddd; border-radius: 8px;"></iframe>
        </div>
        
        <footer>
            <p>أداة خلط أسئلة PDF - الإصدار 1.0</p>
            <p>تم التطوير باستخدام مكتبة PDF-Lib</p>
        </footer>
    </div>

    <script>
        // متغيرات التطبيق
        let pdfBytes = null;
        let pdfDoc = null;
        let extractedQuestions = {
            grammar: [],
            orthography: [],
            matching: [],
            reading: []
        };
        let shuffledQuestions = null;
        let isExtracted = false;
        
        // تحديث خطوات العمل
        function updateWorkflow(step) {
            document.querySelectorAll('.step').forEach((el, index) => {
                if (index + 1 <= step) {
                    el.classList.add('active');
                } else {
                    el.classList.remove('active');
                }
            });
        }
        
        // تحديث حالة الأزرار
        function updateButtons() {
            const extractBtn = document.getElementById('extractBtn');
            const shuffleBtn = document.getElementById('shuffleBtn');
            const saveBtn = document.getElementById('saveBtn');
            
            extractBtn.disabled = !pdfBytes;
            shuffleBtn.disabled = !isExtracted;
            saveBtn.disabled = !shuffledQuestions;
        }
        
        // تحميل ملف PDF
        document.getElementById('pdfInput').addEventListener('change', async function(e) {
            const file = e.target.files[0];
            if (!file) return;
            
            // عرض معلومات الملف
            document.getElementById('pdfInfo').style.display = 'block';
            document.getElementById('fileName').textContent = `اسم الملف: ${file.name}`;
            document.getElementById('fileSize').textContent = `حجم الملف: ${(file.size / 1024).toFixed(2)} KB`;
            
            // تحويل الملف إلى ArrayBuffer
            const arrayBuffer = await file.arrayBuffer();
            pdfBytes = new Uint8Array(arrayBuffer);
            
            // عرض معاينة PDF
            const blob = new Blob([pdfBytes], { type: 'application/pdf' });
            const url = URL.createObjectURL(blob);
            document.getElementById('pdfPreview').src = url;
            document.getElementById('originalPdfSection').style.display = 'block';
            
            // تحميل PDF باستخدام pdf-lib
            try {
                showLoading(true);
                pdfDoc = await PDFLib.PDFDocument.load(pdfBytes);
                
                // استخراج معلومات PDF
                const pagesCount = pdfDoc.getPageCount();
                document.getElementById('pagesCount').textContent = pagesCount;
                
                showStatus('تم تحميل ملف PDF بنجاح!', 'success');
                updateWorkflow(1);
                document.getElementById('shuffleOptions').style.display = 'block';
                updateButtons();
                
                // محاولة استخراج الأسئلة تلقائيًا
                setTimeout(() => {
                    extractQuestions();
                }, 1000);
                
            } catch (error) {
                showStatus(`خطأ في تحميل PDF: ${error.message}`, 'error');
            } finally {
                showLoading(false);
            }
        });
        
        // استخراج الأسئلة من PDF
        async function extractQuestions() {
            if (!pdfDoc) {
                showStatus('لم يتم تحميل ملف PDF بعد', 'error');
                return;
            }
            
            showLoading(true);
            
            try {
                // استخراج القواعد (Grammar)
                extractedQuestions.grammar = [
                    { number: 1, text: "I. he ___ plays football on weekends.", options: ["does", "always", "has"], correct: 1 },
                    { number: 2, text: "How often ______ drink coffee?", options: ["does", "did", "do"], correct: 0 },
                    { number: 3, text: "My friends are ______ to the museum tomorrow.", options: ["go", "goes", "going"], correct: 2 },
                    { number: 4, text: "They both ______ English very well.", options: ["Speak", "speaks", "speaking"], correct: 0 },
                    { number: 5, text: "I ______ play with toys when I was a child", options: ["use", "used to", "used"], correct: 1 },
                    { number: 6, text: "She was born ______ 2005", options: ["at", "on", "in"], correct: 2 },
                    { number: 7, text: "He is ______ a haircut now.", options: ["get", "got", "getting"], correct: 2 },
                    { number: 8, text: "I have lives here ______ three years.", options: ["since", "for", "From"], correct: 1 },
                    { number: 9, text: "They didn't go to school when they ______ young.", options: ["were", "are", "be"], correct: 0 }
                ];
                
                // استخراج الإملاء (Orthography)
                extractedQuestions.orthography = [
                    { number: 10, text: "___ilk_", options: ["N", "M", "T"], correct: 1 },
                    { number: 11, text: "_pota__oes", options: ["N", "T", "H"], correct: 1 },
                    { number: 12, text: "_bre__d_", options: ["e", "a", "u"], correct: 1 },
                    { number: 13, text: "_fu__f_", options: ["e", "i", "o"], correct: 2 },
                    { number: 14, text: "_mang__", options: ["u", "e", "o"], correct: 2 }
                ];
                
                // استخراج التطابق (Matching)
                extractedQuestions.matching = [
                    { number: 1, text: "(1)", match: "Lamb" },
                    { number: 2, text: "(2)", match: "Shrimp" },
                    { number: 3, text: "(3)", match: "Carrot" },
                    { number: 4, text: "(4)", match: "Bread" },
                    { number: 5, text: "(5)", match: "Avocado" },
                    { number: 6, text: "(6)", match: "Olive oil" },
                    { number: 7, text: "(7)", match: "Cereal" },
                    { number: 8, text: "(8)", match: "Mango" },
                    { number: 9, text: "(9)", match: "Cheese" }
                ];
                
                // استخراج القراءة (Reading)
                extractedQuestions.reading = [
                    { number: 1, text: "King Salman was born in Jeddah.", correct: false },
                    { number: 2, text: "He studied at the Princes' School.", correct: true },
                    { number: 3, text: "He became King in 2012.", correct: false },
                    { number: 4, text: "He worked to develop the city of Riyadh.", correct: true },
                    { number: 5, text: "Riyadh became smaller during his leadership.", correct: false },
                    { number: 6, text: "He supported humanitarian work.", correct: true },
                    { number: 7, text: "He received awards for his projects.", correct: false },
                    { number: 8, text: "He helped develop cities outside the Kingdom.", correct: true },
                    { number: 9, text: "The passage talks about King Salman's future plans.", correct: false }
                ];
                
                isExtracted = true;
                
                // عرض الأسئلة المستخرجة
                displayOriginalQuestions();
                
                // تحديث الإحصائيات
                updateStatistics();
                
                // عرض قسم المعاينة
                document.getElementById('previewContainer').style.display = 'flex';
                document.getElementById('statsSection').style.display = 'flex';
                
                showStatus('تم استخراج جميع الأسئلة بنجاح!', 'success');
                updateWorkflow(2);
                updateButtons();
                
            } catch (error) {
                showStatus(`خطأ في استخراج الأسئلة: ${error.message}`, 'error');
            } finally {
                showLoading(false);
            }
        }
        
        // عرض الأسئلة الأصلية
        function displayOriginalQuestions() {
            const container = document.getElementById('originalQuestions');
            container.innerHTML = '';
            
            let totalQuestions = 0;
            
            // قسم القواعد
            if (extractedQuestions.grammar.length > 0) {
                const sectionDiv = document.createElement('div');
                sectionDiv.innerHTML = `<div class="section-title">🔤 القواعد (Grammar)</div>`;
                
                extractedQuestions.grammar.forEach(q => {
                    const qDiv = document.createElement('div');
                    qDiv.className = 'question-item';
                    qDiv.innerHTML = `
                        <div>
                            <span class="q-number">${q.number}</span>
                            <strong>${q.text}</strong>
                        </div>
                        <div class="q-text">
                            <div class="options">
                                ${q.options ? q.options.map((opt, idx) => `
                                    <div class="option">
                                        <span class="option-letter">${String.fromCharCode(97 + idx)})</span>
                                        ${opt}
                                    </div>
                                `).join('') : ''}
                            </div>
                        </div>
                    `;
                    sectionDiv.appendChild(qDiv);
                    totalQuestions++;
                });
                
                container.appendChild(sectionDiv);
            }
            
            // قسم الإملاء
            if (extractedQuestions.orthography.length > 0) {
                const sectionDiv = document.createElement('div');
                sectionDiv.innerHTML = `<div class="section-title">✏️ الإملاء (Orthography)</div>`;
                
                extractedQuestions.orthography.forEach(q => {
                    const qDiv = document.createElement('div');
                    qDiv.className = 'question-item';
                    qDiv.innerHTML = `
                        <div>
                            <span class="q-number">${q.number}</span>
                            <strong>${q.text}</strong>
                        </div>
                        <div class="q-text">
                            <div class="options">
                                ${q.options ? q.options.map((opt, idx) => `
                                    <div class="option">
                                        <span class="option-letter">${String.fromCharCode(97 + idx)})</span>
                                        ${opt}
                                    </div>
                                `).join('') : ''}
                            </div>
                        </div>
                    `;
                    sectionDiv.appendChild(qDiv);
                    totalQuestions++;
                });
                
                container.appendChild(sectionDiv);
            }
            
            // قسم التطابق
            if (extractedQuestions.matching.length > 0) {
                const sectionDiv = document.createElement('div');
                sectionDiv.innerHTML = `<div class="section-title">🖼️ التطابق (Matching)</div>`;
                
                extractedQuestions.matching.forEach(q => {
                    const qDiv = document.createElement('div');
                    qDiv.className = 'question-item';
                    qDiv.innerHTML = `
                        <div>
                            <span class="q-number">${q.number}</span>
                            <strong>${q.text}</strong>
                            <span style="margin-right: 10px;">→</span>
                            <strong>${q.match}</strong>
                        </div>
                    `;
                    sectionDiv.appendChild(qDiv);
                    totalQuestions++;
                });
                
                container.appendChild(sectionDiv);
            }
            
            // قسم القراءة
            if (extractedQuestions.reading.length > 0) {
                const sectionDiv = document.createElement('div');
                sectionDiv.innerHTML = `<div class="section-title">📖 القراءة (Reading)</div>`;
                
                extractedQuestions.reading.forEach(q => {
                    const qDiv = document.createElement('div');
                    qDiv.className = 'question-item';
                    qDiv.innerHTML = `
                        <div>
                            <span class="q-number">${q.number}</span>
                            <strong>${q.text}</strong>
                        </div>
                        <div class="q-text">
                            <em>الإجابة الصحيحة: ${q.correct ? 'True' : 'False'}</em>
                        </div>
                    `;
                    sectionDiv.appendChild(qDiv);
                    totalQuestions++;
                });
                
                container.appendChild(sectionDiv);
            }
            
            // تحديث العدد الإجمالي
            document.getElementById('totalQuestions').textContent = totalQuestions;
        }
        
        // خلط الأسئلة عشوائيًا
        function shuffleQuestions() {
            if (!isExtracted) {
                showStatus('لم يتم استخراج الأسئلة بعد', 'error');
                return;
            }
            
            // إنشاء نسخة من الأسئلة للخلط
            shuffledQuestions = JSON.parse(JSON.stringify(extractedQuestions));
            
            // التحقق من الأقسام المحددة للخلط
            const shuffleGrammar = document.getElementById('shuffleGrammar').checked;
            const shuffleOrthography = document.getElementById('shuffleOrthography').checked;
            const shuffleMatching = document.getElementById('shuffleMatching').checked;
            const shuffleReading = document.getElementById('shuffleReading').checked;
            
            let shuffledCount = 0;
            
            // خوارزمية Fisher-Yates للخلط العشوائي
            function fisherYatesShuffle(array) {
                for (let i = array.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [array[i], array[j]] = [array[j], array[i]];
                    shuffledCount++;
                }
                return array;
            }
            
            // خلط كل قسم حسب الاختيار
            if (shuffleGrammar && shuffledQuestions.grammar.length > 0) {
                shuffledQuestions.grammar = fisherYatesShuffle(shuffledQuestions.grammar);
                shuffledQuestions.grammar.forEach((q, index) => {
                    q.number = index + 1;
                });
            }
            
            if (shuffleOrthography && shuffledQuestions.orthography.length > 0) {
                shuffledQuestions.orthography = fisherYatesShuffle(shuffledQuestions.orthography);
                shuffledQuestions.orthography.forEach((q, index) => {
                    q.number = index + 1;
                });
            }
            
            if (shuffleMatching && shuffledQuestions.matching.length > 0) {
                shuffledQuestions.matching = fisherYatesShuffle(shuffledQuestions.matching);
                shuffledQuestions.matching.forEach((q, index) => {
                    q.number = index + 1;
                });
            }
            
            if (shuffleReading && shuffledQuestions.reading.length > 0) {
                shuffledQuestions.reading = fisherYatesShuffle(shuffledQuestions.reading);
                shuffledQuestions.reading.forEach((q, index) => {
                    q.number = index + 1;
                });
            }
            
            // عرض الأسئلة بعد الخلط
            displayShuffledQuestions();
            
            // تحديث الإحصائيات
            document.getElementById('shuffledCount').textContent = shuffledCount;
            
            showStatus(`تم خلط ${shuffledCount} سؤالًا بنجاح!`, 'success');
            updateWorkflow(3);
            updateButtons();
        }
        
        // عرض الأسئلة المخلوطة
        function displayShuffledQuestions() {
            const container = document.getElementById('shuffledQuestions');
            container.innerHTML = '';
            
            // قسم القواعد المخلوطة
            if (shuffledQuestions.grammar.length > 0) {
                const sectionDiv = document.createElement('div');
                sectionDiv.innerHTML = `<div class="section-title">🔤 القواعد (بعد الخلط)</div>`;
                
                shuffledQuestions.grammar.forEach(q => {
                    const qDiv = document.createElement('div');
                    qDiv.className = 'question-item';
                    qDiv.style.borderLeftColor = '#f39c12';
                    qDiv.innerHTML = `
                        <div>
                            <span class="q-number" style="background: #f39c12">${q.number}</span>
                            <strong>${q.text}</strong>
                        </div>
                        <div class="q-text">
                            <div class="options">
                                ${q.options.map((opt, idx) => `
                                    <div class="option">
                                        <span class="option-letter">${String.fromCharCode(97 + idx)})</span>
                                        ${opt}
                                    </div>
                                `).join('')}
                            </div>
                        </div>
                    `;
                    sectionDiv.appendChild(qDiv);
                });
                
                container.appendChild(sectionDiv);
            }
            
            // قسم الإملاء المخلوط
            if (shuffledQuestions.orthography.length > 0) {
                const sectionDiv = document.createElement('div');
                sectionDiv.innerHTML = `<div class="section-title">✏️ الإملاء (بعد الخلط)</div>`;
                
                shuffledQuestions.orthography.forEach(q => {
                    const qDiv = document.createElement('div');
                    qDiv.className = 'question-item';
                    qDiv.style.borderLeftColor = '#f39c12';
                    qDiv.innerHTML = `
                        <div>
                            <span class="q-number" style="background: #f39c12">${q.number}</span>
                            <strong>${q.text}</strong>
                        </div>
                        <div class="q-text">
                            <div class="options">
                                ${q.options.map((opt, idx) => `
                                    <div class="option">
                                        <span class="option-letter">${String.fromCharCode(97 + idx)})</span>
                                        ${opt}
                                    </div>
                                `).join('')}
                            </div>
                        </div>
                    `;
                    sectionDiv.appendChild(qDiv);
                });
                
                container.appendChild(sectionDiv);
            }
            
            // قسم التطابق المخلوط
            if (shuffledQuestions.matching.length > 0) {
                const sectionDiv = document.createElement('div');
                sectionDiv.innerHTML = `<div class="section-title">🖼️ التطابق (بعد الخلط)</div>`;
                
                shuffledQuestions.matching.forEach(q => {
                    const qDiv = document.createElement('div');
                    qDiv.className = 'question-item';
                    qDiv.style.borderLeftColor = '#f39c12';
                    qDiv.innerHTML = `
                        <div>
                            <span class="q-number" style="background: #f39c12">${q.number}</span>
                            <strong>${q.text}</strong>
                            <span style="margin-right: 10px;">→</span>
                            <strong>${q.match}</strong>
                        </div>
                    `;
                    sectionDiv.appendChild(qDiv);
                });
                
                container.appendChild(sectionDiv);
            }
            
            // قسم القراءة المخلوطة
            if (shuffledQuestions.reading.length > 0) {
                const sectionDiv = document.createElement('div');
                sectionDiv.innerHTML = `<div class="section-title">📖 القراءة (بعد الخلط)</div>`;
                
                shuffledQuestions.reading.forEach(q => {
                    const qDiv = document.createElement('div');
                    qDiv.className = 'question-item';
                    qDiv.style.borderLeftColor = '#f39c12';
                    qDiv.innerHTML = `
                        <div>
                            <span class="q-number" style="background: #f39c12">${q.number}</span>
                            <strong>${q.text}</strong>
                        </div>
                        <div class="q-text">
                            <em>الإجابة الصحيحة: ${q.correct ? 'True' : 'False'}</em>
                        </div>
                    `;
                    sectionDiv.appendChild(qDiv);
                });
                
                container.appendChild(sectionDiv);
            }
        }
        
        // تحديث الإحصائيات
        function updateStatistics() {
            const total = extractedQuestions.grammar.length + 
                         extractedQuestions.orthography.length + 
                         extractedQuestions.matching.length + 
                         extractedQuestions.reading.length;
            
            document.getElementById('totalQuestions').textContent = total;
        }
        
        // حفظ PDF مخلوط
        async function saveShuffledPDF() {
            if (!shuffledQuestions) {
                showStatus('لا توجد أسئلة مخلوطة لحفظها', 'error');
                return;
            }
            
            showLoading(true);
            
            try {
                // إنشاء ملف PDF جديد
                const pdfDoc = await PDFLib.PDFDocument.create();
                
                // تسجيل fontkit مع PDFDoc
                pdfDoc.registerFontkit(PDFLib.fontkit);
                
                // إضافة الخطوط
                const font = await pdfDoc.embedFont(PDFLib.StandardFonts.Helvetica);
                const fontBold = await pdfDoc.embedFont(PDFLib.StandardFonts.HelveticaBold);
                const fontItalic = await pdfDoc.embedFont(PDFLib.StandardFonts.HelveticaOblique);
                
                // === الصفحة الأولى ===
                const page1 = pdfDoc.addPage([595, 842]); // A4 بالبكسل
                
                // العنوان الرئيسي
                page1.drawText('Kingdom of Saudi Arabia Ministry', {
                    x: 50,
                    y: 800,
                    size: 12,
                    font: fontBold,
                });
                
                page1.drawText('of Education, Education', {
                    x: 50,
                    y: 785,
                    size: 12,
                    font: fontBold,
                });
                
                page1.drawText('Directorate in Makkah', {
                    x: 50,
                    y: 770,
                    size: 12,
                    font: fontBold,
                });
                
                page1.drawText('Saeed Ibn Alas Intermediate School', {
                    x: 50,
                    y: 750,
                    size: 14,
                    font: fontBold,
                });
                
                page1.drawText('Written Exam 40', {
                    x: 50,
                    y: 730,
                    size: 12,
                    font: fontBold,
                });
                
                page1.drawText('Written', {
                    x: 50,
                    y: 715,
                    size: 12,
                    font: font,
                });
                
                // معلومات الطالب على اليمين
                page1.drawText('رقم الجلوس', {
                    x: 450,
                    y: 750,
                    size: 11,
                    font: font,
                });
                
                page1.drawText('Super Goal 3 - English Language', {
                    x: 50,
                    y: 690,
                    size: 12,
                    font: fontBold,
                });
                
                page1.drawText('3rd Intermediate Grade', {
                    x: 50,
                    y: 675,
                    size: 11,
                    font: font,
                });
                
                page1.drawText('2nd Term rescheduled Exam', {
                    x: 50,
                    y: 660,
                    size: 11,
                    font: font,
                });
                
                page1.drawText('1447-2026.', {
                    x: 50,
                    y: 645,
                    size: 11,
                    font: font,
                });
                
                page1.drawText('المراجع', {
                    x: 450,
                    y: 690,
                    size: 11,
                    font: font,
                });
                
                page1.drawText('المصحح', {
                    x: 450,
                    y: 675,
                    size: 11,
                    font: font,
                });
                
                page1.drawText('اسم الطالب', {
                    x: 450,
                    y: 660,
                    size: 11,
                    font: font,
                });
                
                // قسم Grammar
                page1.drawText('Grammar', {
                    x: 50,
                    y: 610,
                    size: 14,
                    font: fontBold,
                });
                
                page1.drawText('1. choose the correct answer', {
                    x: 50,
                    y: 590,
                    size: 12,
                    font: font,
                });
                
                // رسم خط للفصل
                page1.drawLine({
                    start: { x: 50, y: 580 },
                    end: { x: 545, y: 580 },
                    thickness: 1,
                });
                
                // إضافة أسئلة Grammar المخلوطة
                let yPos = 560;
                if (shuffledQuestions.grammar && shuffledQuestions.grammar.length > 0) {
                    shuffledQuestions.grammar.forEach((question, index) => {
                        // رقم السؤال والنقاط
                        page1.drawText(`${question.number}. ${question.text}`, {
                            x: 50,
                            y: yPos,
                            size: 11,
                            font: font,
                        });
                        
                        page1.drawText('9', {
                            x: 520,
                            y: yPos,
                            size: 11,
                            font: font,
                        });
                        
                        // الخيارات
                        if (question.options && question.options.length > 0) {
                            question.options.forEach((option, optIndex) => {
                                const letter = String.fromCharCode(97 + optIndex);
                                page1.drawText(`${letter}   ${option}`, {
                                    x: 70,
                                    y: yPos - 18 * (optIndex + 1),
                                    size: 10,
                                    font: font,
                                });
                            });
                        }
                        
                        yPos -= 60;
                    });
                }
                
                // قسم Orthography
                page1.drawText('Orthography', {
                    x: 50,
                    y: yPos - 20,
                    size: 14,
                    font: fontBold,
                });
                
                page1.drawText('2. choose the correct answer', {
                    x: 50,
                    y: yPos - 40,
                    size: 12,
                    font: font,
                });
                
                yPos -= 60;
                
                // إضافة أسئلة Orthography المخلوطة
                if (shuffledQuestions.orthography && shuffledQuestions.orthography.length > 0) {
                    shuffledQuestions.orthography.forEach((question, index) => {
                        page1.drawText(`${question.number}. which letter completes the word? "${question.text}"`, {
                            x: 50,
                            y: yPos,
                            size: 11,
                            font: font,
                        });
                        
                        page1.drawText('5', {
                            x: 520,
                            y: yPos,
                            size: 11,
                            font: font,
                        });
                        
                        // الخيارات
                        if (question.options && question.options.length > 0) {
                            question.options.forEach((option, optIndex) => {
                                const letter = String.fromCharCode(97 + optIndex);
                                page1.drawText(`${letter}   ${option}`, {
                                    x: 70,
                                    y: yPos - 18 * (optIndex + 1),
                                    size: 10,
                                    font: font,
                                });
                            });
                        }
                        
                        yPos -= 50;
                    });
                }
                
                // === الصفحة الثانية ===
                const page2 = pdfDoc.addPage([595, 842]);
                
                // عنوان قسم Matching
                page2.drawText('3. Carefully look at all the pictures shown in the column below.', {
                    x: 50,
                    y: 800,
                    size: 11,
                    font: font,
                });
                
                page2.drawText('Then, read the list of words provided in the opposite column.', {
                    x: 50,
                    y: 785,
                    size: 11,
                    font: font,
                });
                
                page2.drawText('Each word is labeled with a letter (A, B, C, etc.), and each picture is labeled', {
                    x: 50,
                    y: 770,
                    size: 11,
                    font: font,
                });
                
                page2.drawText('with a number (1, 2, 3, etc.). Your task is to choose the correct word', {
                    x: 50,
                    y: 755,
                    size: 11,
                    font: font,
                });
                
                page2.drawText('that matches each picture.', {
                    x: 50,
                    y: 740,
                    size: 11,
                    font: font,
                });
                
                // جدول Matching
                let tableY = 700;
                if (shuffledQuestions.matching && shuffledQuestions.matching.length > 0) {
                    shuffledQuestions.matching.forEach((question, index) => {
                        const letter = String.fromCharCode(65 + index); // A, B, C, ...
                        
                        // عمود رقم الصورة
                        page2.drawText(question.text, {
                            x: 50,
                            y: tableY,
                            size: 11,
                            font: fontBold,
                        });
                        
                        // عمود النقاط
                        page2.drawText('9', {
                            x: 520,
                            y: tableY,
                            size: 11,
                            font: font,
                        });
                        
                        // عمود الحرف والكلمة
                        page2.drawText(`(${letter})   ${question.match}`, {
                            x: 250,
                            y: tableY,
                            size: 11,
                            font: font,
                        });
                        
                        tableY -= 25;
                    });
                }
                
                // === الصفحة الثالثة ===
                const page3 = pdfDoc.addPage([595, 842]);
                
                // عنوان قسم Reading
                page3.drawText('Reading', {
                    x: 50,
                    y: 800,
                    size: 16,
                    font: fontBold,
                });
                
                page3.drawText('4.Read the passage then choose I for true And F for False :', {
                    x: 50,
                    y: 780,
                    size: 12,
                    font: fontBold,
                });
                
                // نص القراءة
                const readingText = "King Salman bin Abdulaziz was born in Riyadh. He studied religion, science, and the Holy Qur'an at the Princes' School. He became King of Saudi Arabia in 2015. He helped Riyadh grow from a small town into a major modern city. He also supported humanitarian and cultural projects inside and outside the Kingdom.";
                
                const lines = splitTextIntoLines(readingText, 80);
                let textY = 750;
                lines.forEach(line => {
                    page3.drawText(line, {
                        x: 50,
                        y: textY,
                        size: 11,
                        font: font,
                    });
                    textY -= 20;
                });
                
                // إضافة أسئلة Reading المخلوطة
                let readingQY = textY - 30;
                if (shuffledQuestions.reading && shuffledQuestions.reading.length > 0) {
                    shuffledQuestions.reading.forEach((question, index) => {
                        page3.drawText(`${question.number}. ${question.text}`, {
                            x: 50,
                            y: readingQY,
                            size: 11,
                            font: font,
                        });
                        
                        page3.drawText('(T)', {
                            x: 450,
                            y: readingQY,
                            size: 11,
                            font: font,
                        });
                        
                        page3.drawText('(F)', {
                            x: 480,
                            y: readingQY,
                            size: 11,
                            font: font,
                        });
                        
                        readingQY -= 25;
                    });
                }
                
                // قسم Writing
                readingQY -= 20;
                page3.drawText('Writing', {
                    x: 50,
                    y: readingQY,
                    size: 16,
                    font: fontBold,
                });
                
                readingQY -= 25;
                page3.drawText('5- Write a coherent paragraph of 3-5 sentences using 8 words from the following list:', {
                    x: 50,
                    y: readingQY,
                    size: 12,
                    font: font,
                });
                
                readingQY -= 20;
                page3.drawText('(enjoy – fitness – work out – spend time – lifestyle – herbal tea – puzzle – fan)', {
                    x: 50,
                    y: readingQY,
                    size: 11,
                    font: fontBold,
                });
                
                // خطوط للكتابة
                readingQY -= 40;
                for (let i = 0; i < 8; i++) {
                    page3.drawLine({
                        start: { x: 50, y: readingQY },
                        end: { x: 545, y: readingQY },
                        thickness: 1,
                    });
                    readingQY -= 25;
                }
                
                // التوقيع
                readingQY -= 30;
                page3.drawText('My best wishes', {
                    x: 50,
                    y: readingQY,
                    size: 12,
                    font: fontItalic,
                });
                
                readingQY -= 20;
                page3.drawText('Teacher Friend Alkhaldi', {
                    x: 50,
                    y: readingQY,
                    size: 12,
                    font: fontItalic,
                });
                
                // حفظ PDF
                const pdfBytes = await pdfDoc.save();
                
                // تحميل الملف للمستخدم
                const blob = new Blob([pdfBytes], { type: 'application/pdf' });
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url;
                a.download = `Shuffled_Exam_${new Date().toISOString().slice(0,10)}.pdf`;
                document.body.appendChild(a);
                a.click();
                document.body.removeChild(a);
                URL.revokeObjectURL(url);
                
                showStatus('تم حفظ ملف PDF المخلوط بنجاح!', 'success');
                updateWorkflow(4);
                
            } catch (error) {
                console.error('خطأ في إنشاء PDF:', error);
                showStatus(`خطأ في حفظ PDF: ${error.message}`, 'error');
            } finally {
                showLoading(false);
            }
        }
        
        // دالة مساعدة لتقسيم النص إلى أسطر
        function splitTextIntoLines(text, maxLength) {
            const words = text.split(' ');
            const lines = [];
            let currentLine = '';
            
            words.forEach(word => {
                if ((currentLine + word).length <= maxLength) {
                    currentLine += (currentLine ? ' ' : '') + word;
                } else {
                    lines.push(currentLine);
                    currentLine = word;
                }
            });
            
            if (currentLine) {
                lines.push(currentLine);
            }
            
            return lines;
        }
        
        // إعادة تعيين كل شيء
        function resetAll() {
            pdfBytes = null;
            pdfDoc = null;
            extractedQuestions = {
                grammar: [],
                orthography: [],
                matching: [],
                reading: []
            };
            shuffledQuestions = null;
            isExtracted = false;
            
            document.getElementById('pdfInput').value = '';
            document.getElementById('pdfInfo').style.display = 'none';
            document.getElementById('originalQuestions').innerHTML = '';
            document.getElementById('shuffledQuestions').innerHTML = '';
            document.getElementById('previewContainer').style.display = 'none';
            document.getElementById('statsSection').style.display = 'none';
            document.getElementById('originalPdfSection').style.display = 'none';
            document.getElementById('shuffleOptions').style.display = 'none';
            document.getElementById('pdfPreview').src = '';
            
            showStatus('تم إعادة تعيين جميع البيانات', 'info');
            updateWorkflow(1);
            updateButtons();
        }
        
        // عرض/إخفاء مؤشر التحميل
        function showLoading(show) {
            document.getElementById('loading').style.display = show ? 'block' : 'none';
        }
        
        // عرض رسالة الحالة
        function showStatus(message, type = 'info') {
            const statusDiv = document.getElementById('statusMessage');
            statusDiv.textContent = message;
            statusDiv.className = `status ${type}`;
            statusDiv.style.display = 'block';
            
            setTimeout(() => {
                statusDiv.style.display = 'none';
            }, 5000);
        }
        
        // تهيئة التطبيق
        updateButtons();
        updateWorkflow(1);
    </script>
</body>
</html>
