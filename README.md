# Mixquestion1
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
            max-width: 1200px;
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
            max-height: 400px;
            overflow-y: auto;
        }
        
        .preview-box h4 {
            margin-top: 0;
            color: #2c3e50;
            padding-bottom: 10px;
            border-bottom: 1px solid #e1e8f0;
        }
        
        .paragraph-item {
            padding: 8px 12px;
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
        
        .paragraph-item.dragging {
            opacity: 0.5;
        }
        
        .paragraph-number {
            display: inline-block;
            background-color: #3498db;
            color: white;
            width: 24px;
            height: 24px;
            border-radius: 50%;
            text-align: center;
            line-height: 24px;
            margin-left: 8px;
            font-size: 12px;
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
    <!-- مكتبة pdf-lib لمعالجة PDF -->
    <script src="https://cdn.jsdelivr.net/npm/pdf-lib@1.17.1/dist/pdf-lib.min.js"></script>
    <!-- مكتبة pdf.js لاستخراج النص من PDF -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.4.120/pdf.min.js"></script>
    <!-- مكتبة jsPDF لإنشاء PDF مع دعم النص العربي -->
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
        </div>
        
        <div class="options-section">
            <h3>خيارات الخلط</h3>
            
            <div class="option-group">
                <label for="shuffleMethod">طريقة الخلط:</label>
                <select id="shuffleMethod">
                    <option value="paragraphs">خلط الفقرات داخل كل صفحة</option>
                    <option value="questions">خلط الأسئلة مع خياراتها</option>
                    <option value="pages">خلط الصفحات كاملة</option>
                    <option value="mixed">خلط شامل (فقرات وصفحات)</option>
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
                    <input type="checkbox" id="preserveFormatting" checked>
                    <label for="preserveFormatting">الحفاظ على التنسيق الأصلي (الخطوط، الألوان، etc.)</label>
                </div>
                <div class="checkbox-group">
                    <input type="checkbox" id="shuffleOptions" checked>
                    <label for="shuffleOptions">خلط خيارات الأسئلة متعددة الخيارات</label>
                </div>
                <div class="checkbox-group">
                    <input type="checkbox" id="identifyPatterns" checked>
                    <label for="identifyPatterns">تحديد أنماط الأسئلة تلقائياً (أسئلة، خيارات، etc.)</label>
                </div>
            </div>
        </div>
        
        <div class="preview-section" id="previewSection" style="display: none;">
            <h3>معاينة الفقرات وإعادة الترتيب اليدوي</h3>
            <div class="preview-container">
                <div class="preview-box">
                    <h4>الفقرات الأصلية</h4>
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
        let pdfTextContent = null;
        let extractedParagraphs = [];
        let shuffledParagraphs = [];
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
        const loading = document.getElementById('loading');
        const status = document.getElementById('status');
        const processBtn = document.getElementById('processBtn');
        const shuffleBtn = document.getElementById('shuffleBtn');
        const resetBtn = document.getElementById('resetBtn');
        const previewSection = document.getElementById('previewSection');
        const originalParagraphs = document.getElementById('originalParagraphs');
        const shuffledParagraphsDiv = document.getElementById('shuffledParagraphs');
        
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
                
                // تحميل PDF باستخدام pdf.js
                const pdf = await pdfjsLib.getDocument({ data: arrayBuffer }).promise;
                let fullText = '';
                
                // استخراج النص من كل صفحة
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
                // تحسين النص للغة العربية
                const normalizedText = text
                    .replace(/\n\s*\n/g, '\n\n') // توحيد الأسطر الفارغة
                    .replace(/([\.\?\!])\s+/g, '$1\n') // فصل الجمل
                    .replace(/(\d+\.)\s+/g, '$1\n'); // فصل الفقرات المرقمة
                
                // تقسيم النص إلى فقرات
                let paragraphs = normalizedText.split(/\n\s*\n/);
                
                // تصفية الفقرات الفارغة أو القصيرة جداً
                paragraphs = paragraphs
                    .map(p => p.trim())
                    .filter(p => p.length > 5); // تخفيض الحد الأدنى لطول الفقرة
                
                if (paragraphs.length === 0) {
                    // إذا لم نتمكن من تقسيم الفقرات، نعيد النص كله كفقرة واحدة
                    paragraphs = [text];
                }
                
                // تحديد إذا كان النص يحتوي على أسئلة متعددة الخيارات
                const isQuestionnaire = paragraphs.some(p => 
                    p.includes('؟') || p.includes('أ)') || p.includes('ب)') || p.includes('ج)') || p.includes('د)') ||
                    p.includes('(أ)') || p.includes('(ب)') || p.includes('(ج)') || p.includes('(د)')
                );
                
                // إذا كان النص يحتوي على أسئلة، معالجتها بشكل خاص
                if (isQuestionnaire && document.getElementById('identifyPatterns').checked) {
                    return processQuestions(paragraphs);
                }
                
                return paragraphs.map((text, index) => ({
                    id: index,
                    text: text,
                    originalIndex: index,
                    type: 'paragraph'
                }));
            } catch (error) {
                console.error('Error detecting paragraphs:', error);
                // في حالة الخطأ، نعيد النص كله كفقرة واحدة
                return [{
                    id: 0,
                    text: text.substring(0, 1000) + (text.length > 1000 ? '...' : ''),
                    originalIndex: 0,
                    type: 'paragraph'
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
                    
                    // اكتشاف بداية سؤال جديد
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
                            type: 'question'
                        };
                    } 
                    // اكتشاف خيارات
                    else if (text.match(/^[أ-د]\)/) || text.match(/^[a-d]\./) || 
                             text.match(/^\([أ-د]\)/) || text.match(/^[A-D]\)/) ||
                             (currentQuestion && text.length < 200 && 
                              (text.includes(')') || text.includes('.') || text.length < 150))) {
                        if (currentQuestion) {
                            currentQuestion.options.push(text);
                        } else {
                            // إذا كان هناك خيارات بدون سؤال، نبدأ بسؤال جديد
                            currentQuestion = {
                                id: questionGroups.length,
                                question: 'سؤال ' + (questionGroups.length + 1),
                                options: [text],
                                originalIndex: i,
                                type: 'question'
                            };
                        }
                    }
                    // فقرات عادية أو استمرار للسؤال
                    else if (currentQuestion) {
                        currentQuestion.question += ' ' + text;
                    } else {
                        // فقرات عادية بدون سؤال
                        questionGroups.push({
                            id: questionGroups.length,
                            text: text,
                            originalIndex: i,
                            type: 'paragraph'
                        });
                    }
                }
                
                // إضافة السؤال الأخير
                if (currentQuestion) {
                    questionGroups.push(currentQuestion);
                }
                
                return questionGroups;
            } catch (error) {
                console.error('Error processing questions:', error);
                // في حالة الخطأ، نعيد الفقرات كفقرات عادية
                return paragraphs.map((text, index) => ({
                    id: index,
                    text: text,
                    originalIndex: index,
                    type: 'paragraph'
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
                
                // استخراج النص باستخدام pdf.js
                const text = await extractTextFromPDF(file);
                
                // اكتشاف الفقرات
                extractedParagraphs = detectParagraphs(text);
                
                // نسخ الفقرات للخلط
                shuffledParagraphs = JSON.parse(JSON.stringify(extractedParagraphs));
                
                // تحديث العداد
                paragraphCount.textContent = extractedParagraphs.length;
                
                // عرض معاينة الفقرات
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
            // عرض الفقرات الأصلية
            originalParagraphs.innerHTML = '';
            extractedParagraphs.forEach((para, index) => {
                const paraElement = createParagraphElement(para, index, false);
                originalParagraphs.appendChild(paraElement);
            });
            
            // عرض الفقرات بعد الخلط
            displayShuffledParagraphs();
        }
        
        // دالة عرض الفقرات المخلوطة
        function displayShuffledParagraphs() {
            shuffledParagraphsDiv.innerHTML = '';
            shuffledParagraphs.forEach((para, index) => {
                const paraElement = createParagraphElement(para, index, true);
                shuffledParagraphsDiv.appendChild(paraElement);
            });
            
            // إضافة إمكانية السحب والإفلات
            makeParagraphsSortable();
        }
        
        // دالة إنشاء عنصر فقرة
        function createParagraphElement(para, index, isShuffled) {
            const div = document.createElement('div');
            div.className = 'paragraph-item';
            div.dataset.id = para.id;
            div.draggable = isShuffled;
            
            let displayText = para.text || para.question || '';
            if (displayText.length > 150) {
                displayText = displayText.substring(0, 150) + '...';
            }
            
            if (para.type === 'question' && para.options && para.options.length > 0) {
                displayText += ` [${para.options.length} خيارات]`;
            }
            
            div.innerHTML = `
                <span class="paragraph-number">${index + 1}</span>
                ${displayText}
            `;
            
            return div;
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
                        
                        // تحديث المصفوفة
                        const [movedItem] = shuffledParagraphs.splice(draggedIndex, 1);
                        shuffledParagraphs.splice(targetIndex, 0, movedItem);
                        
                        // إعادة العرض
                        displayShuffledParagraphs();
                    }
                });
            });
        }
        
        // دالة خلط الفقرات
        function shuffleParagraphs() {
            const shuffleMode = document.getElementById('shuffleMode').value;
            const seedValue = document.getElementById('seedValue').value;
            const shuffleOptions = document.getElementById('shuffleOptions').checked;
            
            // نسخ الفقرات الأصلية
            shuffledParagraphs = JSON.parse(JSON.stringify(extractedParagraphs));
            
            if (shuffleMode === 'manual') {
                // الوضع اليدوي - لا خلط تلقائي
                return;
            }
            
            // إنشاء بذرة للخلط العشوائي
            let randomSeed = seedValue ? hashString(seedValue) : Math.random();
            const random = seededRandom(randomSeed);
            
            // خلط الفقرات
            for (let i = shuffledParagraphs.length - 1; i > 0; i--) {
                const j = Math.floor(random() * (i + 1));
                [shuffledParagraphs[i], shuffledParagraphs[j]] = [shuffledParagraphs[j], shuffledParagraphs[i]];
            }
            
            // إذا كان هناك أسئلة مع خيارات، خلط الخيارات أيضاً
            if (shuffleOptions) {
                shuffledParagraphs.forEach(para => {
                    if (para.type === 'question' && para.options && para.options.length > 1) {
                        // خلط الخيارات داخل السؤال
                        for (let i = para.options.length - 1; i > 0; i--) {
                            const j = Math.floor(random() * (i + 1));
                            [para.options[i], para.options[j]] = [para.options[j], para.options[i]];
                        }
                    }
                });
            }
            
            // إعادة ترقيم الفقرات إذا طلب المستخدم ذلك
            const preserveNumbering = document.getElementById('preserveNumbering').value;
            if (preserveNumbering === 'yes') {
                shuffledParagraphs.forEach((para, index) => {
                    if (para.type === 'paragraph') {
                        // إعادة ترقيم الفقرات المرقمة
                        para.text = para.text.replace(/^\d+[\.\)]\s/, `${index + 1}. `);
                    } else if (para.type === 'question') {
                        // إعادة ترقيم الأسئلة
                        para.question = para.question.replace(/^\d+[\.\)]\s/, `${index + 1}. `);
                    }
                });
            }
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
                
                // خلط الفقرات
                shuffleParagraphs();
                
                // الحصول على صيغة الملف المطلوبة
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
                
                // تحديث عرض الفقرات المخلوطة
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
                
                // إعدادات الصفحة
                const pageWidth = doc.internal.pageSize.getWidth();
                const pageHeight = doc.internal.pageSize.getHeight();
                let y = 20;
                const lineHeight = 7;
                const margin = 20;
                
                // إضافة عنوان
                doc.setFontSize(16);
                doc.text("الملف المخلوط", pageWidth / 2, 15, { align: 'center' });
                doc.setFontSize(12);
                
                // معالجة كل فقرة
                for (let i = 0; i < shuffledParagraphs.length; i++) {
                    const para = shuffledParagraphs[i];
                    let textLines = [];
                    
                    if (para.type === 'question') {
                        // معالجة السؤال
                        let questionText = `${i + 1}. ${para.question || ''}`;
                        textLines = doc.splitTextToSize(questionText, pageWidth - 2 * margin);
                        
                        // التحقق من المساحة في الصفحة
                        if (y + (textLines.length * lineHeight) > pageHeight - margin) {
                            doc.addPage();
                            y = margin;
                        }
                        
                        doc.text(textLines, margin, y);
                        y += textLines.length * lineHeight + 5;
                        
                        // معالجة الخيارات
                        if (para.options && para.options.length > 0) {
                            const optionLetters = ['أ', 'ب', 'ج', 'د', 'ه', 'و', 'ز'];
                            for (let j = 0; j < para.options.length; j++) {
                                if (j < optionLetters.length) {
                                    const optionText = `   ${optionLetters[j]}) ${para.options[j]}`;
                                    const optionLines = doc.splitTextToSize(optionText, pageWidth - 2 * margin - 10);
                                    
                                    // التحقق من المساحة
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
                        // معالجة الفقرة العادية
                        let paragraphText = `${i + 1}. ${para.text || ''}`;
                        textLines = doc.splitTextToSize(paragraphText, pageWidth - 2 * margin);
                        
                        // التحقق من المساحة
                        if (y + (textLines.length * lineHeight) > pageHeight - margin) {
                            doc.addPage();
                            y = margin;
                        }
                        
                        doc.text(textLines, margin, y);
                        y += textLines.length * lineHeight + 10;
                    }
                }
                
                // حفظ الملف
                const timestamp = new Date().toISOString().slice(0, 19).replace(/:/g, '-');
                const fileName = `pdf_مخلوط_${timestamp}.pdf`;
                doc.save(fileName);
                
            } catch (error) {
                console.error('Error creating PDF:', error);
                // في حالة فشل إنشاء PDF، ننشئ ملف نصي بدلاً منه
                showStatus('فشل إنشاء ملف PDF، جاري إنشاء ملف نصي بدلاً منه...', 'info');
                createTextFile();
            }
        }
        
        // دالة إنشاء ملف نصي
        function createTextFile() {
            try {
                // دمج الفقرات المخلوطة في نص واحد
                let combinedText = "الملف المخلوط\n";
                combinedText += "=".repeat(50) + "\n\n";
                
                shuffledParagraphs.forEach((para, index) => {
                    if (para.type === 'question') {
                        combinedText += `${index + 1}. ${para.question || ''}\n\n`;
                        if (para.options && para.options.length > 0) {
                            const optionLetters = ['أ', 'ب', 'ج', 'د', 'ه', 'و', 'ز'];
                            para.options.forEach((option, optIndex) => {
                                if (optIndex < optionLetters.length) {
                                    combinedText += `   ${optionLetters[optIndex]}) ${option}\n`;
                                }
                            });
                            combinedText += '\n';
                        }
                    } else {
                        combinedText += `${index + 1}. ${para.text || ''}\n\n`;
                    }
                });
                
                // إنشاء ملف نصي للتنزيل
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
                // إنشاء محتوى HTML
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
    </style>
</head>
<body>
    <div class="container">
        <h1>الملف المخلوط</h1>
`;
                
                shuffledParagraphs.forEach((para, index) => {
                    const className = para.type === 'question' ? 'paragraph question' : 'paragraph';
                    
                    htmlContent += `<div class="${className}">`;
                    htmlContent += `<span class="number">${index + 1}</span>`;
                    
                    if (para.type === 'question') {
                        htmlContent += `<h3>${para.question || ''}</h3>`;
                        
                        if (para.options && para.options.length > 0) {
                            htmlContent += '<div class="options">';
                            const optionLetters = ['أ', 'ب', 'ج', 'د', 'ه', 'و', 'ز'];
                            para.options.forEach((option, optIndex) => {
                                if (optIndex < optionLetters.length) {
                                    htmlContent += `<div class="option"><strong>${optionLetters[optIndex]})</strong> ${option}</div>`;
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
                
                // إنشاء ملف HTML للتنزيل
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
        
        // دالة إنشاء رقم عشوائي باستخدام بذرة
        function seededRandom(seed) {
            const x = Math.sin(seed) * 10000;
            return x - Math.floor(x);
        }
        
        // دالة إنشاء هاش من نص
        function hashString(str) {
            let hash = 0;
            for (let i = 0; i < str.length; i++) {
                const char = str.charCodeAt(i);
                hash = (hash << 5) - hash + char;
                hash = hash & hash;
            }
            return hash;
        }
        
        // دالة إعادة تعيين كل شيء
        function resetAll() {
            pdfDoc = null;
            pdfTextContent = null;
            extractedParagraphs = [];
            shuffledParagraphs = [];
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
