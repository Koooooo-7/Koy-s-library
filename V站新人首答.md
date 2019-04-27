# 记 ● V站新人首答

表示递归和迭代真的是自己的一块软肋。

### 唯手熟尔。

------

问题链接在[这里](https://www.v2ex.com/t/558972#reply21)。

问题如下:

```
V友的描述：
$a = ['Date','Media','Geo']; 
$b = ['Num'];

$subject = ['Date'=>'2019-04-26','Media'=>'AAA','Geo'=>'CN','Num'=>105]; 求一个函数,处理完, 返回结果为 $res['2019-04-26']['AAA']['CN']['Num'] = 105;

$a 和$b 属于可以随意配置的数组,这两个数组的值,一定在 subject 中存在 key。

我的理解：
$a，$b都是不定长的，最后是要以$a中元素在$subject中的值为键以及$b为键生成最后的一个嵌套数组，数组最内部前台的数组的键值是$b元素最后一个元素在$subject中对应的值。

看到这样的嵌套数组，不知道为什么，我就想用递归来试一下。
```

我的解决办法。

```php
<?php

    $a = [ 'Date','Media','Geo' ];
    $b = [ 'Num'];
    $subject = [ 'Date'=>'2019-04-26','Media'=>'AAA','Geo'=>'CN','Num'=>105];
    $res = myArrayA($subject,$a,$b);
    var_dump($res);
    

    /**
     * 以$a中的元素在$subject中作为键,从$subject中取出对应的值生成新的嵌套数组结构
     * @param $subject
     * @param $a
     * @param $b
     * @return array
     */
    function myArrayA($subject,$a,$b){
        $arr = [];
        if (empty($a)){
            $tmp = myArrayB($subject,$b,$b);
            return $tmp;
        }
        $point = array_shift($a);
        $key = $subject[$point];
        $subject = array_diff($subject,[$point=>1]);
        $arr[$key] =  myArrayA($subject,$a,$b);
        return $arr;

    }

    /**
     * 以$b中的元素作为键生成新的嵌套数组结构
     * @param mixed $subject 为了取出最后一个$b对应的键值
     * @param mixed $b
     * @param mixed $c  原始的数组$b，为了获取出最后一个$b对应的元素去$subject中取值
     * @return array
     */
    function myArrayB($subject,$b,$c){
        $arr = [];
        if (empty($b)){
            return $subject[array_pop($c )];
        }
        $key = array_shift($b);
        $arr[$key] = myArrayB($subject,$b,$c);
        return $arr;
    }
    ?>

```

输出结果:

```
其实楼上的代码是我直接拿了以前的一个项目Demo启动wamp了在首页写的23333，
之后从控制器取出来到那个可以在线测试代码的页面调整的格式Orz。

D:\wamp64\www\我的项目地址不能看\controller\IndexController.php:33:
array (size=1)
  '2019-04-26' => 
    array (size=1)
      'AAA' => 
        array (size=1)
          'CN' => 
            array (size=1)
              ...
```

额外收获：

1.在楼上get到了一个[在线演示代码](https://www.dooccn.com//php7/#id/46ae6d604aee73cdd0e1c3ffce4497cf)的网站，赚了阿。

2.一个大佬用索引写的代码，感觉很厉害,可是没有了，他是用github的一个Gist服务，和gitlab的Snippets挺像的。


总结：
感觉对于递归体的思路还算比较快，但是对递归头的处理不太好，还是要多写，才会有感觉！


