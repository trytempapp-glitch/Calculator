# Calculator 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        .calculator {
            background: #fff;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            width: 320px;
            padding: 20px;
        }

        .display {
            background: #333;
            color: #fff;
            font-size: 2.5rem;
            padding: 20px;
            border-radius: 10px;
            text-align: right;
            margin-bottom: 20px;
            min-height: 80px;
            word-wrap: break-word;
            word-break: break-all;
            overflow: hidden;
        }

        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }

        button {
            padding: 20px;
            font-size: 1.5rem;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.2s;
            font-weight: 600;
        }

        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        button:active {
            transform: translateY(0);
        }

        .number-btn {
            background: #f0f0f0;
            color: #333;
        }

        .number-btn:hover {
            background: #e0e0e0;
        }

        .operator-btn {
            background: #667eea;
            color: #fff;
        }

        .operator-btn:hover {
            background: #5568d3;
        }

        .equals-btn {
            background: #48bb78;
            color: #fff;
            grid-column: span 2;
        }

        .equals-btn:hover {
            background: #38a169;
        }

        .clear-btn {
            background: #f56565;
            color: #fff;
            grid-column: span 2;
        }

        .clear-btn:hover {
            background: #e53e3e;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <div class="display" id="display">0</div>
        <div class="buttons">
            <button class="clear-btn" onclick="clearDisplay()">C</button>
            <button class="operator-btn" onclick="appendOperator('/')">÷</button>
            <button class="operator-btn" onclick="appendOperator('*')">×</button>

            <button class="number-btn" onclick="appendNumber('7')">7</button>
            <button class="number-btn" onclick="appendNumber('8')">8</button>
            <button class="number-btn" onclick="appendNumber('9')">9</button>
            <button class="operator-btn" onclick="appendOperator('-')">−</button>

            <button class="number-btn" onclick="appendNumber('4')">4</button>
            <button class="number-btn" onclick="appendNumber('5')">5</button>
            <button class="number-btn" onclick="appendNumber('6')">6</button>
            <button class="operator-btn" onclick="appendOperator('+')">+</button>

            <button class="number-btn" onclick="appendNumber('1')">1</button>
            <button class="number-btn" onclick="appendNumber('2')">2</button>
            <button class="number-btn" onclick="appendNumber('3')">3</button>
            <button class="number-btn" onclick="appendNumber('.')">.</button>

            <button class="number-btn" onclick="appendNumber('0')" style="grid-column: span 2;">0</button>
            <button class="equals-btn" onclick="calculate()">=</button>
        </div>
    </div>

    <script>
        let display = document.getElementById('display');
        let currentInput = '0';
        let previousInput = '';
        let operator = null;
        let shouldResetDisplay = false;

        function updateDisplay() {
            display.textContent = currentInput;
        }

        function appendNumber(num) {
            if (shouldResetDisplay) {
                currentInput = num;
                shouldResetDisplay = false;
            } else {
                if (currentInput === '0' && num !== '.') {
                    currentInput = num;
                } else if (num === '.' && currentInput.includes('.')) {
                    return;
                } else {
                    currentInput += num;
                }
            }
            updateDisplay();
        }

        function appendOperator(op) {
            if (operator !== null && !shouldResetDisplay) {
                calculate();
            }
            previousInput = currentInput;
            operator = op;
            shouldResetDisplay = true;
        }

        function calculate() {
            if (operator === null || shouldResetDisplay) {
                return;
            }

            let result;
            const prev = parseFloat(previousInput);
            const current = parseFloat(currentInput);

            switch (operator) {
                case '+':
                    result = prev + current;
                    break;
                case '-':
                    result = prev - current;
                    break;
                case '*':
                    result = prev * current;
                    break;
                case '/':
                    result = current !== 0 ? prev / current : 0;
                    break;
                default:
                    return;
            }

            currentInput = result.toString();
            operator = null;
            shouldResetDisplay = true;
            updateDisplay();
        }

        function clearDisplay() {
            currentInput = '0';
            previousInput = '';
            operator = null;
            shouldResetDisplay = false;
            updateDisplay();
        }
    </script>
</body>
</html>
