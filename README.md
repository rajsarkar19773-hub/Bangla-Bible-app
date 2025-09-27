<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Calculator with Ads</title>
  <style>
    body {
      margin: 0;
      background-color: #121212;
      font-family: Arial, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .ad-slot {
      width: 100%;
      max-width: 360px;
      margin: 10px 0;
      background-color: white;
      text-align: center;
    }

    .calculator {
      background-color: #1e1e1e;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 0 15px #000000;
      width: 320px;
    }

    .display {
      background-color: #000;
      color: #0f0;
      font-size: 32px;
      padding: 15px;
      border-radius: 8px;
      text-align: right;
      margin-bottom: 15px;
      height: 60px;
      overflow-x: auto;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }

    button {
      padding: 20px;
      font-size: 20px;
      border: none;
      border-radius: 10px;
      background-color: #333;
      color: #fff;
      cursor: pointer;
    }

    button:hover {
      background-color: #444;
    }

    .operator {
      background-color: #ffa500;
    }

    .clear {
      background-color: #e53935;
    }

    .equals {
      background-color: #00c853;
      grid-column: span 2;
    }
  </style>
</head>
<body>

  <!-- 🔝 Top Ad -->
  <div class="ad-slot">
    <script async="async" data-cfasync="false" src="//pl27108541.profitableratecpm.com/14f2186aede9c982aa64593ce37d869b/invoke.js"></script>
    <div id="container-14f2186aede9c982aa64593ce37d869b"></div>
  </div>

  <!-- 🔢 Calculator -->
  <div class="calculator">
    <div class="display" id="display">0</div>
    <div class="buttons">
      <button class="clear" onclick="clearDisplay()">AC</button>
      <button onclick="append('%')">%</button>
      <button onclick="backspace()">⌫</button>
      <button class="operator" onclick="append('/')">÷</button>

      <button onclick="append('7')">7</button>
      <button onclick="append('8')">8</button>
      <button onclick="append('9')">9</button>
      <button class="operator" onclick="append('*')">×</button>

      <button onclick="append('4')">4</button>
      <button onclick="append('5')">5</button>
      <button onclick="append('6')">6</button>
      <button class="operator" onclick="append('-')">−</button>

      <button onclick="append('1')">1</button>
      <button onclick="append('2')">2</button>
      <button onclick="append('3')">3</button>
      <button class="operator" onclick="append('+')">+</button>

      <button onclick="append('00')">00</button>
      <button onclick="append('0')">0</button>
      <button onclick="append('.')">.</button>
      <button class="equals" onclick="calculate()">=</button>
    </div>
  </div>

  <!-- 🔻 Bottom Ad -->
  <div class="ad-slot">
    <script async="async" data-cfasync="false" src="//pl27108541.profitableratecpm.com/14f2186aede9c982aa64593ce37d869b/invoke.js"></script>
    <div id="container-14f2186aede9c982aa64593ce37d869b"></div>
  </div>

  <script>
    let display = document.getElementById('display');

    function append(char) {
      if (display.innerText === '0' && char !== '.') {
        display.innerText = char;
      } else {
        display.innerText += char;
      }
    }

    function clearDisplay() {
      display.innerText = '0';
    }

    function backspace() {
      display.innerText = display.innerText.slice(0, -1);
      if (display.innerText === '') {
        display.innerText = '0';
      }
    }

    function calculate() {
      try {
        let expression = display.innerText.replace(/÷/g, '/').replace(/×/g, '*');
        let result = eval(expression);
        display.innerText = result;
      } catch {
        display.innerText = 'Error';
      }
    }
  </script>
</body>
</html>
