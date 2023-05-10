# 1、如何在循环内直接终止外部循环

OUT：

循环1

{

​	循环2

​	{

​			break OUT；

​	}

}

实例

```java
package com.gewuyou.array;

import java.util.Random;
import java.util.Scanner;

public class ArrayDemo05 {
    public static void main(String[] args) {
        //猜数字游戏
        //需求
    /*开发一个幸运小游戏，游戏规则如下:
    游戏后台随机生成1-20之间的5个数（无所谓是否重复），然后让大家来猜数字
    1、未猜中提示:"未命中"，并继续猜测
    2、猜中提示:"运气不错，猜中了"，并输出该数据第一次出现的位置，且输出全部5个数据，最终结束本游戏
    分析:
    1、随机生成5个1-20之间的数据储存起来-----使用数组√
    2、定义个死循环，输入数据猜测，遍历数组，判断数据是否在数组中，如果在，进行对应提示并结束死循环；如果没有猜中，提示继续猜测直到猜中为止
     */int []a=new int[5];

        for(int i=0;i<5;i++)
        {
            Random r=new Random();
            a[i]= r.nextInt(20)+1;
        }
        System.out.println("欢迎您游玩猜数字游戏！\n请猜测1-20中的数字！");
        Scanner s=new Scanner(System.in);
        OUT:
        while(true)
        {
            System.out.println("请输入您猜测的数字！");
            int data= s.nextInt();

            for (int i = 0; i < a.length; i++)
            {
                if(a[i]==data)
                {
                    System.out.println("运气不错的说，恭喜您猜对了！您猜中的数据索引是"+i);
                    break OUT;//结束了整个死循环，代表游戏结束了。
                }
            }
            System.out.println("很遗憾，未命中结果，请重新猜测！");
        }
        System.out.println("这5个数分别为");
        for (int i = 0; i < a.length; i++)
        {
            System.out.print("\t"+a[i]);
        }
        System.out.println("游戏结束，感谢您的游玩！");


    }


}

```

