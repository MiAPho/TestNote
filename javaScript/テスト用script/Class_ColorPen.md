```html
<!DOCTYPE html>
<html lang="ja">

<head>
    <meta charset="UTF-8">

    <title>Document</title>
</head>

<body>
    <button class="select">赤を持つ</button>
    <button class="select">緑を持つ</button>
    <button class="select">青を持つ</button>
    <button onclick="writePen()">書く</button>
    <p id="info"></p>
    <p id="gage"></p>
    <script>
        class ColorPen {
            constructor(color, length) {
                this.color = color;
                this.length = length;
                switch (color) {
                    case '赤':
                        this.eColor = 'red';
                        break;
                    case '緑':
                        this.eColor = 'green';
                        break;
                    case '青':
                        this.eColor = 'blue';
                }
            }
            write() {
                let msg = '';
                if (this.length <= 0) {
                    msg = 'もうかけません!';
                } else {
                    this.length -= 0.5;
                    msg = `${this.color}で書いた。残りの長さ${this.length}`;
                }
                return msg;
            }
        }
        const bts = document.querySelectorAll('.select');
        let pens = [new ColorPen('赤', 10), new ColorPen('緑', 10), new ColorPen('青', 10)];
        let pen = null;
        const info = document.getElementById('info');
        const gage = document.getElementById('gage');
        for (let i = 0; i < bts.length; i++) {
            bts[i].addEventListener('click', () => {
                pen = pens[i];
                info.textContent = pen.color + 'を持った。';
                styleVar();
            });
        }
        const writePen = () => {
            let msg = '';
            if (pen == null) {
                msg = 'ペンを持ってください!';
            } else {
                msg = pen.write();
            }
            info.textContent = msg;
            styleVar();
        };
        const styleVar=()=>{
            gage.style.width = `${pen.length}cm`;
            gage.style.height = "1cm";
            gage.style.backgroundColor = `${pen.eColor}`;
            gage.style.color = "yellow";
            gage.style.fontSize = "30px";
            gage.textContent = `${pen.length}cm`;
        };
    </script>
</body>

</html>
