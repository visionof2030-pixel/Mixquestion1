<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>أداة إعداد التقارير</title>

<style>
@font-face {
  font-family: 'KufamLocal';
  src: url('static/Kufam-Regular.ttf') format('truetype');
}
@font-face {
  font-family: 'KufamLocal';
  src: url('static/Kufam-Bold.ttf') format('truetype');
  font-weight: 700;
}

body{
  font-family:'KufamLocal',sans-serif;
  background:#f2f7f6;
  margin:0;
  padding:20px;
}

/* ===== الأداة ===== */
.tool{
  max-width:900px;
  margin:auto;
  background:white;
  padding:30px;
  border-radius:20px;
}

.tool h2{
  text-align:center;
  color:#0a3b40;
  margin-bottom:10px;
}

.tool label{
  font-weight:700;
  margin-top:14px;
  display:block;
}

.tool input,
.tool textarea{
  width:100%;
  padding:12px;
  margin-top:6px;
  border-radius:12px;
  border:2px solid #cfd8dc;
  font-family:inherit;
}

.counter{
  font-size:11px;
  color:#4f6f68;
  margin-top:3px;
}

.hint{
  font-size:11px;
  color:#777;
}

button{
  margin-top:14px;
  padding:14px;
  width:100%;
  background:#0a3b40;
  color:white;
  border:none;
  border-radius:12px;
  font-size:16px;
  font-weight:700;
  cursor:pointer;
}

