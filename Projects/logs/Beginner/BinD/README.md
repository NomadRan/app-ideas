<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>C语言二进制转十进制计算器</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "Microsoft Yahei", sans-serif;
        }
        body {
            width: 100vw;
            height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding-top: 80px;
            background-color: #f5f7fa;
        }
        .container {
            width: 450px;
        }
        /* 第一排：输入区域 */
        .input-box {
            background: #fff;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 2px 12px rgba(0,0,0,0.08);
            margin-bottom: 20px;
        }
        .title {
            font-size: 18px;
            margin-bottom: 15px;
            color: #333;
        }
        .row {
            display: flex;
            gap: 12px;
            margin-bottom: 15px;
        }
        input {
            flex: 1;
            height: 42px;
            padding: 0 px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 16px;
            outline: none;
        }
        input:focus {
            border-color: #409eff;
        }
        .dot-box {
            flex: 0 0 42px;
            height: 42px;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 1px solid #ddd;
            border-radius: 6px;
            background: #fafafa;
            font-size: 20px;
            color: #333;
        }
        button {
            width: 100%;
            height: 44px;
            border: none;
            background: #409eff;
            color: white;
            font-size: 16px;
            border-radius: 6px;
            cursor: pointer;
        }
        button:hover {
            background: #337ecc;
        }
        /* 第二排：输出区域 */
        .output-box {
            background: #fff;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 2px 12px rgba(0,0,0,0.08);
        }
        #result {
            width: 100%;
            min-height: 80px;
            padding: 12px;
            border: 1px solid #eee;
            background: #fafafa;
            border-radius: 6px;
            font-size: 17px;
            color: #222;
            word-break: break-all;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- 第一排：输入框区域 -->
        <div class="input-box">
            <div class="title">输入需要转换的二进制数字</div>
            <div class="row">
                <input type="number" id="inte" placeholder="整数 a">
                <div class="dot-box">.</div>
                <input type="number" id="dec" placeholder="小数 n">
            </div>
            <button onclick="calcPower()">转换为十进制</button>
        </div>

        <!-- 第二排：输出框区域 -->
        <div class="output-box">
            <div class="title">计算结果</div>
            <div id="result"></div>
        </div>
    </div>

    <script>
        // 二进制转十进制
        function calcPower() {
            const inteStr = document.getElementById('inte').value;
            const decStr = document.getElementById('dec').value;
            const resBox = document.getElementById('result');

            if (!/^[01]*$/.test(inteStr) || (decStr !== '' && !/^[01]*$/.test(decStr))) {
                resBox.innerText = "请输入 0 或 1！";
                resBox.style.color = "#f56c6c";
                return;
            }

            const n = inteStr === '' ? 0 : parseInt(inteStr, 10);
            const m = decStr === '' ? 0 : parseInt(decStr, 10);

            let x = 1;
            let y = 0;
            // 计算整数部分的位数
            while (Math.floor(n / x) !== 0) {
                x *= 10;
                y += 1;
            }

            let z = 0;
            let s = 1;
            let num = 0;
            let sum1 = 0;
            while (z < y) {
                num = Math.floor(n / s) % 10;
                s *= 10;
                sum1 += num * Math.pow(2, z);
                z += 1;
            }

            // 计算小数部分的位数
            let a = 1, b = 1;
            while (Math.floor(m / a) !== 0) {
                a *= 10;
                b += 1;
            }

            let l = 1;
            let t = 1;
            let di = 0;
            let sum2 = 0;
            while (l < b) {
                di = Math.floor(m / t) % 10;
                t *= 10;
                sum2 += di * Math.pow(2, -b + (l - 1));
                l += 1;
            }

            resBox.style.color = "#222";
            resBox.innerText = `${sum1+sum2}`;
        }
    </script>
</body>
</html>
