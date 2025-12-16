# Mixquestion1
<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <title>خلط فقرات PDF</title>
    <script src="https://cdn.jsdelivr.net/npm/pdf-lib@1.17.1/dist/pdf-lib.min.js"></script>
</head>
<body dir="rtl">
    <h2>أداة خلط فقرات ملف PDF</h2>
    <input type="file" id="pdfInput" accept="application/pdf">
    <button onclick="shufflePdf()">خلط الفقرات وتنزيل الملف</button>
    
    <script>
        async function shufflePdf() {
            const fileInput = document.getElementById('pdfInput');
            if (fileInput.files.length === 0) {
                alert('يرجى اختيار ملف PDF');
                return;
            }

            const file = fileInput.files[0];
            const arrayBuffer = await file.arrayBuffer();
            const pdfDoc = await PDFLib.PDFDocument.load(arrayBuffer);
            
            const pages = pdfDoc.getPages();
            // هنا تقدر تضيف منطق إعادة ترتيب الفقرات داخل الصفحات كما تريد.
            // حالياً سنقوم بمجرد إعادة ترتيب الصفحات عشوائياً كمثال.

            const shuffledPages = pages.sort(() => Math.random() - 0.5);

            const newPdfDoc = await PDFLib.PDFDocument.create();
            for (let page of shuffledPages) {
                const [copiedPage] = await newPdfDoc.copyPages(pdfDoc, [page.getIndex()]);
                newPdfDoc.addPage(copiedPage);
            }

            const pdfBytes = await newPdfDoc.save();
            const blob = new Blob([pdfBytes], { type: 'application/pdf' });
            const link = document.createElement('a');
            link.href = URL.createObjectURL(blob);
            link.download = 'mixed-questions.pdf';
            link.click();
        }
    </script>
</body>
</html>
