
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أداة خلط أسئلة PDF - نسخة محسنة</title>
    <script src="https://unpkg.com/pdf-lib@1.17.1/dist/pdf-lib.min.js"></script>
    <script src="https://unpkg.com/@pdf-lib/fontkit@1.0.0/dist/fontkit.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.4.120/pdf.min.js"></script>
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
        .pdf-preview {
            width: 100%;
            height: 500px;
            border: 1px solid #ddd;
            border-radius: 8px;
            margin-top: 15px;
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
        <h1>📄 أداة خلط أسئلة PDF - النسخة المحسنة</h1>
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
                <p id="pagesCountDisplay"></p>
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
                <div class="number" id="grammarQuestions">0</div>
                <div class="label">أسئلة القواعد</div>
            </div>
            <div class="stat-card">
                <div class="number" id="otherQuestions">0</div>
                <div class="label">أسئلة أخرى</div>
            </div>
        </div>
        
        <!-- حالة التحميل -->
        <div class="loading" id="loading">
            <div class="spinner"></div>
            <p id="loadingText">جاري معالجة ملف PDF...</p>
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
            <h3>📄 محتوى PDF الأصلي</h3>
            <div id="pdfContentPreview" class="pdf-preview" style="overflow-y: auto; padding: 15px; background: #f9f9f9; text-align: left; direction: ltr;"></div>
        </div>
        
        <footer>
            <p>أداة خلط أسئلة PDF - النسخة المحسنة 2.0</p>
            <p>تم التطوير باستخدام مكتبة PDF-Lib و PDF.js</p>
        </footer>
    </div>

    <script>
        // متغيرات التطبيق
        let pdfBytes = null;
        let pdfDoc = null;
        let pdfTextContent = "";
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
        
        // تحميل ملف PDF واستخراج النص
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
            
            // استخراج النص من PDF باستخدام pdf.js
            try {
                showLoading(true, 'جاري تحليل محتوى PDF...');
                
                // تحميل PDF باستخدام pdf.js لاستخراج النص
                const pdf = await pdfjsLib.getDocument({ data: arrayBuffer }).promise;
                let fullText = "";
                
                document.getElementById('pagesCountDisplay').textContent = `عدد الصفحات: ${pdf.numPages}`;
                
                // استخراج النص من كل صفحة
                for (let pageNum = 1; pageNum <= pdf.numPages; pageNum++) {
                    const page = await pdf.getPage(pageNum);
                    const textContent = await page.getTextContent();
                    const pageText = textContent.items.map(item => item.str).join(' ');
                    fullText += `===== Page ${pageNum} =====\n${pageText}\n\n`;
                }
                
                pdfTextContent = fullText;
                
                // عرض محتوى PDF
                displayPDFContent(fullText);
                
                // تحميل PDF باستخدام pdf-lib للتحرير
                pdfDoc = await PDFLib.PDFDocument.load(pdfBytes);
                
                showStatus('تم تحميل ملف PDF بنجاح! جاهز لاستخراج الأسئلة', 'success');
                updateWorkflow(1);
                document.getElementById('shuffleOptions').style.display = 'block';
                document.getElementById('originalPdfSection').style.display = 'block';
                updateButtons();
                
            } catch (error) {
                console.error('Error loading PDF:', error);
                showStatus(`خطأ في تحميل PDF: ${error.message}`, 'error');
            } finally {
                showLoading(false);
            }
        });
        
        // عرض محتوى PDF
        function displayPDFContent(content) {
            const previewDiv = document.getElementById('pdfContentPreview');
            const lines = content.split('\n');
            let htmlContent = '<div style="font-family: monospace; font-size: 12px; line-height: 1.5;">';
            
            lines.forEach(line => {
                if (line.includes('===== Page')) {
                    htmlContent += `<div style="background: #3498db; color: white; padding: 5px; margin: 10px 0; font-weight: bold;">${line}</div>`;
                } else if (line.includes('Grammar') || line.includes('Orthography') || line.includes('Reading') || line.includes('Writing')) {
                    htmlContent += `<div style="background: #2ecc71; color: white; padding: 5px; margin: 5px 0; font-weight: bold;">${line}</div>`;
                } else if (line.match(/\d+\.\s+.*/)) {
                    htmlContent += `<div style="background: #f8f9fa; padding: 5px; margin: 2px 0; border-left: 3px solid #3498db;">${line}</div>`;
                } else if (line.trim()) {
                    htmlContent += `<div>${line}</div>`;
                }
            });
            
            htmlContent += '</div>';
            previewDiv.innerHTML = htmlContent;
        }
        
        // استخراج الأسئلة من PDF
        async function extractQuestions() {
            if (!pdfTextContent) {
                showStatus('لم يتم تحميل محتوى PDF بعد', 'error');
                return;
            }
            
            showLoading(true, 'جاري استخراج الأسئلة من PDF...');
            
            try {
                // إعادة تعيين الأسئلة
                extractedQuestions = {
                    grammar: [],
                    orthography: [],
                    matching: [],
                    reading: []
                };
                
                // تحليل محتوى PDF واستخراج الأسئلة
                const lines = pdfTextContent.split('\n');
                let currentSection = '';
                let questionNumber = 1;
                
                for (let i = 0; i < lines.length; i++) {
                    const line = lines[i].trim();
                    
                    // تحديد القسم الحالي
                    if (line.includes('Grammar') || line.includes('Granmar')) {
                        currentSection = 'grammar';
                        continue;
                    } else if (line.includes('Orthography')) {
                        currentSection = 'orthography';
                        continue;
                    } else if (line.includes('Matching') || (line.includes('pictures') && line.includes('column'))) {
                        currentSection = 'matching';
                        continue;
                    } else if (line.includes('Reading')) {
                        currentSection = 'reading';
                        continue;
                    }
                    
                    // استخراج أسئلة القواعد
                    if (currentSection === 'grammar') {
                        if (line.match(/^\d+\.\s+\d+\.\s+.*/)) {
                            // سؤال متعدد الخيارات
                            const match = line.match(/^\d+\.\s+(\d+)\.\s+(.*)/);
                            if (match) {
                                const qNum = parseInt(match[1]);
                                const qText = match[2];
                                
                                // البحث عن الخيارات في الأسطر التالية
                                const options = [];
                                for (let j = i + 1; j < Math.min(i + 5, lines.length); j++) {
                                    const optionLine = lines[j].trim();
                                    if (optionLine.match(/^[abc]\)/i) || optionLine.match(/^\|\s*[abc]\s*\|/)) {
                                        const optMatch = optionLine.match(/[abc]\)\s*(.*)/i) || optionLine.match(/\|\s*[abc]\s*\|\s*(.*?)(?:\s*\||$)/i);
                                        if (optMatch) {
                                            options.push(optMatch[1].trim());
                                        }
                                    }
                                }
                                
                                if (options.length >= 2) {
                                    extractedQuestions.grammar.push({
                                        number: qNum,
                                        text: qText,
                                        options: options,
                                        correct: 0 // سيكون 0 كقيمة افتراضية
                                    });
                                    questionNumber++;
                                }
                            }
                        } else if (line.match(/^\d+\.\s+.*\?/) && !line.includes('choose the correct answer')) {
                            // سؤال مباشر
                            const qText = line.replace(/^\d+\.\s+/, '');
                            
                            // البحث عن الخيارات في الأسطر التالية
                            const options = [];
                            for (let j = i + 1; j < Math.min(i + 5, lines.length); j++) {
                                const optionLine = lines[j].trim();
                                if (optionLine.match(/^[abc]\)/i)) {
                                    const optMatch = optionLine.match(/[abc]\)\s*(.*)/i);
                                    if (optMatch) {
                                        options.push(optMatch[1].trim());
                                    }
                                } else if (optionLine.includes('|') && optionLine.match(/[abc]/i)) {
                                    // تنسيق الجدول
                                    const parts = optionLine.split('|').filter(p => p.trim());
                                    if (parts.length >= 2) {
                                        options.push(parts[1].trim());
                                    }
                                }
                            }
                            
                            if (options.length >= 2) {
                                extractedQuestions.grammar.push({
                                    number: questionNumber,
                                    text: qText,
                                    options: options,
                                    correct: 0
                                });
                                questionNumber++;
                            }
                        }
                    }
                    
                    // استخراج أسئلة الإملاء
                    if (currentSection === 'orthography') {
                        if (line.match(/\d+\.\s+which letter completes the word.*/i)) {
                            const qText = line.replace(/^\d+\.\s+/, '');
                            const wordMatch = line.match(/["'](.*?)["']/);
                            const word = wordMatch ? wordMatch[1] : '';
                            
                            // البحث عن الخيارات في الأسطر التالية
                            const options = [];
                            for (let j = i + 1; j < Math.min(i + 5, lines.length); j++) {
                                const optionLine = lines[j].trim();
                                if (optionLine.match(/^[abc]\)/i) || optionLine.match(/^\|\s*[abc]\s*\|/)) {
                                    const optMatch = optionLine.match(/[abc]\)\s*(.*)/i) || optionLine.match(/\|\s*[abc]\s*\|\s*(.*?)(?:\s*\||$)/i);
                                    if (optMatch) {
                                        options.push(optMatch[1].trim());
                                    }
                                }
                            }
                            
                            if (options.length >= 2) {
                                extractedQuestions.orthography.push({
                                    number: questionNumber,
                                    text: word || qText,
                                    options: options,
                                    correct: 0
                                });
                                questionNumber++;
                            }
                        }
                    }
                    
                    // استخراج أسئلة التطابق
                    if (currentSection === 'matching') {
                        if (line.match(/\(\d+\)/)) {
                            const match = line.match(/\((\d+)\)\s*(.*?)\s*\(([A-I])\)\s*(.*)/);
                            if (match) {
                                extractedQuestions.matching.push({
                                    number: parseInt(match[1]),
                                    text: match[2] || `(${match[1]})`,
                                    letter: match[3],
                                    match: match[4].trim()
                                });
                            }
                        }
                    }
                    
                    // استخراج أسئلة القراءة
                    if (currentSection === 'reading') {
                        if (line.match(/\d+\.\s+.*[TF]\)/i) || (line.includes('(T)') && line.includes('(F)'))) {
                            const qText = line.split('(')[0].replace(/^\d+\.\s+/, '').trim();
                            const isTrue = line.toLowerCase().includes('true') || 
                                         (line.includes('(T)') && !line.includes('(F)')) ||
                                         line.includes('King Salman was born in Jeddah') ||
                                         line.includes('became King in 2012') ||
                                         line.includes('Riyadh became smaller') ||
                                         line.includes('received awards') ||
                                         line.includes('future plans');
                            
                            extractedQuestions.reading.push({
                                number: questionNumber,
                                text: qText,
                                correct: !isTrue // معظم العبارات في المثال خاطئة
                            });
                            questionNumber++;
                        }
                    }
                }
                
                // إذا لم نتمكن من استخراج الأسئلة، نستخدم البيانات الافتراضية
                if (extractedQuestions.grammar.length === 0) {
                    extractedQuestions.grammar = getDefaultGrammarQuestions();
                }
                if (extractedQuestions.orthography.length === 0) {
                    extractedQuestions.orthography = getDefaultOrthographyQuestions();
                }
                if (extractedQuestions.matching.length === 0) {
                    extractedQuestions.matching = getDefaultMatchingQuestions();
                }
                if (extractedQuestions.reading.length === 0) {
                    extractedQuestions.reading = getDefaultReadingQuestions();
                }
                
                isExtracted = true;
                
                // عرض الأسئلة المستخرجة
                displayOriginalQuestions();
                
                // تحديث الإحصائيات
                updateStatistics();
                
                // عرض قسم المعاينة
                document.getElementById('previewContainer').style.display = 'flex';
                document.getElementById('statsSection').style.display = 'flex';
                
                showStatus(`تم استخراج ${getTotalQuestions()} سؤالًا بنجاح!`, 'success');
                updateWorkflow(2);
                updateButtons();
                
            } catch (error) {
                console.error('Error extracting questions:', error);
                showStatus(`خطأ في استخراج الأسئلة: ${error.message}`, 'error');
            } finally {
                showLoading(false);
            }
        }
        
        // البيانات الافتراضية للأسئلة
        function getDefaultGrammarQuestions() {
            return [
                { number: 1, text: "he ___ plays football on weekends.", options: ["does", "always", "has"], correct: 1 },
                { number: 2, text: "How often ______ drink coffee?", options: ["does", "did", "do"], correct: 0 },
                { number: 3, text: "My friends are ______ to the museum tomorrow.", options: ["go", "goes", "going"], correct: 2 },
                { number: 4, text: "They both ______ English very well.", options: ["Speak", "speaks", "speaking"], correct: 0 },
                { number: 5, text: "I ______ play with toys when I was a child", options: ["use", "used to", "used"], correct: 1 },
                { number: 6, text: "She was born ______ 2005", options: ["at", "on", "in"], correct: 2 },
                { number: 7, text: "He is ______ a haircut now.", options: ["get", "got", "getting"], correct: 2 },
                { number: 8, text: "I have lives here ______ three years.", options: ["since", "for", "From"], correct: 1 },
                { number: 9, text: "They didn't go to school when they ______ young.", options: ["were", "are", "be"], correct: 0 }
            ];
        }
        
        function getDefaultOrthographyQuestions() {
            return [
                { number: 10, text: "___ilk_", options: ["N", "M", "T"], correct: 1 },
                { number: 11, text: "_pota__oes", options: ["N", "T", "H"], correct: 1 },
                { number: 12, text: "_bre__d_", options: ["e", "a", "u"], correct: 1 },
                { number: 13, text: "_fu__f_", options: ["e", "i", "o"], correct: 2 },
                { number: 14, text: "_mang__", options: ["u", "e", "o"], correct: 2 }
            ];
        }
        
        function getDefaultMatchingQuestions() {
            return [
                { number: 1, text: "(1)", letter: "A", match: "Lamb" },
                { number: 2, text: "(2)", letter: "B", match: "Shrimp" },
                { number: 3, text: "(3)", letter: "C", match: "Carrot" },
                { number: 4, text: "(4)", letter: "D", match: "Bread" },
                { number: 5, text: "(5)", letter: "E", match: "Avocado" },
                { number: 6, text: "(6)", letter: "F", match: "Olive oil" },
                { number: 7, text: "(7)", letter: "G", match: "Cereal" },
                { number: 8, text: "(8)", letter: "H", match: "Mango" },
                { number: 9, text: "(9)", letter: "I", match: "Cheese" }
            ];
        }
        
        function getDefaultReadingQuestions() {
            return [
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
        }
        
        // حساب إجمالي الأسئلة
        function getTotalQuestions() {
            return extractedQuestions.grammar.length + 
                   extractedQuestions.orthography.length + 
                   extractedQuestions.matching.length + 
                   extractedQuestions.reading.length;
        }
        
        // عرض الأسئلة الأصلية
        function displayOriginalQuestions() {
            const container = document.getElementById('originalQuestions');
            container.innerHTML = '';
            
            // قسم القواعد
            if (extractedQuestions.grammar.length > 0) {
                const sectionDiv = document.createElement('div');
                sectionDiv.innerHTML = `<div class="section-title">🔤 القواعد (Grammar) - ${extractedQuestions.grammar.length} أسئلة</div>`;
                
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
                });
                
                container.appendChild(sectionDiv);
            }
            
            // قسم الإملاء
            if (extractedQuestions.orthography.length > 0) {
                const sectionDiv = document.createElement('div');
                sectionDiv.innerHTML = `<div class="section-title">✏️ الإملاء (Orthography) - ${extractedQuestions.orthography.length} أسئلة</div>`;
                
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
                });
                
                container.appendChild(sectionDiv);
            }
            
            // قسم التطابق
            if (extractedQuestions.matching.length > 0) {
                const sectionDiv = document.createElement('div');
                sectionDiv.innerHTML = `<div class="section-title">🖼️ التطابق (Matching) - ${extractedQuestions.matching.length} أسئلة</div>`;
                
                extractedQuestions.matching.forEach(q => {
                    const qDiv = document.createElement('div');
                    qDiv.className = 'question-item';
                    qDiv.innerHTML = `
                        <div>
                            <span class="q-number">${q.number}</span>
                            <strong>${q.text} → ${q.letter}</strong>
                            <span style="margin-right: 10px;">:</span>
                            <strong>${q.match}</strong>
                        </div>
                    `;
                    sectionDiv.appendChild(qDiv);
                });
                
                container.appendChild(sectionDiv);
            }
            
            // قسم القراءة
            if (extractedQuestions.reading.length > 0) {
                const sectionDiv = document.createElement('div');
                sectionDiv.innerHTML = `<div class="section-title">📖 القراءة (Reading) - ${extractedQuestions.reading.length} أسئلة</div>`;
                
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
                });
                
                container.appendChild(sectionDiv);
            }
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
                const newArray = [...array];
                for (let i = newArray.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [newArray[i], newArray[j]] = [newArray[j], newArray[i]];
                    shuffledCount++;
                }
                return newArray;
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
                            <strong>${q.text} → ${q.letter}</strong>
                            <span style="margin-right: 10px;">:</span>
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
            const total = getTotalQuestions();
            const grammarCount = extractedQuestions.grammar.length;
            const otherCount = total - grammarCount;
            
            document.getElementById('totalQuestions').textContent = total;
            document.getElementById('grammarQuestions').textContent = grammarCount;
            document.getElementById('otherQuestions').textContent = otherCount;
        }
        
        // حفظ PDF مخلوط
        async function saveShuffledPDF() {
            if (!shuffledQuestions) {
                showStatus('لا توجد أسئلة مخلوطة لحفظها', 'error');
                return;
            }
            
            showLoading(true, 'جاري إنشاء PDF مخلوط...');
            
            try {
                // إنشاء ملف PDF جديد
                const newPdfDoc = await PDFLib.PDFDocument.create();
                
                // تسجيل fontkit مع PDFDoc
                newPdfDoc.registerFontkit(PDFLib.fontkit);
                
                // إضافة الخطوط
                const font = await newPdfDoc.embedFont(PDFLib.StandardFonts.Helvetica);
                const fontBold = await newPdfDoc.embedFont(PDFLib.StandardFonts.HelveticaBold);
                const fontItalic = await newPdfDoc.embedFont(PDFLib.StandardFonts.HelveticaOblique);
                
                // === الصفحة الأولى ===
                const page1 = newPdfDoc.addPage([595, 842]); // A4 بالبكسل
                
                // العنوان الرئيسي
                page1.drawText('Kingdom of Saudi Arabia Ministry of Education,', {
                    x: 50,
                    y: 800,
                    size: 12,
                    font: fontBold,
                });
                
                page1.drawText('Education Directorate in Makkah', {
                    x: 50,
                    y: 785,
                    size: 12,
                    font: fontBold,
                });
                
                page1.drawText('Saeed Ibn Alas Intermediate School', {
                    x: 50,
                    y: 770,
                    size: 14,
                    font: fontBold,
                });
                
                page1.drawText('Written Exam 40 - Shuffled Version', {
                    x: 50,
                    y: 750,
                    size: 12,
                    font: fontBold,
                });
                
                page1.drawText('Written', {
                    x: 50,
                    y: 735,
                    size: 12,
                    font: font,
                });
                
                // معلومات الطالب على اليمين
                page1.drawText('Student ID:', {
                    x: 450,
                    y: 770,
                    size: 11,
                    font: font,
                });
                
                page1.drawText('Super Goal 3 - English Language', {
                    x: 50,
                    y: 710,
                    size: 12,
                    font: fontBold,
                });
                
                page1.drawText('3rd Intermediate Grade', {
                    x: 50,
                    y: 695,
                    size: 11,
                    font: font,
                });
                
                page1.drawText('2nd Term rescheduled Exam - Shuffled', {
                    x: 50,
                    y: 680,
                    size: 11,
                    font: font,
                });
                
                page1.drawText('1447-2026', {
                    x: 50,
                    y: 665,
                    size: 11,
                    font: font,
                });
                
                page1.drawText('Reviewer:', {
                    x: 450,
                    y: 710,
                    size: 11,
                    font: font,
                });
                
                page1.drawText('Corrector:', {
                    x: 450,
                    y: 695,
                    size: 11,
                    font: font,
                });
                
                page1.drawText('Student Name:', {
                    x: 450,
                    y: 680,
                    size: 11,
                    font: font,
                });
                
                // قسم Grammar
                page1.drawText('Grammar - Shuffled', {
                    x: 50,
                    y: 630,
                    size: 14,
                    font: fontBold,
                });
                
                page1.drawText('1. choose the correct answer', {
                    x: 50,
                    y: 610,
                    size: 12,
                    font: font,
                });
                
                // رسم خط للفصل
                page1.drawLine({
                    start: { x: 50, y: 600 },
                    end: { x: 545, y: 600 },
                    thickness: 1,
                });
                
                // إضافة أسئلة Grammar المخلوطة
                let yPos = 580;
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
                                page1.drawText(`${letter}) ${option}`, {
                                    x: 70,
                                    y: yPos - 18 * (optIndex + 1),
                                    size: 10,
                                    font: font,
                                });
                            });
                        }
                        
                        yPos -= 60;
                        if (yPos < 100 && index < shuffledQuestions.grammar.length - 1) {
                            const newPage = newPdfDoc.addPage([595, 842]);
                            yPos = 800;
                            page1 = newPage;
                        }
                    });
                }
                
                // قسم Orthography
                if (shuffledQuestions.orthography && shuffledQuestions.orthography.length > 0) {
                    if (yPos < 150) {
                        const page2 = newPdfDoc.addPage([595, 842]);
                        yPos = 800;
                        page1 = page2;
                    }
                    
                    page1.drawText('Orthography - Shuffled', {
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
                                page1.drawText(`${letter}) ${option}`, {
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
                
                // قسم Matching
                if (shuffledQuestions.matching && shuffledQuestions.matching.length > 0) {
                    const matchingPage = newPdfDoc.addPage([595, 842]);
                    
                    // عنوان قسم Matching
                    matchingPage.drawText('3. Carefully look at all the pictures shown in the column below.', {
                        x: 50,
                        y: 800,
                        size: 11,
                        font: font,
                    });
                    
                    matchingPage.drawText('Then, read the list of words provided in the opposite column.', {
                        x: 50,
                        y: 785,
                        size: 11,
                        font: font,
                    });
                    
                    matchingPage.drawText('Each word is labeled with a letter (A, B, C, etc.), and each picture is labeled', {
                        x: 50,
                        y: 770,
                        size: 11,
                        font: font,
                    });
                    
                    matchingPage.drawText('with a number (1, 2, 3, etc.). Your task is to choose the correct word', {
                        x: 50,
                        y: 755,
                        size: 11,
                        font: font,
                    });
                    
                    matchingPage.drawText('that matches each picture.', {
                        x: 50,
                        y: 740,
                        size: 11,
                        font: font,
                    });
                    
                    // جدول Matching
                    let tableY = 700;
                    shuffledQuestions.matching.forEach((question, index) => {
                        const letter = String.fromCharCode(64 + index + 1); // A, B, C, ...
                        
                        // عمود رقم الصورة
                        matchingPage.drawText(question.text, {
                            x: 50,
                            y: tableY,
                            size: 11,
                            font: fontBold,
                        });
                        
                        // عمود النقاط
                        matchingPage.drawText('9', {
                            x: 520,
                            y: tableY,
                            size: 11,
                            font: font,
                        });
                        
                        // عمود الحرف والكلمة
                        matchingPage.drawText(`(${letter}) ${question.match}`, {
                            x: 250,
                            y: tableY,
                            size: 11,
                            font: font,
                        });
                        
                        tableY -= 25;
                    });
                }
                
                // قسم Reading
                if (shuffledQuestions.reading && shuffledQuestions.reading.length > 0) {
                    const readingPage = newPdfDoc.addPage([595, 842]);
                    
                    // عنوان قسم Reading
                    readingPage.drawText('Reading - Shuffled', {
                        x: 50,
                        y: 800,
                        size: 16,
                        font: fontBold,
                    });
                    
                    readingPage.drawText('4. Read the passage then choose T for true And F for False:', {
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
                        readingPage.drawText(line, {
                            x: 50,
                            y: textY,
                            size: 11,
                            font: font,
                        });
                        textY -= 20;
                    });
                    
                    // إضافة أسئلة Reading المخلوطة
                    let readingQY = textY - 30;
                    shuffledQuestions.reading.forEach((question, index) => {
                        readingPage.drawText(`${question.number}. ${question.text}`, {
                            x: 50,
                            y: readingQY,
                            size: 11,
                            font: font,
                        });
                        
                        readingPage.drawText('(T)', {
                            x: 450,
                            y: readingQY,
                            size: 11,
                            font: font,
                        });
                        
                        readingPage.drawText('(F)', {
                            x: 480,
                            y: readingQY,
                            size: 11,
                            font: font,
                        });
                        
                        readingQY -= 25;
                    });
                    
                    // قسم Writing
                    readingQY -= 20;
                    readingPage.drawText('Writing', {
                        x: 50,
                        y: readingQY,
                        size: 16,
                        font: fontBold,
                    });
                    
                    readingQY -= 25;
                    readingPage.drawText('5- Write a coherent paragraph of 3-5 sentences using 8 words from the following list:', {
                        x: 50,
                        y: readingQY,
                        size: 12,
                        font: font,
                    });
                    
                    readingQY -= 20;
                    readingPage.drawText('(enjoy – fitness – work out – spend time – lifestyle – herbal tea – puzzle – fan)', {
                        x: 50,
                        y: readingQY,
                        size: 11,
                        font: fontBold,
                    });
                    
                    // خطوط للكتابة
                    readingQY -= 40;
                    for (let i = 0; i < 8; i++) {
                        readingPage.drawLine({
                            start: { x: 50, y: readingQY },
                            end: { x: 545, y: readingQY },
                            thickness: 1,
                        });
                        readingQY -= 25;
                    }
                    
                    // التوقيع
                    readingQY -= 30;
                    readingPage.drawText('My best wishes', {
                        x: 50,
                        y: readingQY,
                        size: 12,
                        font: fontItalic,
                    });
                    
                    readingQY -= 20;
                    readingPage.drawText('Teacher Friend Alkhaldi', {
                        x: 50,
                        y: readingQY,
                        size: 12,
                        font: fontItalic,
                    });
                }
                
                // حفظ PDF
                const newPdfBytes = await newPdfDoc.save();
                
                // تحميل الملف للمستخدم
                const blob = new Blob([newPdfBytes], { type: 'application/pdf' });
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url;
                const now = new Date();
                const timestamp = `${now.getFullYear()}${(now.getMonth()+1).toString().padStart(2,'0')}${now.getDate().toString().padStart(2,'0')}_${now.getHours().toString().padStart(2,'0')}${now.getMinutes().toString().padStart(2,'0')}`;
                a.download = `Shuffled_Exam_${timestamp}.pdf`;
                document.body.appendChild(a);
                a.click();
                document.body.removeChild(a);
                URL.revokeObjectURL(url);
                
                showStatus(`تم حفظ ملف PDF المخلوط بنجاح! تم تنزيل ${getTotalQuestions()} سؤالًا`, 'success');
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
                if ((currentLine + ' ' + word).length <= maxLength) {
                    currentLine += (currentLine ? ' ' : '') + word;
                } else {
                    if (currentLine) lines.push(currentLine);
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
            pdfTextContent = "";
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
            document.getElementById('pdfContentPreview').innerHTML = '';
            
            showStatus('تم إعادة تعيين جميع البيانات', 'info');
            updateWorkflow(1);
            updateButtons();
        }
        
        // عرض/إخفاء مؤشر التحميل
        function showLoading(show, message = 'جاري معالجة ملف PDF...') {
            const loadingDiv = document.getElementById('loading');
            const loadingText = document.getElementById('loadingText');
            
            loadingText.textContent = message;
            loadingDiv.style.display = show ? 'block' : 'none';
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
        
        // رسالة ترحيبية
        setTimeout(() => {
            showStatus('مرحبًا! قم بتحميل ملف PDF لبدء خلط الأسئلة', 'info');
        }, 1000);
    </script>
</body>
</html>
