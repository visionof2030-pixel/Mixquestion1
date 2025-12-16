<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>محرر اختبار Super Goal 3 - نسخة مطابقة للأصل</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <style>
        * {
            box-sizing: border-box;
            font-family: 'Arial', sans-serif;
        }
        body {
            background-color: #f8f9fa;
            margin: 0;
            padding: 20px;
            color: #333;
        }
        .container {
            max-width: 1000px;
            margin: auto;
            background: white;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 0 15px rgba(0,0,0,0.1);
        }
        .exam-template {
            width: 794px; /* A4 width in pixels */
            height: 1123px; /* A4 height in pixels */
            background: white;
            padding: 40px;
            margin: 20px auto;
            border: 1px solid #ccc;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            page-break-after: always;
            font-family: 'Times New Roman', serif;
        }
        .exam-header {
            text-align: center;
            border-bottom: 2px solid #000;
            padding-bottom: 15px;
            margin-bottom: 30px;
        }
        .exam-header h1 {
            font-size: 18px;
            margin: 5px 0;
            font-weight: bold;
        }
        .exam-header h2 {
            font-size: 16px;
            margin: 5px 0;
        }
        .student-info {
            display: flex;
            justify-content: space-between;
            margin-bottom: 30px;
            font-size: 14px;
        }
        .section-title {
            font-size: 16px;
            font-weight: bold;
            margin: 25px 0 15px 0;
            padding-bottom: 5px;
            border-bottom: 1px solid #ccc;
        }
        .question-table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 20px;
        }
        .question-table td {
            padding: 8px 5px;
            vertical-align: top;
            border: 1px solid #ddd;
        }
        .question-table .q-number {
            width: 30px;
            text-align: center;
            font-weight: bold;
            background: #f5f5f5;
        }
        .question-table .q-text {
            width: 70%;
        }
        .question-table .q-options {
            width: 30%;
        }
        .question-table .q-points {
            width: 30px;
            text-align: center;
            font-weight: bold;
        }
        .option-label {
            display: inline-block;
            width: 20px;
            font-weight: bold;
        }
        .matching-table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        .matching-table td {
            padding: 8px;
            border: 1px solid #ddd;
            vertical-align: middle;
        }
        .matching-img {
            text-align: center;
            font-weight: bold;
            background: #f9f9f9;
            width: 60px;
        }
        .matching-word {
            padding-left: 20px !important;
        }
        .reading-passage {
            background: #f9f9f9;
            padding: 15px;
            border-right: 3px solid #ccc;
            margin: 20px 0;
            line-height: 1.6;
        }
        .true-false-table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        .true-false-table td {
            padding: 8px;
            border: 1px solid #ddd;
        }
        .true-false-table .q-text {
            width: 80%;
        }
        .true-false-table .q-answer {
            width: 20%;
            text-align: center;
        }
        .writing-section {
            margin: 30px 0;
            padding: 15px;
            background: #f9f9f9;
            border-radius: 5px;
        }
        .word-list {
            font-weight: bold;
            color: #2c3e50;
            margin: 10px 0;
            padding: 10px;
            background: #e8f4fc;
            border-right: 3px solid #3498db;
        }
        .editor-container {
            background: #fff;
            padding: 20px;
            border: 2px dashed #3498db;
            border-radius: 10px;
            margin: 20px 0;
        }
        .editor-section {
            margin-bottom: 30px;
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 10px;
            background: #fefefe;
        }
        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 2px solid #3498db;
        }
        .question-block {
            margin-bottom: 15px;
            padding: 15px;
            border: 1px dashed #aaa;
            border-radius: 8px;
            background: #f9f9f9;
            cursor: move;
            position: relative;
        }
        .question-number {
            position: absolute;
            left: 10px;
            top: 10px;
            background: #3498db;
            color: white;
            width: 25px;
            height: 25px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }
        .question-content {
            margin-right: 40px;
        }
        .controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 30px 0;
            flex-wrap: wrap;
        }
        button {
            padding: 12px 24px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            cursor: pointer;
            transition: 0.3s;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .btn-shuffle {
            background: linear-gradient(135deg, #f39c12, #e67e22);
            color: white;
        }
        .btn-shuffle-all {
            background: linear-gradient(135deg, #8e44ad, #9b59b6);
            color: white;
        }
        .btn-preview {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
        }
        .btn-export {
            background: linear-gradient(135deg, #27ae60, #2ecc71);
            color: white;
        }
        .btn-reset {
            background: linear-gradient(135deg, #e74c3c, #c0392b);
            color: white;
        }
        button:hover {
            opacity: 0.9;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        .tab-container {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 2px solid #3498db;
        }
        .tab {
            padding: 12px 24px;
            background: #f5f5f5;
            border: none;
            border-radius: 8px 8px 0 0;
            margin-right: 5px;
            cursor: pointer;
            font-weight: bold;
            transition: 0.3s;
        }
        .tab.active {
            background: #3498db;
            color: white;
        }
        .tab:hover {
            background: #2980b9;
            color: white;
        }
        .tab-content {
            display: none;
        }
        .tab-content.active {
            display: block;
        }
        .footer-note {
            text-align: center;
            font-style: italic;
            color: #7f8c8d;
            margin-top: 30px;
            padding-top: 15px;
            border-top: 1px solid #eee;
        }
        .pdf-viewer-container {
            margin: 20px 0;
            border: 2px solid #3498db;
            border-radius: 10px;
            overflow: hidden;
            height: 500px;
        }
        #pdfViewer {
            width: 100%;
            height: 100%;
            border: none;
        }
        .pdf-upload {
            text-align: center;
            margin: 15px 0;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 8px;
            border: 2px dashed #ddd;
        }
        .pdf-upload input {
            padding: 10px;
            margin-top: 10px;
        }
        @media print {
            .no-print {
                display: none !important;
            }
            .exam-template {
                box-shadow: none;
                border: 1px solid #ccc;
                margin: 0;
                page-break-inside: avoid;
            }
        }
    </style>
</head>
<body>
    <div class="container no-print">
        <h1 style="text-align: center; color: #2c3e50; margin-bottom: 10px;">✏️ محرر اختبار Super Goal 3</h1>
        <p style="text-align: center; color: #7f8c8d; margin-bottom: 30px;">قم بتعديل وخلط الأسئلة ثم تصديرها بنفس تنسيق الملف الأصلي</p>
        
        <!-- ===== قسم عرض PDF الأصلي ===== -->
        <div class="pdf-upload">
            <h3>📄 رفع ملف الاختبار الأصلي (PDF)</h3>
            <input type="file" accept="application/pdf" onchange="loadPDF(this)" id="pdfUpload">
            <p style="color: #666; font-size: 14px; margin-top: 10px;">يمكنك رفع ملف PDF الأصلي كمرجع أثناء التعديل</p>
        </div>
        
        <div class="pdf-viewer-container">
            <iframe id="pdfViewer"></iframe>
        </div>
        
        <div class="tab-container">
            <button class="tab active" onclick="showTab('editor')">✏️ محرر الأسئلة</button>
            <button class="tab" onclick="showTab('preview')">👁️ معاينة النموذج</button>
        </div>
        
        <!-- Tab 1: Editor -->
        <div id="editor-tab" class="tab-content active">
            <div class="editor-container">
                <!-- Grammar Editor -->
                <div class="editor-section">
                    <div class="section-header">
                        <h3>📘 Grammar Questions (أسئلة القواعد)</h3>
                        <button class="btn-shuffle" onclick="shuffleQuestions('grammar')">🔀 خلط عشوائي</button>
                    </div>
                    <div id="grammar-questions">
                        <!-- سيتم ملؤها بالجافاسكريبت -->
                    </div>
                </div>
                
                <!-- Orthography Editor -->
                <div class="editor-section">
                    <div class="section-header">
                        <h3>🔤 Orthography Questions (أسئلة الإملاء)</h3>
                        <button class="btn-shuffle" onclick="shuffleQuestions('orthography')">🔀 خلط عشوائي</button>
                    </div>
                    <div id="orthography-questions">
                        <!-- سيتم ملؤها بالجافاسكريبت -->
                    </div>
                </div>
                
                <!-- Matching Editor -->
                <div class="editor-section">
                    <div class="section-header">
                        <h3>🖼️ Vocabulary Matching (التطابق)</h3>
                        <button class="btn-shuffle" onclick="shuffleQuestions('matching')">🔀 خلط عشوائي</button>
                    </div>
                    <div id="matching-questions">
                        <!-- سيتم ملؤها بالجافاسكريبت -->
                    </div>
                </div>
                
                <!-- Reading Editor -->
                <div class="editor-section">
                    <div class="section-header">
                        <h3>📖 Reading Comprehension (القراءة)</h3>
                        <button class="btn-shuffle" onclick="shuffleQuestions('reading')">🔀 خلط عشوائي</button>
                    </div>
                    <textarea id="reading-text" rows="4" style="width:100%; padding:10px; margin-bottom:15px;" 
                              placeholder="نص القراءة...">King Salman bin Abdulaziz was born in Riyadh. He studied religion, science, and the Holy Qur'an at the Princes' School. He became King of Saudi Arabia in 2015. He helped Riyadh grow from a small town into a major modern city. He also supported humanitarian and cultural projects inside and outside the Kingdom.</textarea>
                    <div id="reading-questions">
                        <!-- سيتم ملؤها بالجافاسكريبت -->
                    </div>
                </div>
                
                <!-- Writing Editor -->
                <div class="editor-section">
                    <div class="section-header">
                        <h3>✍️ Writing Task (الكتابة)</h3>
                        <button class="btn-shuffle" onclick="shuffleWritingWords()">🔀 خلط الكلمات</button>
                    </div>
                    <textarea id="writing-prompt" rows="3" style="width:100%; padding:10px; margin-bottom:10px;">Write a coherent paragraph of 3-5 sentences using 8 words from the following list:</textarea>
                    <input type="text" id="word-list" value="(enjoy – fitness – work out – spend time – lifestyle – herbal tea – puzzle – fan)" style="width:100%; padding:10px;">
                </div>
            </div>
        </div>
        
        <!-- Tab 2: Preview -->
        <div id="preview-tab" class="tab-content">
            <div id="exam-preview">
                <!-- سيتم ملؤها بالجافاسكريبت -->
            </div>
        </div>
        
        <!-- Main Controls -->
        <div class="controls no-print">
            <button class="btn-shuffle-all" onclick="shuffleAllSections()">🔀 خلط كل الأسئلة</button>
            <button class="btn-preview" onclick="generatePreview()">👁️ تحديث المعاينة</button>
            <button class="btn-export" onclick="exportToPDF()">📥 تصدير PDF نهائي</button>
            <button class="btn-reset" onclick="resetToOriginal()">🔄 استعادة النسخة الأصلية</button>
        </div>
        
        <div class="footer-note no-print">
            <p>💡 يمكنك رفع ملف PDF الأصلي كمرجع، ثم تعديل وخلط الأسئلة، وأخيراً تصدير نسخة جديدة</p>
            <p>📊 PDF النهائي سيكون بنفس تنسيق محرر الأسئلة مع الأسئلة المخلوطة</p>
        </div>
    </div>

    <script>
        // البيانات الأصلية من الملف
        const originalData = {
            school: "Saeed Ibn Alas Intermediate School",
            grade: "3rd Intermediate Grade",
            term: "2nd Term rescheduled Exam",
            year: "1447-2026",
            grammar: [
                { q: "I. he ___ plays football on weekends.", options: ["does", "always", "has"], correct: 1, points: 9 },
                { q: "How often ______ drink coffee?", options: ["does", "did", "do"], correct: 0, points: 9 },
                { q: "My friends are ______ to the museum tomorrow.", options: ["go", "goes", "going"], correct: 2, points: 9 },
                { q: "They both ______ English very well.", options: ["Speak", "speaks", "speaking"], correct: 0, points: 9 },
                { q: "I ______ play with toys when I was a child", options: ["use", "used to", "used"], correct: 1, points: 9 },
                { q: "She was born ______ 2005", options: ["at", "on", "in"], correct: 2, points: 9 },
                { q: "He is ______ a haircut now.", options: ["get", "got", "getting"], correct: 2, points: 9 },
                { q: "I have lives here ______ three years.", options: ["since", "for", "From"], correct: 1, points: 9 },
                { q: "They didn't go to school when they ______ young.", options: ["were", "are", "be"], correct: 0, points: 9 }
            ],
            orthography: [
                { word: "___ilk_", options: ["N", "M", "T"], correct: 1, points: 5 },
                { word: "_pota__oes", options: ["N", "T", "H"], correct: 1, points: 5 },
                { word: "_bre__d_", options: ["e", "a", "u"], correct: 1, points: 5 },
                { word: "_fu__f_", options: ["e", "i", "o"], correct: 2, points: 5 },
                { word: "_mang__", options: ["u", "e", "o"], correct: 2, points: 5 }
            ],
            matching: [
                { img: "(1)", word: "Lamb", points: 9 },
                { img: "(2)", word: "Shrimp", points: 9 },
                { img: "(3)", word: "Carrot", points: 9 },
                { img: "(4)", word: "Bread", points: 9 },
                { img: "(5)", word: "Avocado", points: 9 },
                { img: "(6)", word: "Olive oil", points: 9 },
                { img: "(7)", word: "Cereal", points: 9 },
                { img: "(8)", word: "Mango", points: 9 },
                { img: "(9)", word: "Cheese", points: 9 }
            ],
            reading: {
                text: "King Salman bin Abdulaziz was born in Riyadh. He studied religion, science, and the Holy Qur'an at the Princes' School. He became King of Saudi Arabia in 2015. He helped Riyadh grow from a small town into a major modern city. He also supported humanitarian and cultural projects inside and outside the Kingdom.",
                questions: [
                    { q: "King Salman was born in Jeddah.", answer: false },
                    { q: "He studied at the Princes' School.", answer: true },
                    { q: "He became King in 2012.", answer: false },
                    { q: "He worked to develop the city of Riyadh.", answer: true },
                    { q: "Riyadh became smaller during his leadership.", answer: false },
                    { q: "He supported humanitarian work.", answer: true },
                    { q: "He received awards for his projects.", answer: false },
                    { q: "He helped develop cities outside the Kingdom.", answer: true },
                    { q: "The passage talks about King Salman's future plans.", answer: false }
                ]
            },
            writing: {
                prompt: "Write a coherent paragraph of 3-5 sentences using 8 words from the following list:",
                words: "(enjoy – fitness – work out – spend time – lifestyle – herbal tea – puzzle – fan)"
            }
        };

        let currentData = JSON.parse(JSON.stringify(originalData));

        // ===== 1. تحميل وعرض PDF الأصلي =====
        function loadPDF(input) {
            const file = input.files[0];
            if (!file) return;
            
            const url = URL.createObjectURL(file);
            const viewer = document.getElementById("pdfViewer");
            viewer.src = url;
            
            // إضافة معلومات للمستخدم
            alert(`✓ تم تحميل ملف PDF: ${file.name}\n\nيمكنك الآن استخدامه كمرجع أثناء تعديل الأسئلة`);
            
            // حفظ رابط الملف مؤقتاً
            sessionStorage.setItem('pdfReference', url);
        }

        // ===== 2. تهيئة المحرر =====
        function initEditor() {
            renderGrammarEditor();
            renderOrthographyEditor();
            renderMatchingEditor();
            renderReadingEditor();
            makeSortable('grammar-questions');
            makeSortable('orthography-questions');
            makeSortable('matching-questions');
            makeSortable('reading-questions');
        }

        // ===== محرر القواعد =====
        function renderGrammarEditor() {
            const container = document.getElementById('grammar-questions');
            container.innerHTML = '';
            currentData.grammar.forEach((item, idx) => {
                const div = document.createElement('div');
                div.className = 'question-block';
                div.setAttribute('data-id', idx);
                div.innerHTML = `
                    <div class="question-number">${idx + 1}</div>
                    <div class="question-content">
                        <input type="text" value="${item.q}" onchange="updateGrammar(${idx}, 'q', this.value)" 
                               style="width:100%; padding:8px; margin-bottom:10px;" placeholder="نص السؤال">
                        <div style="display: flex; gap: 15px; flex-wrap: wrap;">
                            ${item.options.map((opt, optIdx) => `
                                <div style="display: flex; align-items: center; gap: 5px;">
                                    <input type="radio" name="grammar-${idx}" ${optIdx == item.correct ? 'checked' : ''} 
                                           onchange="updateGrammar(${idx}, 'correct', ${optIdx})">
                                    <span style="font-weight:bold;">${String.fromCharCode(97 + optIdx)})</span>
                                    <input type="text" value="${opt}" onchange="updateGrammar(${idx}, 'options', ${optIdx}, this.value)"
                                           style="width:100px; padding:5px;">
                                </div>
                            `).join('')}
                        </div>
                        <div style="margin-top:10px; display:flex; justify-content:space-between;">
                            <span>النقاط: <input type="number" value="${item.points}" onchange="updateGrammar(${idx}, 'points', this.value)" style="width:50px;"></span>
                            <button onclick="removeQuestion('grammar', ${idx})" style="background:#e74c3c; color:white; padding:5px 10px; border:none; border-radius:4px;">حذف</button>
                        </div>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        // ===== محرر الإملاء =====
        function renderOrthographyEditor() {
            const container = document.getElementById('orthography-questions');
            container.innerHTML = '';
            currentData.orthography.forEach((item, idx) => {
                const div = document.createElement('div');
                div.className = 'question-block';
                div.setAttribute('data-id', idx);
                div.innerHTML = `
                    <div class="question-number">${idx + 1}</div>
                    <div class="question-content">
                        <div style="display: flex; align-items: center; gap: 15px; margin-bottom: 10px;">
                            <strong>الكلمة:</strong>
                            <input type="text" value="${item.word}" onchange="updateOrthography(${idx}, 'word', this.value)" 
                                   style="width:200px; padding:8px;" placeholder="___word_">
                            <span>النقاط: <input type="number" value="${item.points}" onchange="updateOrthography(${idx}, 'points', this.value)" style="width:50px;"></span>
                        </div>
                        <div style="display: flex; gap: 15px; flex-wrap: wrap;">
                            ${item.options.map((opt, optIdx) => `
                                <div style="display: flex; align-items: center; gap: 5px;">
                                    <input type="radio" name="ortho-${idx}" ${optIdx == item.correct ? 'checked' : ''} 
                                           onchange="updateOrthography(${idx}, 'correct', ${optIdx})">
                                    <span style="font-weight:bold;">${String.fromCharCode(97 + optIdx)})</span>
                                    <input type="text" value="${opt}" onchange="updateOrthography(${idx}, 'options', ${optIdx}, this.value)"
                                           style="width:50px; padding:5px;">
                                </div>
                            `).join('')}
                        </div>
                        <div style="margin-top:10px; text-align:left;">
                            <button onclick="removeQuestion('orthography', ${idx})" style="background:#e74c12; color:white; padding:5px 10px; border:none; border-radius:4px;">حذف</button>
                        </div>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        // ===== محرر التطابق =====
        function renderMatchingEditor() {
            const container = document.getElementById('matching-questions');
            container.innerHTML = '';
            currentData.matching.forEach((item, idx) => {
                const div = document.createElement('div');
                div.className = 'question-block';
                div.setAttribute('data-id', idx);
                div.innerHTML = `
                    <div class="question-number">${idx + 1}</div>
                    <div class="question-content">
                        <div style="display: flex; align-items: center; gap: 15px; flex-wrap: wrap;">
                            <div>
                                <strong>رقم الصورة:</strong>
                                <input type="text" value="${item.img}" onchange="updateMatching(${idx}, 'img', this.value)" 
                                       style="width:80px; padding:8px; margin:0 10px;">
                            </div>
                            <div>
                                <strong>الكلمة:</strong>
                                <input type="text" value="${item.word}" onchange="updateMatching(${idx}, 'word', this.value)" 
                                       style="width:150px; padding:8px; margin:0 10px;">
                            </div>
                            <div>
                                <span>النقاط: <input type="number" value="${item.points}" onchange="updateMatching(${idx}, 'points', this.value)" style="width:50px;"></span>
                            </div>
                            <div>
                                <button onclick="removeQuestion('matching', ${idx})" style="background:#e74c3c; color:white; padding:5px 10px; border:none; border-radius:4px;">حذف</button>
                            </div>
                        </div>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        // ===== محرر القراءة =====
        function renderReadingEditor() {
            const container = document.getElementById('reading-questions');
            container.innerHTML = '';
            currentData.reading.questions.forEach((item, idx) => {
                const div = document.createElement('div');
                div.className = 'question-block';
                div.setAttribute('data-id', idx);
                div.innerHTML = `
                    <div class="question-number">${idx + 1}</div>
                    <div class="question-content">
                        <div style="display: flex; align-items: center; gap: 15px; flex-wrap: wrap;">
                            <input type="text" value="${item.q}" onchange="updateReadingQuestion(${idx}, 'q', this.value)" 
                                   style="flex:1; padding:8px; min-width:300px;" placeholder="نص السؤال">
                            <select onchange="updateReadingQuestion(${idx}, 'answer', this.value === 'true')" style="padding:8px;">
                                <option value="true" ${item.answer ? 'selected' : ''}>True</option>
                                <option value="false" ${!item.answer ? 'selected' : ''}>False</option>
                            </select>
                            <button onclick="removeQuestion('reading', ${idx})" style="background:#e74c3c; color:white; padding:5px 10px; border:none; border-radius:4px;">حذف</button>
                        </div>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        // ===== تحديث البيانات =====
        function updateGrammar(idx, field, val, optIdx = null) {
            if (field === 'options') {
                currentData.grammar[idx].options[optIdx] = val;
            } else if (field === 'correct') {
                currentData.grammar[idx].correct = val;
            } else {
                currentData.grammar[idx][field] = val;
            }
        }

        function updateOrthography(idx, field, val, optIdx = null) {
            if (field === 'options') {
                currentData.orthography[idx].options[optIdx] = val;
            } else if (field === 'correct') {
                currentData.orthography[idx].correct = val;
            } else {
                currentData.orthography[idx][field] = val;
            }
        }

        function updateMatching(idx, field, val) {
            currentData.matching[idx][field] = val;
        }

        function updateReadingQuestion(idx, field, val) {
            if (field === 'q') {
                currentData.reading.questions[idx].q = val;
            } else {
                currentData.reading.questions[idx].answer = val;
            }
        }

        // ===== خلط الأسئلة =====
        function shuffleQuestions(sectionType) {
            if (confirm(`هل تريد خلط أسئلة قسم ${sectionType} عشوائيًا؟`)) {
                let arrayToShuffle;
                
                switch(sectionType) {
                    case 'grammar':
                        arrayToShuffle = currentData.grammar;
                        for (let i = arrayToShuffle.length - 1; i > 0; i--) {
                            const j = Math.floor(Math.random() * (i + 1));
                            [arrayToShuffle[i], arrayToShuffle[j]] = [arrayToShuffle[j], arrayToShuffle[i]];
                        }
                        renderGrammarEditor();
                        break;
                    case 'orthography':
                        arrayToShuffle = currentData.orthography;
                        for (let i = arrayToShuffle.length - 1; i > 0; i--) {
                            const j = Math.floor(Math.random() * (i + 1));
                            [arrayToShuffle[i], arrayToShuffle[j]] = [arrayToShuffle[j], arrayToShuffle[i]];
                        }
                        renderOrthographyEditor();
                        break;
                    case 'matching':
                        arrayToShuffle = currentData.matching;
                        for (let i = arrayToShuffle.length - 1; i > 0; i--) {
                            const j = Math.floor(Math.random() * (i + 1));
                            [arrayToShuffle[i], arrayToShuffle[j]] = [arrayToShuffle[j], arrayToShuffle[i]];
                        }
                        renderMatchingEditor();
                        break;
                    case 'reading':
                        arrayToShuffle = currentData.reading.questions;
                        for (let i = arrayToShuffle.length - 1; i > 0; i--) {
                            const j = Math.floor(Math.random() * (i + 1));
                            [arrayToShuffle[i], arrayToShuffle[j]] = [arrayToShuffle[j], arrayToShuffle[i]];
                        }
                        renderReadingEditor();
                        break;
                }
                
                alert(`✓ تم خلط ${arrayToShuffle.length} سؤالًا في قسم ${sectionType}`);
            }
        }

        function shuffleAllSections() {
            if (confirm("هل تريد خلط جميع أسئلة الاختبار عشوائيًا؟")) {
                shuffleQuestions('grammar');
                shuffleQuestions('orthography');
                shuffleQuestions('matching');
                shuffleQuestions('reading');
                shuffleWritingWords();
                alert("✓ تم خلط جميع أقسام الاختبار بنجاح");
            }
        }

        function shuffleWritingWords() {
            const wordsInput = document.getElementById('word-list');
            const matches = wordsInput.value.match(/[a-zA-Z\u0600-\u06FF\u0750-\u077F][a-zA-Z\u0600-\u06FF\u0750-\u077F\s\-]*[a-zA-Z\u0600-\u06FF\u0750-\u077F]/g);
            if (matches && matches.length > 1) {
                const words = matches;
                for (let i = words.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [words[i], words[j]] = [words[j], words[i]];
                }
                wordsInput.value = "(" + words.join(" – ") + ")";
                currentData.writing.words = wordsInput.value;
            }
        }

        // ===== حذف الأسئلة =====
        function removeQuestion(type, idx) {
            if (confirm("هل أنت متأكد من حذف هذا السؤال؟")) {
                switch(type) {
                    case 'grammar':
                        currentData.grammar.splice(idx, 1);
                        renderGrammarEditor();
                        break;
                    case 'orthography':
                        currentData.orthography.splice(idx, 1);
                        renderOrthographyEditor();
                        break;
                    case 'matching':
                        currentData.matching.splice(idx, 1);
                        renderMatchingEditor();
                        break;
                    case 'reading':
                        currentData.reading.questions.splice(idx, 1);
                        renderReadingEditor();
                        break;
                }
            }
        }

        // ===== السحب والإفلات =====
        function makeSortable(id) {
            const el = document.getElementById(id);
            let dragItem = null;
            
            el.addEventListener('dragstart', e => {
                dragItem = e.target.closest('.question-block');
                e.dataTransfer.effectAllowed = 'move';
                setTimeout(() => dragItem.style.opacity = '0.4', 0);
            });
            
            el.addEventListener('dragover', e => {
                e.preventDefault();
                const afterElement = getDragAfterElement(el, e.clientY);
                if (afterElement == null) {
                    el.appendChild(dragItem);
                } else {
                    el.insertBefore(dragItem, afterElement);
                }
            });
            
            el.addEventListener('dragend', () => {
                dragItem.style.opacity = '1';
                updateOrderFromDOM(id);
            });
        }

        function getDragAfterElement(container, y) {
            const draggableElements = [...container.querySelectorAll('.question-block')];
            return draggableElements.reduce((closest, child) => {
                const box = child.getBoundingClientRect();
                const offset = y - box.top - box.height / 2;
                if (offset < 0 && offset > closest.offset) {
                    return { offset: offset, element: child };
                } else {
                    return closest;
                }
            }, { offset: Number.NEGATIVE_INFINITY }).element;
        }

        function updateOrderFromDOM(id) {
            const items = [...document.getElementById(id).querySelectorAll('.question-block')];
            const newOrder = items.map(item => parseInt(item.getAttribute('data-id')));
            
            if (id === 'grammar-questions') {
                const reordered = newOrder.map(idx => currentData.grammar[idx]);
                currentData.grammar = reordered;
                renderGrammarEditor();
            } else if (id === 'orthography-questions') {
                const reordered = newOrder.map(idx => currentData.orthography[idx]);
                currentData.orthography = reordered;
                renderOrthographyEditor();
            } else if (id === 'matching-questions') {
                const reordered = newOrder.map(idx => currentData.matching[idx]);
                currentData.matching = reordered;
                renderMatchingEditor();
            } else if (id === 'reading-questions') {
                const reordered = newOrder.map(idx => currentData.reading.questions[idx]);
                currentData.reading.questions = reordered;
                renderReadingEditor();
            }
        }

        // ===== معاينة النموذج =====
        function generatePreview() {
            const preview = document.getElementById('exam-preview');
            preview.innerHTML = '';
            
            // تحديث البيانات من الحقول
            currentData.reading.text = document.getElementById('reading-text').value;
            currentData.writing.prompt = document.getElementById('writing-prompt').value;
            currentData.writing.words = document.getElementById('word-list').value;
            
            // إنشاء نسخة من النموذج الأصلي
            const examDiv = document.createElement('div');
            examDiv.className = 'exam-template';
            examDiv.innerHTML = `
                <div class="exam-header">
                    <h1>Kingdom of Saudi Arabia Ministry of Education</h1>
                    <h1>Education Directorate in Makkah</h1>
                    <h2>${currentData.school}</h2>
                    <h2>Written Exam 40 - Written</h2>
                    <h2>Super Goal 3 - English Language</h2>
                    <h2>${currentData.grade}</h2>
                    <h2>${currentData.term}</h2>
                    <h2>${currentData.year}</h2>
                </div>
                
                <div class="student-info">
                    <div>رقم الجلوس: ____________</div>
                    <div>اسم الطالب: ____________</div>
                    <div>المراجع: ____________</div>
                    <div>المصحح: ____________</div>
                </div>
                
                <div class="section-title">Grammar</div>
                <table class="question-table">
                    ${currentData.grammar.map((item, idx) => `
                        <tr>
                            <td class="q-number">${idx + 1}</td>
                            <td class="q-text">${item.q}</td>
                            <td class="q-options">
                                ${item.options.map((opt, optIdx) => `
                                    <div><span class="option-label">${String.fromCharCode(97 + optIdx)})</span> ${opt}</div>
                                `).join('')}
                            </td>
                            <td class="q-points">${item.points}</td>
                        </tr>
                    `).join('')}
                </table>
                
                <div class="section-title">Orthography</div>
                <table class="question-table">
                    ${currentData.orthography.map((item, idx) => `
                        <tr>
                            <td class="q-number">${idx + 1}</td>
                            <td class="q-text">${item.word}</td>
                            <td class="q-options">
                                ${item.options.map((opt, optIdx) => `
                                    <div><span class="option-label">${String.fromCharCode(97 + optIdx)})</span> ${opt}</div>
                                `).join('')}
                            </td>
                            <td class="q-points">${item.points}</td>
                        </tr>
                    `).join('')}
                </table>
                
                <div class="section-title">Vocabulary Matching</div>
                <p style="text-align: center; margin: 10px 0;">Carefully look at all the pictures shown in the column below. Then, read the list of words provided in the opposite column. Each word is labeled with a letter (A, B, C, etc.), and each picture is labeled with a number (1, 2, 3, etc.). Your task is to choose the correct word that matches each picture.</p>
                <table class="matching-table">
                    ${currentData.matching.map((item, idx) => `
                        <tr>
                            <td class="matching-img">${item.img}</td>
                            <td class="matching-word">${String.fromCharCode(65 + idx)}) ${item.word}</td>
                            <td style="width: 60px; text-align: center;">${item.points}</td>
                        </tr>
                    `).join('')}
                </table>
                
                <div class="section-title">Reading</div>
                <div class="reading-passage">
                    ${currentData.reading.text}
                </div>
                <table class="true-false-table">
                    ${currentData.reading.questions.map((item, idx) => `
                        <tr>
                            <td class="q-number">${idx + 1}</td>
                            <td class="q-text">${item.q}</td>
                            <td class="q-answer">(T) &nbsp;&nbsp; (F)</td>
                        </tr>
                    `).join('')}
                </table>
                
                <div class="section-title">Writing</div>
                <div class="writing-section">
                    <p><strong>${currentData.writing.prompt}</strong></p>
                    <div class="word-list">${currentData.writing.words}</div>
                    <div style="margin-top: 20px; height: 150px; border: 1px solid #ccc; padding: 10px;">
                        <!-- مساحة للكتابة -->
                    </div>
                </div>
                
                <div style="text-align: center; margin-top: 40px; font-style: italic;">
                    <p>My best wishes</p>
                    <p>Teacher Friend Alkhaldi</p>
                </div>
            `;
            
            preview.appendChild(examDiv);
            showTab('preview');
        }

        // ===== 3. تصدير PDF نهائي (باستخدام html2canvas) =====
        function exportToPDF() {
            // تحديث البيانات أولاً
            currentData.reading.text = document.getElementById('reading-text').value;
            currentData.writing.prompt = document.getElementById('writing-prompt').value;
            currentData.writing.words = document.getElementById('word-list').value;
            
            // إنشاء معاينة مؤقتة للتصدير
            const tempContainer = document.createElement('div');
            tempContainer.style.position = 'absolute';
            tempContainer.style.left = '-9999px';
            tempContainer.style.top = '0';
            tempContainer.style.width = '794px';
            tempContainer.style.background = 'white';
            tempContainer.style.padding = '40px';
            tempContainer.style.fontFamily = 'Arial, sans-serif';
            
            // نسخ محتوى المعاينة
            const previewContent = document.getElementById('exam-preview').innerHTML;
            tempContainer.innerHTML = previewContent || createExportHTML();
            
            document.body.appendChild(tempContainer);
            
            // استخدام html2canvas لالتقاط الصورة
            html2canvas(tempContainer, {
                scale: 2,
                useCORS: true,
                logging: false,
                backgroundColor: '#ffffff'
            }).then(canvas => {
                // تنظيف العنصر المؤقت
                document.body.removeChild(tempContainer);
                
                const imgData = canvas.toDataURL('image/png', 1.0);
                const { jsPDF } = window.jspdf;
                const pdf = new jsPDF('p', 'mm', 'a4');
                
                const width = pdf.internal.pageSize.getWidth();
                const height = (canvas.height * width) / canvas.width;
                
                // حساب عدد الصفحات المطلوبة
                const pageHeight = pdf.internal.pageSize.getHeight();
                let position = 0;
                
                // إضافة الصفحات حسب الطول
                while (position < height) {
                    if (position > 0) {
                        pdf.addPage();
                    }
                    
                    const sourceHeight = Math.min(canvas.height, (pageHeight * canvas.width) / width);
                    const sourceY = (position * canvas.height) / height;
                    
                    pdf.addImage(
                        imgData,
                        'PNG',
                        0,
                        0 - position,
                        width,
                        height
                    );
                    
                    position += pageHeight;
                }
                
                // حفظ الملف
                const fileName = `Exam_Modified_${new Date().toISOString().slice(0, 10)}.pdf`;
                pdf.save(fileName);
                
                alert(`✓ تم تصدير الملف بنجاح: ${fileName}\n\nالملف يحتوي على:\n• ${currentData.grammar.length} سؤال قواعد\n• ${currentData.orthography.length} سؤال إملاء\n• ${currentData.matching.length} سؤال تطابق\n• ${currentData.reading.questions.length} سؤال قراءة`);
            }).catch(error => {
                console.error('خطأ في التصدير:', error);
                alert('حدث خطأ أثناء التصدير. يرجى المحاولة مرة أخرى.');
            });
        }

        // إنشاء HTML للتصدير في حالة عدم وجود معاينة
        function createExportHTML() {
            return `
                <div class="exam-header">
                    <h1>Kingdom of Saudi Arabia Ministry of Education</h1>
                    <h1>Education Directorate in Makkah</h1>
                    <h2>${currentData.school}</h2>
                    <h2>Written Exam 40 - Written</h2>
                    <h2>Super Goal 3 - English Language</h2>
                    <h2>${currentData.grade}</h2>
                    <h2>${currentData.term}</h2>
                    <h2>${currentData.year}</h2>
                </div>
                
                <div class="student-info">
                    <div>رقم الجلوس: ____________</div>
                    <div>اسم الطالب: ____________</div>
                    <div>المراجع: ____________</div>
                    <div>المصحح: ____________</div>
                </div>
                
                <div class="section-title">Grammar</div>
                <table class="question-table">
                    ${currentData.grammar.map((item, idx) => `
                        <tr>
                            <td class="q-number">${idx + 1}</td>
                            <td class="q-text">${item.q}</td>
                            <td class="q-options">
                                ${item.options.map((opt, optIdx) => `
                                    <div><span class="option-label">${String.fromCharCode(97 + optIdx)})</span> ${opt}</div>
                                `).join('')}
                            </td>
                            <td class="q-points">${item.points}</td>
                        </tr>
                    `).join('')}
                </table>
                
                <div class="section-title">Orthography</div>
                <table class="question-table">
                    ${currentData.orthography.map((item, idx) => `
                        <tr>
                            <td class="q-number">${idx + 1}</td>
                            <td class="q-text">${item.word}</td>
                            <td class="q-options">
                                ${item.options.map((opt, optIdx) => `
                                    <div><span class="option-label">${String.fromCharCode(97 + optIdx)})</span> ${opt}</div>
                                `).join('')}
                            </td>
                            <td class="q-points">${item.points}</td>
                        </tr>
                    `).join('')}
                </table>
                
                <div class="section-title">Vocabulary Matching</div>
                <p style="text-align: center; margin: 10px 0;">Carefully look at all the pictures shown in the column below. Then, read the list of words provided in the opposite column. Each word is labeled with a letter (A, B, C, etc.), and each picture is labeled with a number (1, 2, 3, etc.). Your task is to choose the correct word that matches each picture.</p>
                <table class="matching-table">
                    ${currentData.matching.map((item, idx) => `
                        <tr>
                            <td class="matching-img">${item.img}</td>
                            <td class="matching-word">${String.fromCharCode(65 + idx)}) ${item.word}</td>
                            <td style="width: 60px; text-align: center;">${item.points}</td>
                        </tr>
                    `).join('')}
                </table>
                
                <div class="section-title">Reading</div>
                <div class="reading-passage">
                    ${currentData.reading.text}
                </div>
                <table class="true-false-table">
                    ${currentData.reading.questions.map((item, idx) => `
                        <tr>
                            <td class="q-number">${idx + 1}</td>
                            <td class="q-text">${item.q}</td>
                            <td class="q-answer">(T) &nbsp;&nbsp; (F)</td>
                        </tr>
                    `).join('')}
                </table>
                
                <div class="section-title">Writing</div>
                <div class="writing-section">
                    <p><strong>${currentData.writing.prompt}</strong></p>
                    <div class="word-list">${currentData.writing.words}</div>
                    <div style="margin-top: 20px; height: 150px; border: 1px solid #ccc; padding: 10px;">
                        <!-- مساحة للكتابة -->
                    </div>
                </div>
                
                <div style="text-align: center; margin-top: 40px; font-style: italic;">
                    <p>My best wishes</p>
                    <p>Teacher Friend Alkhaldi</p>
                </div>
            `;
        }

        // ===== وظائف مساعدة =====
        function showTab(tabName) {
            // إخفاء جميع التبويبات
            document.querySelectorAll('.tab').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
            
            // إظهار التبويب المحدد
            document.querySelector(`.tab[onclick*="${tabName}"]`).classList.add('active');
            document.getElementById(`${tabName}-tab`).classList.add('active');
        }

        function resetToOriginal() {
            if (confirm('هل أنت متأكد من استعادة النسخة الأصلية؟ سيتم فقدان جميع التغييرات.')) {
                currentData = JSON.parse(JSON.stringify(originalData));
                document.getElementById('reading-text').value = currentData.reading.text;
                document.getElementById('writing-prompt').value = currentData.writing.prompt;
                document.getElementById('word-list').value = currentData.writing.words;
                initEditor();
                alert('تم استعادة النسخة الأصلية.');
            }
        }

        // تحميل البيانات المحفوظة
        window.onload = function() {
            const saved = localStorage.getItem('examData');
            if (saved) {
                const savedData = JSON.parse(saved);
                currentData = { ...currentData, ...savedData };
                document.getElementById('reading-text').value = currentData.reading.text;
                document.getElementById('writing-prompt').value = currentData.writing.prompt;
                document.getElementById('word-list').value = currentData.writing.words;
            }
            initEditor();
            showTab('editor');
        };
    </script>
</body>
</html>
