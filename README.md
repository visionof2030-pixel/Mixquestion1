<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>أداة إعداد التقارير</title>

<style>
@font-face{
  font-family:'KufamLocal';
  src:url('static/Kufam-Regular.ttf') format('truetype');
}
@font-face{
  font-family:'KufamLocal';
  src:url('static/Kufam-Bold.ttf') format('truetype');
  font-weight:700;
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
}

.tool label{
  font-weight:700;
  margin-top:14px;
  display:block;
}

.tool input,
.tool textarea{
  width:100%;
  padding:10px;
  margin-top:6px;
  border-radius:10px;
  border:2px solid #cfd8dc;
  font-family:inherit;
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

/* ===== الشريط العلوي ===== */
.top-bar{
  font-size:9.5px;
  color:#0a3b40;
  text-align:center;
  margin-bottom:4px;
  border-bottom:1px solid #cfd8dc;
  padding-bottom:2px;
}

/* ===== الهيدر المصغّر جدًا ===== */
.header{
  background:#0a3b40;
  color:white;
  padding:4px;
  border-radius:6px;
  text-align:center;
  margin-bottom:8px;
}

.header img{
  width:22px;
  vertical-align:middle;
  margin-left:6px;
}

.header span{
  font-size:11px;
  font-weight:700;
}

/* ===== مربعات المعلومات ===== */
.info-grid{
  display:grid;
  grid-template-columns:repeat(5,1fr);
  gap:6px;
  margin-bottom:12px;
}

.info-box{
  border:2px solid #cfd8dc;
  border-radius:8px;
  padding:5px;
  text-align:center;
  font-size:10.5px;
}

.info-box span{
  display:block;
  background:#0a3b40;
  color:white;
  border-radius:6px;
  padding:2px;
  font-weight:700;
  margin-bottom:2px;
}

/* ===== المحتوى ===== */
.grid-desc{
  display:flex;
  gap:8px;
  min-height:130px;
}

.desc-box{
  flex:1;
  border:2px solid #cfd8dc;
  border-radius:10px;
  padding:8px;
  background:#f9fbfb;
  font-size:12px;
  line-height:1.6;
}

.desc-box strong{
  border-bottom:1px dashed #cfd8dc;
  display:block;
  margin-bottom:4px;
  color:#0a3b40;
}

.vertical{
  width:40px;
  background:#eef3f1;
  border-radius:10px;
  display:flex;
  align-items:center;
  justify-content:center;
  font-size:12px;
  font-weight:700;
}

/* ===== التوقيعات ===== */
.signatures{
  margin-top:24px;
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:30px;
  text-align:center;
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

<div class="tool">
<h2>أداة إعداد التقارير</h2>

<label>رقم التقرير</label>
<input oninput="sync('repNo',this.value)">

<label>العام الدراسي</label>
<input oninput="sync('year',this.value)">

<label>الفصل الدراسي</label>
<input oninput="sync('term',this.value)">

<label>جهة الإعداد</label>
<input oninput="sync('org',this.value)">

<label>رمز البند التربوي</label>
<input oninput="sync('code',this.value)">

<label>اسم المدرسة</label>
<input oninput="sync('school',this.value)">

<label>عنوان التقرير</label>
<input oninput="sync('title',this.value)">

<label>تاريخ التنفيذ</label>
<input oninput="sync('date',this.value)">

<label>المستهدفون</label>
<input oninput="sync('target',this.value)">

<label>عدد المستفيدين</label>
<input oninput="sync('count',this.value)">

<button onclick="window.print()">تصدير PDF</button>
<button class="reset-btn" onclick="location.reload()">مسح</button>
</div>

<div class="report">
<div class="page">

<div class="top-bar">
<span id="repNo"></span> |
<span id="year"></span> |
<span id="term"></span> |
<span id="org"></span> |
<span id="code"></span>
</div>

<div class="header">
<img src="https://i.ibb.co/kshh2Tf8/IMG-2109.jpg">
<span>وزارة التعليم – <span id="school"></span></span>
</div>

<div class="info-grid">
<div class="info-box"><span>العنوان</span><div id="title"></div></div>
<div class="info-box"><span>التاريخ</span><div id="date"></div></div>
<div class="info-box"><span>المستهدفون</span><div id="target"></div></div>
<div class="info-box"><span>عدد المستفيدين</span><div id="count"></div></div>
</div>

<div class="grid-desc">
<div class="desc-box"><strong>وصف مختصر</strong></div>
<div class="vertical">⇄</div>
<div class="desc-box"><strong>إجراءات التنفيذ</strong></div>
</div>

<div class="signatures">
<div>اسم المعلم<div class="signature-line"></div>التوقيع</div>
<div>مدير المدرسة<div class="signature-line"></div>التوقيع</div>
</div>

</div>
</div>

<script>
function sync(id,val){
  document.getElementById(id).textContent=val;
}
</script>

</body>
</html>