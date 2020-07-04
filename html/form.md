<https://joytas.net/programming/website/website06>  
input type="text"
入力欄の囲い

name="username"
ラベル、関連付け

value=""
入力欄の初期値

placeholder="お名前を入力"
ユーザーが名前を入力しやすくなる

***
input type="submit" 
ボタン作成

value=" "
ボタン内部の表示
***
type radio 一つしか押せない
type checkbox 沢山押せる
```
<textarea name="comment" rows="5" cols"40">コメントを入れてください。</textarea>
5行40列のtext入力欄を表示
```

ボタン系のvalueはチェックが入った場合valueの内容を返す
***
数字系入力欄
```
a:<input type="number" min="0" max="100" name="a">
```
リンクを踏んださいの警告表示
```html
<a href="/todoapp/Delete?id=<%=t.getId()%>"onclick="returnconfirm('[<%=t.getTitle()%>]を削除してよろしいですか？');">削除</a>
```
