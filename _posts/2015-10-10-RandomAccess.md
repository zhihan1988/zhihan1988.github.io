---
layout: post
title: RandomAccess
---

用以标示是否支持快速随机访问 通常通过以下方式对大的集合数组进行区分遍历

{% highlight java%}

         if (list instance of RandomAccess) {
            for(int m = 0; m < list.size(); m++){}
         }else{
            Iterator iter = list.iterator();
            while(iter.hasNext()){}
         }

{% endhighlight %}


# 参考链接(包括：接口介绍 性能测试)：

http://blog.csdn.net/keda8997110/article/details/8635005
