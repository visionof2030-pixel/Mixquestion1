<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>محرر اختبار Super Goal 3</title>
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
        h1, h2, h3 {
            text-align: center;
            color: #2c3e50;
        }
        .header-info {
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            border-bottom: 2px solid #3498db;
            padding-bottom: 15px;
            margin-bottom: 20px;
        }
        .section {
            margin-bottom: 30px;
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 10px;
            background: #fefefe;
            position: relative;
        }
        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
        .section-header h2 {
            margin: 0;
        }
        .section-controls {
            display: flex;
            gap: 10px;
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
        .question-block:hover {
            background: #eef7ff;
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
        textarea, input[type="text"] {
            width: 100%;
            padding: 10px;
            margin-top: 5px;
            border: 1px solid #bbb;
            border-radius: 6px;
            font-size: 16px;
        }
        .options {
            margin-top: 10px;
            padding-right: 20px;
        }
        .option {
            display: flex;
            align-items: center;
            margin-bottom: 8px;
        }
        .option input[type="radio"] {
            margin-left: 10px;
        }
        .controls {
            display: flex;
            justify-content: space-between;
            margin-top: 25px;
            flex-wrap: wrap;
            gap: 10px;
        }
        button {
            padding: 10px 20px;
            border: none;
            border-radius: 8px;
            font-size: 14px;
            cursor: pointer;
            transition: 0.3s;
        }
        .btn-shuffle {
            background-color: #f39c12;
            color: white;
        }
        .btn-add {
            background-color: #27ae60;
            color: white;
        }
        .btn-delete {
            background-color: #e74c3c;
            color: white;
            padding: 5px 10px;
            font-size: 12px;
            margin-top: 5px;
        }
        #saveBtn {
            background-color: #2ecc71;
            color: white;
        }
        #resetBtn {
            background-color: #e74c3c;
            color: white;
        }
        #pdfBtn {
            background-color: #3498db;
            color: white;
        }
        #printBtn {
            background-color: #9b59b6;
            color: white;
        }
        #shuffleAllBtn {
            background-color: #8e44ad;
            color: white;
        }
        button:hover {
            opacity: 0.85;
            transform: scale(1.03);
        }
        .sortable-ghost {
            opacity: 0.4;
        }
        .instructions {
            background: #e8f4fc;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            border-right: 5px solid #3498db;
        }
        .instructions ul {
            padding-right: 20px;
        }
        @media print {
            .no-print {
                display: none;
            }
            .container {
                box-shadow: none;
                border: none;
            }
            .question-number {
                background: none;
                color: black;
                border: 1px solid black;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>✏️ محرر اختبار Super Goal 3 مع خاصية الخلط العشوائي</h1>
        
        <div class="instructions">
            <h3>📋 تعليمات الاستخدام:</h3>
            <ul>
                <li>يمكنك تعديل أي نص في الأسئلة أو الخيارات مباشرة.</li>
                <li>اسحب وأفلت الفقرات داخل كل قسم لإعادة ترتيبها يدويًا.</li>
                <li>استخدم زر "🔀 خلط عشوائي" في كل قسم لخلط الأسئلة آليًا.</li>
                <li>زر "🔀 خلط كل الأسئلة" يقوم بخلط جميع أقسام الاختبار مرة واحدة.</li>
                <li>اضغط على "💾 حفظ التغييرات" لتحديث المحتوى في الذاكرة.</li>
                <li>يمكنك تصدير الاختبار كملف PDF أو طباعته مباشرة.</li>
            </ul>
        </div>

        <div class="header-info">
            <div>
                <strong>المدرسة:</strong> <input type="text" id="school" value="Saeed Ibn Alas Intermediate School">
            </div>
            <div>
                <strong>الصف:</strong> <input type="text" id="grade" value="3rd Intermediate Grade">
            </div>
            <div>
                <strong>الفصل الدراسي:</strong> <input type="text" id="term" value="2nd Term rescheduled Exam">
            </div>
        </div>

        <!-- Grammar Section -->
        <div class="section" id="grammar-section">
            <div class="section-header">
                <h2>📘 Grammar</h2>
                <div class="section-controls">
                    <button class="btn-shuffle no-print" onclick="shuffleQuestions('grammar')">🔀 خلط عشوائي</button>
                    <button class="btn-add no-print" onclick="addQuestion('grammar')">+ إضافة سؤال</button>
                </div>
            </div>
            <div id="grammar-questions">
                <!-- سيتم ملؤها بالجافاسكريبت -->
            </div>
        </div>

        <!-- Orthography Section -->
        <div class="section" id="orthography-section">
            <div class="section-header">
                <h2>🔤 Orthography</h2>
                <div class="section-controls">
                    <button class="btn-shuffle no-print" onclick="shuffleQuestions('orthography')">🔀 خلط عشوائي</button>
                    <button class="btn-add no-print" onclick="addQuestion('orthography')">+ إضافة سؤال</button>
                </div>
            </div>
            <div id="orthography-questions">
                <!-- سيتم ملؤها بالجافاسكريبت -->
            </div>
        </div>

        <!-- Vocabulary Matching Section -->
        <div class="section">
            <div class="section-header">
                <h2>🖼️ Vocabulary Matching</h2>
                <div class="section-controls">
                    <button class="btn-shuffle no-print" onclick="shuffleQuestions('matching')">🔀 خلط عشوائي</button>
                    <button class="btn-add no-print" onclick="addMatchingPair()">+ إضافة تطابق</button>
                </div>
            </div>
            <div id="matching-questions">
                <!-- سيتم ملؤها بالجافاسكريبت -->
            </div>
        </div>

        <!-- Reading Section -->
        <div class="section">
            <div class="section-header">
                <h2>📖 Reading</h2>
                <div class="section-controls">
                    <button class="btn-shuffle no-print" onclick="shuffleQuestions('reading')">🔀 خلط عشوائي</button>
                    <button class="btn-add no-print" onclick="addReadingQuestion()">+ إضافة سؤال</button>
                </div>
            </div>
            <textarea id="reading-text" rows="5">King Salman bin Abdulaziz was born in Riyadh. He studied religion, science, and the Holy Qur'an at the Princes' School. He became King of Saudi Arabia in 2015. He helped Riyadh grow from a small town into a major modern city. He also supported humanitarian and cultural projects inside and outside the Kingdom.</textarea>
            <div id="reading-questions">
                <!-- سيتم ملؤها بالجافاسكريبت -->
            </div>
        </div>

        <!-- Writing Section -->
        <div class="section">
            <div class="section-header">
                <h2>✍️ Writing</h2>
                <div class="section-controls">
                    <button class="btn-shuffle no-print" onclick="shuffleWritingWords()">🔀 خلط الكلمات</button>
                </div>
            </div>
            <textarea id="writing-prompt" rows="3">Write a coherent paragraph of 3-5 sentences using 8 words from the following list:</textarea>
            <input type="text" id="word-list" value="(enjoy – fitness – work out – spend time – lifestyle – herbal tea – puzzle – fan)" style="margin-top:10px; width:100%;">
        </div>

        <!-- Controls -->
        <div class="controls no-print">
            <button id="shuffleAllBtn" onclick="shuffleAllSections()">🔀 خلط كل الأسئلة</button>
            <button id="saveBtn" onclick="saveChanges()">💾 حفظ التغييرات</button>
            <button id="resetBtn" onclick="resetToOriginal()">🔄 استعادة الأصل</button>
            <button id="pdfBtn" onclick="generatePDF()">📥 تصدير PDF</button>
            <button id="printBtn" onclick="window.print()">🖨️ طباعة</button>
        </div>
    </div>

    <script>
        // البيانات الأصلية من الملف
        const originalData = {
            grammar: [
                { q: "I. he ___ plays football on weekends.", options: ["does", "always", "has"], correct: 1 },
                { q: "How often ______ drink coffee?", options: ["does", "did", "do"], correct: 0 },
                { q: "My friends are ______ to the museum tomorrow.", options: ["go", "goes", "going"], correct: 2 },
                { q: "They both ______ English very well.", options: ["Speak", "speaks", "speaking"], correct: 0 },
                { q: "I ______ play with toys when I was a child", options: ["use", "used to", "used"], correct: 1 },
                { q: "She was born ______ 2005", options: ["at", "on", "in"], correct: 2 },
                { q: "He is ______ a haircut now.", options: ["get", "got", "getting"], correct: 2 },
                { q: "I have lives here ______ three years.", options: ["since", "for", "From"], correct: 1 },
                { q: "They didn't go to school when they ______ young.", options: ["were", "are", "be"], correct: 0 }
            ],
            orthography: [
                { word: "___ilk_", options: ["N", "M", "T"], correct: 1 },
                { word: "_pota__oes", options: ["N", "T", "H"], correct: 1 },
                { word: "_bre__d_", options: ["e", "a", "u"], correct: 1 },
                { word: "_fu__f_", options: ["e", "i", "o"], correct: 2 },
                { word: "_mang__", options: ["u", "e", "o"], correct: 2 }
            ],
            matching: [
                { img: "(1)", word: "Lamb" },
                { img: "(2)", word: "Shrimp" },
                { img: "(3)", word: "Carrot" },
                { img: "(4)", word: "Bread" },
                { img: "(5)", word: "Avocado" },
                { img: "(6)", word: "Olive oil" },
                { img: "(7)", word: "Cereal" },
                { img: "(8)", word: "Mango" },
                { img: "(9)", word: "Cheese" }
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

        // تهيئة الصفحة
        function init() {
            renderGrammar();
            renderOrthography();
            renderMatching();
            renderReading();
            makeSortable('grammar-questions');
            makeSortable('orthography-questions');
            makeSortable('matching-questions');
            makeSortable('reading-questions');
        }

        function renderGrammar() {
            const container = document.getElementById('grammar-questions');
            container.innerHTML = '';
            currentData.grammar.forEach((item, idx) => {
                const div = document.createElement('div');
                div.className = 'question-block';
                div.setAttribute('data-id', idx);
                div.innerHTML = `
                    <div class="question-number">${idx + 1}</div>
                    <div style="margin-right: 40px;">
                        <input type="text" value="${item.q}" onchange="updateGrammar(${idx}, 'q', this.value)" style="width:100%;">
                        <div class="options">
                            ${item.options.map((opt, optIdx) => `
                                <div class="option">
                                    <input type="radio" name="grammar-${idx}" ${optIdx == item.correct ? 'checked' : ''} 
                                        onchange="updateGrammar(${idx}, 'correct', ${optIdx})">
                                    <input type="text" value="${opt}" onchange="updateGrammar(${idx}, 'options', ${optIdx}, this.value)" style="width:150px;">
                                </div>
                            `).join('')}
                        </div>
                        <button onclick="removeQuestion('grammar', ${idx})" class="btn-delete no-print">حذف السؤال</button>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        function renderOrthography() {
            const container = document.getElementById('orthography-questions');
            container.innerHTML = '';
            currentData.orthography.forEach((item, idx) => {
                const div = document.createElement('div');
                div.className = 'question-block';
                div.setAttribute('data-id', idx);
                div.innerHTML = `
                    <div class="question-number">${idx + 1}</div>
                    <div style="margin-right: 40px;">
                        <strong>الكلمة:</strong>
                        <input type="text" value="${item.word}" onchange="updateOrthography(${idx}, 'word', this.value)" style="width:200px; margin:0 10px;">
                        <div class="options">
                            ${item.options.map((opt, optIdx) => `
                                <div class="option">
                                    <input type="radio" name="ortho-${idx}" ${optIdx == item.correct ? 'checked' : ''} 
                                        onchange="updateOrthography(${idx}, 'correct', ${optIdx})">
                                    <input type="text" value="${opt}" onchange="updateOrthography(${idx}, 'options', ${optIdx}, this.value)" style="width:50px;">
                                    <span>${String.fromCharCode(97 + optIdx)})</span>
                                </div>
                            `).join('')}
                        </div>
                        <button onclick="removeQuestion('orthography', ${idx})" class="btn-delete no-print">حذف السؤال</button>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        function renderMatching() {
            const container = document.getElementById('matching-questions');
            container.innerHTML = '';
            currentData.matching.forEach((item, idx) => {
                const div = document.createElement('div');
                div.className = 'question-block';
                div.setAttribute('data-id', idx);
                div.innerHTML = `
                    <div class="question-number">${idx + 1}</div>
                    <div style="margin-right: 40px;">
                        <strong>رقم الصورة:</strong>
                        <input type="text" value="${item.img}" onchange="updateMatching(${idx}, 'img', this.value)" style="width:80px; margin:0 10px;">
                        <strong>الكلمة:</strong>
                        <input type="text" value="${item.word}" onchange="updateMatching(${idx}, 'word', this.value)" style="width:150px; margin:0 10px;">
                        <button onclick="removeQuestion('matching', ${idx})" class="btn-delete no-print">حذف</button>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        function renderReading() {
            document.getElementById('reading-text').value = currentData.reading.text;
            const container = document.getElementById('reading-questions');
            container.innerHTML = '';
            currentData.reading.questions.forEach((item, idx) => {
                const div = document.createElement('div');
                div.className = 'question-block';
                div.setAttribute('data-id', idx);
                div.innerHTML = `
                    <div class="question-number">${idx + 1}</div>
                    <div style="margin-right: 40px;">
                        <input type="text" value="${item.q}" onchange="updateReadingQuestion(${idx}, 'q', this.value)" style="width:calc(100% - 100px);">
                        <select onchange="updateReadingQuestion(${idx}, 'answer', this.value === 'true')" style="margin-right:10px;">
                            <option value="true" ${item.answer ? 'selected' : ''}>True</option>
                            <option value="false" ${!item.answer ? 'selected' : ''}>False</option>
                        </select>
                        <button onclick="removeQuestion('reading', ${idx})" class="btn-delete no-print">حذف</button>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        // تحديث البيانات
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

        // إضافة أسئلة جديدة
        function addQuestion(type) {
            if (type === 'grammar') {
                currentData.grammar.push({ q: "سؤال جديد؟", options: ["خيار أ", "خيار ب", "خيار ج"], correct: 0 });
                renderGrammar();
            } else if (type === 'orthography') {
                currentData.orthography.push({ word: "___كلمة_", options: ["أ", "ب", "ج"], correct: 0 });
                renderOrthography();
            }
        }

        function addMatchingPair() {
            currentData.matching.push({ img: "(?)", word: "كلمة جديدة" });
            renderMatching();
        }

        function addReadingQuestion() {
            currentData.reading.questions.push({ q: "جملة جديدة؟", answer: true });
            renderReading();
        }

        // حذف سؤال
        function removeQuestion(type, idx) {
            if (confirm("هل أنت متأكد من حذف هذا السؤال؟")) {
                if (type === 'grammar') currentData.grammar.splice(idx, 1);
                else if (type === 'orthography') currentData.orthography.splice(idx, 1);
                else if (type === 'matching') currentData.matching.splice(idx, 1);
                else if (type === 'reading') currentData.reading.questions.splice(idx, 1);
                init();
            }
        }

        // خلط عشوائي للأسئلة داخل قسم معين
        function shuffleQuestions(sectionType) {
            if (confirm(`هل تريد خلط أسئلة قسم ${sectionType} عشوائيًا؟`)) {
                let arrayToShuffle;
                
                switch(sectionType) {
                    case 'grammar':
                        arrayToShuffle = currentData.grammar;
                        break;
                    case 'orthography':
                        arrayToShuffle = currentData.orthography;
                        break;
                    case 'matching':
                        arrayToShuffle = currentData.matching;
                        break;
                    case 'reading':
                        arrayToShuffle = currentData.reading.questions;
                        break;
                    default:
                        return;
                }
                
                // خوارزمية Fisher-Yates للخلط العشوائي
                for (let i = arrayToShuffle.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [arrayToShuffle[i], arrayToShuffle[j]] = [arrayToShuffle[j], arrayToShuffle[i]];
                }
                
                // إعادة التصيير
                switch(sectionType) {
                    case 'grammar':
                        renderGrammar();
                        break;
                    case 'orthography':
                        renderOrthography();
                        break;
                    case 'matching':
                        renderMatching();
                        break;
                    case 'reading':
                        renderReading();
                        break;
                }
                
                alert(`✓ تم خلط أسئلة قسم ${sectionType} عشوائيًا`);
            }
        }

        // خلط جميع الأقسام مرة واحدة
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

        // خلط كلمات قسم الكتابة
        function shuffleWritingWords() {
            const wordsInput = document.getElementById('word-list');
            const words = wordsInput.value.match(/[a-zA-Z\u0600-\u06FF\u0750-\u077F]+/g) || [];
            
            if (words.length > 1) {
                // خلط الكلمات
                for (let i = words.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [words[i], words[j]] = [words[j], words[i]];
                }
                
                // تحديث الحقل
                wordsInput.value = "(" + words.join(" – ") + ")";
                currentData.writing.words = wordsInput.value;
            }
        }

        // جعل العناصر قابلة للسحب والإفلات (ترتيب يدوي)
        function makeSortable(id) {
            const el = document.getElementById(id);
            let dragItem = null;
            
            el.addEventListener('dragstart', e => {
                dragItem = e.target.closest('.question-block');
                e.dataTransfer.effectAllowed = 'move';
                setTimeout(() => dragItem.classList.add('sortable-ghost'), 0);
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
                dragItem.classList.remove('sortable-ghost');
                updateOrderFromDOM(id);
            });
        }

        function getDragAfterElement(container, y) {
            const draggableElements = [...container.querySelectorAll('.question-block:not(.sortable-ghost)')];
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
            
            // إعادة ترتيب البيانات حسب الترتيب الجديد
            if (id === 'grammar-questions') {
                const reordered = newOrder.map(idx => currentData.grammar[idx]);
                currentData.grammar = reordered;
            } else if (id === 'orthography-questions') {
                const reordered = newOrder.map(idx => currentData.orthography[idx]);
                currentData.orthography = reordered;
            } else if (id === 'matching-questions') {
                const reordered = newOrder.map(idx => currentData.matching[idx]);
                currentData.matching = reordered;
            } else if (id === 'reading-questions') {
                const reordered = newOrder.map(idx => currentData.reading.questions[idx]);
                currentData.reading.questions = reordered;
            }
            
            // إعادة التصيير مع تحديث الأرقام
            init();
        }

        // حفظ التغييرات
        function saveChanges() {
            currentData.reading.text = document.getElementById('reading-text').value;
            currentData.writing.prompt = document.getElementById('writing-prompt').value;
            currentData.writing.words = document.getElementById('word-list').value;
            localStorage.setItem('examData', JSON.stringify(currentData));
            alert('✅ تم حفظ التغييرات في الذاكرة المحلية.');
        }

        // استعادة البيانات الأصلية
        function resetToOriginal() {
            if (confirm('هل أنت متأكد من استعادة النسخة الأصلية؟ سيتم فقدان جميع التغييرات.')) {
                currentData = JSON.parse(JSON.stringify(originalData));
                init();
                document.getElementById('reading-text').value = currentData.reading.text;
                document.getElementById('writing-prompt').value = currentData.writing.prompt;
                document.getElementById('word-list').value = currentData.writing.words;
                alert('تم الاستعادة.');
            }
        }

        // إنشاء PDF
        function generatePDF() {
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();
            
            // العنوان
            doc.setFontSize(18);
            doc.text("Kingdom of Saudi Arabia Ministry of Education", 105, 15, null, null, 'center');
            doc.setFontSize(14);
            doc.text(document.getElementById('school').value, 105, 25, null, null, 'center');
            doc.text(document.getElementById('grade').value + " - " + document.getElementById('term').value, 105, 32, null, null, 'center');
            doc.line(20, 40, 190, 40);
            
            let y = 50;
            
            // قسم Grammar
            doc.setFontSize(16);
            doc.text("Grammar", 20, y); y += 10;
            doc.setFontSize(12);
            currentData.grammar.forEach((q, i) => {
                doc.text(`${i+1}. ${q.q}`, 20, y); y += 8;
                q.options.forEach((opt, j) => {
                    const letter = String.fromCharCode(97 + j);
                    doc.text(`   ${letter}) ${opt}`, 25, y); y += 6;
                });
                y += 4;
            });
            
            // قسم Orthography
            y += 5;
            doc.setFontSize(16);
            doc.text("Orthography", 20, y); y += 10;
            doc.setFontSize(12);
            currentData.orthography.forEach((item, i) => {
                doc.text(`${i+1}. ${item.word}`, 20, y); y += 8;
                item.options.forEach((opt, j) => {
                    const letter = String.fromCharCode(97 + j);
                    doc.text(`   ${letter}) ${opt}`, 25, y); y += 6;
                });
                y += 4;
            });
            
            // قسم Matching
            y += 5;
            doc.setFontSize(16);
            doc.text("Vocabulary Matching", 20, y); y += 10;
            doc.setFontSize(12);
            currentData.matching.forEach((item, i) => {
                doc.text(`${i+1}. ${item.img} - ${item.word}`, 20, y); y += 8;
            });
            
            // قسم Reading
            y += 5;
            doc.setFontSize(16);
            doc.text("Reading", 20, y); y += 10;
            doc.setFontSize(12);
            const readingLines = doc.splitTextToSize(currentData.reading.text, 170);
            readingLines.forEach(line => {
                doc.text(line, 20, y); y += 7;
            });
            y += 5;
            currentData.reading.questions.forEach((q, i) => {
                doc.text(`${i+1}. ${q.q} (True/False)`, 20, y); y += 8;
            });
            
            // قسم Writing
            y += 5;
            doc.setFontSize(16);
            doc.text("Writing", 20, y); y += 10;
            doc.setFontSize(12);
            doc.text(currentData.writing.prompt, 20, y); y += 7;
            doc.text(currentData.writing.words, 20, y); y += 15;
            doc.text("________________________________________________________________________________", 20, y);
            y += 10;
            doc.text("________________________________________________________________________________", 20, y);
            y += 10;
            doc.text("________________________________________________________________________________", 20, y);
            y += 10;
            doc.text("________________________________________________________________________________", 20, y);
            
            doc.save('exam_modified_' + new Date().toISOString().slice(0,10) + '.pdf');
        }

        // تحميل البيانات المحفوظة
        window.onload = function() {
            const saved = localStorage.getItem('examData');
            if (saved) {
                currentData = JSON.parse(saved);
                document.getElementById('reading-text').value = currentData.reading.text;
                document.getElementById('writing-prompt').value = currentData.writing.prompt;
                document.getElementById('word-list').value = currentData.writing.words;
            }
            init();
        };
    </script>
</body>
</html>
