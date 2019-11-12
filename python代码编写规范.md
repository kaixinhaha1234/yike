# 亦可技术团队Python代码编写规范

##  一、每个文件的文件头、写入作者姓名，文件作用
```python
"""
###################### File Introduction ######################
* Author: 亦可
* Function:这个文件主要用于定义中文拆分的一些函数和文件读写
######################*******************######################
"""
```

## 二、函数规范

* Function: 写出该函数的作用，标准为：接受XXX的调用（可有可无，视功能而定），传入XXX参数，返回XXX

* Args:列出每个参数的名字, 并在名字后使用一个冒号和一个空格, 分隔对该参数的描述.如果描述太长超过了单行80字符,使用2或者4个空格的悬挂缩进(与文件其他部分保持一致). 描述应该包括所需的类型和含义. 如果一个函数接受foo(可变长度参数列表)或者bar (任意关键字参数), 应该详细列出foo和bar.

* Returns: (或者 Yields: 用于生成器)描述返回值的类型和语义. 如果函数返回None, 这一部分可以省略.

* Raises:列出与接口有关的所有异常（这一部分如果有，就写清楚，没有就ignore）.

```python
"""
###################
# * function：这个get_radical函数用于接受中文字符串，返回拆解的偏旁数组
# * args：（Chinses_string）
#   * Chinses_string：中文字符串
# * return radicals
#   * radicals是一个偏旁组成的数组[a,b,c,d,e]
# * raise:未设置异常检测
###################
"""

def get_radical(Chinses_string)
    ......
    return radicals
```


## 三、变量命名
### 1.模块名： 
* 小写字母，单词之间用_分割  ad_stats.py 
* 包名： 和模块名一样 
* 类名： 单词首字母大写 AdStats  ConfigUtil 
* 全局变量名（类变量，在java中相当于static变量）： 大写字母，单词之间用_分割  NUMBER COLOR_WRITE 
* 普通变量： 小写字母，单词之间用_分割  this_is_a_var 
* 实例变量： 以_开头，其他和普通变量一样 _price    _instance_var 
* 私有实例变量（外部访问会报错）：  以__开头（2个下划线），其他和普通变量一样  __private_var 
* 专有变量： __开头，__结尾，一般为python的自有变量，不要以这种方式命名 __doc__  __class__ 

### 2.普通函数： 
* 和普通变量一样： get_name() count_number() ad_stat() 


## 字符串链接
### 避免在循环中用+和+=操作符来累加字符串.
```python
Yes: x = '%s, %s!' % (imperative, expletive)
       x = '{}, {}!'.format(imperative, expletive)
       x = 'name: %s; score: %d' % (name, n)
       x = 'name: {}; score: {}'.format(name, n)
     
 
No: x = imperative + ', ' + expletive + '!'
      x = 'name: ' + name + '; score: ' + str(n)
```

## 四、Model 规范

```python

zhuangtai_CHOICES = (
    (-2,u'已经删除'),
    (0,u'等待生成数据'),
    (1,u'生成成功'),
)

class FangWeiXinXi(models.Model):
    mingcheng = models.CharField(u'活动名称',max_length=150,unique=True)
    zhuangtai = models.IntegerField(u'状态',choices =zhuangtai_CHOICES, default=0)
    shuliang = models.IntegerField(u'生成数量', default=0)
    isdo = models.BooleanField(u'是否正在处理',default=False)
    dodate= models.DateTimeField(u'执行时间',auto_now_add=True,blank=True,null=True)
    adddate = models.DateTimeField(u'录入时间',auto_now_add=True,blank=True)
    enddate= models.DateTimeField(u'结束时间',auto_now_add=True,blank=True,null=True)

    def __unicode__(self):
        return self.mingcheng

    class Meta:
        verbose_name = u'v.信息码活动表'
        verbose_name_plural = u'v.信息码活动表'
        ordering = ['-id']

```


