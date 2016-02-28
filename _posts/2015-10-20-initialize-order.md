---
layout: post
title: 初始化顺序
---

1.static其中无论成员还是静态块 按先后顺序初始化

2.成员变量

3.构造函数

类别优先 同一类别 父类优先


{% highlight java%}

    public class Child extends Parent {
        Child(){
            System.out.println("子类构造函数");
        }
        static Print print1 = new Print("静态成员1");

        static {
            System.out.println("静态块初始化");
        }
        static Print print2 = new Print("静态成员2");
        private Print print4 = new Print("普通成员");


        public static void main(String[] args) {
            Child child = new Child();
        }

    }

{% endhighlight %}

{% highlight java%}

    public class Parent {
        static Print print1 = new Print("父类静态成员1");
        static {
            System.out.println("父类静态块初始化");
        }
        static Print print2 = new Print("父类静态成员2");
        private Print print3 = new Print("父类普通成员");
    }

{% endhighlight %}

{% highlight java%}

    public class Print {
        Print(String message){
            System.out.println(message);
        }
    }

{% endhighlight %}

#运行结果

{% highlight java%}

    父类静态成员1
    父类静态块初始化
    父类静态成员2
    静态成员1
    静态块初始化
    静态成员2
    父类普通成员
    普通成员
    子类构造函数

{% endhighlight %}
