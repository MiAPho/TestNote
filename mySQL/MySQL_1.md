* データベース作成
```
CREATE DATABASE myapp
DEFAULT CHARACTER SET utf8;
```
* データベース消去
```
ROP DATABASE  IF EXISTS myapp;
```
* テーブル作成
```
CREATE TABLE members(
id INT PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(30),
depart VARCHAR(20) DEFAULT '無所属',
age INT,
updated DATE
);
```
* テーブル消去
```
DROP TABLE IF EXISTS members;
```
* カラムには型を指定する
```
INT
FLOAT
DOUBLE
CHAR /*固定長文字列*/
VARCHAR(len) /*len桁の可変長文字列*/
TEXT /*長い文字列*/
DATETIME /*日付時刻 2017-08-31 23:10:20*/
DATE /*日付 2017-08-31*/
TIME /*23:10:20*/
BLOB /*バイナリデータ*/
```
* 4つの基本機能CRUD(CREATE,READ,UPDATE,DELETE)
```
CREATE:INSERT
READ:SELECT
UPDATE=UPDATE
DELETE=DELETE
```
* INSERT(INSERT INTO テーブル名(カラムの並び) VALUES(値の並び))
```
INSERT INTO members(id,name,depart,age,updated)
VALUES(1,'山田太郎','営業部',40,'2014-12-01');
 
INSERT INTO members(name,age)
VALUES ('鈴木さくら',25);
 
/*全カラムに対して挿入はカラムの並び省略化)*/
INSERT INTO members
VALUES(3,'佐藤次郎','人事部',35,'2015-01-15');
 
/*連続入力化*/
INSERT INTO members(name,depart,age)
VALUES('田中一郎','経理部',48),
('山口弘子','営業部',28),
('渡辺順二','人事部',58),
('中島博之','総務部',49),
('山下圭吾','経理部',23);

```
* SELECT(SELECT 欲しいもの FROM テーブル)
```
/*全件抽出*/
SELECT * FROM members;
 
/*nameカラム取得*/
SELECT name FROM members;
 
/*name,ageカラム取得*/
SELECT name,age FROM members;
 
/*WHERE句で絞り込み*/
SELECT * FROM members WHERE age=25;
SELECT * FROM members WHERE age>25;
SELECT * FROM members WHERE age>=25;
//<>でない
SELECT * FROM members WHERE age<>25;
SELECT * FROM members WHERE age>25 AND age <40
SELECT * FROM members WHERE age>25 OR updated <='2015-01-15'
//BETWEEN(端の値含む)
SELECT * FROM members WHERE updated BETWEEN '2015-01-15' AND '2015-02-15'
//INの中にあるデータを抽出
SELECT * FROM members WHERE depart IN('営業部','人事部');
//null判定
SELECT * FROM members WHERE updated IS NULL;
SELECT * FROM members WHERE updated IS NOT NULL;
//あいまい検索
SELECT * FROM members WHERE name LIKE '鈴木%';
SELECT * FROM members WHERE name LIKE '%木%';
SELECT * FROM members WHERE name LIKE '%田';
//北が含まれない
SELECT * FROM members WHERE name NOT LIKE '%北%';
 
/*ORDER BY （並び替え)*/
//年齢降順
SELECT * FROM members ORDER BY age DESC;
//updatedがnullでないデータを年齢昇順
SELECT * FROM members WHERE updated IS NOT NULL
ORDER BY age ASC;
//ORDER BYは複数指定できる
SELECT * FROM members ORDER BY age DESC,name ASC;
//LIMIT 件数を制限できる
SELECT * FROM members ORDER BY age DESC LIMIT 3;
 
/*LIMIT と合わせてOFFSET指定＊/
//２番目に年齢を高い人から3人取得
SELECT * FROM members ORDER BY age DESC LIMIT 3 OFFSET 1;
```
* UPDATE(UPDATE テーブル　SET カラム=値　)
```
/*鈴木さくらの部署を人事部に変更*/
UPDATE members SET depart='人事部'
WHERE name='鈴木さくら';
/*鈴木さくらの部署を人事部に変更,年齢を1歳あげる*/
UPDATE members SET depart='人事部',age=age+1
WHERE name='鈴木さくら';
```
* DELETE(DELETE FROM テーブル　)  
idが３のデータを消去
```
DELETE FROM members WHERE id=3;
```
[集計関数]
```
*集計関数。結果は基本1行*/
/*count(*) 登録データ件数*/
SELECT count(*) FROM members;
 
/*avg(age) 年齢の平均*/
SELECT avg(age) FROM members;
 
/*max(age)　年齢の最大*/
SELECT max(age) FROM members;
 
/*min(age)*　年齢の最小/
SELECT min(age) FROM members;
 
/*sum(age)*　年齢の合計/
SELECT sum(age) FROM members;
```
[GROUP BY(同一項目をまとめる、主に集計関数と共に使う。結果はGROUP BYした項目数行)]  
/*departでGROUP BY 結果はdepartの種類の数出力される。*/  
/*GROUP BYした項目は取得カラムに設定可能*/
```
SELECT depart,avg(age) FROM members 
GROUP BY depart;
```
[HAVING(GROUP BY した結果に対する絞込み)]  
/*departでGROUP BYしてその平均年齢を集計し平均年齢30以上を取得*/
```
SELECT depart,avg(age) FROM members 
GROUP BY depart
HAVING avg(age) >= 30;
```
