<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Проверка знаний</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    font-family: -apple-system, 'Segoe UI', Roboto, sans-serif;
    background: #0a0a0f;
    color: #e8e8f0;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
    overflow: hidden;
  }
  .glow {
    position: fixed;
    width: 400px; height: 400px;
    background: radial-gradient(circle, #6d28d9 0%, transparent 70%);
    filter: blur(80px);
    opacity: 0.4;
    top: -100px; left: -100px;
    z-index: 0;
  }
  .glow2 {
    position: fixed;
    width: 400px; height: 400px;
    background: radial-gradient(circle, #2563eb 0%, transparent 70%);
    filter: blur(80px);
    opacity: 0.3;
    bottom: -100px; right: -100px;
    z-index: 0;
  }
  .card {
    position: relative;
    z-index: 1;
    background: rgba(20, 20, 30, 0.85);
    backdrop-filter: blur(20px);
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 20px;
    padding: 35px 28px;
    width: 100%;
    max-width: 380px;
    box-shadow: 0 20px 60px rgba(0,0,0,0.5);
    animation: fadeIn 0.5s ease;
  }
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }
  .logo {
    width: 60px; height: 60px;
    background: linear-gradient(135deg, #6d28d9, #2563eb);
    border-radius: 16px;
    margin: 0 auto 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 28px;
  }
  h1 {
    font-size: 22px;
    text-align: center;
    margin-bottom: 8px;
    font-weight: 600;
  }
  .subtitle {
    text-align: center;
    color: #8a8a9a;
    font-size: 14px;
    margin-bottom: 28px;
    line-height: 1.5;
  }
  label {
    display: block;
    font-size: 13px;
    color: #a0a0b0;
    margin-bottom: 8px;
    margin-top: 16px;
  }
  input {
    width: 100%;
    padding: 14px 16px;
    background: rgba(255,255,255,0.04);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 12px;
    color: #e8e8f0;
    font-size: 15px;
    outline: none;
    transition: 0.2s;
  }
  input:focus {
    border-color: #6d28d9;
    background: rgba(109,40,217,0.08);
  }
  input::placeholder { color: #5a5a6a; }
  button {
    width: 100%;
    padding: 15px;
    background: linear-gradient(135deg, #6d28d9, #2563eb);
    color: white;
    border: none;
    border-radius: 12px;
    font-size: 16px;
    font-weight: 600;
    margin-top: 24px;
    cursor: pointer;
    transition: 0.2s;
  }
  button:active { transform: scale(0.98); }
  .busted {
    display: none;
    text-align: center;
    animation: shake 0.6s;
  }
  @keyframes shake {
    0%,100% { transform: translateX(0); }
    20% { transform: translateX(-10px); }
    40% { transform: translateX(10px); }
    60% { transform: translateX(-8px); }
    80% { transform: translateX(8px); }
  }
  .busted .emoji {
    font-size: 70px;
    margin-bottom: 16px;
    display: block;
  }
  .busted h2 {
    font-size: 26px;
    color: #ff3b5c;
    margin-bottom: 14px;
  }
  .busted p {
    color: #b0b0c0;
    font-size: 15px;
    line-height: 1.6;
    margin-bottom: 12px;
  }
  .tip {
    background: rgba(255,59,92,0.1);
    border: 1px solid rgba(255,59,92,0.3);
    border-radius: 12px;
    padding: 14px;
    margin-top: 20px;
    font-size: 14px;
    color: #ff8a9c;
    text-align: left;
    line-height: 1.5;
  }
  .again {
    background: rgba(255,255,255,0.06);
    border: 1px solid rgba(255,255,255,0.1);
    color: #e8e8f0;
    margin-top: 20px;
  }
</style>
</head>
<body>

<div class="glow"></div>
<div class="glow2"></div>

<div class="card">
  <div id="form-screen">
    <div class="logo">🎓</div>
    <h1>Проверка знаний</h1>
    <p class="subtitle">Введи свои данные, чтобы начать тестирование</p>

    <label>ФИО</label>
    <input type="text" id="fio" placeholder="Иванов Иван Иванович">

    <label>Класс</label>
    <input type="text" id="class" placeholder="10 А">

    <button onclick="bust()">Продолжить →</button>
  </div>

  <div class="busted" id="busted-screen">
    <span class="emoji">🚨</span>
    <h2>ПОПАЛСЯ!</h2>
    <p>Ты только что ввёл свои данные на <b>незнакомом сайте</b>.</p>
    <p>Именно так работают мошенники — они делают красивые страницы, чтобы украсть твои данные.</p>

    <div class="tip">
      <b>💡 Запомни:</b><br>
      • Всегда проверяй адрес сайта<br>
      • Никогда не вводи ФИО, пароли и телефоны на подозрительных страницах<br>
      • Если торопят и пугают — это фишинг
    </div>

    <button class="again" onclick="location.reload()">Попробовать снова</button>
  </div>
</div>

<script>
function bust() {
  const fio = document.getElementById('fio').value.trim();
  const cls = document.getElementById('class').value.trim();

  if (!fio) {
    alert('Введи ФИО');
    return;
  }

  document.getElementById('form-screen').style.display = 'none';
  document.getElementById('busted-screen').style.display = 'block';
}
</script>

</body>
</html>
