* lesson_appデータベースを文字コードUTF-8で作成する。
```
CREATE DATABASE lesson_app
DEFAULT CHARACTER SET utf8;
```
* lesson_appにbooksテーブルを作成する。カラム構成は以下
```
id 整数　主キー　自動連番
category 可変長文字列(30) デフォルト値 未分類
title 可変長文字列(255) NOTNULL制約
price 整数
updated 日付
```
```
CREATE TABLE books(
id INT PRIMARY KEY AUTO_INCREMENT,
category VARCHAR(30) DEFAULT '未分類',
title VARCHAR(255) NOT NULL,
price INT,
updated DATE
);
```
* booksテーブルに以下のデータを挿入する
```
INSERT INTO books VALUES
(1,'雑誌','ジャンプ',300,'2018-08-31'),
(2,'雑誌','サンデー',290,'2018-08-31'),
(3,'漫画','タッチ',620,'2000-01-11'),
(4,'漫画','ドラゴンボール',580,'1982-12-11'),
(5,'漫画','北斗の拳',430,'1983-02-27'),
(6,'小説','ノルウェイの森',1700,'1987-05-26'),
(7,'小説','海辺のカフカ',1820,'2004-08-15'),
(8,'小説','騎士団長殺し',1830,'2017-03-10'),
(9,null,'君が僕を知ってる',960,null),
(10,null,'この世に猫がいなかったら',1200,'2016-11-01'),
(11,null,'花図鑑',2600,'2018-09-01'),
(12,null,'スキー入門',1340,'2018-09-01'),
(13,null,'必勝麻雀',1420,'2018-09-01');
```
1.全てのデータを抽出せよ。
```
SELECT * FROM books;
```
2.以下の本を追加せよ。’漫画’、’アラレちゃん’、400,’1978-12-11′
```
INSERT INTO books(category,title,price,updated)
VALUES('漫画','アラレちゃん',400,'1978-12-11');
```
3.idが10のデータのカテゴリーを小説にせよ。
```
UPDATE books SET category='小説'
WHERE id=10;
```
4.タイトルに図鑑が入っている本を削除せよ。
```
DELETE FROM books
WHERE title LIKE '%図鑑%';
```
5.カテゴリーが小説のデータを抽出せよ。取得カラムはtitle,priceとすること
```
SELECT title,price FROM books
WHERE category='小説';
```
6.カテゴリーがnullの項目を’未分類’に変更せよ。
```
UPDATE books SET category='未分類'
WHERE category IS NULL;
```
7.次のデータを挿入せよ。’Java入門’,1800
```
INSERT INTO books(title,price)
VALUES ('Java入門',1800);
```
8.値段の高い順に抽出せよ。
```
SELECT * FROM books
ORDER BY price DESC;
```
9.登録件数を抽出せよ。
```
SELECT count(*) FROM books;
```
10.1000円以上の本を抽出せよ。
```
SELECT * FROM books
WHERE price>=1000;
```
11.カテゴリーが漫画のデータを一律50円値下げせよ。
```
UPDATE books SET price = price-50
WHERE category='漫画';
```
12.一番値段の高い本を抽出せよ。取得列はtitle,priceとすること。
```
SELECT title,price FROM books
ORDER BY price DESC LIMIT 1;
```
13.すべての本の価格の平均を求めよ。
```
SELECT avg(price) FROM books;
```
14.更新日が1980~1990年のデータを日付昇順で抽出せよ。
```
SELECT * FROM books
WHERE updated BETWEEN '1980-01-01' AND '1990-12-31'
ORDER BY updated ASC;
```
15.値段の安い本３冊を抽出せよ。
```
SELECT * FROM books
ORDER BY price ASC
LIMIT 3;
```
16.値段が２番目に高い本を抽出せよ。取得カラムはtitle,priceとする。
```
SELECT title,price FROM books
ORDER BY price DESC
LIMIT 1 OFFSET 1;
```
17.更新日がnullでなく、カテゴリーが小説でないデータを抽出せよ。
```
SELECT * FROM books
WHERE updated IS NOT NULL
AND category <> '小説';
```
18.カテゴリーが未分類の本を抽出せよ。
```
SELECT * FROM books
WHERE category='未分類';
```
19.カテゴリー毎の平均価格を求め、降順に抽出せよ。取得カラムはcategory,avg(price)とすること。
```
SELECT category,avg(price) FROM books
GROUP BY category
ORDER BY avg(price) DESC;
```
20.カテゴリー毎の合計価格を求め,合計価格が5000円以上の項目を抽出せよ。取得カラムはcategory,sum(price)とする。
```
SELECT category,sum(price) FROM books
GROUP BY category
HAVING sum(price) >=5000;
```
