# 1、对数字取位数

实例

```java
package com.gewuyou.loop;

public class ForDemo03 {
    public static void main(String[] args) {
        //目标:在控制台输出所有的水仙花数
        //水仙花数要求:1.水仙花数是一个三位数 2:水仙花数的个位、十位、百位的数字的立方和等于原数
        int num=0;
        for(int i=100;i<1000;i++)
        {
            int ge=i%10;
            int shi=(i/10)%10;
            int bai=i/100;

            if(ge*ge*ge+shi*shi*shi+bai*bai*bai==i)
            {
                System.out.println(i);
            }
        }
    }
}

```

利用int对于小数的舍去与取余来提取数字上各位置的数

# 2、快速将一段代码放入某个循环

使用快捷键

Ctrl+Alt+T键

步骤

1、选定要放入的代码

![](笔记图片资源包\屏幕截图 2022-01-15 141359.png)

2,、按顺序按下Ctrl-Alt-T

![](笔记图片资源包\屏幕截图 2022-01-15 141542.png)

3.选择自己想要的循环



# 3、如何快捷的将方法创建

使用快捷键

Alt+回车

步骤

1、将鼠标指针放在要创建的方法名处

2、然后按下Alt+回车，出现如下界面

3选择第一个选项即可

# 4、信号位的使用

格式：boolean 名称=逻辑值；

- 在死循环头上声明信号位，当满足该布尔值为目标逻辑值时，break;跳出循环。

实例

```java
package com.gewuyou.demo;

import java.util.Scanner;

public class ShopCarTest {
    public static void main(String[] args) {
        //1、定义商品类用于后期创建商品对象
        //2、定义购物车对象；使用一个数组对象表示
        Goods[] shopCar=new Goods[100];//[null][null][null]...
        //3、搭建操作架构
        System.out.println("欢迎来到购物车系统！");
        boolean flag=true;//信号位！！！！
        while (true)
        {
            System.out.println("请选择如下命令!");
            System.out.println("添加商品到购物车(add)\n查看添加的商品(query)");
            System.out.println("修改要购买的数量(updata)\n结算价格(pay)\n退出购物车(over)");
            Scanner s=new Scanner(System.in);
            System.out.println("请您输入命令！");
            String command=s.next();
            switch (command)
            {
                case "add":
                    //添加商品到购物车
                    addGoods(shopCar,s);
                    break;
                case "query":
                    //查看添加的商品
                    queryGoods(shopCar);
                    break;
                case "updata":
                    //修改要购买的数量
                    updataGoods(shopCar,s);
                    break;
                case "pay":
                    //结算价格
                    flag=pay(shopCar,flag);
                    break;
                case "over":
                    flag=false;//结束循环
                default:
                    System.out.println("错误，无法接收该指令！请检查您命令的正确性！");
            }
            if(flag==false)
            {
                break;
            }
        }
    }

    public static boolean pay(Goods[] shopCar,boolean flag)
    {
        double money=0;
        //遍历购物车数组中的全部商品对象，累加其单价*数量
        System.out.println("-------------------------------------------");
        queryGoods(shopCar);
        for (int i = 0; i < shopCar.length; i++)
        {
            Goods g =shopCar[i];
            if (g != null)
            {
                money+=(g.buyNumber*g.price);
            }
            else
            {
                break;
            }

        }
        System.out.println("订单总金额为"+money);
        flag=false;
        return flag;
    }
//需求：让用户输入商品id，找出对应的商品修改其购买数量
/*分析：
定义方法能够根据用户输入的id去购物车数组中查看是否存在该商品对象。
如果存在则返回该商品对象地址，反之则返回null
判断返回地址是否存在，存在则修改其购买数量，不存在就继续

 */
    public static void updataGoods(Goods[] shopCar,Scanner s)
    {
        while (true) {
            System.out.println("请输入您要修改的商品的id！");
            int id=s.nextInt();
            Goods g=getGoodsByid(shopCar,id);
            if(g==null)
            {
                System.out.println("抱歉！未能找到该商品，请您检查您是否添加了该商品");
            }
            else
            {
                System.out.println("请您输入"+g.name+"商品的最新购买数量：");
                g.buyNumber=s.nextInt();
                System.out.println("修改完成！您现在的购物车商品信息为：");
                queryGoods(shopCar);
                break;

            }
        }


    }
    public static Goods getGoodsByid(Goods[] shopCar,int id)
    {
        for (int i = 0; i < shopCar.length; i++)
        {
            Goods g=shopCar[i];
            if(g!=null)
            {
                //判断这个商品对象的id是否是我们要找的
                if(g.id==id)
                {
                    return g;//找到了需要的商品
                }
            }
            else{
                return null;//找完了前面的对象，依旧没有找到存在的商品id
            }
        }
        return null;//代表找完100个商品都没有找到id一样的商品
    }
//查询购物车中的商品对象信息并展示
    public static void queryGoods(Goods[] shopCar)
    {
        System.out.println("==============查询购物车信息=============");
        System.out.println("编号\t\t名称\t\t\t价格\t\t\t购买数量");
        //shopCar=[g1,g2,g3,null,null,.....]
        for (int i = 0; i < shopCar.length; i++)
        {
            Goods g=shopCar[i];
            if(g!=null)
            {
                //展示这个商品对象
                System.out.println(" "+g.id+"\t\t"+g.name+"\t\t"+ g.price+"\t\t\t\t"+g.buyNumber);
            }
            else
            {
                //商品对象已查询完毕结束循环
                break;
            }
        }
    }
    //需求:让用户输入商品信息，并加入到购物车中去，且可立即查看购物车信息
    //分析:需要让用户录入商品信息，创建商品对象封装信息，并把商品对象加入到购物车数组中去，
    //查询购物车信息，就是遍历购物车数组中的每个商品对象。
    //完成商品添加到购物车的功能

    public static void addGoods(Goods[] shopCar,Scanner s)
    {
        System.out.println("请您输入商品的编号(不重复)：");
        int id=s.nextInt();
        System.out.println("请您输入您的商品名称：");
        String name=s.next();
        System.out.println("请您输入您要购买的数量：");
        int buyNumber=s.nextInt();
        System.out.println("请您输入商品的价格：");
        double price=s.nextDouble();
        System.out.println("添加成功！");

        //把这些购买商品的信息封装成一个商品对象
        Goods g=new Goods();
        g.id=id;
        g.name=name;
        g.price=price;
        g.buyNumber=buyNumber;
        //3、把这个商品对象添加到购物车数组当中去
        //shopCar=[null,null...]
        for (int i = 0; i < shopCar.length; i++)
        {
            if(shopCar[i]==null)//说明此位置没有元素，把我们新买的商品添加到此处即可
            {
                shopCar[i]=g;
                break;//结束循环，因为商品已经存入了空位置中，已经不需要再寻找空位置了
            }
        }
        System.out.println("您的商品"+g.name+"添加到购物车完成");
    }


}

```

