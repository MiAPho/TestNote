```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        let pen={color:"red",length:10};
        console.log(pen.color);//red
        pen.weight=5.0;
        console.log(pen.weight);//5.0
        class Zombie{
            constructor(name,hp){
                this.name=name;
                this.hp=hp;
            }
            attack(){
                console.log(`${this.name}は攻撃した`);
            }
        }
        let z1=new Zombie('John',100);
        z1.attack();
        z1.mp=20;
        console.log(z1.mp);
        class User{
            constructor(name,address){
                this.name=name;
                this.address=address;
            }
            greet(){
                console.log(`こんにちは!${this.name}です`);
            }
            introduce(){
                this.greet();
                console.log(`${this.address}に住んでいます`);
            }
        }
        let user=new User("山田","東京");
        console.log(user);
        user.greet();
        user.introduce();
        class BusinessUser extends User{
            constructor(name,address,job){
                super(name,address);
                this.job=job;
            }
            usersJob(){
                console.log(`職業は${this.job}です`);
            }
            introduce(){
                this.greet();
                console.log(`${this.address}に住んでいます`);
                this.usersJob();
            }
        }
        const businessuser1=new BusinessUser("田中一郎","大阪府","銀行員");
        businessuser1.introduce();
    </script>
</body>
</html>
```
