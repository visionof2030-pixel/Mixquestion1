<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>خلط الأسئلة المختارة فقط (مع الحفاظ على PDF)</title>

<script src="https://cdn.jsdelivr.net/npm/pdf-lib@1.17.1/dist/pdf-lib.min.js"></script>

<style>
body{
    font-family: Arial;
    background:#f5f7fa;
    padding:30px;
}
.container{
    max-width:900px;
    margin:auto;
    background:#fff;
    padding:25px;
    border-radius:10px;
}
.page{
    padding:10px;
    border:1px solid #ddd;
    margin-bottom:8px;
    border-radius:6px;
}
button{
    padding:12px 20px;
    font-size:16px;
    cursor:pointer;
    background:#3498db;
    color:#fff;
    border:none;
    border-radius:6px;
}
button:disabled{
    background:#aaa;
}
</style>
</head>

<body>
<div class="container">
    <h2>خلط الأسئلة المختارة فقط (PDF بدون تغيير)</h2>

    <input type="file" id="pdfInput" accept="application/pdf"><br><br>

    <div id="pages"></div>

    <br>
    <button onclick="shuffleSelected()">خلط وتنزيل PDF</button>
</div>

<script>
let pdfDoc;
let selectedPages = new Set();

document.getElementById("pdfInput").addEventListener("change", async e => {
    const file = e.target.files[0];
    if(!file) return;

    const bytes = await file.arrayBuffer();
    pdfDoc = await PDFLib.PDFDocument.load(bytes);

    const pagesDiv = document.getElementById("pages");
    pagesDiv.innerHTML = "";

    pdfDoc.getPages().forEach((_, i) => {
        const div = document.createElement("div");
        div.className = "page";
        div.innerHTML = `
            <label>
                <input type="checkbox" onchange="toggle(${i},this.checked)">


                سؤال / صفحة رقم ${i+1}
            </label>
        `;
        pagesDiv.appendChild(div);
    });
});

function toggle(i, checked){
    checked ? selectedPages.add(i) : selectedPages.delete(i);
}

async function shuffleSelected(){
    if(selectedPages.size < 2){
        alert("اختر صفحتين على الأقل");
        return;
    }

    const originalBytes = await document.getElementById("pdfInput").files[0].arrayBuffer();
    const originalPdf = await PDFLib.PDFDocument.load(originalBytes);
    const newPdf = await PDFLib.PDFDocument.create();

    const total = originalPdf.getPageCount();
    let selected = Array.from(selectedPages);

    // خلط الصفحات المختارة فقط
    for(let i=selected.length-1;i>0;i--){
        const j = Math.floor(Math.random()*(i+1));
        [selected[i],selected[j]]=[selected[j],selected[i]];
    }

    let selIndex = 0;

    for(let i=0;i<total;i++){
        let pageIndex = selectedPages.has(i) ? selected[selIndex++] : i;
        const [p] = await newPdf.copyPages(originalPdf,[pageIndex]);
        newPdf.addPage(p);
    }

    const bytes = await newPdf.save();
    const blob = new Blob([bytes],{type:"application/pdf"});
    const a = document.createElement("a");
    a.href = URL.createObjectURL(blob);
    a.download = "PDF_مخلوط_نفس_التنسيق.pdf";
    a.click();
}
</script>
</body>
</html
>