# 5、快速创建setter与getter

1、在创建成员变量后

![](笔记图片资源包\屏幕截图 2022-01-17 113737.png)

2、对空白处右键呼出选项

![](笔记图片资源包\屏幕截图 2022-01-17 113925.png)

3、选择Generater(或者按下组合键Alt+Insert)

![](笔记图片资源包\屏幕截图 2022-01-17 114139.png)

4、选择Getter and Setter

![](笔记图片资源包\屏幕截图 2022-01-17 114307.png)

5、按住Shift全选，然后点OK即可



# 6、快速创造有参无参构造器

1、前面步骤参考5

2、在![](笔记图片资源包\屏幕截图 2022-01-17 114139.png)

里面选择Constructor

3、直接点OK是创建有参构造器，Select None则是创建无参构造器

![](笔记图片资源包\屏幕截图 2022-01-17 115124.png)

# 7、在IDEA中快速更改某个变量在全部位置的名字

快捷键 Shift+F6选择第二个选项

# 8、在IDEA中快速补全某个声明

Ctrl+Alt+V

# 9、IDEA如何进行整列编辑

按住Alt用左键点击所要编辑的列然后从上部拖动即可从初始位置开始选中所编辑字段了、

# 10、IDEA怎么看某个接口或者类的总关系

快捷键Ctrl+h

# 11、IDEA怎么直接查看某个类或接口下的所有属性

Ctrl+F12

# 12、IDEA怎么给注释打书签

在注释中打TODO即可

```java
//DOTO 内容
<!--DOTO 内容-->
```

# 13、IDEA查看类图快捷键

Ctrl+Alt+U

# 14、IDEA查看方法的上级继承快捷键

Ctrl+Alt+B

# 15、IDEA抽取代码的快捷键

Ctrl+Alt+M

# 16、IDEA对单词全大写的快捷键

Ctrl+Shift+U

# 17、IDEA如何打开Service控制台

Alt+8
