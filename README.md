<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أداة خلط فقرات PDF المتقدمة</title>
    <style>
        * {
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            direction: rtl;
            margin: 0;
            padding: 20px;
            background-color: #f5f9ff;
            color: #333;
            line-height: 1.6;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            background-color: white;
            border-radius: 12px;
            box-shadow: 0 5px 20px rgba(0, 0, 100, 0.08);
            padding: 30px;
        }
        
        h1 {
            color: #2c3e50;
            text-align: center;
            margin-bottom: 10px;
            padding-bottom: 15px;
            border-bottom: 2px solid #eaeff5;
        }
        
        .description {
            text-align: center;
            color: #5a6c7d;
            margin-bottom: 30px;
            font-size: 1.05rem;
        }
        
        .upload-area {
            border: 2px dashed #3498db;
            border-radius: 10px;
            padding: 40px 20px;
            text-align: center;
            margin-bottom: 30px;
            background-color: #f8fbff;
            transition: all 0.3s;
        }
        
        .upload-area:hover, .upload-area.dragover {
            background-color: #e8f4ff;
            border-color: #2980b9;
        }
        
        .upload-area i {
            font-size: 48px;
            color: #3498db;
            margin-bottom: 15px;
        }
        
        .upload-area p {
            margin: 10px 0;
            color: #5a6c7d;
        }
        
        #pdfInput {
            display: none;
        }
        
        .upload-btn {
            display: inline-block;
            background-color: #3498db;
            color: white;
            padding: 12px 24px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            transition: background-color 0.3s;
            border: none;
            font-size: 16px;
            margin-top: 10px;
        }
        
        .upload-btn:hover {
            background-color: #2980b9;
        }
        
        .options-section {
            background-color: #f8fafc;
            padding: 25px;
            border-radius: 10px;
            margin-bottom: 30px;
            border: 1px solid #eaeff5;
        }
        
        .options-section h3 {
            color: #2c3e50;
            margin-top: 0;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 1px solid #e1e8f0;
        }
        
        .option-group {
            margin-bottom: 20px;
        }
        
        .option-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #2c3e50;
        }
        
        .option-group select, .option-group input {
            width: 100%;
            padding: 10px 12px;
            border: 1px solid #d1d9e6;
            border-radius: 6px;
            font-size: 16px;
            background-color: white;
        }
        
        .checkbox-group {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .checkbox-group input {
            width: auto;
            margin-left: 10px;
        }
        
        .buttons {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 30px;
            flex-wrap: wrap;
        }
        
        .btn {
            padding: 14px 28px;
            border-radius: 6px;
            border: none;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            min-width: 180px;
            margin: 5px;
        }
        
        .btn-primary {
            background-color: #2ecc71;
            color: white;
        }
        
        .btn-primary:hover {
            background-color: #27ae60;
        }
        
        .btn-secondary {
            background-color: #e74c3c;
            color: white;
        }
        
        .btn-secondary:hover {
            background-color: #c0392b;
        }
        
        .btn-tertiary {
            background-color: #3498db;
            color: white;
        }
        
        .btn-tertiary:hover {
            background-color: #2980b9;
        }
        
        .btn:disabled {
            background-color: #bdc3c7;
            cursor: not-allowed;
        }
        
        .status {
            margin-top: 25px;
            padding: 15px;
            border-radius: 6px;
            text-align: center;
            font-weight: 600;
            display: none;
        }
        
        .status.success {
            background-color: #d5f4e6;
            color: #27ae60;
            display: block;
        }
        
        .status.error {
            background-color: #fdeaea;
            color: #e74c3c;
            display: block;
        }
        
        .status.info {
            background-color: #e8f4fc;
            color: #3498db;
            display: block;
        }
        
        .file-info {
            margin-top: 20px;
            padding: 15px;
            background-color: #f0f7ff;
            border-radius: 8px;
            border-right: 4px solid #3498db;
            display: none;
        }
        
        .file-info.show {
            display: block;
        }
        
        .file-info p {
            margin: 8px 0;
        }
        
        .loading {
            display: none;
            text-align: center;
            margin: 20px 0;
        }
        
        .loading.show {
            display: block;
        }
        
        .spinner {
            border: 5px solid #f3f3f3;
            border-top: 5px solid #3498db;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            animation: spin 1s linear infinite;
            margin: 0 auto 15px;
        }
        
        .preview-section {
            margin-top: 30px;
            border-top: 2px solid #eaeff5;
            padding-top: 20px;
        }
        
        .preview-section h3 {
            color: #2c3e50;
            margin-bottom: 15px;
        }
        
        .preview-container {
            display: flex;
            gap: 20px;
            flex-wrap: wrap;
        }
        
        .preview-box {
            flex: 1;
            min-width: 300px;
            background-color: #f8fafc;
            border: 1px solid #e1e8f0;
            border-radius: 8px;
            padding: 15px;
            max-height: 500px;
            overflow-y: auto;
        }
        
        .preview-box h4 {
            margin-top: 0;
            color: #2c3e50;
            padding-bottom: 10px;
            border-bottom: 1px solid #e1e8f0;
        }
        
        .paragraph-item {
            padding: 10px 12px;
            margin-bottom: 8px;
            background-color: white;
            border: 1px solid #e1e8f0;
            border-radius: 5px;
            cursor: move;
            transition: all 0.2s;
        }
        
        .paragraph-item:hover {
            background-color: #f0f7ff;
            transform: translateX(-5px);
        }
        
        .paragraph-item.selected {
            background-color: #e8f4fc;
            border-color: #3498db;
        }
        
        .paragraph-item.dragging {
            opacity: 0.5;
        }
        
        .paragraph-number {
            display: inline-block;
            background-color: #3498db;
            color: white;
            width: 28px;
            height: 28px;
            border-radius: 50%;
            text-align: center;
            line-height: 28px;
            margin-left: 8px;
            font-size: 14px;
        }
        
        .paragraph-select {
            margin-left: 10px;
            transform: scale(1.2);
        }
        
        .selection-controls {
            margin: 15px 0;
            padding: 10px;
            background-color: #f0f7ff;
            border-radius: 5px;
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }
        
        .selection-controls button {
            padding: 8px 16px;
            background-color: #3498db;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 14px;
        }
        
        .selection-controls button:hover {
            background-color: #2980b9;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        @media (max-width: 768px) {
            .container {
                padding: 20px;
            }
            
            .buttons {
                flex-direction: column;
            }
            
            .btn {
                width: 100%;
            }
            
            .preview-container {
                flex-direction: column;
            }
        }
    </style>
    <script src="https://cdn.jsdelivr.net/npm/pdf-lib@1.17.1/dist/pdf-lib.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.4.120/pdf.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
</head>
<body>
    <div class="container">
        <h1>أداة خلط فقرات PDF المتقدمة</h1>
        <p class="description">أداة متكاملة لخلط فقرات ملفات PDF مع الخيارات بشكل متقن، مثالية لإنشاء أسئلة امتحانية مختلفة</p>
        
        <div class="upload-area" id="uploadArea">
            <div>📄</div>
            <p><strong>اسحب وأفلت ملف PDF هنا</strong></p>
            <p>أو</p>
            <label for="pdfInput" class="upload-btn">اختر ملف PDF</label>
            <input type="file" id="pdfInput" accept="application/pdf">
        </div>
        
        <div class="file-info" id="fileInfo">
            <p><strong>اسم الملف:</strong> <span id="fileName"></span></p>
            <p><strong>حجم الملف:</strong> <span id="fileSize"></span></p>
            <p><strong>عدد الصفحات:</strong> <span id="pageCount"></span></p>
            <p><strong>عدد الفقرات المستخرجة:</strong> <span id="paragraphCount">0</span></p>
            <p><strong>عدد الفقرات المختارة للخلط:</strong> <span id="selectedCount">0</span></p>
        </div>
        
        <div class="options-section">
            <h3>خيارات الخلط</h3>
            
            <div class="option-group">
                <label for="shuffleScope">نطاق الخلط:</label>
                <select id="shuffleScope">
                    <option value="all">خلط جميع الفقرات</option>
                    <option value="selected">خلط الفقرات المختارة فقط</option>
                    <option value="questions">خلط الأسئلة فقط</option>
                    <option value="within-question">خلط داخل السؤال الواحد</option>
                </select>
            </div>
            
            <div class="option-group">
                <label for="shuffleMethod">نوع الخلط داخل السؤال:</label>
                <select id="shuffleMethod">
                    <option value="options">خلط خيارات الأسئلة فقط</option>
                    <option value="subparagraphs">خلط فقرات السؤال الداخلية</option>
                    <option value="both">خلط الخيارات والفقرات معاً</option>
                </select>
            </div>
            
            <div class="option-group">
                <label for="shuffleMode">وضع الخلط:</label>
                <select id="shuffleMode">
                    <option value="auto">خلط تلقائي</option>
                    <option value="manual">ترتيب يدوي</option>
                    <option value="both">الخلط ثم التعديل اليدوي</option>
                </select>
            </div>
            
            <div class="option-group">
                <label for="outputFormat">صيغة الملف الناتج:</label>
                <select id="outputFormat">
                    <option value="pdf">PDF (باستخدام jsPDF)</option>
                    <option value="text">ملف نصي (TXT)</option>
                    <option value="html">ملف HTML</option>
                </select>
            </div>
            
            <div class="option-group">
                <label for="preserveNumbering">حفظ ترقيم الفقرات بعد الخلط:</label>
                <select id="preserveNumbering">
                    <option value="yes">نعم، إعادة ترقيم الفقرات</option>
                    <option value="no">لا، الاحتفاظ بالأرقام الأصلية</option>
                </select>
            </div>
            
            <div class="option-group">
                <label for="seedValue">قيمة البذرة (Seed) للخلط العشوائي:</label>
                <input type="text" id="seedValue" placeholder="اتركه فارغاً للخلط العشوائي الكامل">
                <small>استخدم نفس القيمة للحصول على نفس الترتيب في كل مرة</small>
            </div>
            
            <div class="option-group">
                <label>خيارات إضافية:</label>
                <div class="checkbox-group">
                    <input type="checkbox" id="identifyPatterns" checked>
                    <label for="identifyPatterns">تحديد أنماط الأسئلة تلقائياً</label>
                </div>
                <div class="checkbox-group">
                    <input type="checkbox" id="autoSelectQuestions" checked>
                    <label for="autoSelectQuestions">تحديد الأسئلة تلقائياً للخلط</label>
                </div>
            </div>
        </div>
        
        <div class="preview-section" id="previewSection" style="display: none;">
            <h3>معاينة الفقرات وإعادة الترتيب اليدوي</h3>
            
            <div class="selection-controls">
                <button onclick="selectAll()">تحديد الكل</button>
                <button onclick="deselectAll()">إلغاء تحديد الكل</button>
                <button onclick="selectQuestionsOnly()">تحديد الأسئلة فقط</button>
                <button onclick="selectParagraphsOnly()">تحديد الفقرات فقط</button>
                <button onclick="selectRandom(5)">تحديد 5 عشوائياً</button>
                <button onclick="selectRandom(10)">تحديد 10 عشوائياً</button>
                <div style="margin-right: auto; font-weight: bold; color: #2c3e50;">
                    <span id="selectionSummary">0 فقرة مختارة</span>
                </div>
            </div>
            
            <div class="preview-container">
                <div class="preview-box">
                    <h4>الفقرات الأصلية (انقر لتحديد)</h4>
                    <div id="originalParagraphs"></div>
                </div>
                <div class="preview-box">
                    <h4>الفقرات بعد الخلط</h4>
                    <div id="shuffledParagraphs"></div>
                </div>
            </div>
        </div>
        
        <div class="loading" id="loading">
            <div class="spinner"></div>
            <p>جاري معالجة ملف PDF...</p>
            <p>يرجى الانتظار، قد تستغرق العملية بعض الوقت حسب حجم الملف</p>
        </div>
        
        <div class="status" id="status"></div>
        
        <div class="buttons">
            <button class="btn btn-tertiary" onclick="processPdf()" id="processBtn">
                <span>🔍</span> استخراج الفقرات
            </button>
            <button class="btn btn-primary" onclick="shuffleAndDownload()" id="shuffleBtn" disabled>
                <span>🔀</span> خلط وتنزيل الملف
            </button>
            <button class="btn btn-secondary" onclick="resetAll()" id="resetBtn">
                <span>🔄</span> إعادة تعيين
            </button>
        </div>
    </div>

    <script>
        // متغيرات عامة
        let pdfDoc = null;
        let extractedParagraphs = [];
        let shuffledParagraphs = [];
        let selectedParagraphs = new Set();
        let pdfName = "";
        let pdfPagesCount = 0;
        
        // تعريف عناصر DOM
        const pdfInput = document.getElementById('pdfInput');
        const uploadArea = document.getElementById('uploadArea');
        const fileInfo = document.getElementById('fileInfo');
        const fileName = document.getElementById('fileName');
        const fileSize = document.getElementById('fileSize');
        const pageCount = document.getElementById('pageCount');
        const paragraphCount = document.getElementById('paragraphCount');
        const selectedCount = document.getElementById('selectedCount');
        const loading = document.getElementById('loading');
        const status = document.getElementById('status');
        const processBtn = document.getElementById('processBtn');
        const shuffleBtn = document.getElementById('shuffleBtn');
        const resetBtn = document.getElementById('resetBtn');
        const previewSection = document.getElementById('previewSection');
        const originalParagraphs = document.getElementById('originalParagraphs');
        const shuffledParagraphsDiv = document.getElementById('shuffledParagraphs');
        const selectionSummary = document.getElementById('selectionSummary');
        
        // تهيئة مكتبة pdf.js
        pdfjsLib.GlobalWorkerOptions.workerSrc = `https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.4.120/pdf.worker.min.js`;
        
        // إضافة أحداث السحب والإفلات
        uploadArea.addEventListener('dragover', (e) => {
            e.preventDefault();
            uploadArea.classList.add('dragover');
        });
        
        uploadArea.addEventListener('dragleave', () => {
            uploadArea.classList.remove('dragover');
        });
        
        uploadArea.addEventListener('drop', (e) => {
            e.preventDefault();
            uploadArea.classList.remove('dragover');
            
            if (e.dataTransfer.files.length) {
                const file = e.dataTransfer.files[0];
                if (file.type === 'application/pdf') {
                    pdfInput.files = e.dataTransfer.files;
                    handleFileUpload(file);
                } else {
                    showStatus('يرجى اختيار ملف PDF فقط', 'error');
                }
            }
        });
        
        // حدث اختيار الملف
        pdfInput.addEventListener('change', (e) => {
            if (e.target.files.length) {
                handleFileUpload(e.target.files[0]);
            }
        });
        
        // دالة معالجة رفع الملف
        async function handleFileUpload(file) {
            try {
                showLoading(true);
                showStatus('جاري تحميل ملف PDF...', 'info');
                
                pdfName = file.name;
                const fileSizeMB = (file.size / (1024 * 1024)).toFixed(2);
                
                // تحميل ملف PDF باستخدام pdf-lib
                const arrayBuffer = await file.arrayBuffer();
                pdfDoc = await PDFLib.PDFDocument.load(arrayBuffer);
                pdfPagesCount = pdfDoc.getPages().length;
                
                // عرض معلومات الملف
                fileName.textContent = pdfName;
                fileSize.textContent = `${fileSizeMB} MB`;
                pageCount.textContent = pdfPagesCount;
                fileInfo.classList.add('show');
                
                showStatus('تم تحميل ملف PDF بنجاح! يمكنك الآن استخراج الفقرات', 'success');
                processBtn.disabled = false;
                shuffleBtn.disabled = true;
            } catch (error) {
                console.error('Error loading PDF:', error);
                showStatus('حدث خطأ في تحميل ملف PDF. يرجى التأكد من صحة الملف.', 'error');
            } finally {
                showLoading(false);
            }
        }
        
        // دالة استخراج الفقرات من PDF
        async function extractTextFromPDF(file) {
            try {
                const arrayBuffer = await file.arrayBuffer();
                const pdf = await pdfjsLib.getDocument({ data: arrayBuffer }).promise;
                let fullText = '';
                
                for (let i = 1; i <= pdf.numPages; i++) {
                    const page = await pdf.getPage(i);
                    const textContent = await page.getTextContent();
                    const pageText = textContent.items.map(item => item.str).join(' ');
                    fullText += pageText + '\n\n';
                }
                
                return fullText;
            } catch (error) {
                console.error('Error extracting text from PDF:', error);
                throw new Error('فشل في استخراج النص من ملف PDF');
            }
        }
        
        // دالة اكتشاف الفقرات من النص
        function detectParagraphs(text) {
            try {
                const normalizedText = text
                    .replace(/\n\s*\n/g, '\n\n')
                    .replace(/([\.\?\!])\s+/g, '$1\n')
                    .replace(/(\d+\.)\s+/g, '$1\n');
                
                let paragraphs = normalizedText.split(/\n\s*\n/);
                paragraphs = paragraphs
                    .map(p => p.trim())
                    .filter(p => p.length > 5);
                
                if (paragraphs.length === 0) {
                    paragraphs = [text];
                }
                
                const isQuestionnaire = paragraphs.some(p => 
                    p.includes('؟') || p.includes('أ)') || p.includes('ب)') || p.includes('ج)') || p.includes('د)') ||
                    p.includes('(أ)') || p.includes('(ب)') || p.includes('(ج)') || p.includes('(د)')
                );
                
                if (isQuestionnaire && document.getElementById('identifyPatterns').checked) {
                    return processQuestions(paragraphs);
                }
                
                return paragraphs.map((text, index) => ({
                    id: index,
                    text: text,
                    originalIndex: index,
                    type: 'paragraph',
                    selected: false
                }));
            } catch (error) {
                console.error('Error detecting paragraphs:', error);
                return [{
                    id: 0,
                    text: text.substring(0, 1000) + (text.length > 1000 ? '...' : ''),
                    originalIndex: 0,
                    type: 'paragraph',
                    selected: false
                }];
            }
        }
        
        // دالة معالجة الأسئلة متعددة الخيارات
        function processQuestions(paragraphs) {
            try {
                const questionGroups = [];
                let currentQuestion = null;
                
                for (let i = 0; i < paragraphs.length; i++) {
                    const text = paragraphs[i];
                    
                    if (text.match(/^\d+[\.\)]\s/) || text.includes('؟') || text.length > 100 || 
                        text.match(/^سؤال/) || text.match(/^السؤال/)) {
                        if (currentQuestion) {
                            questionGroups.push(currentQuestion);
                        }
                        currentQuestion = {
                            id: questionGroups.length,
                            question: text,
                            options: [],
                            originalIndex: i,
                            type: 'question',
                            selected: document.getElementById('autoSelectQuestions').checked,
                            subparagraphs: []
                        };
                    } 
                    else if (text.match(/^[أ-د]\)/) || text.match(/^[a-d]\./) || 
                             text.match(/^\([أ-د]\)/) || text.match(/^[A-D]\)/) ||
                             (currentQuestion && text.length < 200 && 
                              (text.includes(')') || text.includes('.') || text.length < 150))) {
                        if (currentQuestion) {
                            currentQuestion.options.push({
                                text: text,
                                originalIndex: currentQuestion.options.length
                            });
                        }
                    }
                    else if (currentQuestion && text.length > 30 && text.length < 300) {
                        currentQuestion.subparagraphs.push({
                            text: text,
                            originalIndex: currentQuestion.subparagraphs.length
                        });
                    }
                    else if (currentQuestion) {
                        currentQuestion.question += ' ' + text;
                    } else {
                        questionGroups.push({
                            id: questionGroups.length,
                            text: text,
                            originalIndex: i,
                            type: 'paragraph',
                            selected: false
                        });
                    }
                }
                
                if (currentQuestion) {
                    questionGroups.push(currentQuestion);
                }
                
                return questionGroups;
            } catch (error) {
                console.error('Error processing questions:', error);
                return paragraphs.map((text, index) => ({
                    id: index,
                    text: text,
                    originalIndex: index,
                    type: 'paragraph',
                    selected: false
                }));
            }
        }
        
        // دالة معالجة PDF (استخراج الفقرات)
        async function processPdf() {
            if (!pdfDoc || pdfInput.files.length === 0) {
                showStatus('يرجى تحميل ملف PDF أولاً', 'error');
                return;
            }
            
            try {
                showLoading(true);
                showStatus('جاري استخراج الفقرات من ملف PDF...', 'info');
                
                const file = pdfInput.files[0];
                const text = await extractTextFromPDF(file);
                extractedParagraphs = detectParagraphs(text);
                
                selectedParagraphs.clear();
                extractedParagraphs.forEach((para, index) => {
                    if (para.selected) {
                        selectedParagraphs.add(index);
                    }
                });
                
                shuffledParagraphs = JSON.parse(JSON.stringify(extractedParagraphs));
                paragraphCount.textContent = extractedParagraphs.length;
                updateSelectionCount();
                
                displayParagraphsPreview();
                previewSection.style.display = 'block';
                
                showStatus(`تم استخراج ${extractedParagraphs.length} فقرة بنجاح!`, 'success');
                shuffleBtn.disabled = false;
                
            } catch (error) {
                console.error('Error processing PDF:', error);
                showStatus('حدث خطأ أثناء استخراج الفقرات من PDF: ' + error.message, 'error');
            } finally {
                showLoading(false);
            }
        }
        
        // دالة عرض معاينة الفقرات
        function displayParagraphsPreview() {
            originalParagraphs.innerHTML = '';
            extractedParagraphs.forEach((para, index) => {
                const paraElement = createParagraphElement(para, index, false);
                originalParagraphs.appendChild(paraElement);
            });
            displayShuffledParagraphs();
        }
        
        // دالة عرض الفقرات المخلوطة
        function displayShuffledParagraphs() {
            shuffledParagraphsDiv.innerHTML = '';
            shuffledParagraphs.forEach((para, index) => {
                const paraElement = createParagraphElement(para, index, true);
                shuffledParagraphsDiv.appendChild(paraElement);
            });
            makeParagraphsSortable();
        }
        
        // دالة إنشاء عنصر فقرة
        function createParagraphElement(para, index, isShuffled) {
            const div = document.createElement('div');
            div.className = 'paragraph-item';
            if (selectedParagraphs.has(index)) {
                div.classList.add('selected');
            }
            div.dataset.id = para.id;
            div.dataset.index = index;
            div.draggable = isShuffled;
            
            let displayText = para.text || para.question || '';
            if (displayText.length > 120) {
                displayText = displayText.substring(0, 120) + '...';
            }
            
            const isSelected = selectedParagraphs.has(index);
            
            div.innerHTML = `
                <input type="checkbox" class="paragraph-select" ${isSelected ? 'checked' : ''} 
                       onclick="toggleSelection(${index}, this.checked)">
                <span class="paragraph-number">${index + 1}</span>
                <strong>${para.type === 'question' ? '[سؤال] ' : '[فقرة] '}</strong>
                ${displayText}
            `;
            
            if (para.type === 'question' && para.options && para.options.length > 0) {
                div.innerHTML += ` <span style="color:#2ecc71; font-size:0.9em;">(${para.options.length} خيارات)</span>`;
            }
            
            div.addEventListener('click', (e) => {
                if (!e.target.classList.contains('paragraph-select')) {
                    const checkbox = div.querySelector('.paragraph-select');
                    checkbox.checked = !checkbox.checked;
                    toggleSelection(index, checkbox.checked);
                }
            });
            
            return div;
        }
        
        // دالة تبديل تحديد الفقرة
        function toggleSelection(index, isSelected) {
            if (isSelected) {
                selectedParagraphs.add(index);
            } else {
                selectedParagraphs.delete(index);
            }
            
            const item = document.querySelector(`.paragraph-item[data-index="${index}"]`);
            if (item) {
                if (isSelected) {
                    item.classList.add('selected');
                } else {
                    item.classList.remove('selected');
                }
            }
            
            updateSelectionCount();
        }
        
        // دالة تحديث عداد الفقرات المختارة
        function updateSelectionCount() {
            const count = selectedParagraphs.size;
            selectedCount.textContent = count;
            selectionSummary.textContent = `${count} فقرة مختارة`;
        }
        
        // دالة تحديد كل الفقرات
        function selectAll() {
            extractedParagraphs.forEach((_, index) => {
                selectedParagraphs.add(index);
            });
            updateSelectionDisplay();
            updateSelectionCount();
        }
        
        // دالة إلغاء تحديد كل الفقرات
        function deselectAll() {
            selectedParagraphs.clear();
            updateSelectionDisplay();
            updateSelectionCount();
        }
        
        // دالة تحديد الأسئلة فقط
        function selectQuestionsOnly() {
            selectedParagraphs.clear();
            extractedParagraphs.forEach((para, index) => {
                if (para.type === 'question') {
                    selectedParagraphs.add(index);
                }
            });
            updateSelectionDisplay();
            updateSelectionCount();
        }
        
        // دالة تحديد الفقرات فقط
        function selectParagraphsOnly() {
            selectedParagraphs.clear();
            extractedParagraphs.forEach((para, index) => {
                if (para.type === 'paragraph') {
                    selectedParagraphs.add(index);
                }
            });
            updateSelectionDisplay();
            updateSelectionCount();
        }
        
        // دالة تحديد عشوائي
        function selectRandom(count) {
            const indices = Array.from({length: extractedParagraphs.length}, (_, i) => i);
            
            for (let i = indices.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [indices[i], indices[j]] = [indices[j], indices[i]];
            }
            
            selectedParagraphs.clear();
            for (let i = 0; i < Math.min(count, indices.length); i++) {
                selectedParagraphs.add(indices[i]);
            }
            
            updateSelectionDisplay();
            updateSelectionCount();
        }
        
        // دالة تحديث عرض التحديد
        function updateSelectionDisplay() {
            extractedParagraphs.forEach((_, index) => {
                const item = document.querySelector(`.paragraph-item[data-index="${index}"]`);
                if (item) {
                    const checkbox = item.querySelector('.paragraph-select');
                    if (checkbox) {
                        checkbox.checked = selectedParagraphs.has(index);
                        if (selectedParagraphs.has(index)) {
                            item.classList.add('selected');
                        } else {
                            item.classList.remove('selected');
                        }
                    }
                }
            });
        }
        
        // دالة خلط داخل السؤال الواحد
        function shuffleWithinQuestion(question) {
            const shuffleMethod = document.getElementById('shuffleMethod').value;
            const seed = document.getElementById('seedValue').value || Date.now();
            const random = createSeededRandom(seed);
            
            if (shuffleMethod === 'options' || shuffleMethod === 'both') {
                if (question.options && question.options.length > 1) {
                    for (let i = question.options.length - 1; i > 0; i--) {
                        const j = Math.floor(random() * (i + 1));
                        [question.options[i], question.options[j]] = [question.options[j], question.options[i]];
                    }
                }
            }
            
            if (shuffleMethod === 'subparagraphs' || shuffleMethod === 'both') {
                if (question.subparagraphs && question.subparagraphs.length > 1) {
                    for (let i = question.subparagraphs.length - 1; i > 0; i--) {
                        const j = Math.floor(random() * (i + 1));
                        [question.subparagraphs[i], question.subparagraphs[j]] = [question.subparagraphs[j], question.subparagraphs[i]];
                    }
                }
            }
            
            return question;
        }
        
        // دالة إنشاء مولد أرقام عشوائية باستخدام بذرة
        function createSeededRandom(seed) {
            return function() {
                seed = (seed * 9301 + 49297) % 233280;
                return seed / 233280;
            };
        }
        
        // دالة خلط الفقرات
        function shuffleParagraphs() {
            const shuffleScope = document.getElementById('shuffleScope').value;
            const shuffleMode = document.getElementById('shuffleMode').value;
            const seedValue = document.getElementById('seedValue').value;
            const preserveNumbering = document.getElementById('preserveNumbering').value;
            
            shuffledParagraphs = JSON.parse(JSON.stringify(extractedParagraphs));
            
            if (shuffleMode === 'manual') {
                return;
            }
            
            const seed = seedValue ? hashString(seedValue) : Date.now();
            const random = createSeededRandom(seed);
            
            if (shuffleScope === 'within-question') {
                shuffledParagraphs.forEach(para => {
                    if (para.type === 'question') {
                        shuffleWithinQuestion(para);
                    }
                });
            } else if (shuffleScope === 'selected') {
                const selectedIndices = Array.from(selectedParagraphs);
                if (selectedIndices.length > 1) {
                    for (let i = selectedIndices.length - 1; i > 0; i--) {
                        const j = Math.floor(random() * (i + 1));
                        [selectedIndices[i], selectedIndices[j]] = [selectedIndices[j], selectedIndices[i]];
                    }
                    
                    const newOrder = [];
                    let selectedIndex = 0;
                    
                    for (let i = 0; i < shuffledParagraphs.length; i++) {
                        if (selectedParagraphs.has(i)) {
                            const originalIndex = selectedIndices[selectedIndex];
                            newOrder.push(JSON.parse(JSON.stringify(shuffledParagraphs[originalIndex])));
                            selectedIndex++;
                        } else {
                            newOrder.push(shuffledParagraphs[i]);
                        }
                    }
                    
                    shuffledParagraphs = newOrder;
                }
            } else if (shuffleScope === 'questions') {
                const questionIndices = [];
                shuffledParagraphs.forEach((para, index) => {
                    if (para.type === 'question') {
                        questionIndices.push(index);
                    }
                });
                
                if (questionIndices.length > 1) {
                    for (let i = questionIndices.length - 1; i > 0; i--) {
                        const j = Math.floor(random() * (i + 1));
                        [questionIndices[i], questionIndices[j]] = [questionIndices[j], questionIndices[i]];
                    }
                    
                    const shuffledQuestions = [];
                    questionIndices.forEach(index => {
                        shuffledQuestions.push(JSON.parse(JSON.stringify(shuffledParagraphs[index])));
                    });
                    
                    let questionCounter = 0;
                    shuffledParagraphs.forEach((para, index) => {
                        if (para.type === 'question') {
                            shuffledParagraphs[index] = shuffledQuestions[questionCounter];
                            questionCounter++;
                        }
                    });
                }
            } else {
                for (let i = shuffledParagraphs.length - 1; i > 0; i--) {
                    const j = Math.floor(random() * (i + 1));
                    [shuffledParagraphs[i], shuffledParagraphs[j]] = [shuffledParagraphs[j], shuffledParagraphs[i]];
                }
            }
            
            if (preserveNumbering === 'yes') {
                shuffledParagraphs.forEach((para, index) => {
                    if (para.type === 'paragraph') {
                        para.text = para.text.replace(/^\d+[\.\)]\s/, `${index + 1}. `);
                    } else if (para.type === 'question') {
                        para.question = para.question.replace(/^\d+[\.\)]\s/, `${index + 1}. `);
                    }
                });
            }
        }
        
        // دالة جعل الفقرات قابلة للسحب والفرز
        function makeParagraphsSortable() {
            const items = shuffledParagraphsDiv.querySelectorAll('.paragraph-item');
            let draggedItem = null;
            
            items.forEach(item => {
                item.addEventListener('dragstart', function(e) {
                    draggedItem = this;
                    setTimeout(() => this.classList.add('dragging'), 0);
                });
                
                item.addEventListener('dragend', function(e) {
                    setTimeout(() => this.classList.remove('dragging'), 0);
                    draggedItem = null;
                });
                
                item.addEventListener('dragover', function(e) {
                    e.preventDefault();
                });
                
                item.addEventListener('dragenter', function(e) {
                    e.preventDefault();
                    if (this !== draggedItem) {
                        this.classList.add('dragover');
                    }
                });
                
                item.addEventListener('dragleave', function() {
                    this.classList.remove('dragover');
                });
                
                item.addEventListener('drop', function(e) {
                    e.preventDefault();
                    this.classList.remove('dragover');
                    
                    if (this !== draggedItem) {
                        const shuffledItems = Array.from(shuffledParagraphsDiv.children);
                        const draggedIndex = shuffledItems.indexOf(draggedItem);
                        const targetIndex = shuffledItems.indexOf(this);
                        
                        const [movedItem] = shuffledParagraphs.splice(draggedIndex, 1);
                        shuffledParagraphs.splice(targetIndex, 0, movedItem);
                        
                        displayShuffledParagraphs();
                    }
                });
            });
        }
        
        // دالة خلط وإنشاء الملف
        async function shuffleAndDownload() {
            if (extractedParagraphs.length === 0) {
                showStatus('يرجى استخراج الفقرات أولاً', 'error');
                return;
            }

            try {
                showLoading(true);
                showStatus('جاري خلط الفقرات وإنشاء الملف...', 'info');
                
                shuffleParagraphs();
                
                const outputFormat = document.getElementById('outputFormat').value;
                
                switch(outputFormat) {
                    case 'pdf':
                        await createPdfFile();
                        break;
                    case 'text':
                        createTextFile();
                        break;
                    case 'html':
                        createHtmlFile();
                        break;
                    default:
                        createTextFile();
                }
                
                showStatus('تم إنشاء الملف المخلوط بنجاح!', 'success');
                
                displayShuffledParagraphs();
                
            } catch (error) {
                console.error('Error creating shuffled file:', error);
                showStatus('حدث خطأ أثناء إنشاء الملف المخلوط: ' + error.message, 'error');
            } finally {
                showLoading(false);
            }
        }
        
        // دالة إنشاء ملف PDF باستخدام jsPDF
        async function createPdfFile() {
            try {
                const { jsPDF } = window.jspdf;
                const doc = new jsPDF({
                    orientation: 'portrait',
                    unit: 'mm',
                    format: 'a4'
                });
                
                const pageWidth = doc.internal.pageSize.getWidth();
                const pageHeight = doc.internal.pageSize.getHeight();
                let y = 20;
                const lineHeight = 7;
                const margin = 20;
                
                doc.setFontSize(16);
                doc.text("الملف المخلوط", pageWidth / 2, 15, { align: 'center' });
                doc.setFontSize(12);
                
                for (let i = 0; i < shuffledParagraphs.length; i++) {
                    const para = shuffledParagraphs[i];
                    
                    if (para.type === 'question') {
                        let questionText = `${i + 1}. ${para.question || ''}`;
                        const textLines = doc.splitTextToSize(questionText, pageWidth - 2 * margin);
                        
                        if (y + (textLines.length * lineHeight) > pageHeight - margin) {
                            doc.addPage();
                            y = margin;
                        }
                        
                        doc.text(textLines, margin, y);
                        y += textLines.length * lineHeight + 5;
                        
                        if (para.subparagraphs && para.subparagraphs.length > 0) {
                            for (let j = 0; j < para.subparagraphs.length; j++) {
                                const subText = `   ${String.fromCharCode(97 + j)}) ${para.subparagraphs[j].text}`;
                                const subLines = doc.splitTextToSize(subText, pageWidth - 2 * margin - 10);
                                
                                if (y + (subLines.length * lineHeight) > pageHeight - margin) {
                                    doc.addPage();
                                    y = margin;
                                }
                                
                                doc.text(subLines, margin + 5, y);
                                y += subLines.length * lineHeight + 2;
                            }
                            y += 5;
                        }
                        
                        if (para.options && para.options.length > 0) {
                            const optionLetters = ['أ', 'ب', 'ج', 'د', 'ه', 'و', 'ز'];
                            for (let j = 0; j < para.options.length; j++) {
                                if (j < optionLetters.length) {
                                    const optionText = `   ${optionLetters[j]}) ${para.options[j].text}`;
                                    const optionLines = doc.splitTextToSize(optionText, pageWidth - 2 * margin - 10);
                                    
                                    if (y + (optionLines.length * lineHeight) > pageHeight - margin) {
                                        doc.addPage();
                                        y = margin;
                                    }
                                    
                                    doc.text(optionLines, margin + 5, y);
                                    y += optionLines.length * lineHeight + 2;
                                }
                            }
                            y += 5;
                        }
                    } else {
                        let paragraphText = `${i + 1}. ${para.text || ''}`;
                        const textLines = doc.splitTextToSize(paragraphText, pageWidth - 2 * margin);
                        
                        if (y + (textLines.length * lineHeight) > pageHeight - margin) {
                            doc.addPage();
                            y = margin;
                        }
                        
                        doc.text(textLines, margin, y);
                        y += textLines.length * lineHeight + 10;
                    }
                }
                
                const timestamp = new Date().toISOString().slice(0, 19).replace(/:/g, '-');
                const fileName = `pdf_مخلوط_${timestamp}.pdf`;
                doc.save(fileName);
                
            } catch (error) {
                console.error('Error creating PDF:', error);
                showStatus('فشل إنشاء ملف PDF، جاري إنشاء ملف نصي بدلاً منه...', 'info');
                createTextFile();
            }
        }
        
        // دالة إنشاء ملف نصي
        function createTextFile() {
            try {
                let combinedText = "الملف المخلوط\n";
                combinedText += "=".repeat(50) + "\n\n";
                
                shuffledParagraphs.forEach((para, index) => {
                    if (para.type === 'question') {
                        combinedText += `${index + 1}. ${para.question || ''}\n\n`;
                        
                        if (para.subparagraphs && para.subparagraphs.length > 0) {
                            para.subparagraphs.forEach((sub, subIndex) => {
                                combinedText += `   ${String.fromCharCode(97 + subIndex)}) ${sub.text}\n`;
                            });
                            combinedText += '\n';
                        }
                        
                        if (para.options && para.options.length > 0) {
                            const optionLetters = ['أ', 'ب', 'ج', 'د', 'ه', 'و', 'ز'];
                            para.options.forEach((option, optIndex) => {
                                if (optIndex < optionLetters.length) {
                                    combinedText += `   ${optionLetters[optIndex]}) ${option.text}\n`;
                                }
                            });
                            combinedText += '\n';
                        }
                    } else {
                        combinedText += `${index + 1}. ${para.text || ''}\n\n`;
                    }
                });
                
                const blob = new Blob([combinedText], { type: 'text/plain;charset=utf-8' });
                const link = document.createElement('a');
                link.href = URL.createObjectURL(blob);
                
                const timestamp = new Date().toISOString().slice(0, 19).replace(/:/g, '-');
                link.download = `نص_مخلوط_${timestamp}.txt`;
                link.click();
                
            } catch (error) {
                console.error('Error creating text file:', error);
                throw new Error('فشل في إنشاء الملف النصي');
            }
        }
        
        // دالة إنشاء ملف HTML
        function createHtmlFile() {
            try {
                let htmlContent = `
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>الملف المخلوط</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            line-height: 1.8;
            margin: 40px;
            background-color: #f5f5f5;
            color: #333;
            direction: rtl;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0,0,0,0.1);
        }
        h1 {
            text-align: center;
            color: #2c3e50;
            border-bottom: 2px solid #3498db;
            padding-bottom: 10px;
        }
        .paragraph {
            margin-bottom: 20px;
            padding: 15px;
            background-color: #f9f9f9;
            border-right: 4px solid #3498db;
            border-radius: 5px;
        }
        .question {
            background-color: #e8f4fc;
            border-right-color: #2980b9;
        }
        .option {
            margin-right: 20px;
            padding: 5px 10px;
            background-color: white;
            border-radius: 3px;
            margin-bottom: 5px;
        }
        .subparagraph {
            margin-right: 30px;
            padding: 8px 12px;
            background-color: #f0f7ff;
            border-radius: 3px;
            margin-bottom: 5px;
            border-right: 2px solid #2ecc71;
        }
        .number {
            display: inline-block;
            background-color: #3498db;
            color: white;
            width: 30px;
            height: 30px;
            text-align: center;
            line-height: 30px;
            border-radius: 50%;
            margin-left: 10px;
        }
        .question-type {
            color: #e74c3c;
            font-weight: bold;
            margin-right: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>الملف المخلوط</h1>
        <p style="text-align: center; color: #7f8c8d;">تم خلط الفقرات باستخدام أداة خلط PDF المتقدمة</p>
`;
                
                shuffledParagraphs.forEach((para, index) => {
                    const className = para.type === 'question' ? 'paragraph question' : 'paragraph';
                    
                    htmlContent += `<div class="${className}">`;
                    htmlContent += `<span class="number">${index + 1}</span>`;
                    htmlContent += `<span class="question-type">${para.type === 'question' ? '[سؤال]' : '[فقرة]'}</span>`;
                    
                    if (para.type === 'question') {
                        htmlContent += `<h3>${para.question || ''}</h3>`;
                        
                        if (para.subparagraphs && para.subparagraphs.length > 0) {
                            htmlContent += '<div class="subparagraphs" style="margin: 15px 0;">';
                            htmlContent += '<strong>فقرات داخلية:</strong>';
                            para.subparagraphs.forEach((sub, subIndex) => {
                                htmlContent += `<div class="subparagraph">${String.fromCharCode(97 + subIndex)}) ${sub.text}</div>`;
                            });
                            htmlContent += '</div>';
                        }
                        
                        if (para.options && para.options.length > 0) {
                            htmlContent += '<div class="options">';
                            htmlContent += '<strong>الخيارات:</strong>';
                            const optionLetters = ['أ', 'ب', 'ج', 'د', 'ه', 'و', 'ز'];
                            para.options.forEach((option, optIndex) => {
                                if (optIndex < optionLetters.length) {
                                    htmlContent += `<div class="option"><strong>${optionLetters[optIndex]})</strong> ${option.text}</div>`;
                                }
                            });
                            htmlContent += '</div>';
                        }
                    } else {
                        htmlContent += `<p>${para.text || ''}</p>`;
                    }
                    
                    htmlContent += '</div>';
                });
                
                htmlContent += `
    </div>
</body>
</html>`;
                
                const blob = new Blob([htmlContent], { type: 'text/html;charset=utf-8' });
                const link = document.createElement('a');
                link.href = URL.createObjectURL(blob);
                
                const timestamp = new Date().toISOString().slice(0, 19).replace(/:/g, '-');
                link.download = `ملف_مخلوط_${timestamp}.html`;
                link.click();
                
            } catch (error) {
                console.error('Error creating HTML file:', error);
                throw new Error('فشل في إنشاء ملف HTML');
            }
        }
        
        // دالة إنشاء هاش من نص
        function hashString(str) {
            let hash = 0;
            if (str.length === 0) return hash;
            for (let i = 0; i < str.length; i++) {
                const char = str.charCodeAt(i);
                hash = ((hash << 5) - hash) + char;
                hash = hash & hash;
            }
            return Math.abs(hash);
        }
        
        // دالة إعادة تعيين كل شيء
        function resetAll() {
            pdfDoc = null;
            extractedParagraphs = [];
            shuffledParagraphs = [];
            selectedParagraphs.clear();
            pdfInput.value = '';
            fileInfo.classList.remove('show');
            previewSection.style.display = 'none';
            processBtn.disabled = true;
            shuffleBtn.disabled = true;
            document.getElementById('seedValue').value = '';
            showStatus('', '');
        }
        
        // دالة عرض حالة التحميل
        function showLoading(show) {
            if (show) {
                loading.classList.add('show');
                processBtn.disabled = true;
                shuffleBtn.disabled = true;
                resetBtn.disabled = true;
            } else {
                loading.classList.remove('show');
                processBtn.disabled = false;
                shuffleBtn.disabled = (extractedParagraphs.length === 0);
                resetBtn.disabled = false;
            }
        }
        
        // دالة عرض الرسائل
        function showStatus(message, type) {
            if (!message) {
                status.style.display = 'none';
                status.className = 'status';
                return;
            }
            
            status.textContent = message;
            status.className = `status ${type}`;
        }
    </script>
</body>
</html>
