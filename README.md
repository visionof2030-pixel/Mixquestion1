<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>أداة إعداد التقارير</title>

<style>
@font-face{
  font-family:'KufamLocal';
  src:url('static/Kufam-Regular.ttf') format('truetype');
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
  padding:28px;
  border-radius:18px;
}
.tool h2{
  text-align:center;
  color:#0a3b40;
  margin-bottom:12px;
}
label{
  font-weight:700;
  margin-top:12px;
  display:block;
}
input,textarea{
  width:100%;
  padding:11px;
  margin-top:6px;
  border-radius:10px;
  border:2px solid #cfd8dc;
  font-family:inherit;
}
textarea{resize:none;}
.counter{
  font-size:11px;
  margin-top:3px;
  color:#4f6f68;
}
.counter.limit{color:#c62828;font-weight:700;}
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
.report{display:none;}
@page{size:A4;margin:14mm;}

@media print{
body{background:white;padding:0}
.tool{display:none}
.report{display:block}

/* ===== الهيدر المصغر ===== */
.header{
  background:#0a3b40;
  color:white;
  padding:4px 6px;
  border-radius:6px;
  text-align:center;
  font-size:11px;
  margin-bottom:8px;
}

/* ===== معلومات التقرير ===== */
.info-grid{
  display:grid;
  grid-template-columns:repeat(5,1fr);
  gap:6px;
  margin-bottom:10px;
}
.info-box{
  border:2px solid #cfd8dc;
  border-radius:8px;
  padding:5px;
  text-align:center;
  font-size:11px;
}
.info-box span{
  display:block;
  background:#0a3b40;
  color:white;
  border-radius:6px;
  padding:2px;
  font-weight:700;
  margin-bottom:3px;
}

/* ===== المحتوى ===== */
.grid-desc{
  display:flex;
  gap:8px;
  margin-bottom:8px;
}

.desc-box{
  border:2px solid #cfd8dc;
  border-radius:10px;
  padding:8px;
  background:#f9fbfb;
  font-size:12px;
  display:flex;
  flex-direction:column;
}
.desc-box.big{min-height:110px;flex:1}
.desc-box.small{min-height:80px;flex:1}

.desc-box strong{
  border-bottom:1px dashed #cfd8dc;
  padding-bottom:4px;
  margin-bottom:6px;
  color:#0a3b40;
}
.desc-box p{white-space:pre-line;flex:1}

.vertical{
  width:32px;
  background:#eef3f1;
  border-radius:8px;
  display:flex;
  align-items:center;
  justify-content:center;
  font-weight:700;
}

/* ===== الصور ===== */
.images{
  display:grid;
  grid-template-columns:repeat(2,1fr);
  gap:10px;
  margin-top:12px;
}
.images img{
  width:100%;
  height:120px;
  object-fit:cover;
  border-radius:8px;
}

/* ===== التوقيعات ===== */
.signatures{
  margin-top:22px;
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:40px;
  border-top:2px solid #cfd8dc;
  padding-top:14px;
}
.signature-box{
  text-align:center;
  font-size:12px;
}
.signature-line{
  border-bottom:2px solid #000;
  height:26px;
  margin:8px 0;
}
}
</style>
</head>

<body>

<div class="tool">
<h2>أداة إعداد التقارير</h2>

<label>إدارة التعليم</label>
<input oninput="sync('edu',this.value)">

<label>اسم المدرسة</label>
<input oninput="sync('school',this.value)">

<label>البند التربوي</label>
<input oninput="sync('axis',this.value)">

<label>عنوان التقرير</label>
<input oninput="sync('title',this.value)">

<label>تاريخ التنفيذ</label>
<input oninput="sync('date',this.value)">

<label>المستهدفون</label>
<input oninput="sync('target',this.value)">

<label>عدد المستفيدين</label>
<input oninput="sync('count',this.value)">

<label>اسم المعلم</label>
<input oninput="sync('teacher',this.value)">

<label>اسم مدير المدرسة</label>
<input oninput="sync('principal',this.value)">

<label>وصف مختصر (15 كلمة)</label>
<textarea oninput="limitWords(this,'desc1','c1')"></textarea>
<div class="counter" id="c1">0 / 15 كلمة</div>

<label>إجراءات التنفيذ (15 كلمة)</label>
<textarea oninput="limitWords(this,'desc2','c2')"></textarea>
<div class="counter" id="c2">0 / 15 كلمة</div>

<label>النتائج (15 كلمة)</label>
<textarea oninput="limitWords(this,'desc3','c3')"></textarea>
<div class="counter" id="c3">0 / 15 كلمة</div>

<label>التوصيات (15 كلمة)</label>
<textarea oninput="limitWords(this,'desc4','c4')"></textarea>
<div class="counter" id="c4">0 / 15 كلمة</div>

<label>إرفاق الصور (صورتان كحد أقصى)</label>
<input type="file" id="imagesInput" multiple accept="image/*">

<button onclick="window.print()">تصدير PDF</button>
<button class="reset-btn" onclick="resetForm()">مسح جميع الخانات</button>
</div>

<div class="report">

<div class="header">
<div id="edu"></div>
<div id="school"></div>
</div>

<div class="info-grid">
<div class="info-box"><span>البند التربوي</span><div id="axis"></div></div>
<div class="info-box"><span>عنوان التقرير</span><div id="title"></div></div>
<div class="info-box"><span>تاريخ التنفيذ</span><div id="date"></div></div>
<div class="info-box"><span>المستهدفون</span><div id="target"></div></div>
<div class="info-box"><span>عدد المستفيدين</span><div id="count"></div></div>
</div>

<div class="grid-desc">
<div class="desc-box big"><strong>وصف مختصر</strong><p id="desc1"></p></div>
<div class="vertical">⇄</div>
<div class="desc-box big"><strong>إجراءات التنفيذ</strong><p id="desc2"></p></div>
</div>

<div class="grid-desc">
<div class="desc-box small"><strong>النتائج</strong><p id="desc3"></p></div>
<div class="vertical">⇄</div>
<div class="desc-box small"><strong>التوصيات</strong><p id="desc4"></p></div>
</div>

<div class="images" id="imagesContainer"></div>

<div class="signatures">
<div class="signature-box">
اسم المعلم: <strong id="teacher"></strong>
<div class="signature-line"></div>
التوقيع
</div>
<div class="signature-box">
مدير المدرسة: <strong id="principal"></strong>
<div class="signature-line"></div>
التوقيع
</div>
</div>

</div>

<script>
function sync(id,val){document.getElementById(id).textContent=val}

function limitWords(el,target,counterId){
  let words=el.value.trim().replace(/\s+/g,' ').split(' ').filter(w=>w);
  if(words.length>15){
    words=words.slice(0,15);
    el.value=words.join(' ');
  }
  const c=document.getElementById(counterId);
  c.textContent=`${words.length} / 15 كلمة`;
  c.classList.toggle('limit',words.length===15);
  document.getElementById(target).textContent=el.value;
}

const imagesInput=document.getElementById('imagesInput');
const imagesContainer=document.getElementById('imagesContainer');

imagesInput.addEventListener('change',e=>{
  imagesContainer.innerHTML='';
  const files=[...e.target.files];
  if(files.length>2){
    alert('يسمح بإرفاق صورتين فقط');
    imagesInput.value='';
    return;
  }
  files.forEach(f=>{
    const r=new FileReader();
    r.onload=ev=>{
      const img=document.createElement('img');
      img.src=ev.target.result;
      imagesContainer.appendChild(img);
    };
    r.readAsDataURL(f);
  });
});

function resetForm(){
  if(!confirm('مسح جميع الخانات؟'))return;
  document.querySelectorAll('input,textarea').forEach(e=>e.value='');
  document.querySelectorAll('[id]').forEach(e=>e.textContent='');
  imagesContainer.innerHTML='';
}
</script>

</body>
</html>