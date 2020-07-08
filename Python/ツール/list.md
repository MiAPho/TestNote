```Python
members=['工藤','松田','浅木']
print(members[1])
print(members)
print(len(members))
print(members[2])

members.append('菅原')
members=members+['湊','朝香']
print(members)

members.remove('松田')
del members[0]
print(members)
del members[-1]
```
```Python
a=[1,2,3]
b=[4,5,6]
c=[a,b]
print(c)
print(c[0])
print(c[1][2])
```
```Python
リスト内の要素のシャッフル
random.shuffle(リスト名)
```
