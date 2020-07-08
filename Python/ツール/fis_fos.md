書き込み							
```python
text=input('何を記録しますか?')
file=open('diary.txt','a')
file.write(text+'\n')
file.close()
```

```python
text=input('今日は何をした?>>')
with open('diary.txt','a') as file:
    file.write(text+'\n')
```

読み込んで、書き込み
```python
fis=open('diary.txt','r')
fos=open('copy.txt','a')
for line in fis:
    fos.write(line)
fos.close()
fis.close()
```
