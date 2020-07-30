Lambda

与[匿名类](https://how2j.cn/k/interface-inheritance/interface-inheritance-inner-class/322.html#step687) 概念相比较，
Lambda 其实就是**匿名方法**，这是一种**把方法作为参数**进行传递的编程思想。

虽然代码是这么写

```java
filter(heros, h -> h.hp > 100 && h.damage < 50);
```

但是，Java会在背后，悄悄的，把这些都还原成[匿名类方式](https://how2j.cn/k/lambda/lambda-lamdba-tutorials/697.html#step2552)。
引入Lambda表达式，会使得代码更加紧凑，而不是各种接口和匿名类到处飞。



### demo

主类

```java
public class TestLambda {
    public static void main(String[] args) {
        List<Hero> heroList = new ArrayList<>();
        Hero hero1 = new Hero("hero1", 12, 600, 100);
        Hero hero2 = new Hero("hero2", 12, 700, 200);
        Hero hero3 = new Hero("hero3", 12, 800, 300);
        Hero hero4 = new Hero("hero4", 12, 900, 400);
        Hero hero5 = new Hero("hero5", 12, 1000, 500);
        //
        heroList.add(hero1);
        heroList.add(hero2);
        heroList.add(hero3);
        heroList.add(hero4);
        heroList.add(hero5);
        //
        Checker checker = new Checker() {
            @Override
            public boolean check(Hero hero) {
                return hero.getHp() > 800 && hero.getDamage() > 300;
            }
        };

        //匿名内部类方式
        filter(heroList, checker);
        
        //lambda 方式
        filter(heroList, hero -> hero.getHp() > 800 && hero.getDamage() > 300);
    }

    public static void filter(List<Hero> heroList, Checker checker) {
        for (Hero hero : heroList) {
            if (checker.check(hero)) {
                System.out.println(hero);
            }
        }
    }
}

class Hero {
    private String name;
    private int age;
    private int hp;
    private int damage;

    public Hero() {
    }

    public Hero(String name, int age, int hp, int damage) {
        this.name = name;
        this.age = age;
        this.hp = hp;
        this.damage = damage;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public int getHp() {
        return hp;
    }

    public void setHp(int hp) {
        this.hp = hp;
    }

    public int getDamage() {
        return damage;
    }

    public void setDamage(int damage) {
        this.damage = damage;
    }

    @Override
    public String toString() {
        return "Hero{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", hp=" + hp +
                ", damage=" + damage +
                '}';
    }
}
```



接口

```java
public interface Checker {
    public boolean check(Hero hero);
}
```





###### 完 