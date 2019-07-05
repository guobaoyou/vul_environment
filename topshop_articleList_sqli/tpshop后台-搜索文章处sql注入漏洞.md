## 前言

最近看了下tpshop，审计出几个鸡肋的漏洞，这个SQL注入漏洞是其中之一。然后审计完网上搜了一下发现有一堆后台的sql注入漏洞，应该是觉得后台的SQL不用修叭（我个人是可以理解的）。


## 漏洞触发点

首先要登录后台，这也是我说漏洞很鸡肋的原因。 
漏洞位于在后台的商城-》文章->文章列表处的搜索 

 ![image](https://github.com/guobaoyou/vul_environment/tree/master/topshop_articleList_sqli/images/1.jpg) 
 
抓包，存在漏洞的参数是keywords，当输入payload 
' or length(database())=10)#时，页面返回文章数0， 

 ![image](https://github.com/guobaoyou/vul_environment/tree/master/topshop_articleList_sqli/images/2.jpg)

而当输入payload' or length(database())=9)#时，页面返回为共33篇文章（总共33篇，数据库名是tpshop2.0） 

 ![image](https://github.com/guobaoyou/vul_environment/tree/master/topshop_articleList_sqli/images/3.jpg)

因此可以通过布尔注入来获取数据库信息，当然延时也可以，只不过我自己是能不用延时就不用延时的人。

## 漏洞成因，分析下代码
分析下代码，原因很简单，where直接拼接了。并且会将查询到的结果返回到页面中。 
`application/admin/controller/Article.php:56`
```php
        $keywords = trim(I('keywords'));
        $keywords && $where.=" and title like '%$keywords%' ";
        $cat_id = I('cat_id',0);
        $cat_id && $where.=" and cat_id = $cat_id ";
        $res = $Article->where($where)->order('article_id desc')->page("$p,$size")->select();
        $count = $Article->where($where)->count();// 查询满足要求的总记录数
        $pager = new Page($count,$size);// 实例化分页类 传入总记录数和每页显示的记录数
        //$page = $pager->show();//分页显示输出
​
        $ArticleCat = new ArticleCatLogic();
        $cats = $ArticleCat->article_cat_list(0,0,false);
        if($res){
         foreach ($res as $val){
          $val['category'] = $cats[$val['cat_id']]['cat_name'];
          $val['add_time'] = date('Y-m-d H:i:s',$val['add_time']);          
          $list[] = $val;
         }
        }
        $this->assign('cats',$cats);
        $this->assign('cat_id',$cat_id);
        $this->assign('list',$list);// 赋值数据集
        $this->assign('pager',$pager);// 赋值分页输出        
        return $this->fetch('articleList');
```
最后执行的sql语句为： 

 ![image](https://github.com/guobaoyou/vul_environment/tree/master/topshop_articleList_sqli/images/4.jpg)

## 其他
我在用payload的时候用的是=,是因为输入做了过滤，会转义> <，用大于号不能直接执行sql，会报错。