.reset-btn{background:#9e9e9e}

/* ===== التقرير ===== */
.report{display:none}

@page{size:A4;margin:14mm}

@media print{

body{background:white;padding:0}
.tool{display:none}
.report{display:block}

/* هيدر صغير جدًا */
.header{
  background:#0a3b40;
  color:white;
  padding:4px;
  border-radius:6px;
  text-align:center;
  font-size:11px;
  margin-bottom:8px;
}

.header img{
  width:26px;
  vertical-align:middle;
  margin-left:6px;
}

/* معلومات */
.info-grid{
  display:grid;
  grid-template-columns:repeat(5,1fr);
  gap:8px;
  margin-bottom:12px;
}

.info-box{
  border:2px solid #cfd8dc;
  border-radius:10px;
  padding:6px;
  text-align:center;
  font-size:11px;
}

.info-box span{
  display:block;
  background:#0a3b40;
  color:white;
  border-radius:6px;
  padding:3px;
  font-weight:700;
  margin-bottom:3px;
}

/* المحتوى */
.grid-desc{
  display:flex;
  gap:10px;
  margin-bottom:12px;
}

.desc-box{
  flex:1;
  border:2px solid #cfd8dc;
  border-radius:12px;
  padding:12px;
  background:#f9fbfb;
  font-size:12px;
  display:flex;
  flex-direction:column;
}

.desc-box strong{
  margin-bottom:6px;
  border-bottom:1px dashed #cfd8dc;
  padding-bottom:4px;
  color:#0a3b40;
}

.desc-box p{
  white-space:pre-line;
  flex:1;
}

.vertical{
  width:40px;
  background:#eef3f1;
  border-radius:12px;
  display:flex;
  align-items:center;
  justify-content:center;
  font-weight:700;
}

/* الصور */
.images{
  display:grid;
  grid-template-columns:repeat(2,1fr);
  gap:10px;
  margin-top:10px;
}

.images img{
  width:100%;
  height:140px;
  object-fit:cover;
  border-radius:8px;
}

/* التوقيعات */
.signatures{
  margin-top:20px;
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:30px;
}

.signature-line{
  border-bottom:2px solid #333;
  height:26px;
  margin:8px 0;
}
}
</style>
</head>

<body>

<!-- ===== الأداة ===== -->
<div class="tool">
<h2>أداة إعداد التقارير</h2>

<label>المنطقة التعليمية</label>
<input oninput="sync('region',this.value)">

<label>عنوان التقرير</label>
<input oninput="sync('title',this.value)">

<label>تاريخ التنفيذ</label>
<input oninput="sync('date',this.value)">

<label>المستهدفون</label>
<input oninput="sync('target',this.value)">

<label>عدد المستفيدين</label>
<input oninput="sync('count',this.value)">

<label>وصف مختصر</label>
<textarea oninput="limitLines(this,'desc1','c1')"></textarea>
<div class="counter" id="c1">0 / 10 أسطر</div>

<label>إجراءات التنفيذ</label>
<textarea oninput="limitLines(this,'desc2','c2')"></textarea>
<div class="counter" id="c2">0 / 10 أسطر</div>

<label>النتائج</label>
<textarea oninput="limitLines(this,'desc3','c3')"></textarea>
<div class="counter" id="c3">0 / 10 أسطر</div>

<label>التوصيات</label>
<textarea oninput="limitLines(this,'desc4','c4')"></textarea>
<div class="counter" id="c4">0 / 10 أسطر</div>

<label>إرفاق الصور (صورتين فقط)</label>
<input type="file" id="imagesInput" accept="image/*" multiple>
<div class="hint">يسمح بإرفاق صورتين فقط</div>

<button onclick="printReport()">تصدير PDF</button>
<button class="reset-btn" onclick="resetForm()">مسح جميع الخانات</button>
</div>

<!-- ===== التقرير ===== -->
<div class="report">

<div class="header">
<img src="https://i.ibb.co/kshh2Tf8/IMG-2109.jpg">
وزارة التعليم
</div>

<div class="info-grid">
<div class="info-box"><span>المنطقة</span><div id="region"></div></div>
<div class="info-box"><span>عنوان التقرير</span><div id="title"></div></div>
<div class="info-box"><span>تاريخ التنفيذ</span><div id="date"></div></div>
<div class="info-box"><span>المستهدفون</span><div id="target"></div></div>
<div class="info-box"><span>عدد المستفيدين</span><div id="count"></div></div>
</div>

<div class="grid-desc">
<div class="desc-box"><strong>وصف مختصر</strong><p id="desc1"></p></div>
<div class="vertical">⇄</div>
<div class="desc-box"><strong>إجراءات التنفيذ</strong><p id="desc2"></p></div>
</div>

<div class="grid-desc">
<div class="desc-box"><strong>النتائج</strong><p id="desc3"></p></div>
<div class="vertical">⇄</div>
<div class="desc-box"><strong>التوصيات</strong><p id="desc4"></p></div>
</div>

<h3 style="text-align:center;margin-top:10px">شواهد الصور</h3>
<div class="images" id="imagesContainer"></div>

<div class="signatures">
<div>اسم المعلم<div class="signature-line"></div>التوقيع</div>
<div>مدير المدرسة<div class="signature-line"></div>التوقيع</div>
</div>

</div>

<script>
const imagesInput=document.getElementById('imagesInput');
const imagesContainer=document.getElementById('imagesContainer');

function sync(id,val){
  document.getElementById(id).textContent=val;
}

function limitLines(el,target,counter){
  let lines=el.value.split('\n');
  if(lines.length>10){
    el.value=lines.slice(0,10).join('\n');
    lines=el.value.split('\n');
  }
  document.getElementById(counter).textContent=`${lines.length} / 10 أسطر`;
  document.getElementById(target).textContent=el.value;
}

imagesInput.addEventListener('change',e=>{
  imagesContainer.innerHTML='';
  const files=[...e.target.files];
  if(files.length>2){
    alert('يسمح بإرفاق صورتين فقط');
    imagesInput.value='';
    return;
  }
  files.forEach((f,i)=>{
    const r=new FileReader();
    r.onload=ev=>{
      const img=document.createElement('img');
      img.src=ev.target.result;
      imagesContainer.appendChild(img);
    };
    r.readAsDataURL(f);
  });
});

function printReport(){
  window.print();
}

function resetForm(){
  if(!confirm('مسح جميع الخانات؟'))return;
  document.querySelectorAll('input,textarea').forEach(e=>e.value='');
  document.querySelectorAll('[id]').forEach(e=>e.textContent='');
  imagesContainer.innerHTML='';
}
</script>

</body>
</html>