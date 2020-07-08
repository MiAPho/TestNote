```Python
name=input('あなたの名前を教えて下さい>')
print('{}さん、こんにちは'.format(name))
food=input('{}さんの好きな食べ物を教えて下さい>'.format(name))
if food=='カレー':
    print('素敵です。カレーは最高ですよね!!')
else:
    print('私も{}が好きですよ'.format(food))
```
```Python
scores=[80,100,20,60]
if 100 in scores:
    print('100点満点の試験があったんですねお目でしょう！')
else:
    print('次はどれか1つでも100点満点をとろう!')
```
