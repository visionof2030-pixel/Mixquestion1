<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0, user-scalable=yes">
<title>تقاريرك - النظام المتكامل (موحد الأدوار)</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<style>
/* جميع الأنماط كما هي دون تغيير (لن أكررها للاختصار) */
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800;900&display=swap');
:root { --primary: #066d4d; --primary-dark: #044a35; --primary-light: #0a9d72; --secondary: #ffd166; --secondary-dark: #ffc145; --danger: #ff6b6b; --success: #25D366; --gray-light: #f8fdfa; --gray: #e0f0ea; --text-dark: #083024; --text-light: #666; --white: #ffffff; --shadow: 0 10px 30px rgba(4, 74, 53, 0.12); --border: #d4ebe2; }
* { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
html, body { font-family: 'Cairo', sans-serif; background: linear-gradient(135deg, #f0f9f6 0%, #e8f4f0 50%, #d4ebe2 100%); direction: rtl; overflow-x: hidden; min-height: 100vh; -webkit-text-size-adjust: 100%; -moz-text-size-adjust: 100%; -ms-text-size-adjust: 100%; text-size-adjust: 100%; touch-action: manipulation; }
.wrapper { max-width: 900px; margin: auto; padding: 20px; width: 100%; }
.top-marquee { position: fixed; top: 0; left: 0; right: 0; width: 100%; background: linear-gradient(135deg, #022e22 0%, #044a35 100%); color: #fff; padding: 10px 5px; font-size: 14px; z-index: 300; overflow: hidden; height: auto; min-height: 45px; white-space: nowrap; border-bottom: 3px solid #ffd166; box-shadow: 0 4px 12px rgba(2, 46, 34, 0.25); display: flex; align-items: center; line-height: 1.5; }
.marquee-inner { display: inline-block; padding-left: 2%; animation: newsScroll 30s linear infinite; color: #e8f4f0; font-weight: 600; white-space: nowrap; }
@keyframes newsScroll { 0% { transform: translateX(-100%); } 100% { transform: translateX(100%); } }
.top-marquee:hover .marquee-inner { animation-play-state: paused; }
.top-small-buttons button, .main-buttons-bar button, #aiFillFloatingBtn { -webkit-tap-highlight-color: rgba(0, 0, 0, 0); box-sizing: border-box; outline: none; -webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale; user-select: none; transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1); }
.top-small-buttons { position: fixed; top: 45px; left: 0; right: 0; width: 100%; z-index: 250; background: linear-gradient(135deg, #ffffff 0%, #f5fcf9 100%); padding: 8px 20px; display: flex; justify-content: center; align-items: center; border-bottom: 1px solid #e0f0ea; box-shadow: 0 2px 8px rgba(4, 74, 53, 0.08); box-sizing: border-box; }
.small-buttons-grid { display: flex; gap: 8px; width: 100%; max-width: 600px; justify-content: center; }
.small-btn { border: 2px solid; padding: 6px 4px; font-size: 10px; border-radius: 8px; cursor: pointer; transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1); font-weight: 700; display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 3px; min-height: 45px; min-width: 90px; box-shadow: 0 1px 4px rgba(0,0,0,0.1); flex: 1; position: relative; overflow: hidden; }
.small-btn:active { box-shadow: 0 0 0 2px rgba(255,255,255,0.5), inset 0 3px 5px rgba(0,0,0,0.1) !important; filter: brightness(0.95); }
#saveTeacherBtn { background: linear-gradient(135deg, #4f7bff 0%, #3b5bdb 100%); color: white; border-color: #3b5bdb; }
#clearBtn { background: linear-gradient(135deg, #ffd166 0%, #ffc145 100%); color: #5a3e00; border-color: #ffc145; }
#savedReportsBtn { background: linear-gradient(135deg, #9D50BB 0%, #6E48AA 100%); color: white; border-color: #6E48AA; }
#settingsBtn { background: linear-gradient(135deg, #718096 0%, #4a5568 100%); color: white; border-color: #4a5568; }
.small-btn-icon { font-size: 12px; color: white; transition: none; }
.small-btn .small-btn-text { font-size: 9px; font-weight: 800; text-align: center; line-height: 1.1; white-space: nowrap; transition: none; }
.main-buttons-bar { position: fixed; top: 98px; left: 0; right: 0; width: 100%; z-index: 240; background: linear-gradient(135deg, #f8fdfa 0%, #f0f9f6 100%); padding: 10px 20px; display: flex; justify-content: center; align-items: center; box-shadow: 0 3px 10px rgba(4, 74, 53, 0.1); border-bottom: 1px solid #d4ebe2; box-sizing: border-box; }
.main-buttons-grid { display: flex; gap: 20px; width: 100%; max-width: 350px; justify-content: center; }
.main-btn { border: 2px solid; padding: 12px 10px; font-size: 13px; border-radius: 12px; cursor: pointer; transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1); font-weight: 700; display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 6px; min-height: 65px; min-width: 130px; box-shadow: 0 3px 10px rgba(0,0,0,0.15); flex: 1; position: relative; overflow: hidden; }
.main-btn:active { box-shadow: 0 0 0 3px rgba(255,255,255,0.5), inset 0 4px 6px rgba(0,0,0,0.1) !important; filter: brightness(0.95); }
#pdfBtn { background: linear-gradient(135deg, #ff6b6b 0%, #ee5a52 100%); color: white; border-color: #ee5a52; }
#whatsappBtn { background: linear-gradient(135deg, #25D366 0%, #1da851 100%); color: white; border-color: #1da851; }
.main-btn-icon { font-size: 18px; color: white; transition: none; }
.main-btn .main-btn-text { font-size: 12px; font-weight: 800; text-align: center; line-height: 1.2; white-space: nowrap; transition: none; }
#aiFillFloatingBtn { position: fixed; bottom: 30px; left: 30px; width: 100px; height: 100px; color: white; border: none; border-radius: 50%; font-size: 16px; font-weight: 900; cursor: pointer; transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1); display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 6px; border: 4px solid rgba(255, 255, 255, 0.7); z-index: 1000; overflow: hidden; transform: translateY(0); animation: floatButton 3s ease-in-out infinite; background: linear-gradient(135deg, #9D50BB 0%, #6E48AA 25%, #533D8B 50%, #3A2569 100%); box-shadow: 0 12px 35px rgba(157, 80, 187, 0.6), 0 0 0 3px rgba(255, 255, 255, 0.3), 0 0 25px rgba(157, 80, 187, 0.5); }
#aiFillFloatingBtn .floating-ai-icon { font-size: 38px; animation: magicalPulse 2s infinite; filter: drop-shadow(0 3px 6px rgba(0, 0, 0, 0.5)); margin-bottom: 2px; color: #FFFFFF; transition: none; }
#aiFillFloatingBtn .floating-ai-text { font-size: 14px; font-weight: 900; letter-spacing: 0.5px; text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5); color: #FFFFFF; background: linear-gradient(45deg, #FFFFFF, #F0F0F0, #FFFFFF); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; background-size: 200% auto; animation: textShine 2s ease-in-out infinite; white-space: nowrap; transition: none; }
@keyframes floatButton { 0%, 100% { transform: translateY(0) rotate(0deg); } 25% { transform: translateY(-12px) rotate(3deg); } 50% { transform: translateY(0) rotate(0deg); } 75% { transform: translateY(-8px) rotate(-3deg); } }
@keyframes magicalPulse { 0%, 100% { transform: scale(1) rotate(0deg); filter: drop-shadow(0 3px 6px rgba(0, 0, 0, 0.5)) brightness(1); } 25% { transform: scale(1.15) rotate(10deg); filter: drop-shadow(0 5px 10px rgba(255, 255, 255, 0.6)) brightness(1.2); } 50% { transform: scale(1.1) rotate(-5deg); filter: drop-shadow(0 4px 8px rgba(255, 255, 255, 0.5)) brightness(1.1); } 75% { transform: scale(1.18) rotate(5deg); filter: drop-shadow(0 6px 12px rgba(255, 255, 255, 0.7)) brightness(1.3); } }
@keyframes textShine { 0%, 100% { background-position: 0% 50%; text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5); } 50% { background-position: 100% 50%; text-shadow: 0 3px 6px rgba(255, 255, 255, 0.3), 0 0 10px rgba(255, 255, 255, 0.2); } }
#aiFillFloatingBtn.loading { animation: loadingMagicalGlow 1.5s ease-in-out infinite; }
@keyframes loadingMagicalGlow { 0%, 100% { box-shadow: 0 12px 35px rgba(0,0,0,0.4), 0 0 0 4px rgba(255, 255, 255, 0.4), 0 0 30px rgba(0,0,0,0.3); } 50% { box-shadow: 0 18px 45px rgba(0,0,0,0.6), 0 0 0 5px rgba(255, 255, 255, 0.7), 0 0 40px rgba(0,0,0,0.5); } }
#aiFillFloatingBtn.loading .floating-ai-icon { animation: magicalSpin 1.2s linear infinite; }
@keyframes magicalSpin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
#activationScreen { position: fixed; top: 0; left: 0; right: 0; bottom: 0; background: linear-gradient(135deg, #022e22, #044a35); z-index: 9999; display: flex; align-items: center; justify-content: center; font-family: 'Cairo', sans-serif; }
#activationScreen .activation-box { background: white; padding: 30px; border-radius: 15px; width: 90%; max-width: 400px; text-align: center; box-shadow: 0 15px 40px rgba(0,0,0,0.3); border: 3px solid #ffd166; }
#activationScreen h3 { color: #044a35; margin-bottom: 20px; font-size: 22px; display: flex; align-items: center; justify-content: center; gap: 10px; }
#activationScreen p { color: #666; font-size: 14px; margin-bottom: 20px; }
#activationCodeInput { width: 100%; padding: 15px; border: 2px solid #d4ebe2; border-radius: 10px; font-size: 16px; text-align: center; margin-bottom: 20px; font-family: 'Cairo', sans-serif; transition: all 0.3s; }
#activationCodeInput:focus { outline: none; border-color: #066d4d; box-shadow: 0 0 0 3px rgba(6, 109, 77, 0.15); }
#activationScreen button { width: 100%; padding: 15px; background: linear-gradient(135deg, #066d4d 0%, #05553d 100%); color: white; border: none; border-radius: 10px; font-weight: 700; cursor: pointer; font-size: 16px; transition: all 0.3s; font-family: 'Cairo', sans-serif; }
#activationScreen button:hover { background: linear-gradient(135deg, #05553d 0%, #044a35 100%); filter: brightness(1.05); }
#contactForTrialBtn { width: 100%; padding: 15px; background: linear-gradient(135deg, #5a67d8 0%, #4c51bf 100%); color: white; border: none; border-radius: 10px; font-weight: 700; cursor: pointer; font-size: 16px; transition: all 0.3s; font-family: 'Cairo', sans-serif; margin-top: 10px; display: flex; align-items: center; justify-content: center; gap: 10px; }
#contactForTrialBtn:hover { background: linear-gradient(135deg, #4c51bf 0%, #434190 100%); filter: brightness(1.05); }
#activationError { color: #d9534f; font-size: 13px; margin-top: 15px; padding: 10px; background: #fee; border-radius: 8px; border-right: 4px solid #d9534f; display: none; }
.input-section { background: #ffffff; padding: 25px; border-radius: 20px; border: 2px solid #e0f0ea; box-shadow: 0 10px 30px rgba(4, 74, 53, 0.12); position: relative; overflow: hidden; margin-top: 170px; }
.input-section::before { content: ''; position: absolute; top: 0; right: 0; width: 100%; height: 5px; background: linear-gradient(to left, #066d4d, #ffd166, #25D366); }
.input-section h2 { color: #044a35; font-size: 24px; margin-bottom: 30px; padding-bottom: 15px; border-bottom: 3px solid #e0f0ea; text-align: center; font-weight: 900; position: relative; }
.input-section h2::after { content: ''; position: absolute; bottom: -3px; right: 50%; transform: translateX(50%); width: 120px; height: 3px; background: linear-gradient(to left, #066d4d, #ffd166); border-radius: 2px; }
.form-group { margin-bottom: 25px; position: relative; }
.form-group label { font-size: 16px; font-weight: 800; margin-bottom: 10px; display: flex; align-items: center; gap: 12px; padding-right: 8px; position: relative; color: #083024; }
.form-group label i { color: #066d4d; font-size: 16px; background: #f0f9f6; padding: 7px; border-radius: 10px; border: 1px solid #d4ebe2; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
.form-group label::before { content: ''; width: 8px; height: 8px; background: #ffd166; border-radius: 50%; display: inline-block; margin-left: 6px; box-shadow: 0 0 6px #ffd166; }
input, select, textarea { width: 100%; padding: 16px; margin-top: 8px; border: 2px solid #d4ebe2; border-radius: 12px; font-size: 18px; background: #f9fcfb; transition: all 0.3s; font-family: 'Cairo', sans-serif; color: #083024; box-shadow: inset 0 2px 8px rgba(0,0,0,0.05); -webkit-appearance: none; }
input:focus, select:focus, textarea:focus { outline: none; border-color: #066d4d; box-shadow: 0 0 0 4px rgba(6,109,77,0.15), inset 0 2px 8px rgba(0,0,0,0.05); background: #ffffff; }
textarea { height: 120px; resize: none; overflow: hidden; line-height: 1.7; font-size: 17px; }
.form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
button[title] { position: relative; }
button[title]:hover::after { content: attr(title); position: absolute; bottom: calc(100% + 10px); right: 50%; transform: translateX(50%); background: rgba(4, 58, 42, 0.95); color: white; padding: 10px 15px; border-radius: 8px; font-size: 12px; white-space: pre-line; z-index: 1000; border: 1px solid #044a35; box-shadow: 0 5px 15px rgba(0,0,0,0.15); max-width: 300px; min-width: 200px; }
button[title]:hover::before { content: ''; position: absolute; bottom: calc(100% + 2px); right: 50%; transform: translateX(50%); border: 6px solid transparent; border-top-color: rgba(4, 58, 42, 0.95); z-index: 1000; }
.notification { position: fixed; top: 150px; right: 10px; left: 10px; background: linear-gradient(135deg, #066d4d 0%, #044a35 100%); color: white; padding: 12px 18px; border-radius: 10px; box-shadow: 0 6px 20px rgba(4, 74, 53, 0.3); z-index: 1000; display: flex; align-items: center; gap: 10px; font-weight: 600; transform: translateX(150%); transition: transform 0.4s cubic-bezier(0.68, -0.55, 0.27, 1.55); border-right: 5px solid #ffd166; text-align: center; justify-content: center; }
.notification.show { transform: translateX(0); }
.notification i { font-size: 18px; }
.levels-container { background: #f8fdfa; border-radius: 12px; padding: 15px; margin-bottom: 20px; border: 2px solid #d4ebe2; box-shadow: 0 4px 10px rgba(0,0,0,0.05); }
.level-indicator { display: flex; align-items: center; justify-content: space-between; margin-bottom: 15px; padding: 8px; background: linear-gradient(135deg, #066d4d 0%, #044a35 100%); border-radius: 8px; color: white; font-weight: 700; font-size: 14px; }
.level-indicator span { background: rgba(255,255,255,0.2); padding: 3px 10px; border-radius: 20px; font-size: 12px; }
.level-select { margin-bottom: 15px; }
.level-select select { width: 100%; padding: 12px; border: 2px solid #d4ebe2; border-radius: 8px; font-family: 'Cairo', sans-serif; font-size: 14px; background: white; cursor: pointer; }
.level-select select:focus { border-color: #066d4d; outline: none; }
.level-select label { font-size: 12px; color: #044a35; font-weight: 600; margin-bottom: 5px; display: flex; align-items: center; gap: 5px; }
.level-select label i { color: #066d4d; font-size: 12px; }
.criterion-info { background: white; border-radius: 8px; padding: 10px 15px; margin: 15px 0; border-right: 4px solid #ffd166; display: flex; align-items: center; justify-content: space-between; box-shadow: 0 2px 8px rgba(0,0,0,0.05); }
.criterion-name { font-weight: 800; color: #044a35; font-size: 14px; }
.criterion-weight { background: #ffd166; color: #5a3e00; padding: 3px 10px; border-radius: 20px; font-weight: 700; font-size: 12px; }
#reportSearchContainer { position: relative; margin-bottom: 15px; }
#searchResults { display: none; position: absolute; top: 100%; left: 0; right: 0; background: white; border: 1px solid #ddd; border-radius: 6px; max-height: 200px; overflow-y: auto; z-index: 1000; box-shadow: 0 4px 12px rgba(0,0,0,0.1); }
#searchResults div { padding: 8px 12px; cursor: pointer; border-bottom: 1px solid #eee; }
#searchResults div:hover { background-color: #f0f9f6 !important; color: #066d4d; }
#searchResults div:last-child { border-bottom: none; }
#reportSearch:focus { outline: none; border-color: #066d4d; box-shadow: 0 0 0 2px rgba(6, 109, 77, 0.2); }
.manual-title-container { margin-top: 15px; padding: 15px; background: #f8fdfa; border-radius: 12px; border: 2px solid #d4ebe2; }
.manual-title-container label { display: flex; align-items: center; gap: 10px; color: #044a35; font-weight: 700; margin-bottom: 10px; }
.manual-title-container input { background: white; border: 2px solid #d4ebe2; padding: 12px; border-radius: 8px; font-size: 16px; }
.tools-section { background: #f8fdfa; padding: 18px; border-radius: 12px; border: 1px solid #d4ebe2; margin-top: 10px; box-shadow: 0 3px 10px rgba(0,0,0,0.05); counter-reset: tool-counter; }
.tools-grid { display: grid; gap: 12px; grid-template-columns: repeat(2, 1fr); }
@media (min-width: 768px) { .tools-grid { grid-template-columns: repeat(3, 1fr); } }
.tool-checkbox { display: flex; align-items: center; gap: 8px; padding: 12px 8px 12px 8px; background: white; border-radius: 12px; border: 2px solid #d4ebe2; transition: all 0.3s; cursor: pointer; position: relative; min-height: 55px; box-shadow: 0 2px 6px rgba(0,0,0,0.03); }
.tool-checkbox::before { counter-increment: tool-counter; content: counter(tool-counter); position: absolute; right: 8px; background: #066d4d; color: white; width: 22px; height: 22px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 12px; font-weight: 700; }
.tool-checkbox:hover { border-color: #066d4d; background: #f0f9f6; box-shadow: 0 6px 12px rgba(6, 109, 77, 0.1); transform: translateY(-2px); }
.tool-checkbox input[type="checkbox"] { width: 20px; height: 20px; cursor: pointer; position: absolute; opacity: 0; z-index: 1; }
.tool-checkbox span { font-size: 14px; font-weight: 700; color: #083024; margin-right: 35px; flex: 1; line-height: 1.4; }
.tool-checkbox.checked { border-color: #066d4d; background: #e8f4f0; box-shadow: 0 4px 12px rgba(6, 109, 77, 0.15); }
.checkmark { color: #066d4d; font-size: 18px; margin-right: 5px; display: none; }
.tool-checkbox.checked .checkmark { display: inline-block; }
.tools-outside-grid { display: grid; gap: 12px; grid-template-columns: repeat(2, 1fr); margin-top: 10px; }
@media (min-width: 768px) { .tools-outside-grid { grid-template-columns: repeat(3, 1fr); } }
.other-tool-container { margin-top: 15px; display: flex; gap: 10px; align-items: center; }
.other-tool-container input { flex: 1; padding: 10px; border-radius: 8px; border: 2px solid #d4ebe2; font-size: 14px; }
.other-tool-container button { background: #066d4d; color: white; border: none; border-radius: 8px; padding: 10px 20px; font-weight: 700; cursor: pointer; transition: all 0.3s; }
.other-tool-container button:hover { background: #044a35; }
.other-tools-list { margin-top: 10px; display: flex; flex-wrap: wrap; gap: 8px; }
.other-tag { background: #e0f0ea; border: 1px solid #b0d5c9; border-radius: 20px; padding: 5px 12px; font-size: 13px; font-weight: 600; display: flex; align-items: center; gap: 5px; }
.other-tag i { color: #d9534f; cursor: pointer; font-size: 12px; }
.small-fields { margin: 20px 0; padding: 15px; background: #f0f9f6; border-radius: 12px; border: 2px solid #d4ebe2; }
.small-fields .form-row { margin-bottom: 0; }
.large-extra-fields { margin-top: 30px; padding: 20px; background: #f8fdfa; border-radius: 12px; border: 2px solid #ffd166; }
.large-extra-fields h4 { color: #044a35; margin-bottom: 15px; display: flex; align-items: center; gap: 10px; font-size: 18px; }
#savedReportsModal { display: none; position: fixed; top: 0; left: 0; right: 0; bottom: 0; background: rgba(0,0,0,0.5); z-index: 6000; align-items: center; justify-content: center; font-family: 'Cairo', sans-serif; }
#savedReportsModal > div { background: white; padding: 25px; border-radius: 15px; width: 90%; max-width: 800px; max-height: 80vh; overflow-y: auto; box-shadow: 0 15px 40px rgba(0,0,0,0.3); border: 3px solid #ffd166; }
#savedReportsModal h3 { color: #044a35; text-align: center; margin-bottom: 20px; font-size: 22px; display: flex; align-items: center; justify-content: center; gap: 10px; position: sticky; top: 0; background: white; padding-bottom: 10px; border-bottom: 2px solid #d4ebe2; }
.progress-bar-container { width: 100%; background: linear-gradient(135deg, #ffffff 0%, #f8fdfa 100%); padding: 16px 20px; margin-bottom: 20px; border: 2px solid #d4ebe2; border-radius: 20px; box-shadow: 0 4px 15px rgba(4, 74, 53, 0.1); display: flex; flex-direction: column; align-items: center; gap: 10px; font-family: 'Cairo', sans-serif; box-sizing: border-box; }
.progress-header { display: flex; justify-content: space-between; align-items: center; width: 100%; max-width: 900px; margin: 0 auto; color: #044a35; font-weight: 700; font-size: 15px; }
.progress-stats { display: flex; gap: 15px; align-items: center; }
.progress-percentage { background: linear-gradient(135deg, #ffd166, #ffc233); color: #5a3e00; padding: 4px 12px; border-radius: 30px; font-size: 13px; font-weight: 800; box-shadow: 0 2px 8px rgba(255, 209, 102, 0.3); border: 1px solid #ffb830; }
.progress-message { color: #066d4d; font-size: 12px; font-weight: 600; background: #e8f4f0; padding: 4px 12px; border-radius: 30px; border: 1px solid #c0e0d6; }
.progress-track { width: 100%; max-width: 900px; margin: 0 auto; height: 16px; background: #e0f0ea; border-radius: 30px; overflow: hidden; border: 1px solid #c0e0d6; box-shadow: inset 0 2px 5px rgba(0,0,0,0.1); position: relative; }
.progress-fill { height: 100%; background: linear-gradient(90deg, #066d4d, #0a9d72); border-radius: 30px; transition: width 0.5s cubic-bezier(0.4, 0, 0.2, 1); position: relative; }
.reports-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 15px; margin-bottom: 20px; }
.report-card { background: #f8fdfa; border: 2px solid #d4ebe2; border-radius: 12px; padding: 15px; transition: all 0.3s; position: relative; overflow: hidden; }
.report-card:hover { border-color: #066d4d; box-shadow: 0 5px 15px rgba(6,109,77,0.15); transform: translateY(-3px); }
.report-card.completed { border-right: 6px solid #066d4d; background: #f0f9f6; }
.report-card .report-title { font-weight: 800; color: #044a35; font-size: 16px; margin-bottom: 10px; padding-left: 25px; }
.report-card .report-criterion { font-size: 12px; color: #066d4d; margin-bottom: 8px; display: flex; align-items: center; gap: 5px; }
.report-card .report-criterion i { font-size: 10px; }
.report-card .report-weight { background: #ffd166; color: #5a3e00; padding: 2px 8px; border-radius: 15px; font-size: 11px; font-weight: 700; display: inline-block; margin-bottom: 10px; }
.report-card .report-date { font-size: 11px; color: #666; margin-bottom: 15px; display: flex; align-items: center; gap: 5px; }
.report-actions { display: flex; gap: 5px; justify-content: flex-end; flex-wrap: wrap; }
.report-actions button { padding: 6px 8px; border: none; border-radius: 6px; font-size: 11px; font-weight: 600; cursor: pointer; transition: all 0.3s; display: flex; align-items: center; gap: 4px; flex: 1 1 auto; justify-content: center; }
.report-actions .load-btn { background: #066d4d; color: white; }
.report-actions .load-btn:hover { background: #044a35; }
.report-actions .pdf-btn { background: #ff6b6b; color: white; }
.report-actions .pdf-btn:hover { background: #ee5a52; }
.report-actions .whatsapp-btn { background: #25D366; color: white; }
.report-actions .whatsapp-btn:hover { background: #1da851; }
.report-actions .delete-btn { background: #fee; color: #d9534f; border: 1px solid #fcc; }
.report-actions .delete-btn:hover { background: #fdd; color: #b52b27; }
.close-reports-btn { width: 100%; padding: 12px; background: #066d4d; color: white; border: none; border-radius: 10px; font-weight: 700; cursor: pointer; font-size: 14px; transition: all 0.3s; position: sticky; bottom: 0; }
.close-reports-btn:hover { background: #044a35; }
.empty-reports { text-align: center; padding: 30px; color: #666; font-size: 14px; background: #f8fdfa; border-radius: 10px; border: 2px dashed #d4ebe2; }
.empty-reports i { font-size: 40px; color: #c0e0d6; margin-bottom: 10px; }
#settingsModal { display: none; position: fixed; top: 0; left: 0; right: 0; bottom: 0; background: rgba(0,0,0,0.5); z-index: 5000; align-items: center; justify-content: center; font-family: 'Cairo', sans-serif; }
#settingsModal > div { background: white; padding: 25px; border-radius: 15px; width: 90%; max-width: 400px; max-height: 80vh; overflow-y: auto; box-shadow: 0 15px 40px rgba(0,0,0,0.3); border: 3px solid #ffd166; }
#settingsModal h3 { color: #044a35; text-align: center; margin-bottom: 15px; font-size: 22px; display: flex; align-items: center; justify-content: center; gap: 10px; }
#settingsModal #subInfo { font-size: 14px; line-height: 2; color: #333; text-align: center; margin-bottom: 15px; }
#settingsModal label { font-weight: 700; color: #044a35; display: block; margin-bottom: 8px; display: flex; align-items: center; gap: 8px; }
#settingsModal input[type="date"] { width: 100%; margin-top: 8px; padding: 10px; border-radius: 8px; border: 2px solid #d4ebe2; font-family: 'Cairo', sans-serif; font-size: 16px; }
#settingsModal input[type="date"]:focus { outline: none; border-color: #066d4d; box-shadow: 0 0 0 3px rgba(6,109,77,0.15); }
#settingsModal button { width: 100%; padding: 12px; background: #066d4d; color: white; border: none; border-radius: 10px; font-weight: 700; cursor: pointer; font-family: 'Cairo', sans-serif; transition: all 0.3s; margin-top: 10px; }
#settingsModal button:hover { background: #05553d; filter: brightness(1.05); }
#settingsModal .btn-secondary { background: #4f7bff; margin-top: 5px; }
#settingsModal .btn-secondary:hover { background: #3b5bdb; filter: brightness(1.05); }
#settingsModal hr { margin: 15px 0; border: none; border-top: 1px solid #d4ebe2; }
.theme-light-blue body { background: linear-gradient(135deg, #e8f0ff 0%, #d6e4ff 50%, #c2d4ff 100%) !important; }
.theme-light-blue .input-section { background: #ffffff; border: 2px solid #c2d4ff; box-shadow: 0 10px 30px rgba(66, 133, 244, 0.15); }
.theme-light-blue .input-section::before { background: linear-gradient(to left, #4285f4, #34a853, #fbbc05); }
.theme-light-blue .input-section h2 { color: #4285f4; }
.theme-light-blue .top-marquee { background: linear-gradient(135deg, #1a73e8 0%, #4285f4 100%); }
.theme-light-blue #aiFillFloatingBtn { background: linear-gradient(135deg, #4285f4 0%, #34a853 25%, #fbbc05 50%, #ea4335 100%) !important; }
.theme-dark body { background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%) !important; color: #e0e0e0; }
.theme-dark .input-section { background: #1e293b; border: 2px solid #334155; color: #e0e0e0; }
.theme-dark .input-section h2 { color: #60a5fa; }
.theme-dark input, .theme-dark select, .theme-dark textarea { background: #1e293b; border-color: #475569; color: #e0e0e0; }
.theme-dark .top-marquee { background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%); }
.theme-dark #aiFillFloatingBtn { background: linear-gradient(135deg, #6d28d9 0%, #7c3aed 25%, #8b5cf6 50%, #a78bfa 100%) !important; }
.theme-green body { background: linear-gradient(135deg, #e6f7ef 0%, #d4f0e4 50%, #c2e8d9 100%) !important; }
.theme-green .input-section { background: #ffffff; border: 2px solid #2ecc71; box-shadow: 0 10px 30px rgba(46, 204, 113, 0.15); }
.theme-green .input-section h2 { color: #27ae60; }
.theme-green .top-marquee { background: linear-gradient(135deg, #1e8449 0%, #27ae60 100%); }
.theme-green #aiFillFloatingBtn { background: linear-gradient(135deg, #27ae60 0%, #2ecc71 25%, #3498db 50%, #9b59b6 100%) !important; }
@page { size: A4; margin: 10mm; }
:root { --main: #062f25; --border: #2f9e8f; --bg: #ffffff; }
[id^="report-content"] { width: 100%; max-width: 210mm; margin: 4mm auto 0 auto; padding: 0 6mm; box-sizing: border-box; display: none; font-family: 'Cairo', sans-serif; background: var(--bg); }
.header { background: var(--main); height: 150px; border-radius: 8px; color: #fff; display: flex; align-items: center; justify-content: center; position: relative; margin-bottom: 8px; }
.header img { width: 260px; filter: brightness(0) invert(1); }
.header-school { position: absolute; right: 12px; top: 45px; font-size: 16px; font-weight: 700; max-width: 70%; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; text-align: right; }
.header-education { position: absolute; left: 50%; bottom: 18px; transform: translateX(-50%); font-size: 16px; font-weight: 800; text-align: center; width: 100%; }
.header-date { position: absolute; left: 12px; top: 10px; font-size: 12px; text-align: right; }
.info-grid { display: grid; grid-template-columns: repeat(5, 1fr); gap: 6px; margin-bottom: 6px; }
.info-grid2 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 6px; margin-bottom: 6px; }
.info-box { border: 1px solid var(--border); border-radius: 7px; padding: 14px 4px 6px; position: relative; text-align: center; font-size: 10px; min-height: 34px; overflow: hidden; background: var(--bg); }
.info-title { position: absolute; top: 4px; right: 50%; transform: translateX(50%); font-size: 8px; font-weight: 800; color: var(--main); white-space: nowrap; }
.info-value { font-size: 10px; font-weight: 600; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
.box-objective { border: 1px solid var(--border); border-radius: 8px; padding: 8px; margin-bottom: 6px; height: 110px; display: flex; flex-direction: column; overflow: hidden; background: var(--bg); }
.box-objective .box-title { text-align: center; color: var(--main); font-weight: 800; font-size: 11px; margin-bottom: 4px; }
.box-objective .box-content { font-size: 11px; line-height: 1.5; text-align: center; overflow: hidden; }
.box { border: 1px solid var(--border); border-radius: 8px; padding: 8px; margin-bottom: 6px; height: 150px; display: flex; flex-direction: column; overflow: hidden; background: var(--bg); }
.box-title { text-align: center; color: var(--main); font-weight: 800; font-size: 11px; margin-bottom: 4px; }
.box-content { font-size: 11px; line-height: 1.5; text-align: center; overflow: hidden; }
.row { display: grid; grid-template-columns: 1fr 1fr; gap: 6px; }
.images { display: grid; grid-template-columns: 1fr 1fr; gap: 6px; margin-bottom: 6px; }
.image-box { border: 1px dashed var(--border); height: 125px; display: flex; align-items: center; justify-content: center; overflow: hidden; background: #f9fdfb; position: relative; }
.image-box::before { content: 'صورة توثيقية'; position: absolute; top: 4px; right: 4px; font-size: 12px; background: rgba(255,255,255,.9); padding: 1px 5px; border-radius: 3px; z-index: 1; }
.image-box img { width: 65%; height: 100%; object-fit: contain; display: block; }
.signatures { display: grid; grid-template-columns: 1fr 1fr; gap: 30px; text-align: center; font-size: 10px; margin-bottom: 6px; }
.signature-role { font-size: 9px; color: var(--main); font-weight: 600; margin-bottom: 2px; }
.signature-name { font-size: 11px; font-weight: 700; }
.sign-line { border-top: 1px solid #000; margin: 6px auto 0; width: 70%; }
.footer-box { background: var(--main); color: #fff; text-align: center; font-size: 8px; padding: 3px 4px; border-radius: 6px; }
.pdf-export * { -webkit-print-color-adjust: exact !important; print-color-adjust: exact !important; color-adjust: exact !important; }
@media (max-width: 768px) { .top-small-buttons { padding: 6px 15px; } .small-buttons-grid { gap: 6px; } .small-btn { min-height: 38px; min-width: 70px; padding: 4px 3px; font-size: 9px; } .small-btn-icon { font-size: 10px; } .small-btn .small-btn-text { font-size: 8px; } .main-buttons-bar { padding: 8px 15px; } .main-buttons-grid { gap: 12px; max-width: 280px; } .main-btn { min-height: 55px; min-width: 110px; padding: 8px 6px; } .main-btn-icon { font-size: 16px; } .main-btn .main-btn-text { font-size: 11px; } .input-section { padding: 15px; margin-top: 160px; } .input-section h2 { font-size: 20px; } .form-row { grid-template-columns: 1fr; gap: 15px; } .tools-grid { grid-template-columns: repeat(2, 1fr); } #aiFillFloatingBtn { width: 85px; height: 85px; bottom: 20px; left: 20px; } #aiFillFloatingBtn .floating-ai-icon { font-size: 32px; } #aiFillFloatingBtn .floating-ai-text { font-size: 12px; } }
@media (max-width: 480px) { .top-marquee { font-size: 12px; min-height: 40px; } .marquee-inner { animation-duration: 35s; } .small-btn { min-height: 35px; min-width: 60px; padding: 3px 2px; font-size: 8px; } .small-btn-icon { font-size: 9px; } .small-btn .small-btn-text { font-size: 7px; } .main-btn { min-height: 50px; min-width: 95px; } .main-btn-icon { font-size: 14px; } .main-btn .main-btn-text { font-size: 10px; } #aiFillFloatingBtn { width: 75px; height: 75px; bottom: 15px; left: 15px; } #aiFillFloatingBtn .floating-ai-icon { font-size: 28px; } #aiFillFloatingBtn .floating-ai-text { font-size: 11px; } .input-section { padding: 12px; margin-top: 150px; } input, select, textarea { padding: 12px; font-size: 16px; } .form-group label { font-size: 13px; } .tool-checkbox { padding: 10px 5px; } .tool-checkbox span { font-size: 12px; margin-right: 32px; } .tools-grid { grid-template-columns: repeat(2, 1fr); } }
.ai-guide-box { position: fixed; bottom: 150px; left: 30px; background: white; border-radius: 20px; padding: 20px; box-shadow: 0 10px 40px rgba(0,0,0,0.3); border: 3px solid #ff6b6b; z-index: 2000; max-width: 280px; text-align: center; animation: slideIn 0.5s ease; direction: rtl; }
@keyframes slideIn { from { transform: translateX(100px); opacity: 0; } to { transform: translateX(0); opacity: 1; } }
.ai-guide-arrow { font-size: 50px; color: #ff6b6b; position: absolute; bottom: -20px; left: -20px; transform: rotate(45deg); animation: bounceArrow 1s infinite; }
@keyframes bounceArrow { 0%, 100% { transform: rotate(45deg) translateX(0); } 50% { transform: rotate(45deg) translateX(-10px); } }
.ai-guide-content h4 { color: #044a35; margin-bottom: 10px; font-size: 18px; }
.ai-guide-timer { font-size: 24px; font-weight: 900; color: #ff6b6b; margin: 10px 0; }
.ai-guide-btn { background: #ff6b6b; color: white; border: none; border-radius: 50px; padding: 12px 25px; font-size: 18px; font-weight: 700; cursor: pointer; width: 100%; margin: 10px 0; transition: all 0.3s; display: flex; align-items: center; justify-content: center; gap: 10px; }
.ai-guide-btn:hover { background: #ee5a52; transform: scale(1.05); }
.ai-guide-close { background: none; border: none; color: #666; font-size: 14px; cursor: pointer; text-decoration: underline; margin-top: 5px; }
</style>
</head>

<body class="theme-default">

<!-- زر التعبئة الذكية العائم -->
<button id="aiFillFloatingBtn" onclick="fillWithAI()" title="تعبئة الحقول تلقائياً باستخدام الذكاء الاصطناعي">
    <i class="fas fa-wand-magic-sparkles floating-ai-icon"></i>
    <span class="floating-ai-text">تعبئة ذكية</span>
</button>

<!-- شاشة كود التفعيل -->
<div id="activationScreen">
    <div class="activation-box">
        <h3><i class="fas fa-lock"></i> تفعيل الأداة</h3>
        <p>أدخل كود التفعيل الذي حصلت عليه من المطور</p>
        <input id="activationCodeInput" placeholder="أدخل كود التفعيل هنا">
        <button onclick="activateTool()">تفعيل</button>
        <button id="contactForTrialBtn" onclick="contactForTrial()">
            <i class="fas fa-comments"></i>
            تواصل للتجربة أو الاشتراك
        </button>
        <div id="activationError">كود غير صالح. الرجاء التأكد من الكود والمحاولة مرة أخرى.</div>
    </div>
</div>

<!-- شريط الأخبار العلوي -->
<div class="top-marquee">
<div class="marquee-inner">
<i class="fas fa-star" style="margin-left:8px;"></i> 
✨ نظام تقاريرك المتكامل: أنشئ تقارير تربوية احترافية بسهولة - حفظ تلقائي - تعبئة ذكية بالذكاء الاصطناعي - معايير أداء محدثة - مشاركة PDF وواتساب - دعم كامل للهواتف - تقارير غير محدودة للمشتركين ✨
<i class="fas fa-gem" style="margin-right:8px;"></i>
</div>
</div>

<!-- ========== المجموعة الأولى: الأزرار الصغيرة ========== -->
<div class="top-small-buttons">
    <div class="small-buttons-grid">
        <button class="small-btn" id="saveTeacherBtn" onclick="saveTeacherData()" title="حفظ بيانات المعلم والمدرسة">
            <i class="fas fa-save small-btn-icon"></i>
            <span class="small-btn-text">حفظ البيانات</span>
        </button>
        <button class="small-btn" id="clearBtn" onclick="clearData()" title="مسح بيانات المعلم والنصوص المولدة فقط">
            <i class="fas fa-trash-alt small-btn-icon"></i>
            <span class="small-btn-text">مسح البيانات</span>
        </button>
        <button class="small-btn" id="savedReportsBtn" onclick="openSavedReports()" title="عرض التقارير المحفوظة">
            <i class="fas fa-folder-open small-btn-icon"></i>
            <span class="small-btn-text">التقارير المحفوظة</span>
        </button>
        <button class="small-btn" id="settingsBtn" onclick="openSettings()" title="إعدادات الاشتراك">
            <i class="fas fa-cog small-btn-icon"></i>
            <span class="small-btn-text">الضبط</span>
        </button>
    </div>
</div>

<!-- ========== المجموعة الثانية: الأزرار الكبيرة ========== -->
<div class="main-buttons-bar">
    <div class="main-buttons-grid">
        <button class="main-btn" id="whatsappBtn" onclick="sharePDFWhatsApp()" title="مشاركة التقرير عبر واتساب">
            <i class="fab fa-whatsapp main-btn-icon"></i>
            <span class="main-btn-text">مشاركة واتساب</span>
        </button>
        <button class="main-btn" id="pdfBtn" onclick="downloadPDF()" title="تحويل التقرير إلى PDF وتنزيله">
            <i class="fas fa-file-pdf main-btn-icon"></i>
            <span class="main-btn-text">تنزيل PDF</span>
        </button>
    </div>
</div>

<!-- المحتوى الرئيسي -->
<div class="wrapper">
<div class="input-section">
  
  <h2><i class="fas fa-tools" style="margin-left:10px;"></i>تقاريرك - النظام المتكامل</h2>
  
  <!-- ========== اختيار مقدم التقرير (الدور) ========== -->
  <div class="form-group">
    <label for="role"><i class="fas fa-user-tie"></i> مقدم التقرير</label>
    <select id="role" name="role" required onchange="handleRoleChange()">
      <option value="">اختر الصفة المهنية</option>
      <option value="teacher">معلم / معلمة</option>
      <option value="school_principal">مدير المدرسة / مديرة المدرسة</option>
      <option value="vice_principal">وكيل المدرسة / وكيلة المدرسة</option>
      <option value="student_guide">الموجه الطلابي / الموجهة الطلابية</option>
      <option value="health_guide">الموجه الصحي / الموجهة الصحية</option>
      <option value="activity_leader">رائد النشاط / رائدة النشاط</option>
      <option value="educational_supervisor">المشرف التربوي / المشرفة التربوية</option>
    </select>
  </div>
  
  <!-- ========== القوائم المتتالية (اختيارية) ========== -->
  <div class="levels-container">
    <div class="level-indicator">
      <span>اختر المعايير والتصنيفات (اختياري)</span>
      <span><i class="fas fa-layer-group"></i> للمساعدة</span>
    </div>
    
    <!-- المستوى الأول: المعايير التربوية -->
    <div class="level-select">
      <label><i class="fas fa-star"></i> معيار الاداء الوظيفي</label>
      <select id="criterionSelect" onchange="loadSubcategories()">
        <option value="">اختر معيار الاداء الوظيفي</option>
      </select>
    </div>
    
    <!-- معلومات المعيار المحدد (تظهر دائماً مع الوزن) -->
    <div id="criterionInfo" class="criterion-info" style="display: none;">
      <span id="selectedCriterionName" class="criterion-name"></span>
      <span id="selectedCriterionWeight" class="criterion-weight"></span>
    </div>
    
    <!-- المستوى الثاني: التصنيفات الفرعية -->
    <div class="level-select">
      <label><i class="fas fa-list-ul"></i> التصنيف الفرعي</label>
      <select id="subcategorySelect" onchange="loadReports()" disabled>
        <option value="">اختر التصنيف الفرعي</option>
      </select>
    </div>
    
    <!-- المستوى الثالث: التقارير -->
    <div class="level-select">
      <label><i class="fas fa-file-alt"></i> التقرير</label>
      <select id="reportSelect" onchange="updateReportFromSelection()" disabled>
        <option value="">اختر التقرير</option>
      </select>
    </div>
    
    <!-- البحث المتقدم -->
    <div id="reportSearchContainer">
        <input type="text" id="reportSearch" placeholder="ابحث عن تقرير (اختياري)..." style="width:100%; padding:12px; border:2px solid #d4ebe2; border-radius:8px; font-size:14px;">
        <div id="searchResults"></div>
    </div>
    
    <!-- خانة عنوان التقرير اليدوية (إلزامي) -->
    <div class="manual-title-container">
        <label><i class="fas fa-heading"></i> عنوان التقرير <span style="color:#ff6b6b;">*</span></label>
        <input type="text" id="manualReportTitle" placeholder="أدخل عنوان التقرير (مثال: تقرير زيارة صفية)" oninput="updateReport()" required>
    </div>
  </div>
  
  <!-- حقول أساسية مشتركة -->
  <div class="form-group">
    <label for="education"><i class="fas fa-university"></i> إدارة التعليم</label>
    <select id="education" oninput="updateReport()">
      <option value="">اختر إدارة التعليم</option>
    </select>
  </div>
  
  <div class="form-group">
    <label for="school"><i class="fas fa-school"></i> اسم المدرسة / المكتب</label>
    <input id="school" placeholder="اسم المدرسة أو المكتب" oninput="updateReport()">
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label for="reporterType"><i class="fas fa-chalkboard-teacher"></i> <span id="reporterTypeLabel">صفة مقدم التقرير</span></label>
      <select id="reporterType" oninput="updateReporterGender()"></select>
    </div>
    <div class="form-group">
      <label for="reporterName"><i class="fas fa-user"></i> <span id="reporterNameLabel">اسم مقدم التقرير</span></label>
      <input id="reporterName" placeholder="اسم مقدم التقرير" oninput="updateReport()">
    </div>
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label for="principalTypeDisplay"><i class="fas fa-user-cog"></i> صفة المدير (تلقائي)</label>
      <input type="text" id="principalTypeDisplay" readonly style="background:#f0f0f0;" value="المدير">
    </div>
    <div class="form-group">
      <label for="principal"><i class="fas fa-user-cog"></i> اسم المدير / المسؤول</label>
      <input id="principal" placeholder="اسم المدير" oninput="updateReport()">
    </div>
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label for="place"><i class="fas fa-map-marker-alt"></i> مكان التنفيذ</label>
      <select id="place" onchange="togglePlaceFields()" oninput="updateReport()">
        <option value="داخل الصف">داخل الصف</option>
        <option value="خارج الصف">خارج الصف</option>
      </select>
    </div>
    <div class="form-group">
      <label for="term"><i class="fas fa-calendar-alt"></i> الفصل الدراسي</label>
      <select id="term" oninput="updateReport()">
        <option value="">اختر الفصل</option>
        <option value="الأول">الأول</option>
        <option value="الثاني">الثاني</option>
        <option value="الثالث">الثالث</option>
      </select>
    </div>
  </div>

  <!-- تفاصيل المكان -->
  <div class="form-group">
    <label><i class="fas fa-location-dot"></i> حدد المكان بالضبط</label>
    <div style="display: flex; gap: 10px; flex-wrap: wrap;">
      <select id="detailedPlaceSelect" style="flex: 2;" onchange="toggleDetailedPlaceInput()">
        <option value="">اختر موقعاً محدداً</option>
        <option value="الفناء المدرسي">الفناء المدرسي</option>
        <option value="غرفة المدير">غرفة المدير</option>
        <option value="غرفة الاجتماعات">غرفة الاجتماعات</option>
        <option value="رحلة خارج المدرسة">رحلة خارج المدرسة</option>
        <option value="أخرى">أخرى (اكتب)</option>
      </select>
      <input type="text" id="detailedPlaceInput" placeholder="اكتب موقعاً آخر" style="flex: 3; display: none;" oninput="updateReport()">
    </div>
  </div>

  <!-- الحقول الخاصة بالمعلم (تظهر فقط إذا كان الدور teacher والمكان داخل الصف) -->
  <div id="teacherFields" style="display: none;">
    <div class="form-row">
      <div class="form-group">
        <label for="grade"><i class="fas fa-users-class"></i> الصف</label>
        <input id="grade" placeholder="مثال: ٥/٣" oninput="updateReport()">
      </div>
    </div>
    <div class="form-row">
      <div class="form-group">
        <label for="subject"><i class="fas fa-book"></i> المادة / البرنامج</label>
        <input id="subject" placeholder="مثال: لغتي" oninput="updateReport()">
      </div>
      <div class="form-group">
        <label for="lesson"><i class="fas fa-book-open"></i> الدرس / النشاط</label>
        <input id="lesson" placeholder="مثال: درس الضرب" oninput="updateReport()">
      </div>
    </div>
  </div>

  <!-- الحقول الصغيرة الخاصة بالدور (تظهر في الأعلى) -->
  <div id="smallRoleFields" class="small-fields" style="display: none;"></div>

  <!-- المستهدفون والعدد (حقول مشتركة) -->
  <div class="form-row">
    <div class="form-group">
      <label for="target"><i class="fas fa-bullseye"></i> المستهدفون / الفئة</label>
      <input id="target" placeholder="مثال: جميع طلاب الصف" oninput="updateReport()">
    </div>
    <div class="form-group">
      <label for="count"><i class="fas fa-user-check"></i> العدد / الحضور</label>
      <input id="count" placeholder="مثال: ٢٥" oninput="updateReport()">
    </div>
  </div>

  <!-- ========== الحقول النصية الكبيرة ========== -->
  <div class="form-group">
    <label for="goal"><i class="fas fa-flag"></i> <span id="goalLabel">الهدف التربوي</span></label>
    <textarea id="goal" placeholder="أدخل الهدف" oninput="updateReport()"></textarea>
  </div>
  
  <div class="form-group">
    <label for="summary"><i class="fas fa-file-signature"></i> <span id="summaryLabel">نبذة مختصرة</span></label>
    <textarea id="summary" placeholder="أدخل نبذة مختصرة" oninput="updateReport()"></textarea>
  </div>
  
  <div class="form-group">
    <label for="steps"><i class="fas fa-tasks"></i> <span id="stepsLabel">إجراءات التنفيذ</span></label>
    <textarea id="steps" placeholder="كيف تم تنفيذ النشاط؟" oninput="updateReport()"></textarea>
  </div>
  
  <div class="form-group">
    <label for="strategies"><i class="fas fa-chess-board"></i> <span id="strategiesLabel">الاستراتيجيات</span></label>
    <textarea id="strategies" placeholder="ما هي الاستراتيجيات المستخدمة" oninput="updateReport()"></textarea>
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label for="strengths"><i class="fas fa-thumbs-up"></i> <span id="strengthsLabel">نقاط القوة</span></label>
      <textarea id="strengths" placeholder="نقاط القوة" oninput="updateReport()"></textarea>
    </div>
    <div class="form-group">
      <label for="improve"><i class="fas fa-tools"></i> <span id="improveLabel">نقاط التحسين</span></label>
      <textarea id="improve" placeholder="نقاط تحتاج تطوير" oninput="updateReport()"></textarea>
    </div>
  </div>
  
  <!-- حقل التوصيات/خطة المتابعة -->
  <div class="form-group">
    <label for="recomm"><i class="fas fa-lightbulb"></i> <span id="recommLabel">التوصيات</span></label>
    <textarea id="recomm" placeholder="أدخل النص" oninput="updateReport()"></textarea>
  </div>

  <!-- الحقول الكبيرة الإضافية (للتوجيه الطلابي) -->
  <div id="largeExtraFields" class="large-extra-fields" style="display: none;">
    <h4><i class="fas fa-list"></i> تفاصيل إضافية</h4>
  </div>
  
  <!-- قسم الأدوات والوسائل التعليمية - داخل الصف -->
  <div id="insideToolsSection" class="form-group">
    <label><i class="fas fa-tools"></i> الأدوات والوسائل التعليمية (داخل الصف)</label>
    <div class="tools-section" id="toolsSection">
      <div class="tools-grid" id="toolsGrid">
        <p style="text-align:center;color:#666;">جارٍ تحميل الأدوات التعليمية...</p>
      </div>
      <div style="text-align:center; margin-top:10px; font-size:11px; color:#666;">
        <i class="fas fa-info-circle"></i> اضغط على الأداة لتحديدها
      </div>
    </div>
  </div>

  <!-- قسم الأدوات والوسائل التعليمية - خارج الصف -->
  <div id="outsideToolsSection" class="form-group" style="display: none;">
    <label><i class="fas fa-tools"></i> الأدوات والوسائل (خارج الصف)</label>
    <div class="tools-section">
      <div class="tools-outside-grid" id="outsideToolsGrid"></div>
      <div class="other-tool-container">
        <input type="text" id="otherToolInput" placeholder="أداة أخرى...">
        <button onclick="addOtherTool()">إضافة</button>
      </div>
      <div class="other-tools-list" id="otherToolsList"></div>
    </div>
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label><i class="fas fa-camera"></i> الصورة 1</label>
      <input type="file" accept="image/*" onchange="loadImage(this,'imgBox1','outsideImgBox1','adminImgBox1','supervisorImgBox1','activityImgBox1','studentImgBox1','healthImgBox1')">
    </div>
    <div class="form-group">
      <label><i class="fas fa-camera"></i> الصورة 2</label>
      <input type="file" accept="image/*" onchange="loadImage(this,'imgBox2','outsideImgBox2','adminImgBox2','supervisorImgBox2','activityImgBox2','studentImgBox2','healthImgBox2')">
    </div>
  </div>

</div>
</div>

<!-- ========== قوالب PDF السبعة (نفس القوالب الأصلية، لم يتم تضمينها هنا للاختصار ولكنها موجودة في الملف الأصلي) ========== -->

<!-- نافذة التقارير المحفوظة -->
<div id="savedReportsModal">
  <div>
    <h3><i class="fas fa-folder-open"></i> التقارير المحفوظة</h3>
    <div id="progressBarContainer" class="progress-bar-container"><!-- المحتوى --></div>
    <div id="savedReportsList" class="reports-grid"></div>
    <button class="close-reports-btn" onclick="closeSavedReports()">إغلاق</button>
  </div>
</div>

<!-- نافذة الإعدادات -->
<div id="settingsModal"><!-- المحتوى --></div>

<!-- صندوق التوجيه بعد التوليد -->
<div id="aiGuideBox" class="ai-guide-box" style="display: none;"><!-- المحتوى --></div>

<script>
// ==================== متغيرات عامة ====================
window.__ACTIVATED__ = false;
window.allCriteria = [];
window.subcategoriesByCriterion = {};
window.reportsBySubcategory = {};
window.allReportsList = [];
window.otherTools = [];
window.currentRole = 'teacher';
window.guideTimerInterval = null;

const ACTIVATION_KEY_NAME = "activation_code";
const BACKEND_URL = "https://deep-qphc.onrender.com";
const APP_THEME_KEY = "app_theme";
const PDF_THEME_KEY = "pdf_theme";
const REPORTS_STORAGE_KEY = "saved_educational_reports";

let currentHijriDate = '';
let currentGregorianDate = '';

const roleToBackendMap = {
  'teacher': 'teacher',
  'school_principal': 'school_principal',
  'vice_principal': 'vice_principal',
  'student_guide': 'student_guide',
  'health_guide': 'health_guide',
  'activity_leader': 'activity_leader',
  'educational_supervisor': 'educational_supervisor'
};

function getBackendRole(uiRole) {
  return roleToBackendMap[uiRole] || uiRole;
}

function formatWeight(weight) {
    if (weight === undefined || weight === null || weight === '') return '0%';
    let num = parseFloat(String(weight).replace(/%/g, '').trim());
    if (isNaN(num)) return '0%';
    return num + '%';
}

// ==================== التفعيل ====================
function hideActivationScreen() {
    if (window.__ACTIVATED__) {
        document.getElementById("activationScreen").style.display = "none";
        document.body.style.overflow = "auto";
    }
}

function showActivationError() {
    document.getElementById("activationError").style.display = "block";
}

async function activateTool() {
    const code = document.getElementById("activationCodeInput").value.trim();
    if (!code) { showActivationError(); return; }
    try {
        const res = await fetch(BACKEND_URL + "/health", { headers: { "X-Activation-Code": code } });
        if (!res.ok) throw new Error("Invalid");
        localStorage.setItem(ACTIVATION_KEY_NAME, code);
        window.__ACTIVATED__ = true;
        hideActivationScreen();
        showNotification("تم تفعيل الأداة بنجاح! ✓");
    } catch {
        showActivationError();
    }
}

function contactForTrial() {
    const message = encodeURIComponent("أرغب في تجربة أداة إصدار التقارير التربوية أو الاشتراك فيها.\n\nيرجى التواصل معي للمزيد من المعلومات.");
    window.open(`https://wa.me/966597077245?text=${message}`, '_blank');
}

// ==================== التاريخ ====================
async function loadDates() {
    let g = new Date();
    currentGregorianDate = `${g.getDate()}/${g.getMonth()+1}/${g.getFullYear()}`;
    const customDate = localStorage.getItem("custom_report_date");
    if (customDate) {
        g = new Date(customDate);
        currentGregorianDate = `${g.getDate()}/${g.getMonth()+1}/${g.getFullYear()}`;
    }
    try {
        const response = await fetch(`https://api.aladhan.com/v1/gToH?date=${g.getDate()}-${g.getMonth()+1}-${g.getFullYear()}`);
        const data = await response.json();
        const hijri = data.data.hijri;
        const toArabic = n => n.toString().replace(/[0-9]/g, d => '٠١٢٣٤٥٦٧٨٩'[d]);
        currentHijriDate = `${toArabic(hijri.year)}/${toArabic(hijri.month.number)}/${toArabic(hijri.day)}`;

        const dateElements = ['hDate','gDate','outsideHDate','outsideGDate','adminHDate','adminGDate','supervisorHDate','supervisorGDate','activityHDate','activityGDate','studentHDate','studentGDate','healthHDate','healthGDate'];
        for (let id of dateElements) {
            let el = document.getElementById(id);
            if (el) {
                if (id.includes('H')) el.innerHTML = currentHijriDate + " هـ";
                else el.innerHTML = currentGregorianDate + " م";
            }
        }
    } catch (error) {
        console.error("خطأ في تحميل التاريخ:", error);
        currentHijriDate = "١٤٤٦/٠٦/٠١";
    }
}

// ==================== الثيمات ====================
function loadThemeSettings() {
    const savedAppTheme = localStorage.getItem(APP_THEME_KEY) || 'default';
    document.getElementById('appThemeSelect').value = savedAppTheme;
    applyAppTheme(savedAppTheme);
    const savedPdfTheme = localStorage.getItem(PDF_THEME_KEY) || 'classic';
    document.getElementById('pdfThemeSelect').value = savedPdfTheme;
    applyPdfTheme(savedPdfTheme);
}

function applyAppTheme(themeName) {
    document.body.classList.remove('theme-light-blue', 'theme-dark', 'theme-green', 'theme-default');
    document.body.classList.add('theme-' + themeName);
    updateAiButtonTheme(themeName);
    localStorage.setItem(APP_THEME_KEY, themeName);
}

function updateAiButtonTheme(themeName) {
    const aiButton = document.getElementById('aiFillFloatingBtn');
    const aiIcon = aiButton.querySelector('.floating-ai-icon');
    const aiText = aiButton.querySelector('.floating-ai-text');
    switch(themeName) {
        case 'light-blue':
            aiButton.style.background = 'linear-gradient(135deg, #4285f4 0%, #34a853 25%, #fbbc05 50%, #ea4335 100%)';
            aiButton.style.boxShadow = '0 12px 35px rgba(66, 133, 244, 0.6), 0 0 0 3px rgba(255, 255, 255, 0.3), 0 0 25px rgba(66, 133, 244, 0.5)';
            break;
        case 'dark':
            aiButton.style.background = 'linear-gradient(135deg, #6d28d9 0%, #7c3aed 25%, #8b5cf6 50%, #a78bfa 100%)';
            aiButton.style.boxShadow = '0 12px 35px rgba(109, 40, 217, 0.6), 0 0 0 3px rgba(255, 255, 255, 0.3), 0 0 25px rgba(109, 40, 217, 0.5)';
            break;
        case 'green':
            aiButton.style.background = 'linear-gradient(135deg, #27ae60 0%, #2ecc71 25%, #3498db 50%, #9b59b6 100%)';
            aiButton.style.boxShadow = '0 12px 35px rgba(46, 204, 113, 0.6), 0 0 0 3px rgba(255, 255, 255, 0.3), 0 0 25px rgba(46, 204, 113, 0.5)';
            break;
        default:
            aiButton.style.background = 'linear-gradient(135deg, #9D50BB 0%, #6E48AA 25%, #533D8B 50%, #3A2569 100%)';
            aiButton.style.boxShadow = '0 12px 35px rgba(157, 80, 187, 0.6), 0 0 0 3px rgba(255, 255, 255, 0.3), 0 0 25px rgba(157, 80, 187, 0.5)';
    }
    aiIcon.style.color = '#FFFFFF';
    aiText.style.background = 'linear-gradient(45deg, #FFFFFF, #F0F9F6, #FFFFFF)';
    aiText.style.webkitBackgroundClip = 'text';
    aiText.style.webkitTextFillColor = 'transparent';
    aiText.style.backgroundClip = 'text';
}

function applyPdfTheme(themeName) {
    const templates = ['report-content','report-content-outside','report-content-admin','report-content-supervisor','report-content-activity','report-content-student','report-content-health'];
    templates.forEach(id => {
        let el = document.getElementById(id);
        if (el) {
            el.classList.remove('pdf-theme-classic','pdf-theme-professional','pdf-theme-minimal','pdf-theme-tech','pdf-theme-educational');
            el.classList.add('pdf-theme-' + themeName);
        }
    });
    localStorage.setItem(PDF_THEME_KEY, themeName);
}

function applyThemes() {
    const appTheme = document.getElementById('appThemeSelect').value;
    const pdfTheme = document.getElementById('pdfThemeSelect').value;
    applyAppTheme(appTheme);
    applyPdfTheme(pdfTheme);
    showNotification('تم تطبيق الثيمات بنجاح! ✓');
    closeSettings();
}

// ==================== دوال إظهار/إخفاء الحقول ====================
function togglePlaceFields() {
    const place = document.getElementById('place').value;
    const role = document.getElementById('role').value;
    const insideTools = document.getElementById('insideToolsSection');
    const outsideTools = document.getElementById('outsideToolsSection');
    if (place === 'خارج الصف') {
        insideTools.style.display = 'none';
        outsideTools.style.display = 'block';
    } else {
        insideTools.style.display = 'block';
        outsideTools.style.display = 'none';
    }
    // إظهار أو إخفاء حقول المعلم حسب المكان والدور
    const teacherFields = document.getElementById('teacherFields');
    if (role === 'teacher') {
        teacherFields.style.display = place === 'داخل الصف' ? 'block' : 'none';
    } else {
        teacherFields.style.display = 'none';
    }
    updateReport();
}

function toggleDetailedPlaceInput() {
    const select = document.getElementById('detailedPlaceSelect');
    const input = document.getElementById('detailedPlaceInput');
    if (select.value === 'أخرى') {
        input.style.display = 'block';
    } else {
        input.style.display = 'none';
    }
    updateReport();
}

function getDetailedPlaceValue() {
    const select = document.getElementById('detailedPlaceSelect');
    const input = document.getElementById('detailedPlaceInput');
    if (select.value === 'أخرى') {
        return input.value.trim() || 'مكان آخر';
    } else if (select.value) {
        return select.value;
    } else {
        return '';
    }
}

// ==================== تحديث الحقول الخاصة بالدور ====================
function updateRoleSpecificFields(role) {
    const smallContainer = document.getElementById('smallRoleFields');
    const largeContainer = document.getElementById('largeExtraFields');
    const place = document.getElementById('place').value;

    smallContainer.innerHTML = '';
    smallContainer.style.display = 'none';
    largeContainer.innerHTML = '<h4><i class="fas fa-list"></i> تفاصيل إضافية</h4>';
    largeContainer.style.display = 'none';

    let smallHtml = '';
    let largeHtml = '';

    if (role === 'teacher') {
        // حقول المعلم: تظهر فقط إذا كان المكان "داخل الصف"
        if (place === 'داخل الصف') {
            smallHtml = `
                <div class="form-row">
                    <div class="form-group">
                        <label><i class="fas fa-users-class"></i> الصف</label>
                        <input type="text" id="grade" placeholder="مثال: ٥/٣" oninput="updateReport()">
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label><i class="fas fa-book"></i> المادة / البرنامج</label>
                        <input type="text" id="subject" placeholder="مثال: لغتي" oninput="updateReport()">
                    </div>
                    <div class="form-group">
                        <label><i class="fas fa-book-open"></i> الدرس / النشاط</label>
                        <input type="text" id="lesson" placeholder="مثال: درس الضرب" oninput="updateReport()">
                    </div>
                </div>
            `;
        }
    } else if (role === 'school_principal' || role === 'vice_principal') {
        smallHtml = `
            <div class="form-row">
                <div class="form-group">
                    <label><i class="fas fa-tag"></i> المجال</label>
                    <input type="text" id="fieldInput" placeholder="مثال: تربوي" value="تربوي" oninput="updateReport()">
                </div>
                <div class="form-group">
                    <label><i class="fas fa-lightbulb"></i> المبادرة</label>
                    <input type="text" id="initiativeInput" placeholder="اسم المبادرة" oninput="updateReport()">
                </div>
            </div>
            <div class="form-row">
                <div class="form-group">
                    <label><i class="fas fa-clock"></i> مدة التنفيذ</label>
                    <input type="text" id="durationInput" placeholder="مثال: أسبوع" oninput="updateReport()">
                </div>
            </div>
        `;
    } else if (role === 'educational_supervisor') {
        smallHtml = `
            <div class="form-row">
                <div class="form-group">
                    <label><i class="fas fa-tag"></i> المجال</label>
                    <input type="text" id="fieldInput" placeholder="مثال: تربوي" value="تربوي" oninput="updateReport()">
                </div>
                <div class="form-group">
                    <label><i class="fas fa-lightbulb"></i> المبادرة</label>
                    <input type="text" id="initiativeInput" placeholder="اسم المبادرة" value="دعم الأداء الصفي" oninput="updateReport()">
                </div>
            </div>
            <div class="form-row">
                <div class="form-group">
                    <label><i class="fas fa-clock"></i> مدة التنفيذ</label>
                    <input type="text" id="durationInput" placeholder="مثال: حصة واحدة" oninput="updateReport()">
                </div>
            </div>
        `;
    } else if (role === 'activity_leader') {
        smallHtml = `
            <div class="form-row">
                <div class="form-group">
                    <label><i class="fas fa-tag"></i> المجال</label>
                    <input type="text" id="fieldInput" placeholder="مثال: اجتماعي" value="اجتماعي" oninput="updateReport()">
                </div>
                <div class="form-group">
                    <label><i class="fas fa-tag"></i> نوع البرنامج</label>
                    <input type="text" id="programTypeInput" placeholder="نوع البرنامج" value="برنامج تحفيزي" oninput="updateReport()">
                </div>
            </div>
            <div class="form-row">
                <div class="form-group">
                    <label><i class="fas fa-clock"></i> مدة التنفيذ</label>
                    <input type="text" id="durationInput" placeholder="مثال: يوم واحد" oninput="updateReport()">
                </div>
            </div>
        `;
    } else if (role === 'health_guide') {
        smallHtml = `
            <div class="form-row">
                <div class="form-group">
                    <label><i class="fas fa-tag"></i> المجال الصحي</label>
                    <input type="text" id="fieldInput" placeholder="مثال: توعوي" value="توعوي" oninput="updateReport()">
                </div>
                <div class="form-group">
                    <label><i class="fas fa-tag"></i> نوع البرنامج الصحي</label>
                    <input type="text" id="programTypeInput" placeholder="نوع البرنامج" value="حملة توعوية" oninput="updateReport()">
                </div>
            </div>
            <div class="form-row">
                <div class="form-group">
                    <label><i class="fas fa-clock"></i> مدة التنفيذ</label>
                    <input type="text" id="durationInput" placeholder="مثال: يوم واحد" oninput="updateReport()">
                </div>
            </div>
        `;
    } else if (role === 'student_guide') {
        smallHtml = `
            <div class="form-row">
                <div class="form-group">
                    <label><i class="fas fa-lightbulb"></i> المبادرة</label>
                    <input type="text" id="initiativeInput" placeholder="اسم المبادرة" oninput="updateReport()">
                </div>
                <div class="form-group">
                    <label><i class="fas fa-clock"></i> مدة التنفيذ</label>
                    <input type="text" id="durationInput" placeholder="مثال: أسبوع" oninput="updateReport()">
                </div>
            </div>
        `;
        largeHtml = `
            <div class="form-row">
                <div class="form-group">
                    <label><i class="fas fa-hands-helping"></i> الرعاية الطلابية</label>
                    <textarea id="careInput" placeholder="الرعاية الطلابية" oninput="updateReport()"></textarea>
                </div>
                <div class="form-group">
                    <label><i class="fas fa-shield-alt"></i> الوقاية والتوعية</label>
                    <textarea id="awarenessInput" placeholder="الوقاية والتوعية" oninput="updateReport()"></textarea>
                </div>
            </div>
            <div class="form-row">
                <div class="form-group">
                    <label><i class="fas fa-first-aid"></i> التدخل ومعالجة الحالات</label>
                    <textarea id="interventionInput" placeholder="التدخل" oninput="updateReport()"></textarea>
                </div>
                <div class="form-group">
                    <label><i class="fas fa-chart-line"></i> التمكين والدعم</label>
                    <textarea id="supportInput" placeholder="التمكين والدعم" oninput="updateReport()"></textarea>
                </div>
            </div>
            <div class="form-row">
                <div class="form-group">
                    <label><i class="fas fa-family"></i> الشراكة الأسرية</label>
                    <textarea id="familyInput" placeholder="الشراكة الأسرية" oninput="updateReport()"></textarea>
                </div>
                <div class="form-group">
                    <label><i class="fas fa-school"></i> تطوير البيئة المدرسية</label>
                    <textarea id="envInput" placeholder="تطوير البيئة" oninput="updateReport()"></textarea>
                </div>
            </div>
        `;
    }

    if (smallHtml) {
        smallContainer.innerHTML = smallHtml;
        smallContainer.style.display = 'block';
    }
    if (largeHtml) {
        largeContainer.innerHTML += largeHtml;
        largeContainer.style.display = 'block';
    }
}

function updateFieldLabelsByRole(role) {
    const labels = {
        goalLabel: 'الهدف التربوي',
        summaryLabel: 'نبذة مختصرة',
        stepsLabel: 'إجراءات التنفيذ',
        strategiesLabel: 'الاستراتيجيات',
        strengthsLabel: 'نقاط القوة',
        improveLabel: 'نقاط التحسين',
        recommLabel: 'التوصيات'
    };

    if (role === 'school_principal' || role === 'vice_principal') {
        labels.goalLabel = 'الأهداف الإدارية';
        labels.summaryLabel = 'النتائج';
        labels.stepsLabel = 'الإجراءات المنفذة';
        labels.strategiesLabel = 'الاستراتيجيات المتبعة';
        labels.strengthsLabel = 'نقاط القوة';
        labels.improveLabel = 'أولويات التطوير';
        labels.recommLabel = 'خطة المتابعة';
    } else if (role === 'educational_supervisor') {
        // هنا العناوين المطلوبة للمشرف التربوي
        labels.goalLabel = 'الأهداف الإشرافية';
        labels.summaryLabel = 'مستوى الأداء';
        labels.stepsLabel = 'الإجراءات';
        labels.strategiesLabel = 'جوانب التميز';
        labels.strengthsLabel = 'خطة الدعم والمتابعة';
        labels.improveLabel = 'مجالات التحسين';
        labels.recommLabel = 'التوصيات';
    } else if (role === 'activity_leader') {
        labels.goalLabel = 'أهداف البرنامج';
        labels.summaryLabel = 'مستوى التفاعل والمشاركة';
        labels.stepsLabel = 'آلية التنفيذ';
        labels.strategiesLabel = 'أبرز الإنجازات';
        labels.strengthsLabel = 'خطة المتابعة';
        labels.improveLabel = 'التحديات';
        labels.recommLabel = 'التوصيات التطويرية';
    } else if (role === 'student_guide') {
        labels.goalLabel = 'الأهداف';
        labels.summaryLabel = 'الرعاية الطلابية';
        labels.stepsLabel = 'الوقاية والتوعية';
        labels.strategiesLabel = 'التدخل ومعالجة الحالات';
        labels.strengthsLabel = 'التمكين والدعم';
        labels.improveLabel = 'الشراكة الأسرية';
        labels.recommLabel = 'تطوير البيئة المدرسية';
    } else if (role === 'health_guide') {
        labels.goalLabel = 'أهداف البرنامج الصحي';
        labels.summaryLabel = 'مستوى الاستفادة';
        labels.stepsLabel = 'الإجراءات المتخذة';
        labels.strategiesLabel = 'أبرز النتائج';
        labels.strengthsLabel = 'خطة المتابعة الصحية';
        labels.improveLabel = 'التحديات الصحية';
        labels.recommLabel = 'التوصيات الوقائية';
    }

    document.getElementById('goalLabel').textContent = labels.goalLabel;
    document.getElementById('summaryLabel').textContent = labels.summaryLabel;
    document.getElementById('stepsLabel').textContent = labels.stepsLabel;
    document.getElementById('strategiesLabel').textContent = labels.strategiesLabel;
    document.getElementById('strengthsLabel').textContent = labels.strengthsLabel;
    document.getElementById('improveLabel').textContent = labels.improveLabel;
    document.getElementById('recommLabel').textContent = labels.recommLabel;
}

function updateReporterFields(backendRole) {
    const reporterTypeLabel = document.getElementById('reporterTypeLabel');
    const reporterNameLabel = document.getElementById('reporterNameLabel');
    let typeOptions = [];
    let defaultType = '';

    switch (backendRole) {
        case 'teacher':
            reporterTypeLabel.textContent = 'صفة المعلّم';
            reporterNameLabel.textContent = 'اسم المعلّم';
            typeOptions = ['المعلم', 'المعلمة'];
            defaultType = 'المعلم';
            break;
        case 'school_principal':
            reporterTypeLabel.textContent = 'صفة مدير المدرسة';
            reporterNameLabel.textContent = 'اسم مدير المدرسة';
            typeOptions = ['مدير المدرسة', 'مديرة المدرسة'];
            defaultType = 'مدير المدرسة';
            break;
        case 'vice_principal':
            reporterTypeLabel.textContent = 'صفة الوكيل';
            reporterNameLabel.textContent = 'اسم الوكيل';
            typeOptions = ['وكيل المدرسة', 'وكيلة المدرسة'];
            defaultType = 'وكيل المدرسة';
            break;
        case 'student_guide':
            reporterTypeLabel.textContent = 'صفة الموجه الطلابي';
            reporterNameLabel.textContent = 'اسم الموجه الطلابي';
            typeOptions = ['موجه طلابي', 'موجهة طلابية'];
            defaultType = 'موجه طلابي';
            break;
        case 'health_guide':
            reporterTypeLabel.textContent = 'صفة الموجه الصحي';
            reporterNameLabel.textContent = 'اسم الموجه الصحي';
            typeOptions = ['موجه صحي', 'موجهة صحية'];
            defaultType = 'موجه صحي';
            break;
        case 'activity_leader':
            reporterTypeLabel.textContent = 'صفة رائد النشاط';
            reporterNameLabel.textContent = 'اسم رائد النشاط';
            typeOptions = ['رائد نشاط', 'رائدة نشاط'];
            defaultType = 'رائد نشاط';
            break;
        case 'educational_supervisor':
            reporterTypeLabel.textContent = 'صفة المشرف التربوي';
            reporterNameLabel.textContent = 'اسم المشرف التربوي';
            typeOptions = ['مشرف تربوي', 'مشرفة تربوية'];
            defaultType = 'مشرف تربوي';
            break;
        default:
            reporterTypeLabel.textContent = 'صفة مقدم التقرير';
            reporterNameLabel.textContent = 'اسم مقدم التقرير';
            typeOptions = ['مقدم التقرير', 'مقدمة التقرير'];
            defaultType = 'مقدم التقرير';
    }

    const typeSelect = document.getElementById('reporterType');
    typeSelect.innerHTML = '';
    typeOptions.forEach(opt => {
        const option = document.createElement('option');
        option.value = opt;
        option.textContent = opt;
        typeSelect.appendChild(option);
    });
    typeSelect.value = defaultType;

    updatePrincipalType();
    document.getElementById('selectedCriterionWeight').style.display = 'inline-block';
    
    updateFieldLabelsByRole(backendRole);
    updateRoleSpecificFields(backendRole);
    
    // إظهار أو إخفاء حقول المعلم حسب الدور
    const teacherFields = document.getElementById('teacherFields');
    if (backendRole === 'teacher') {
        teacherFields.style.display = document.getElementById('place').value === 'داخل الصف' ? 'block' : 'none';
    } else {
        teacherFields.style.display = 'none';
    }
    
    updateReport();
}

function updatePrincipalType() {
    const reporterType = document.getElementById('reporterType').value;
    const isFemale = reporterType.includes('ة') || reporterType.includes('معلمة') || reporterType.includes('وكيلة') || reporterType.includes('موجهة') || reporterType.includes('رائدة');
    document.getElementById('principalTypeDisplay').value = isFemale ? 'المديرة' : 'المدير';
}

function updateReporterGender() {
    updatePrincipalType();
    updateReport();
}

// ==================== الأدوات الخارجية ====================
function initOutsideTools() {
    const outsideToolsGrid = document.getElementById('outsideToolsGrid');
    const predefinedTools = [
        'مكبر صوت متنقل','أقماع تنظيم','صدريات فرق','بطاقات تعريف','أدوات رسم','حقيبة إسعافات أولية','جهاز لوحي للتوثيق'
    ];
    outsideToolsGrid.innerHTML = '';
    predefinedTools.forEach((tool, index) => {
        const toolId = `outsideTool${index}`;
        const label = document.createElement('label');
        label.className = 'tool-checkbox';
        label.setAttribute('onclick', 'toggleOutsideTool(this)');
        label.innerHTML = `<input type="checkbox" id="${toolId}" value="${tool}" style="display:none;"><span>${tool}</span><span class="checkmark">✅</span>`;
        outsideToolsGrid.appendChild(label);
    });
}

function toggleOutsideTool(element) {
    const checkbox = element.querySelector('input[type="checkbox"]');
    checkbox.checked = !checkbox.checked;
    if (checkbox.checked) element.classList.add('checked');
    else element.classList.remove('checked');
    updateOutsideToolsList();
    updateReport();
}

function addOtherTool() {
    const input = document.getElementById('otherToolInput');
    const toolName = input.value.trim();
    if (toolName === '') return;
    window.otherTools.push(toolName);
    input.value = '';
    updateOtherToolsList();
    updateReport();
}

function removeOtherTool(index) {
    window.otherTools.splice(index, 1);
    updateOtherToolsList();
    updateReport();
}

function updateOtherToolsList() {
    const listContainer = document.getElementById('otherToolsList');
    listContainer.innerHTML = '';
    window.otherTools.forEach((tool, index) => {
        const tag = document.createElement('span');
        tag.className = 'other-tag';
        tag.innerHTML = `${tool} <i class="fas fa-times" onclick="removeOtherTool(${index})"></i>`;
        listContainer.appendChild(tag);
    });
}

function updateOutsideToolsList() {
    const toolsListBox = document.getElementById('outsideToolsListBox');
    if (!toolsListBox) return;
    toolsListBox.innerHTML = '';
    const selectedTools = [];
    document.querySelectorAll('#outsideToolsGrid .tool-checkbox input[type="checkbox"]').forEach(cb => { if (cb.checked) selectedTools.push(cb.value); });
    selectedTools.push(...window.otherTools);
    selectedTools.forEach(tool => {
        const toolElement = document.createElement('div');
        toolElement.className = 'tool';
        toolElement.innerHTML = `<span>✓</span> ${tool}`;
        toolsListBox.appendChild(toolElement);
    });
    if (selectedTools.length === 0) {
        const noToolsMessage = document.createElement('div');
        noToolsMessage.style.textAlign = 'center';
        noToolsMessage.style.color = '#666';
        noToolsMessage.style.fontSize = '9px';
        noToolsMessage.style.padding = '4px';
        noToolsMessage.textContent = 'لم يتم اختيار أي أدوات';
        toolsListBox.appendChild(noToolsMessage);
    }
}

// ==================== تحديثات PDF (مع فحص وجود العناصر) ====================
function updateReport() {
    // تحديث القالب الرئيسي للمعلم (داخل الصف) - مع فحص وجود العناصر
    const role = document.getElementById('role').value;
    const place = document.getElementById('place').value;
    
    const educationBox = document.getElementById('educationBox');
    if (educationBox) educationBox.innerText = document.getElementById('education').value || 'غير محدد';
    
    const schoolBox = document.getElementById('schoolBox');
    if (schoolBox) schoolBox.innerText = document.getElementById('school').value || 'غير محدد';
    
    const termBox = document.getElementById('termBox');
    if (termBox) {
        const termValue = document.getElementById('term').value;
        termBox.innerText = termValue ? `الفصل الدراسي ${termValue}` : 'غير محدد';
    }
    
    const gradeBox = document.getElementById('gradeBox');
    if (gradeBox) gradeBox.innerText = document.getElementById('grade')?.value || 'غير محدد';
    
    const countBox = document.getElementById('countBox');
    if (countBox) countBox.innerText = document.getElementById('count').value || 'غير محدد';
    
    const reportTypeBox = document.getElementById('reportTypeBox');
    if (reportTypeBox) reportTypeBox.innerText = document.getElementById('manualReportTitle').value || 'تقرير';
    
    const targetBox = document.getElementById('targetBox');
    if (targetBox) targetBox.innerText = document.getElementById('target').value || 'غير محدد';
    
    const placeBox = document.getElementById('placeBox');
    if (placeBox) {
        const placeValue = document.getElementById('place').value;
        placeBox.innerText = placeValue === 'داخل الصف' ? 'داخل الصف' : (getDetailedPlaceValue() || 'خارج الصف');
    }
    
    const subjectBox = document.getElementById('subjectBox');
    if (subjectBox) subjectBox.innerText = document.getElementById('subject')?.value || 'غير محدد';
    
    const lessonBox = document.getElementById('lessonBox');
    if (lessonBox) lessonBox.innerText = document.getElementById('lesson')?.value || 'غير محدد';
    
    const reporterNameBox = document.getElementById('reporterNameBox');
    if (reporterNameBox) reporterNameBox.innerText = document.getElementById('reporterName').value || 'غير محدد';
    
    const principalBox = document.getElementById('principalBox');
    if (principalBox) principalBox.innerText = document.getElementById('principal').value || 'غير محدد';
    
    const reporterTypeBox = document.getElementById('reporterTypeBox');
    if (reporterTypeBox) reporterTypeBox.innerText = document.getElementById('reporterType').value || 'مقدم التقرير';
    
    const principalTypeBox = document.getElementById('principalTypeBox');
    if (principalTypeBox) principalTypeBox.innerText = document.getElementById('principalTypeDisplay').value || 'المدير';
    
    const goalBox = document.getElementById('goalBox');
    if (goalBox) goalBox.innerText = document.getElementById('goal').value || 'لم يتم تحديد الهدف التربوي';
    
    const summaryBox = document.getElementById('summaryBox');
    if (summaryBox) summaryBox.innerText = document.getElementById('summary').value || 'لم يتم إضافة نبذة مختصرة';
    
    const stepsBox = document.getElementById('stepsBox');
    if (stepsBox) stepsBox.innerText = document.getElementById('steps').value || 'لم يتم تحديد إجراءات التنفيذ';
    
    const strategiesBox = document.getElementById('strategiesBox');
    if (strategiesBox) strategiesBox.innerText = document.getElementById('strategies').value || 'لم يتم تحديد الاستراتيجيات';
    
    const strengthsBox = document.getElementById('strengthsBox');
    if (strengthsBox) strengthsBox.innerText = document.getElementById('strengths').value || 'لم يتم تحديد نقاط القوة';
    
    const improveBox = document.getElementById('improveBox');
    if (improveBox) improveBox.innerText = document.getElementById('improve').value || 'لم يتم تحديد نقاط التحسين';
    
    const recommBox = document.getElementById('recommBox');
    if (recommBox) recommBox.innerText = document.getElementById('recomm').value || 'لم يتم تحديد التوصيات';
    
    updateToolsDisplay();
    
    // تحديث القوالب الأخرى
    updateOutsideReport();
    updateAdminReport();
    updateSupervisorReport();
    updateActivityReport();
    updateStudentReport();
    updateHealthReport();
}

function updateOutsideReport() {
    // تحديث قالب خارج الصف - مع فحص وجود العناصر
    const place = document.getElementById('place').value;
    if (place !== 'خارج الصف') return;
    
    const schoolBox = document.getElementById('outsideSchoolBox');
    if (schoolBox) schoolBox.innerText = document.getElementById('school').value || 'غير محدد';
    
    const educationBox = document.getElementById('outsideEducationBox');
    if (educationBox) educationBox.innerText = document.getElementById('education').value || 'غير محدد';
    
    const termBox = document.getElementById('outsideTermBox');
    if (termBox) termBox.innerText = document.getElementById('term').value ? `الفصل الدراسي ${document.getElementById('term').value}` : 'غير محدد';
    
    const countBox = document.getElementById('outsideCountBox');
    if (countBox) countBox.innerText = document.getElementById('count').value || 'غير محدد';
    
    const reportTypeBox = document.getElementById('outsideReportTypeBox');
    if (reportTypeBox) reportTypeBox.innerText = document.getElementById('manualReportTitle').value || 'تقرير';
    
    const targetBox = document.getElementById('outsideTargetBox');
    if (targetBox) targetBox.innerText = document.getElementById('target').value || 'غير محدد';
    
    const detailedPlaceBox = document.getElementById('outsideDetailedPlaceBox');
    if (detailedPlaceBox) detailedPlaceBox.innerText = getDetailedPlaceValue() || 'غير محدد';
    
    const reporterNameBox = document.getElementById('outsideReporterNameBox');
    if (reporterNameBox) reporterNameBox.innerText = document.getElementById('reporterName').value || 'غير محدد';
    
    const principalBox = document.getElementById('outsidePrincipalBox');
    if (principalBox) principalBox.innerText = document.getElementById('principal').value || 'غير محدد';
    
    const reporterTypeBox = document.getElementById('outsideReporterTypeBox');
    if (reporterTypeBox) reporterTypeBox.innerText = document.getElementById('reporterType').value || 'مقدم التقرير';
    
    const principalTypeBox = document.getElementById('outsidePrincipalTypeBox');
    if (principalTypeBox) principalTypeBox.innerText = document.getElementById('principalTypeDisplay').value || 'المدير';
    
    const goalBox = document.getElementById('outsideGoalBox');
    if (goalBox) goalBox.innerText = document.getElementById('goal').value || 'لم يتم تحديد الهدف التربوي';
    
    const summaryBox = document.getElementById('outsideSummaryBox');
    if (summaryBox) summaryBox.innerText = document.getElementById('summary').value || 'لم يتم إضافة نبذة مختصرة';
    
    const stepsBox = document.getElementById('outsideStepsBox');
    if (stepsBox) stepsBox.innerText = document.getElementById('steps').value || 'لم يتم تحديد إجراءات التنفيذ';
    
    const strategiesBox = document.getElementById('outsideStrategiesBox');
    if (strategiesBox) strategiesBox.innerText = document.getElementById('strategies').value || 'لم يتم تحديد الاستراتيجيات';
    
    const strengthsBox = document.getElementById('outsideStrengthsBox');
    if (strengthsBox) strengthsBox.innerText = document.getElementById('strengths').value || 'لم يتم تحديد نقاط القوة';
    
    const improveBox = document.getElementById('outsideImproveBox');
    if (improveBox) improveBox.innerText = document.getElementById('improve').value || 'لم يتم تحديد نقاط التحسين';
    
    const recommBox = document.getElementById('outsideRecommBox');
    if (recommBox) recommBox.innerText = document.getElementById('recomm').value || 'لم يتم تحديد التوصيات';
    
    updateOutsideToolsList();
}

function updateAdminReport() {
    const role = document.getElementById('role').value;
    if (role !== 'school_principal' && role !== 'vice_principal') return;
    
    // الحقول الأساسية
    const schoolBox = document.getElementById('adminSchoolBox');
    if (schoolBox) schoolBox.innerText = document.getElementById('school').value || 'غير محدد';
    
    const educationBox = document.getElementById('adminEducationBox');
    if (educationBox) educationBox.innerText = document.getElementById('education').value || 'غير محدد';
    
    const termBox = document.getElementById('adminTermBox');
    if (termBox) termBox.innerText = document.getElementById('term').value || 'غير محدد';
    
    const placeBox = document.getElementById('adminPlaceBox');
    if (placeBox) placeBox.innerText = getDetailedPlaceValue() || 'غير محدد';
    
    const targetBox = document.getElementById('adminTargetBox');
    if (targetBox) targetBox.innerText = document.getElementById('target').value || 'غير محدد';
    
    const countBox = document.getElementById('adminCountBox');
    if (countBox) countBox.innerText = document.getElementById('count').value || 'غير محدد';
    
    const reportTypeBox = document.getElementById('adminReportTypeBox');
    if (reportTypeBox) reportTypeBox.innerText = document.getElementById('manualReportTitle').value || 'تقرير إداري';
    
    // الحقول النصية الكبيرة
    const goalBox = document.getElementById('adminGoalBox');
    if (goalBox) goalBox.innerText = document.getElementById('goal').value || '';
    
    const stepsBox = document.getElementById('adminStepsBox');
    if (stepsBox) stepsBox.innerText = document.getElementById('steps').value || '';
    
    const summaryBox = document.getElementById('adminSummaryBox');
    if (summaryBox) summaryBox.innerText = document.getElementById('summary').value || '';
    
    // استراتيجيات
    const strategiesBox = document.getElementById('adminStrategiesBox');
    if (strategiesBox) strategiesBox.innerText = document.getElementById('strategies').value || '';
    
    const strengthsBox = document.getElementById('adminStrengthsBox');
    if (strengthsBox) strengthsBox.innerText = document.getElementById('strengths').value || '';
    
    const improveBox = document.getElementById('adminImproveBox');
    if (improveBox) improveBox.innerText = document.getElementById('improve').value || '';
    
    const followupBox = document.getElementById('adminFollowupBox');
    if (followupBox) followupBox.innerText = document.getElementById('recomm').value || 'متابعة مستمرة';
    
    // التوقيعات
    const reporterNameBox = document.getElementById('adminReporterNameBox');
    if (reporterNameBox) reporterNameBox.innerText = document.getElementById('reporterName').value || '';
    
    const principalBox = document.getElementById('adminPrincipalBox');
    if (principalBox) principalBox.innerText = document.getElementById('principal').value || '';

    // الحقول الصغيرة
    const fieldInput = document.getElementById('fieldInput');
    const fieldBox = document.getElementById('adminFieldBox');
    if (fieldBox) fieldBox.innerText = fieldInput ? fieldInput.value || 'تربوي' : 'تربوي';
    
    const initiativeInput = document.getElementById('initiativeInput');
    const initiativeBox = document.getElementById('adminInitiativeBox');
    if (initiativeBox) initiativeBox.innerText = initiativeInput ? initiativeInput.value || ('مبادرة ' + (document.getElementById('manualReportTitle').value || '')) : ('مبادرة ' + (document.getElementById('manualReportTitle').value || ''));
    
    const durationInput = document.getElementById('durationInput');
    const durationBox = document.getElementById('adminDurationBox');
    if (durationBox) durationBox.innerText = durationInput ? durationInput.value || 'يوم واحد' : 'يوم واحد';
}

function updateSupervisorReport() {
    const role = document.getElementById('role').value;
    if (role !== 'educational_supervisor') return;
    
    const schoolBox = document.getElementById('supervisorSchoolBox');
    if (schoolBox) schoolBox.innerText = document.getElementById('school').value || 'مكتب الإشراف';
    
    const educationBox = document.getElementById('supervisorEducationBox');
    if (educationBox) educationBox.innerText = document.getElementById('education').value || 'غير محدد';
    
    const termBox = document.getElementById('supervisorTermBox');
    if (termBox) termBox.innerText = document.getElementById('term').value || 'غير محدد';
    
    const placeBox = document.getElementById('supervisorPlaceBox');
    if (placeBox) placeBox.innerText = getDetailedPlaceValue() || 'غير محدد';
    
    const targetBox = document.getElementById('supervisorTargetBox');
    if (targetBox) targetBox.innerText = document.getElementById('target').value || 'غير محدد';
    
    const countBox = document.getElementById('supervisorCountBox');
    if (countBox) countBox.innerText = document.getElementById('count').value || 'غير محدد';
    
    const reportTypeBox = document.getElementById('supervisorReportTypeBox');
    if (reportTypeBox) reportTypeBox.innerText = document.getElementById('manualReportTitle').value || 'تقرير إشرافي';
    
    const goalBox = document.getElementById('supervisorGoalBox');
    if (goalBox) goalBox.innerText = document.getElementById('goal').value || '';
    
    const stepsBox = document.getElementById('supervisorStepsBox');
    if (stepsBox) stepsBox.innerText = document.getElementById('steps').value || '';
    
    const performanceBox = document.getElementById('supervisorPerformanceBox');
    if (performanceBox) performanceBox.innerText = document.getElementById('summary').value || '';
    
    const strengthsBox = document.getElementById('supervisorStrengthsBox');
    if (strengthsBox) strengthsBox.innerText = document.getElementById('strategies').value || '';
    
    const improveBox = document.getElementById('supervisorImproveBox');
    if (improveBox) improveBox.innerText = document.getElementById('improve').value || '';
    
    const recommBox = document.getElementById('supervisorRecommBox');
    if (recommBox) recommBox.innerText = document.getElementById('recomm').value || '';
    
    // خطة الدعم والمتابعة تأخذ من حقل strengths
    const followupBox = document.getElementById('supervisorFollowupBox');
    if (followupBox) followupBox.innerText = document.getElementById('strengths').value || '';
    
    const reporterNameBox = document.getElementById('supervisorReporterNameBox');
    if (reporterNameBox) reporterNameBox.innerText = document.getElementById('reporterName').value || '';
    
    const principalBox = document.getElementById('supervisorPrincipalBox');
    if (principalBox) principalBox.innerText = document.getElementById('principal').value || '';

    const fieldInput = document.getElementById('fieldInput');
    const fieldBox = document.getElementById('supervisorFieldBox');
    if (fieldBox) fieldBox.innerText = fieldInput ? fieldInput.value || 'تربوي' : 'تربوي';
    
    const initiativeInput = document.getElementById('initiativeInput');
    const initiativeBox = document.getElementById('supervisorInitiativeBox');
    if (initiativeBox) initiativeBox.innerText = initiativeInput ? initiativeInput.value || 'دعم الأداء الصفي' : 'دعم الأداء الصفي';
    
    const durationInput = document.getElementById('durationInput');
    const durationBox = document.getElementById('supervisorDurationBox');
    if (durationBox) durationBox.innerText = durationInput ? durationInput.value || 'حصة واحدة' : 'حصة واحدة';
}

function updateActivityReport() {
    const role = document.getElementById('role').value;
    if (role !== 'activity_leader') return;
    
    const schoolBox = document.getElementById('activitySchoolBox');
    if (schoolBox) schoolBox.innerText = document.getElementById('school').value || 'مدرسة ................';
    
    const educationBox = document.getElementById('activityEducationBox');
    if (educationBox) educationBox.innerText = document.getElementById('education').value || 'غير محدد';
    
    const termBox = document.getElementById('activityTermBox');
    if (termBox) termBox.innerText = document.getElementById('term').value || 'غير محدد';
    
    const placeBox = document.getElementById('activityPlaceBox');
    if (placeBox) placeBox.innerText = getDetailedPlaceValue() || 'غير محدد';
    
    const targetBox = document.getElementById('activityTargetBox');
    if (targetBox) targetBox.innerText = document.getElementById('target').value || 'غير محدد';
    
    const countBox = document.getElementById('activityCountBox');
    if (countBox) countBox.innerText = document.getElementById('count').value || 'غير محدد';
    
    const reportTypeBox = document.getElementById('activityReportTypeBox');
    if (reportTypeBox) reportTypeBox.innerText = document.getElementById('manualReportTitle').value || 'تقرير نشاط';
    
    const goalBox = document.getElementById('activityGoalBox');
    if (goalBox) goalBox.innerText = document.getElementById('goal').value || '';
    
    const stepsBox = document.getElementById('activityStepsBox');
    if (stepsBox) stepsBox.innerText = document.getElementById('steps').value || '';
    
    const interactionBox = document.getElementById('activityInteractionBox');
    if (interactionBox) interactionBox.innerText = document.getElementById('summary').value || '';
    
    const strengthsBox = document.getElementById('activityStrengthsBox');
    if (strengthsBox) strengthsBox.innerText = document.getElementById('strategies').value || '';
    
    const improveBox = document.getElementById('activityImproveBox');
    if (improveBox) improveBox.innerText = document.getElementById('improve').value || '';
    
    const recommBox = document.getElementById('activityRecommBox');
    if (recommBox) recommBox.innerText = document.getElementById('recomm').value || '';
    
    const followupBox = document.getElementById('activityFollowupBox');
    if (followupBox) followupBox.innerText = document.getElementById('strengths').value || '';
    
    const reporterNameBox = document.getElementById('activityReporterNameBox');
    if (reporterNameBox) reporterNameBox.innerText = document.getElementById('reporterName').value || '';
    
    const principalBox = document.getElementById('activityPrincipalBox');
    if (principalBox) principalBox.innerText = document.getElementById('principal').value || '';

    const fieldInput = document.getElementById('fieldInput');
    const fieldBox = document.getElementById('activityFieldBox');
    if (fieldBox) fieldBox.innerText = fieldInput ? fieldInput.value || 'اجتماعي' : 'اجتماعي';
    
    const programTypeInput = document.getElementById('programTypeInput');
    const programTypeBox = document.getElementById('activityTypeBox');
    if (programTypeBox) programTypeBox.innerText = programTypeInput ? programTypeInput.value || 'برنامج تحفيزي' : 'برنامج تحفيزي';
    
    const durationInput = document.getElementById('durationInput');
    const durationBox = document.getElementById('activityDurationBox');
    if (durationBox) durationBox.innerText = durationInput ? durationInput.value || 'يوم واحد' : 'يوم واحد';
}

function updateStudentReport() {
    const role = document.getElementById('role').value;
    if (role !== 'student_guide') return;
    
    const schoolBox = document.getElementById('studentSchoolBox');
    if (schoolBox) schoolBox.innerText = document.getElementById('school').value || 'اسم المدرسة';
    
    const educationBox = document.getElementById('studentEducationBox');
    if (educationBox) educationBox.innerText = document.getElementById('education').value || 'غير محدد';
    
    const termBox = document.getElementById('studentTermBox');
    if (termBox) termBox.innerText = document.getElementById('term').value || 'غير محدد';
    
    const placeBox = document.getElementById('studentPlaceBox');
    if (placeBox) placeBox.innerText = getDetailedPlaceValue() || 'غير محدد';
    
    const targetBox = document.getElementById('studentTargetBox');
    if (targetBox) targetBox.innerText = document.getElementById('target').value || 'غير محدد';
    
    const countBox = document.getElementById('studentCountBox');
    if (countBox) countBox.innerText = document.getElementById('count').value || 'غير محدد';
    
    const reportTypeBox = document.getElementById('studentReportTypeBox');
    if (reportTypeBox) reportTypeBox.innerText = document.getElementById('manualReportTitle').value || 'تقرير توجيه طلابي';
    
    const goalBox = document.getElementById('studentGoalBox');
    if (goalBox) goalBox.innerText = document.getElementById('goal').value || '';

    // الحقول الكبيرة
    const careInput = document.getElementById('careInput');
    const careBox = document.getElementById('studentCareBox');
    if (careBox) careBox.innerText = careInput ? careInput.value || '' : '';
    
    const awarenessInput = document.getElementById('awarenessInput');
    const awarenessBox = document.getElementById('studentAwarenessBox');
    if (awarenessBox) awarenessBox.innerText = awarenessInput ? awarenessInput.value || '' : '';
    
    const interventionInput = document.getElementById('interventionInput');
    const interventionBox = document.getElementById('studentInterventionBox');
    if (interventionBox) interventionBox.innerText = interventionInput ? interventionInput.value || '' : '';
    
    const supportInput = document.getElementById('supportInput');
    const supportBox = document.getElementById('studentSupportBox');
    if (supportBox) supportBox.innerText = supportInput ? supportInput.value || '' : '';
    
    const familyInput = document.getElementById('familyInput');
    const familyBox = document.getElementById('studentFamilyBox');
    if (familyBox) familyBox.innerText = familyInput ? familyInput.value || '' : '';
    
    const envInput = document.getElementById('envInput');
    const envBox = document.getElementById('studentEnvBox');
    if (envBox) envBox.innerText = envInput ? envInput.value || '' : '';

    // التوقيعات
    const reporterNameBox = document.getElementById('studentReporterNameBox');
    if (reporterNameBox) reporterNameBox.innerText = document.getElementById('reporterName').value || '';
    
    const principalBox = document.getElementById('studentPrincipalBox');
    if (principalBox) principalBox.innerText = document.getElementById('principal').value || '';

    // الحقول الصغيرة
    const initiativeInput = document.getElementById('initiativeInput');
    const initiativeBox = document.getElementById('studentInitiativeBox');
    if (initiativeBox) initiativeBox.innerText = initiativeInput ? initiativeInput.value || ('مبادرة ' + (document.getElementById('manualReportTitle').value || '')) : ('مبادرة ' + (document.getElementById('manualReportTitle').value || ''));
    
    const durationInput = document.getElementById('durationInput');
    const durationBox = document.getElementById('studentDurationBox');
    if (durationBox) durationBox.innerText = durationInput ? durationInput.value || 'أسبوع' : 'أسبوع';
}

function updateHealthReport() {
    const role = document.getElementById('role').value;
    if (role !== 'health_guide') return;
    
    const schoolBox = document.getElementById('healthSchoolBox');
    if (schoolBox) schoolBox.innerText = document.getElementById('school').value || 'اسم المدرسة';
    
    const educationBox = document.getElementById('healthEducationBox');
    if (educationBox) educationBox.innerText = document.getElementById('education').value || 'غير محدد';
    
    const termBox = document.getElementById('healthTermBox');
    if (termBox) termBox.innerText = document.getElementById('term').value || 'غير محدد';
    
    const placeBox = document.getElementById('healthPlaceBox');
    if (placeBox) placeBox.innerText = getDetailedPlaceValue() || 'غير محدد';
    
    const targetBox = document.getElementById('healthTargetBox');
    if (targetBox) targetBox.innerText = document.getElementById('target').value || 'غير محدد';
    
    const countBox = document.getElementById('healthCountBox');
    if (countBox) countBox.innerText = document.getElementById('count').value || 'غير محدد';
    
    const reportTypeBox = document.getElementById('healthReportTypeBox');
    if (reportTypeBox) reportTypeBox.innerText = document.getElementById('manualReportTitle').value || 'تقرير صحي';
    
    const goalBox = document.getElementById('healthGoalBox');
    if (goalBox) goalBox.innerText = document.getElementById('goal').value || '';
    
    const stepsBox = document.getElementById('healthStepsBox');
    if (stepsBox) stepsBox.innerText = document.getElementById('steps').value || '';
    
    const benefitBox = document.getElementById('healthBenefitBox');
    if (benefitBox) benefitBox.innerText = document.getElementById('summary').value || '';
    
    const challengesBox = document.getElementById('healthChallengesBox');
    if (challengesBox) challengesBox.innerText = document.getElementById('improve').value || '';
    
    const resultsBox = document.getElementById('healthResultsBox');
    if (resultsBox) resultsBox.innerText = document.getElementById('strategies').value || '';
    
    const recommBox = document.getElementById('healthRecommBox');
    if (recommBox) recommBox.innerText = document.getElementById('recomm').value || '';
    
    const followupBox = document.getElementById('healthFollowupBox');
    if (followupBox) followupBox.innerText = document.getElementById('strengths').value || '';
    
    const reporterNameBox = document.getElementById('healthReporterNameBox');
    if (reporterNameBox) reporterNameBox.innerText = document.getElementById('reporterName').value || '';
    
    const principalBox = document.getElementById('healthPrincipalBox');
    if (principalBox) principalBox.innerText = document.getElementById('principal').value || '';

    const fieldInput = document.getElementById('fieldInput');
    const fieldBox = document.getElementById('healthFieldBox');
    if (fieldBox) fieldBox.innerText = fieldInput ? fieldInput.value || 'توعوي' : 'توعوي';
    
    const programTypeInput = document.getElementById('programTypeInput');
    const programBox = document.getElementById('healthProgramBox');
    if (programBox) programBox.innerText = programTypeInput ? programTypeInput.value || 'حملة توعوية' : 'حملة توعوية';
    
    const durationInput = document.getElementById('durationInput');
    const durationBox = document.getElementById('healthDurationBox');
    if (durationBox) durationBox.innerText = durationInput ? durationInput.value || 'يوم واحد' : 'يوم واحد';
}

function toggleTool(element) {
    const checkbox = element.querySelector('input[type="checkbox"]');
    checkbox.checked = !checkbox.checked;
    if (checkbox.checked) element.classList.add('checked'); else element.classList.remove('checked');
    updateToolsDisplay();
}

function updateToolsDisplay() {
    const toolsListBox = document.getElementById('toolsListBox');
    if (!toolsListBox) return;
    toolsListBox.innerHTML = '';
    const selectedTools = [];
    document.querySelectorAll('#toolsGrid .tool-checkbox input[type="checkbox"]').forEach(cb => { if (cb.checked) selectedTools.push(cb.value); });
    selectedTools.forEach(tool => {
        const toolElement = document.createElement('div');
        toolElement.className = 'tool';
        toolElement.innerHTML = `<span>✓</span> ${tool}`;
        toolsListBox.appendChild(toolElement);
    });
    if (selectedTools.length === 0) {
        const noToolsMessage = document.createElement('div');
        noToolsMessage.style.textAlign = 'center';
        noToolsMessage.style.color = '#666';
        noToolsMessage.style.fontSize = '9px';
        noToolsMessage.style.padding = '4px';
        noToolsMessage.textContent = 'لم يتم اختيار أي أدوات';
        toolsListBox.appendChild(noToolsMessage);
    }
}

function loadImage(input, ...targetIds) {
    if (input.files && input.files[0]) {
        const reader = new FileReader();
        reader.onload = function(e) {
            targetIds.forEach(id => {
                const imgBox = document.getElementById(id);
                if (imgBox) {
                    imgBox.innerHTML = '';
                    const img = document.createElement('img');
                    img.src = e.target.result;
                    imgBox.appendChild(img);
                }
            });
        };
        reader.readAsDataURL(input.files[0]);
    }
}

// ==================== دالة تعيين الحقول حسب الدور ====================
function getFieldMappingByRole(role) {
    // التعيين الافتراضي للمعلم وبقية الأدوار (ما عدا المدير والمشرف التربوي)
    const defaultMapping = {
        '1': 'goal',
        '2': 'summary',
        '3': 'steps',
        '4': 'strategies',
        '5': 'strengths',
        '6': 'improve',
        '7': 'recomm'
    };

    // تعيين خاص للمدير والوكيل
    if (role === 'school_principal' || role === 'vice_principal') {
        return {
            '1': 'goal',      // الهدف القيادي
            '2': 'summary',    // النتائج
            '3': 'steps',      // الإجراءات المنفذة
            '4': 'strategies', // الاستراتيجيات المتبعة
            '5': 'strengths',  // نقاط القوة
            '6': 'improve',    // أولويات التطوير
            '7': 'recomm'      // خطة المتابعة
        };
    }
    
    // تعيين خاص للمشرف التربوي
    if (role === 'educational_supervisor') {
        return {
            '1': 'goal',      // الأهداف الإشرافية
            '2': 'steps',     // الإجراءات
            '3': 'summary',   // مستوى الأداء
            '4': 'strategies', // جوانب التميز
            '5': 'improve',   // مجالات التحسين
            '6': 'recomm',    // التوصيات
            '7': 'strengths'  // خطة الدعم والمتابعة
        };
    }

    // تعيين خاص للموجه الطلابي
    if (role === 'student_guide') {
        return {
            '1': 'goal',      // الأهداف
            '2': 'summary',    // الرعاية الطلابية
            '3': 'steps',      // الوقاية والتوعية
            '4': 'strategies', // التدخل ومعالجة الحالات
            '5': 'strengths',  // التمكين والدعم
            '6': 'improve',    // الشراكة الأسرية
            '7': 'recomm'      // تطوير البيئة المدرسية
        };
    }

    // تعيين خاص للموجه الصحي
    if (role === 'health_guide') {
        return {
            '1': 'goal',      // أهداف البرنامج الصحي
            '2': 'steps',     // الإجراءات المتخذة
            '3': 'summary',   // مستوى الاستفادة
            '4': 'improve',   // التحديات الصحية
            '5': 'strategies', // أبرز النتائج
            '6': 'recomm',    // التوصيات الوقائية
            '7': 'strengths'  // خطة المتابعة الصحية
        };
    }

    // تعيين خاص لرائد النشاط
    if (role === 'activity_leader') {
        return {
            '1': 'goal',      // أهداف البرنامج
            '2': 'steps',     // آلية التنفيذ
            '3': 'summary',   // مستوى التفاعل والمشاركة
            '4': 'strategies', // أبرز الإنجازات
            '5': 'improve',   // التحديات
            '6': 'recomm',    // التوصيات التطويرية
            '7': 'strengths'  // خطة المتابعة
        };
    }

    return defaultMapping;
}

// ==================== دالة parseAIResponseProfessional المعدلة ====================
function parseAIResponseProfessional(response) {
    const role = document.getElementById('role').value;
    const fieldMapping = getFieldMappingByRole(role);
    
    const lines = response.split('\n').filter(l => l.trim());
    let found = 0;
    
    lines.forEach(line => {
        const match = line.match(/^(\d+)[\.\-]\s*(.+)/);
        if (match) {
            const num = match[1];
            let content = match[2].trim();
            content = removeFieldTitles(content);
            
            if (fieldMapping[num]) {
                content = ensureWordCount(content, 25);
                document.getElementById(fieldMapping[num]).value = content;
                found++;
            }
        }
    });
    
    if (found < 3) fallbackProfessionalAIParsing(response, role);
    updateReport();
}

// ==================== دالة fallbackProfessionalAIParsing المعدلة ====================
function fallbackProfessionalAIParsing(response, role) {
    const fieldMapping = getFieldMappingByRole(role);
    const sentences = response.split(/[\.\n]/).filter(s => s.trim().length > 20 && !s.match(/الهدف|نبذة|إجراءات|الاستراتيجيات|نقاط القوة|نقاط التحسين|التوصيات|خطة المتابعة/i));
    
    // ترتيب الحقول حسب الأهمية (نفس ترتيب الأرقام)
    const orderedFields = ['goal', 'summary', 'steps', 'strategies', 'strengths', 'improve', 'recomm'];
    
    let idx = 0;
    orderedFields.forEach(field => {
        if (idx < sentences.length) {
            let content = sentences[idx].trim();
            content = removeFieldTitles(content);
            content = ensureWordCount(content, 25);
            document.getElementById(field).value = content;
            idx++;
        }
    });
}

function removeFieldTitles(content) {
    const titles = ['الهدف التربوي','نبذة مختصرة','إجراءات التنفيذ','الاستراتيجيات','نقاط القوة','نقاط التحسين','التوصيات','هو:','تشمل:','يتضمن:','يتمثل في','يشمل','تحتوي','تتضمن'];
    let cleaned = content;
    titles.forEach(t => {
        cleaned = cleaned.replace(new RegExp(`^${t}[:\\.\\-]?\\s*`,'i'), '');
        cleaned = cleaned.replace(new RegExp(`\\s*${t}[:\\.\\-]?\\s*`,'gi'), ' ');
    });
    return cleaned.trim().replace(/\s+/g, ' ') || content;
}

function ensureWordCount(content, target) {
    const words = content.split(' ');
    if (words.length >= target-5 && words.length <= target+5) return content;
    if (words.length < target-5) {
        const phrases = ['مع التركيز على تحقيق أهداف التعلم وتنمية المهارات الأساسية','بما يسهم في رفع مستوى التحصيل الدراسي وتحسين المخرجات التعليمية','مع مراعاة الفروق الفردية وتنويع أساليب التدريس','لضمان تحقيق رؤية التعليم وتطوير العملية التعليمية','مع الاستفادة من أفضل الممارسات التربوية والتقنيات التعليمية الحديثة'];
        let extended = content;
        while (extended.split(' ').length < target) extended += ' ' + phrases[Math.floor(Math.random()*phrases.length)];
        return extended;
    }
    return words.slice(0,target).join(' ');
}

// ==================== حفظ واستعراض التقارير ====================
function saveCurrentReport() {
    const reportTitle = document.getElementById('manualReportTitle').value.trim();
    if (!reportTitle) { showNotification('الرجاء إدخال عنوان التقرير'); return false; }
    const criterionId = document.getElementById('criterionSelect').value || 'manual_' + Date.now();
    const criterionName = document.getElementById('selectedCriterionName')?.textContent || 'تقرير يدوي';
    const criterionWeight = document.getElementById('selectedCriterionWeight')?.textContent || '0%';
    const savedReports = JSON.parse(localStorage.getItem(REPORTS_STORAGE_KEY)) || {};
    let tools = [];
    const place = document.getElementById('place').value;
    const role = document.getElementById('role').value;
    
    // جمع الأدوات فقط إذا كان الدور معلم
    if (role === 'teacher') {
        if (place === 'خارج الصف') {
            document.querySelectorAll('#outsideToolsGrid .tool-checkbox input[type="checkbox"]').forEach(cb => { if (cb.checked) tools.push(cb.value); });
            tools = tools.concat(window.otherTools);
        } else {
            document.querySelectorAll('#toolsGrid .tool-checkbox input[type="checkbox"]').forEach(cb => { if (cb.checked) tools.push(cb.value); });
        }
    }
    
    const uiRole = role;

    // جمع البيانات من الحقول المشتركة والحقول الخاصة
    let extraData = {};
    // الحقول الصغيرة
    if (document.getElementById('grade')) extraData.grade = document.getElementById('grade').value;
    if (document.getElementById('subject')) extraData.subject = document.getElementById('subject').value;
    if (document.getElementById('lesson')) extraData.lesson = document.getElementById('lesson').value;
    if (document.getElementById('fieldInput')) extraData.field = document.getElementById('fieldInput').value;
    if (document.getElementById('initiativeInput')) extraData.initiative = document.getElementById('initiativeInput').value;
    if (document.getElementById('durationInput')) extraData.duration = document.getElementById('durationInput').value;
    if (document.getElementById('programTypeInput')) extraData.programType = document.getElementById('programTypeInput').value;
    if (document.getElementById('careInput')) extraData.care = document.getElementById('careInput').value;
    if (document.getElementById('awarenessInput')) extraData.awareness = document.getElementById('awarenessInput').value;
    if (document.getElementById('interventionInput')) extraData.intervention = document.getElementById('interventionInput').value;
    if (document.getElementById('supportInput')) extraData.support = document.getElementById('supportInput').value;
    if (document.getElementById('familyInput')) extraData.family = document.getElementById('familyInput').value;
    if (document.getElementById('envInput')) extraData.env = document.getElementById('envInput').value;

    const reportData = {
        id: Date.now().toString(),
        title: reportTitle,
        criterionId, criterionName, weight: criterionWeight,
        date: currentGregorianDate, hijriDate: currentHijriDate,
        place, detailedPlace: getDetailedPlaceValue(),
        role: uiRole,
        data: {
            education: document.getElementById('education').value,
            school: document.getElementById('school').value,
            reporterType: document.getElementById('reporterType').value,
            reporterName: document.getElementById('reporterName').value,
            principal: document.getElementById('principal').value,
            term: document.getElementById('term').value,
            target: document.getElementById('target').value,
            count: document.getElementById('count').value,
            place, detailedPlace: getDetailedPlaceValue(),
            goal: document.getElementById('goal').value,
            summary: document.getElementById('summary').value,
            steps: document.getElementById('steps').value,
            strategies: document.getElementById('strategies').value,
            strengths: document.getElementById('strengths').value,
            improve: document.getElementById('improve').value,
            recomm: document.getElementById('recomm').value,
            tools, otherTools: window.otherTools,
            ...extraData
        }
    };

    savedReports[criterionId] = reportData;
    localStorage.setItem(REPORTS_STORAGE_KEY, JSON.stringify(savedReports));
    calculateProgress();
    return true;
}

function calculateProgress() {
    const progressContainer = document.getElementById('progressBarContainer');
    if (!progressContainer) return;
    const savedReports = JSON.parse(localStorage.getItem(REPORTS_STORAGE_KEY)) || {};
    const criteria = window.allCriteria || [];
    if (criteria.length === 0) { progressContainer.style.display = 'none'; return; }
    const totalWeight = criteria.reduce((sum, c) => sum + (parseFloat(c.weight) || 0), 0);
    let completedWeight = 0, completedCount = 0;
    criteria.forEach(c => { if (savedReports[c.id]) { completedWeight += (parseFloat(c.weight)||0); completedCount++; } });
    const percentage = totalWeight > 0 ? Math.round((completedWeight / totalWeight) * 100) : 0;
    document.getElementById('progressPercentage').textContent = percentage + '%';
    document.getElementById('progressFill').style.width = percentage + '%';
    document.getElementById('progressMessage').textContent = `${completedCount} من ${criteria.length} معايير مكتملة (${completedWeight} من ${totalWeight} نقطة)`;
}

function loadSavedReport(criterionId) {
    const savedReports = JSON.parse(localStorage.getItem(REPORTS_STORAGE_KEY)) || {};
    const report = savedReports[criterionId];
    if (!report) return false;

    if (report.role) {
        document.getElementById('role').value = report.role;
        const backendRole = getBackendRole(report.role);
        loadDataFromBackend(backendRole);
    }

    // تعبئة الحقول الأساسية
    document.getElementById('education').value = report.data.education || '';
    document.getElementById('school').value = report.data.school || '';
    document.getElementById('reporterType').value = report.data.reporterType || 'المعلم';
    document.getElementById('reporterName').value = report.data.reporterName || '';
    document.getElementById('principal').value = report.data.principal || '';
    document.getElementById('term').value = report.data.term || '';
    document.getElementById('target').value = report.data.target || '';
    document.getElementById('count').value = report.data.count || '';
    document.getElementById('place').value = report.data.place || 'داخل الصف';
    document.getElementById('goal').value = report.data.goal || '';
    document.getElementById('summary').value = report.data.summary || '';
    document.getElementById('steps').value = report.data.steps || '';
    document.getElementById('strategies').value = report.data.strategies || '';
    document.getElementById('strengths').value = report.data.strengths || '';
    document.getElementById('improve').value = report.data.improve || '';
    document.getElementById('recomm').value = report.data.recomm || '';
    document.getElementById('manualReportTitle').value = report.title || '';

    // تعبئة الحقول الخاصة بعد إنشائها (بعد استدعاء updateRoleSpecificFields)
    setTimeout(() => {
        if (document.getElementById('grade')) document.getElementById('grade').value = report.data.grade || '';
        if (document.getElementById('subject')) document.getElementById('subject').value = report.data.subject || '';
        if (document.getElementById('lesson')) document.getElementById('lesson').value = report.data.lesson || '';
        if (document.getElementById('fieldInput')) document.getElementById('fieldInput').value = report.data.field || '';
        if (document.getElementById('initiativeInput')) document.getElementById('initiativeInput').value = report.data.initiative || '';
        if (document.getElementById('durationInput')) document.getElementById('durationInput').value = report.data.duration || '';
        if (document.getElementById('programTypeInput')) document.getElementById('programTypeInput').value = report.data.programType || '';
        if (document.getElementById('careInput')) document.getElementById('careInput').value = report.data.care || '';
        if (document.getElementById('awarenessInput')) document.getElementById('awarenessInput').value = report.data.awareness || '';
        if (document.getElementById('interventionInput')) document.getElementById('interventionInput').value = report.data.intervention || '';
        if (document.getElementById('supportInput')) document.getElementById('supportInput').value = report.data.support || '';
        if (document.getElementById('familyInput')) document.getElementById('familyInput').value = report.data.family || '';
        if (document.getElementById('envInput')) document.getElementById('envInput').value = report.data.env || '';
    }, 200);

    const detailedPlace = report.data.detailedPlace || '';
    const detailedPlaceSelect = document.getElementById('detailedPlaceSelect');
    const detailedPlaceInput = document.getElementById('detailedPlaceInput');
    const options = Array.from(detailedPlaceSelect.options).map(opt => opt.value);
    if (options.includes(detailedPlace)) {
        detailedPlaceSelect.value = detailedPlace;
        detailedPlaceInput.style.display = 'none';
        detailedPlaceInput.value = '';
    } else {
        detailedPlaceSelect.value = 'أخرى';
        detailedPlaceInput.style.display = 'block';
        detailedPlaceInput.value = detailedPlace;
    }

    window.otherTools = report.data.otherTools || [];
    updateOtherToolsList();
    togglePlaceFields();
    if (report.role === 'teacher') {
        if (report.data.place === 'خارج الصف') {
            document.querySelectorAll('#outsideToolsGrid .tool-checkbox').forEach(toolElement => {
                const checkbox = toolElement.querySelector('input[type="checkbox"]');
                if (checkbox && report.data.tools.includes(checkbox.value)) {
                    checkbox.checked = true; toolElement.classList.add('checked');
                } else { checkbox.checked = false; toolElement.classList.remove('checked'); }
            });
        } else {
            document.querySelectorAll('#toolsGrid .tool-checkbox').forEach(toolElement => {
                const checkbox = toolElement.querySelector('input[type="checkbox"]');
                if (checkbox && report.data.tools.includes(checkbox.value)) {
                    checkbox.checked = true; toolElement.classList.add('checked');
                } else { checkbox.checked = false; toolElement.classList.remove('checked'); }
            });
        }
    }
    updateReporterGender();
    updateReport();
    showNotification('تم تحميل التقرير بنجاح!');
    return true;
}

function openSavedReports() {
    const savedReports = JSON.parse(localStorage.getItem(REPORTS_STORAGE_KEY)) || {};
    const reportsList = document.getElementById('savedReportsList');
    calculateProgress();
    if (Object.keys(savedReports).length === 0) {
        reportsList.innerHTML = `<div class="empty-reports"><i class="fas fa-folder-open"></i><p>لا توجد تقارير محفوظة</p><p style="font-size:12px; margin-top:10px;">قم بإنشاء تقرير وحفظه ليظهر هنا</p></div>`;
    } else {
        reportsList.innerHTML = '';
        Object.values(savedReports).sort((a,b)=>b.id-a.id).forEach(report => {
            const card = document.createElement('div');
            card.className = 'report-card completed';
            card.innerHTML = `
                <div class="report-title">${report.title}</div>
                <div class="report-criterion"><i class="fas fa-star"></i> ${report.criterionName}</div>
                <div class="report-weight">الوزن: ${formatWeight(report.weight)}</div>
                <div class="report-date"><i class="fas fa-calendar"></i> ${report.date} | ${report.hijriDate} هـ</div>
                <div class="report-actions">
                    <button class="load-btn" onclick="loadSavedReport('${report.criterionId}'); closeSavedReports();" title="فتح في النموذج"><i class="fas fa-download"></i> فتح</button>
                    <button class="pdf-btn" onclick="downloadSavedReport('${report.criterionId}')" title="تنزيل PDF"><i class="fas fa-file-pdf"></i> PDF</button>
                    <button class="whatsapp-btn" onclick="shareSavedReportWhatsApp('${report.criterionId}')" title="مشاركة عبر واتساب"><i class="fab fa-whatsapp"></i></button>
                    <button class="delete-btn" onclick="deleteSavedReport('${report.criterionId}')" title="حذف"><i class="fas fa-trash"></i></button>
                </div>
            `;
            reportsList.appendChild(card);
        });
    }
    document.getElementById('savedReportsModal').style.display = 'flex';
}

function closeSavedReports() {
    document.getElementById('savedReportsModal').style.display = 'none';
}

async function downloadSavedReport(criterionId) {
    if (loadSavedReport(criterionId)) {
        await new Promise(resolve => setTimeout(resolve, 100));
        await downloadPDF();
    }
}

async function shareSavedReportWhatsApp(criterionId) {
    if (loadSavedReport(criterionId)) {
        await new Promise(resolve => setTimeout(resolve, 100));
        await sharePDFWhatsApp();
    }
}

function deleteSavedReport(criterionId) {
    if (!confirm('هل أنت متأكد من حذف هذا التقرير؟')) return;
    const savedReports = JSON.parse(localStorage.getItem(REPORTS_STORAGE_KEY)) || {};
    delete savedReports[criterionId];
    localStorage.setItem(REPORTS_STORAGE_KEY, JSON.stringify(savedReports));
    calculateProgress();
    if (document.getElementById('savedReportsModal').style.display === 'flex') {
        closeSavedReports(); setTimeout(openSavedReports, 300);
    }
    showNotification('تم حذف التقرير بنجاح!');
}

// ==================== تحميل البيانات من الباك اند ====================
async function loadDataFromBackend(backendRole) {
    window.currentRole = backendRole;
    try {
        const structureResponse = await fetch(BACKEND_URL + "/api/full-structure?role=" + encodeURIComponent(backendRole));
        const structureData = await structureResponse.json();
        const structure = structureData.structure;
        window.allCriteria = structure;
        const criterionSelect = document.getElementById("criterionSelect");
        criterionSelect.innerHTML = '<option value="">اختر معيار الاداء الوظيفي</option>';
        window.subcategoriesByCriterion = {};
        window.reportsBySubcategory = {};
        window.allReportsList = [];
        structure.forEach(criterion => {
            let optionText = `${criterion.name} (${formatWeight(criterion.weight)})`;
            const option = document.createElement("option");
            option.value = criterion.id; option.textContent = optionText;
            criterionSelect.appendChild(option);
            window.subcategoriesByCriterion[criterion.id] = criterion.subcategories || [];
            if (criterion.subcategories) {
                criterion.subcategories.forEach(sub => {
                    window.reportsBySubcategory[sub.id] = sub.reports || [];
                    if (sub.reports) {
                        sub.reports.forEach(report => {
                            window.allReportsList.push({ id: report.id, name: report.name, subcategory_id: sub.id, subcategory_name: sub.name, criterion_id: criterion.id, criterion_name: criterion.name });
                        });
                    }
                });
            }
        });
        const educationResponse = await fetch(BACKEND_URL + "/api/education-offices");
        const educationOffices = await educationResponse.json();
        const educationSelect = document.getElementById("education");
        educationSelect.innerHTML = '<option value="">اختر إدارة التعليم</option>';
        educationOffices.forEach(office => {
            const option = document.createElement("option");
            option.value = office; option.textContent = office;
            educationSelect.appendChild(option);
        });
        const toolsResponse = await fetch(BACKEND_URL + "/api/educational-tools");
        const educationalTools = await toolsResponse.json();
        const toolsGrid = document.getElementById("toolsGrid");
        toolsGrid.innerHTML = "";
        educationalTools.forEach((tool, index) => {
            const toolId = `tool${index+1}`;
            const label = document.createElement("label");
            label.className = "tool-checkbox";
            label.setAttribute("onclick", "toggleTool(this)");
            label.innerHTML = `<input type="checkbox" id="${toolId}" value="${tool}" style="display:none;"><span>${tool}</span><span class="checkmark">✅</span>`;
            toolsGrid.appendChild(label);
        });
        initOutsideTools();
        updateReporterFields(backendRole);
        calculateProgress();
        console.log("تم تحميل البيانات بنجاح للدور:", backendRole);
    } catch (error) {
        console.error("خطأ في تحميل البيانات:", error);
        showNotification("حدث خطأ في تحميل البيانات. سيتم استخدام البيانات المحفوظة محلياً.");
    }
}

function handleRoleChange() {
    const uiRole = document.getElementById('role').value;
    if (!uiRole) return;
    const backendRole = getBackendRole(uiRole);
    loadDataFromBackend(backendRole);
    document.getElementById('criterionSelect').value = '';
    document.getElementById('subcategorySelect').innerHTML = '<option value="">اختر التصنيف الفرعي</option>';
    document.getElementById('subcategorySelect').disabled = true;
    document.getElementById('reportSelect').innerHTML = '<option value="">اختر التقرير</option>';
    document.getElementById('reportSelect').disabled = true;
    document.getElementById('criterionInfo').style.display = 'none';
}

// ==================== القوائم المتتالية ====================
function loadSubcategories() {
    const criterionId = document.getElementById('criterionSelect').value;
    const subcategorySelect = document.getElementById('subcategorySelect');
    const reportSelect = document.getElementById('reportSelect');
    const criterionInfo = document.getElementById('criterionInfo');
    if (!criterionId) {
        subcategorySelect.innerHTML = '<option value="">اختر التصنيف الفرعي</option>';
        subcategorySelect.disabled = true;
        reportSelect.innerHTML = '<option value="">اختر التقرير</option>';
        reportSelect.disabled = true;
        criterionInfo.style.display = 'none';
        return;
    }
    const criterion = window.allCriteria.find(c => c.id === criterionId);
    if (criterion) {
        document.getElementById('selectedCriterionName').textContent = criterion.name;
        document.getElementById('selectedCriterionWeight').textContent = formatWeight(criterion.weight);
        criterionInfo.style.display = 'flex';
    }
    const subcategories = window.subcategoriesByCriterion[criterionId] || [];
    subcategorySelect.innerHTML = '<option value="">اختر التصنيف الفرعي</option>';
    subcategories.forEach(sub => {
        const option = document.createElement("option");
        option.value = sub.id; option.textContent = sub.name;
        subcategorySelect.appendChild(option);
    });
    subcategorySelect.disabled = false;
    reportSelect.innerHTML = '<option value="">اختر التقرير</option>';
    reportSelect.disabled = true;
}

function loadReports() {
    const subcategoryId = document.getElementById('subcategorySelect').value;
    const reportSelect = document.getElementById('reportSelect');
    if (!subcategoryId) {
        reportSelect.innerHTML = '<option value="">اختر التقرير</option>';
        reportSelect.disabled = true;
        return;
    }
    const reports = window.reportsBySubcategory[subcategoryId] || [];
    reportSelect.innerHTML = '<option value="">اختر التقرير</option>';
    reports.forEach(report => {
        const option = document.createElement("option");
        option.value = report.id; option.textContent = report.name;
        reportSelect.appendChild(option);
    });
    reportSelect.disabled = false;
}

function updateReportFromSelection() {
    const reportSelect = document.getElementById('reportSelect');
    if (reportSelect.value && reportSelect.selectedOptions[0]) {
        document.getElementById('manualReportTitle').value = reportSelect.selectedOptions[0].textContent;
    }
    updateReport();
}

function handleReportSearch() {
    const reportSearch = document.getElementById('reportSearch');
    const searchResults = document.getElementById('searchResults');
    const searchTerm = reportSearch.value.trim().toLowerCase();
    if (searchTerm === '') { searchResults.style.display = 'none'; searchResults.innerHTML = ''; return; }
    const filteredReports = window.allReportsList.filter(report => report.name.toLowerCase().includes(searchTerm));
    if (filteredReports.length > 0) {
        searchResults.innerHTML = '';
        filteredReports.slice(0,15).forEach(report => {
            const div = document.createElement('div');
            div.textContent = `${report.name} (${report.criterion_name})`;
            div.style.padding = '8px 12px'; div.style.cursor = 'pointer';
            div.onmouseover = () => div.style.backgroundColor = '#f0f9f6';
            div.onmouseout = () => div.style.backgroundColor = 'white';
            div.onclick = () => {
                document.getElementById('criterionSelect').value = report.criterion_id;
                loadSubcategories();
                setTimeout(() => {
                    document.getElementById('subcategorySelect').value = report.subcategory_id;
                    loadReports();
                    setTimeout(() => {
                        document.getElementById('reportSelect').value = report.id;
                        document.getElementById('manualReportTitle').value = report.name;
                        updateReport();
                    }, 100);
                }, 100);
                reportSearch.value = '';
                searchResults.style.display = 'none';
                showNotification(`تم تحديد التقرير: ${report.name}`);
            };
            searchResults.appendChild(div);
        });
        searchResults.style.display = 'block';
    } else {
        searchResults.innerHTML = '<div style="padding:12px; color:#666; text-align:center;">لا توجد نتائج</div>';
        searchResults.style.display = 'block';
    }
}

// ==================== التعبئة الذكية (المعدلة لإرسال الحقول الإضافية) ====================
async function fillWithAI() {
    const activationCode = localStorage.getItem(ACTIVATION_KEY_NAME);
    if (!activationCode) { alert('الرجاء تفعيل الأداة أولاً باستخدام كود التفعيل'); return; }
    if (!navigator.onLine) { alert('لا يوجد اتصال بالإنترنت.'); return; }
    const reportTitle = document.getElementById('manualReportTitle').value.trim();
    if (!reportTitle) { alert('الرجاء إدخال عنوان التقرير أولاً'); return; }
    const criterionId = document.getElementById('criterionSelect').value || null;
    const subcategoryId = document.getElementById('subcategorySelect').value || null;
    const reportId = document.getElementById('reportSelect').value || null;
    const uiRole = document.getElementById('role').value;
    const backendRole = getBackendRole(uiRole);
    
    // قراءة الحقول الإضافية
    const field = document.getElementById('fieldInput')?.value || '';
    const initiative = document.getElementById('initiativeInput')?.value || '';
    const duration = document.getElementById('durationInput')?.value || '';
    const subject = document.getElementById('subject')?.value || '';
    const lesson = document.getElementById('lesson')?.value || '';
    const grade = document.getElementById('grade')?.value || '';
    
    const aiButton = document.getElementById('aiFillFloatingBtn');
    const originalText = aiButton.querySelector('.floating-ai-text').textContent;
    const originalIcon = aiButton.querySelector('.floating-ai-icon').className;
    aiButton.classList.add('loading');
    aiButton.querySelector('.floating-ai-text').textContent = 'جارٍ...';
    aiButton.querySelector('.floating-ai-icon').className = 'fas fa-spinner fa-spin floating-ai-icon';
    aiButton.disabled = true;
    try {
        const response = await fetch(BACKEND_URL + "/api/generate-report-content", {
            method: 'POST',
            headers: { 'Content-Type': 'application/json', 'X-Activation-Code': activationCode },
            body: JSON.stringify({ 
                criterion_id: criterionId, 
                subcategory_id: subcategoryId, 
                report_id: reportId, 
                role: backendRole, 
                report_data: { 
                    subject: subject,
                    lesson: lesson,
                    grade: grade,
                    target: document.getElementById('target').value || '', 
                    place: document.getElementById('place').value || '', 
                    count: document.getElementById('count').value || '', 
                    title: reportTitle,
                    field: field,
                    initiative: initiative,
                    duration: duration
                } 
            })
        });
        if (!response.ok) throw new Error("تعذر تنفيذ الطلب");
        const data = await response.json();
        if (!data || !data.content) throw new Error('لم يتم الحصول على إجابة من الذكاء الاصطناعي');
        parseAIResponseProfessional(data.content);
        saveCurrentReport();
        showGuideBox();
    } catch (error) {
        console.error('خطأ في الذكاء الاصطناعي:', error);
        alert(error.message || "تعذر تنفيذ الطلب.");
    } finally {
        aiButton.classList.remove('loading');
        aiButton.querySelector('.floating-ai-text').textContent = originalText;
        aiButton.querySelector('.floating-ai-icon').className = originalIcon;
        aiButton.disabled = false;
        updateAiButtonTheme(localStorage.getItem(APP_THEME_KEY) || 'default');
    }
}

function showGuideBox() {
    const guideBox = document.getElementById('aiGuideBox');
    const timerSpan = document.getElementById('guideTimer');
    let seconds = 20;
    if (window.guideTimerInterval) clearInterval(window.guideTimerInterval);
    window.guideTimerInterval = setInterval(() => { seconds--; timerSpan.textContent = seconds; if (seconds <= 0) { clearInterval(window.guideTimerInterval); guideBox.style.display = 'none'; } }, 1000);
    document.getElementById('guideDownloadBtn').onclick = function() { downloadPDF(); clearInterval(window.guideTimerInterval); guideBox.style.display = 'none'; };
    document.getElementById('guideCloseBtn').onclick = function() { clearInterval(window.guideTimerInterval); guideBox.style.display = 'none'; };
    guideBox.style.display = 'block';
}

function saveTeacherData() {
    saveCurrentReport();
    const teacherData = {
        education: document.getElementById('education').value,
        school: document.getElementById('school').value,
        grade: document.getElementById('grade')?.value || '',
        subject: document.getElementById('subject')?.value || '',
        target: document.getElementById('target').value,
        place: document.getElementById('place').value,
        detailedPlace: getDetailedPlaceValue(),
        lesson: document.getElementById('lesson')?.value || '',
        reporterName: document.getElementById('reporterName').value,
        principal: document.getElementById('principal').value,
        reporterType: document.getElementById('reporterType').value,
        term: document.getElementById('term').value,
        count: document.getElementById('count').value,
        manualTitle: document.getElementById('manualReportTitle').value,
        criterion: document.getElementById('criterionSelect').value,
        subcategory: document.getElementById('subcategorySelect').value,
        report: document.getElementById('reportSelect').value,
        role: document.getElementById('role').value,
        tools: []
    };
    const place = document.getElementById('place').value;
    const role = document.getElementById('role').value;
    if (role === 'teacher') {
        if (place === 'خارج الصف') {
            document.querySelectorAll('#outsideToolsGrid .tool-checkbox input[type="checkbox"]').forEach(cb => { if (cb.checked) teacherData.tools.push(cb.value); });
            teacherData.tools = teacherData.tools.concat(window.otherTools);
        } else {
            document.querySelectorAll('#toolsGrid .tool-checkbox input[type="checkbox"]').forEach(cb => { if (cb.checked) teacherData.tools.push(cb.value); });
        }
    }
    ['goal','summary','steps','strategies','strengths','improve','recomm'].forEach(f => teacherData[f] = document.getElementById(f).value);
    // إضافة الحقول الخاصة
    if (document.getElementById('fieldInput')) teacherData.field = document.getElementById('fieldInput').value;
    if (document.getElementById('initiativeInput')) teacherData.initiative = document.getElementById('initiativeInput').value;
    if (document.getElementById('durationInput')) teacherData.duration = document.getElementById('durationInput').value;
    if (document.getElementById('programTypeInput')) teacherData.programType = document.getElementById('programTypeInput').value;
    if (document.getElementById('careInput')) teacherData.care = document.getElementById('careInput').value;
    if (document.getElementById('awarenessInput')) teacherData.awareness = document.getElementById('awarenessInput').value;
    if (document.getElementById('interventionInput')) teacherData.intervention = document.getElementById('interventionInput').value;
    if (document.getElementById('supportInput')) teacherData.support = document.getElementById('supportInput').value;
    if (document.getElementById('familyInput')) teacherData.family = document.getElementById('familyInput').value;
    if (document.getElementById('envInput')) teacherData.env = document.getElementById('envInput').value;
    localStorage.setItem('teacherData', JSON.stringify(teacherData));
    showNotification('تم حفظ بيانات مقدم التقرير بنجاح!');
}

function showNotification(message) {
    const notification = document.createElement('div');
    notification.className = 'notification';
    notification.innerHTML = `<i class="fas fa-check-circle"></i><span>${message}</span>`;
    document.body.appendChild(notification);
    setTimeout(() => notification.classList.add('show'), 10);
    setTimeout(() => { notification.classList.remove('show'); setTimeout(() => document.body.removeChild(notification), 400); }, 3000);
}

function loadTeacherData() {
    const savedData = localStorage.getItem('teacherData');
    if (savedData) {
        const teacherData = JSON.parse(savedData);
        document.getElementById('education').value = teacherData.education || '';
        document.getElementById('school').value = teacherData.school || '';
        if (document.getElementById('grade')) document.getElementById('grade').value = teacherData.grade || '';
        if (document.getElementById('subject')) document.getElementById('subject').value = teacherData.subject || '';
        document.getElementById('target').value = teacherData.target || '';
        document.getElementById('place').value = teacherData.place || 'داخل الصف';
        if (document.getElementById('lesson')) document.getElementById('lesson').value = teacherData.lesson || '';
        document.getElementById('reporterName').value = teacherData.reporterName || '';
        document.getElementById('principal').value = teacherData.principal || '';
        document.getElementById('reporterType').value = teacherData.reporterType || 'المعلم';
        document.getElementById('term').value = teacherData.term || '';
        document.getElementById('count').value = teacherData.count || '';
        document.getElementById('manualReportTitle').value = teacherData.manualTitle || '';
        if (teacherData.role) {
            document.getElementById('role').value = teacherData.role;
            const backendRole = getBackendRole(teacherData.role);
            loadDataFromBackend(backendRole);
        }
        if (teacherData.detailedPlace) {
            const detailedPlaceSelect = document.getElementById('detailedPlaceSelect');
            const detailedPlaceInput = document.getElementById('detailedPlaceInput');
            const options = Array.from(detailedPlaceSelect.options).map(opt => opt.value);
            if (options.includes(teacherData.detailedPlace)) {
                detailedPlaceSelect.value = teacherData.detailedPlace;
                detailedPlaceInput.style.display = 'none';
                detailedPlaceInput.value = '';
            } else {
                detailedPlaceSelect.value = 'أخرى';
                detailedPlaceInput.style.display = 'block';
                detailedPlaceInput.value = teacherData.detailedPlace;
            }
        }
        ['goal','summary','steps','strategies','strengths','improve','recomm'].forEach(f => { if (teacherData[f]) document.getElementById(f).value = teacherData[f]; });
        window.otherTools = teacherData.tools ? teacherData.tools.filter(t => !['مكبر صوت متنقل','أقماع تنظيم','صدريات فرق','بطاقات تعريف','أدوات رسم','حقيبة إسعافات أولية','جهاز لوحي للتوثيق'].includes(t)) : [];
        updateOtherToolsList();
        togglePlaceFields();
        if (teacherData.role === 'teacher') {
            if (teacherData.place === 'خارج الصف') {
                document.querySelectorAll('#outsideToolsGrid .tool-checkbox').forEach(toolElement => {
                    const checkbox = toolElement.querySelector('input[type="checkbox"]');
                    if (checkbox && teacherData.tools && teacherData.tools.includes(checkbox.value)) { checkbox.checked = true; toolElement.classList.add('checked'); }
                    else { checkbox.checked = false; toolElement.classList.remove('checked'); }
                });
            } else {
                document.querySelectorAll('#toolsGrid .tool-checkbox').forEach(toolElement => {
                    const checkbox = toolElement.querySelector('input[type="checkbox"]');
                    if (checkbox && teacherData.tools && teacherData.tools.includes(checkbox.value)) { checkbox.checked = true; toolElement.classList.add('checked'); }
                    else { checkbox.checked = false; toolElement.classList.remove('checked'); }
                });
            }
        }
        updateReporterGender();
        updateReport();
    }
}

function clearData() {
    if (confirm("هل أنت متأكد من مسح بيانات مقدم التقرير والنصوص المولدة؟")) {
        document.getElementById('education').value = '';
        document.getElementById('school').value = '';
        document.getElementById('reporterName').value = '';
        document.getElementById('principal').value = '';
        if (document.getElementById('grade')) document.getElementById('grade').value = '';
        document.getElementById('term').value = '';
        if (document.getElementById('subject')) document.getElementById('subject').value = '';
        if (document.getElementById('lesson')) document.getElementById('lesson').value = '';
        document.getElementById('target').value = '';
        document.getElementById('count').value = '';
        document.getElementById('place').value = 'داخل الصف';
        document.getElementById('manualReportTitle').value = '';
        document.getElementById('detailedPlaceSelect').value = '';
        document.getElementById('detailedPlaceInput').value = '';
        document.getElementById('detailedPlaceInput').style.display = 'none';
        ['goal','summary','steps','strategies','strengths','improve','recomm'].forEach(f => document.getElementById(f).value = '');
        document.querySelectorAll('#toolsGrid .tool-checkbox input[type="checkbox"]').forEach(cb => { cb.checked = false; cb.closest('.tool-checkbox')?.classList.remove('checked'); });
        document.querySelectorAll('#outsideToolsGrid .tool-checkbox input[type="checkbox"]').forEach(cb => { cb.checked = false; cb.closest('.tool-checkbox')?.classList.remove('checked'); });
        window.otherTools = [];
        updateOtherToolsList();
        document.getElementById('criterionSelect').value = '';
        document.getElementById('subcategorySelect').innerHTML = '<option value="">اختر التصنيف الفرعي</option>';
        document.getElementById('subcategorySelect').disabled = true;
        document.getElementById('reportSelect').innerHTML = '<option value="">اختر التقرير</option>';
        document.getElementById('reportSelect').disabled = true;
        document.getElementById('criterionInfo').style.display = 'none';
        // مسح الحقول الخاصة
        const smallContainer = document.getElementById('smallRoleFields');
        if (smallContainer) {
            const inputs = smallContainer.querySelectorAll('input, textarea');
            inputs.forEach(input => input.value = '');
        }
        const largeContainer = document.getElementById('largeExtraFields');
        if (largeContainer) {
            const inputs = largeContainer.querySelectorAll('input, textarea');
            inputs.forEach(input => input.value = '');
        }
        updateReport();
        showNotification('تم مسح بيانات مقدم التقرير والنصوص المولدة.');
    }
}

function getActiveReportTemplate() {
    const role = document.getElementById('role').value;
    const place = document.getElementById('place').value;
    let templateId = '';
    if (role === 'teacher') {
        templateId = (place === 'خارج الصف') ? 'report-content-outside' : 'report-content';
    } else if (role === 'school_principal' || role === 'vice_principal') {
        templateId = 'report-content-admin';
    } else if (role === 'student_guide') {
        templateId = 'report-content-student';
    } else if (role === 'health_guide') {
        templateId = 'report-content-health';
    } else if (role === 'activity_leader') {
        templateId = 'report-content-activity';
    } else if (role === 'educational_supervisor') {
        templateId = 'report-content-supervisor';
    } else {
        alert('الدور غير معروف');
        return null;
    }
    const template = document.getElementById(templateId);
    if (!template) { alert('القالب غير موجود: ' + templateId); return null; }
    return template;
}

async function downloadPDF() {
    await loadDates();
    document.querySelector('.top-small-buttons').style.visibility = 'hidden';
    document.querySelector('.main-buttons-bar').style.visibility = 'hidden';
    document.querySelector('.top-marquee').style.visibility = 'hidden';
    document.getElementById('aiFillFloatingBtn').style.visibility = 'hidden';
    document.body.style.margin = "0";
    document.body.style.background = "white";

    const element = getActiveReportTemplate();
    if (!element) return;

    element.style.display = 'block';
    element.style.visibility = 'visible';
    element.style.opacity = '1';
    element.style.position = 'relative';
    element.style.top = '0';
    element.style.left = '0';

    const cleanFileName = document.getElementById('manualReportTitle').value.replace(/[\/\\:*?"<>|]/g, '_') || 'تقرير';

    await new Promise(resolve => setTimeout(resolve, 300));

    html2pdf().set({
        filename: cleanFileName + ".pdf",
        html2canvas: { scale: 3, useCORS: true, scrollY: 0, backgroundColor: '#ffffff', onclone: function(clonedDoc) { const cloned = clonedDoc.getElementById(element.id); if (cloned) cloned.style.background = '#ffffff'; } },
        jsPDF: { unit: "mm", format: "a4", orientation: "portrait" }
    }).from(element).save().then(() => {
        document.querySelector('.top-small-buttons').style.visibility = 'visible';
        document.querySelector('.main-buttons-bar').style.visibility = 'visible';
        document.querySelector('.top-marquee').style.visibility = 'visible';
        document.getElementById('aiFillFloatingBtn').style.visibility = 'visible';
        document.body.style.margin = "";
        document.body.style.background = "#f9fcfb";
        element.style.display = 'none';
        showNotification("تم تنزيل التقرير بصيغة PDF ✓");
    });
}

async function sharePDFWhatsApp() {
    await loadDates();
    document.querySelector('.top-small-buttons').style.visibility = 'hidden';
    document.querySelector('.main-buttons-bar').style.visibility = 'hidden';
    document.querySelector('.top-marquee').style.visibility = 'visible';
    document.getElementById('aiFillFloatingBtn').style.visibility = 'hidden';
    document.body.style.margin = "0";
    document.body.style.background = "white";

    const element = getActiveReportTemplate();
    if (!element) return;

    element.style.display = 'block';
    element.style.visibility = 'visible';
    element.style.opacity = '1';
    element.style.position = 'relative';
    element.style.top = '0';
    element.style.left = '0';

    const reportName = document.getElementById('manualReportTitle').value || 'تقرير';

    await new Promise(resolve => setTimeout(resolve, 300));

    await html2pdf().set({
        margin: 0,
        image: { type: "jpeg", quality: 1 },
        html2canvas: { scale: 3, scrollY: 0, useCORS: true, backgroundColor: '#ffffff', onclone: function(clonedDoc) { const cloned = clonedDoc.getElementById(element.id); if (cloned) cloned.style.background = '#ffffff'; } },
        jsPDF: { unit: "mm", format: "a4", orientation: "portrait" }
    }).from(element).toPdf().output('blob').then((pdfBlob) => {
        document.querySelector('.top-small-buttons').style.visibility = 'visible';
        document.querySelector('.main-buttons-bar').style.visibility = 'visible';
        document.querySelector('.top-marquee').style.visibility = 'visible';
        document.getElementById('aiFillFloatingBtn').style.visibility = 'visible';
        document.body.style.margin = "";
        document.body.style.background = "#f9fcfb";
        element.style.display = 'none';

        let file = new File([pdfBlob], reportName + ".pdf", { type: "application/pdf" });
        if (navigator.canShare && navigator.canShare({ files: [file] })) {
            navigator.share({ files: [file], title: reportName, text: "تقرير: " + reportName });
        } else {
            let url = URL.createObjectURL(pdfBlob);
            window.open(`https://wa.me/?text=${encodeURIComponent("تقرير: " + reportName + "\n\n" + url)}`, "_blank");
        }
    });
}

function openSettings() {
    document.getElementById("settingsModal").style.display = "flex";
    loadSavedReportDate();
    loadSubscriptionStatus();
}

function closeSettings() {
    document.getElementById("settingsModal").style.display = "none";
}

async function loadSubscriptionStatus() {
    const code = localStorage.getItem(ACTIVATION_KEY_NAME);
    if (!code) { document.getElementById("subInfo").innerHTML = "لم يتم تفعيل الأداة بعد<br>يرجى استخدام كود التفعيل"; return; }
    try {
        const res = await fetch(BACKEND_URL + "/subscription/status", { headers: { "X-Activation-Code": code } });
        if (!res.ok) throw new Error();
        const data = await res.json();
        const expires = data.expires_at ? new Date(data.expires_at).toLocaleDateString('ar-SA') : "غير محدد";
        document.getElementById("subInfo").innerHTML = `<div>📅 <strong>تاريخ الانتهاء:</strong> ${expires}</div><div>📊 <strong>الاستخدام:</strong> ${data.usage_used} / ${data.usage_limit}</div><div>🔋 <strong>المتبقي:</strong> ${data.usage_remaining}</div>`;
    } catch {
        document.getElementById("subInfo").innerHTML = "تعذر تحميل معلومات الاشتراك<br>يرجى التأكد من اتصال الإنترنت";
    }
}

function saveReportDate() {
    const date = document.getElementById("customReportDate").value;
    if (date) {
        localStorage.setItem("custom_report_date", date);
        showNotification("تم حفظ تاريخ التقرير ✓");
        closeSettings();
        loadDates();
    } else {
        showNotification("يرجى اختيار تاريخ صحيح");
    }
}

function loadSavedReportDate() {
    const saved = localStorage.getItem("custom_report_date");
    if (saved) document.getElementById("customReportDate").value = saved;
}

document.addEventListener("DOMContentLoaded", async () => {
    const code = localStorage.getItem(ACTIVATION_KEY_NAME);
    if (!code) {
        document.getElementById("activationScreen").style.display = "flex";
        document.body.style.overflow = "hidden";
    } else {
        try {
            const res = await fetch(BACKEND_URL + "/health", { headers: { "X-Activation-Code": code } });
            if (res.ok) { window.__ACTIVATED__ = true; hideActivationScreen(); }
            else throw new Error();
        } catch {
            localStorage.removeItem(ACTIVATION_KEY_NAME);
            document.getElementById("activationScreen").style.display = "flex";
            document.body.style.overflow = "hidden";
        }
    }
    await loadDates();
    loadThemeSettings();
    document.getElementById('role').value = 'teacher';
    const backendRole = getBackendRole('teacher');
    await loadDataFromBackend(backendRole);
    loadTeacherData();
    updateReport();
    document.getElementById('reportSearch').addEventListener('input', handleReportSearch);
    document.addEventListener('click', function(e) { if (!e.target.closest('#reportSearchContainer')) document.getElementById('searchResults').style.display = 'none'; });
    window.addEventListener('resize', () => {});
    document.getElementById('aiGuideBox').style.display = 'none';
});
</script>
</body>
</html>