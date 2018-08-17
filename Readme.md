# 2018.08.17 update

支持Python 3.6、django 2.1。

1. 修改 xadmin，这里是[另一个版本](https://github.com/vip68/xadmin_bugfix ) 
2. 修改django-pure-pagination。
3. 修改登录验证。
4. 数据库使用sqlite3

感谢原作者。


说明：

1) xadmin修改：
xadmin已经更新，但是插件没有更新：

文件  `extra_apps/xadmin/plugins/images.py`，第45~52行如下：

```python
    # def render(self, name, value, attrs=None):                # <--- 修改前
    def render(self, name, value, attrs=None, renderer=None):   # <--- 修改后
        output = []
        if value and hasattr(value, "url"):
            label = self.attrs.get('label', name)
            output.append('<a href="%s" target="_blank" title="%s" data-gallery="gallery"><img src="%s" class="field_img"/></a><br/>%s ' %
                         (value.url, label, value.url, _('Change:')))
        # output.append(super(AdminImageWidget, self).render(name, value, attrs))           # <--- 修改前
        output.append(super(AdminImageWidget, self).render(name, value, attrs, renderer))   # <--- 修改后
        return mark_safe(u''.join(output))
```

未修改的文件：extra_apps/xadmin/plugins/multiselect.py：
第83~87行
```python
    def render(self, name, value, attrs=None, choices=()):
        if attrs is None:
            attrs = {}
        attrs['class'] = 'selectmultiple selectdropdown'
        return super(SelectMultipleDropdown, self).render(name, value, attrs, choices)
```
不清楚是否能正常工作。


2) django-pure-pagination修改：

文件：paginator.py，第205~210行如下：

```python
        if self.paginator.request:            
            #self.base_queryset['page'] = page_number       # <------ 修改前
            self.base_queryset['page'] = str(page_number)   # <------ 修改后
            return self.base_queryset.urlencode()
        ...
```        

3) 登录验证修改：
`apps/users/views.py`

```python
# 实现用户名邮箱均可登录
# 继承ModelBackend类，因为它有方法authenticate，可点进源码查看
class CustomBackend(ModelBackend):
    # def authenticate(self, username=None, password=None, **kwargs):           # <------ 修改前
    def authenticate(self, request, username=None, password=None, **kwargs):    # <------ 修改后
        try:
        ...
```


# Mxonline3

[![Build Status](https://travis-ci.org/mtianyan/hexoBlog-Github.svg?branch=master)](https://travis-ci.org/mtianyan/hexoBlog-Github)
[![MIT Licence](https://badges.frapsoft.com/os/mit/mit.svg?v=103)](https://opensource.org/licenses/mit-license.php)

使用Python3.x与Django2.0.1开发的在线教育平台网站: http://mxonline.mtianyan.cn

## Quick Start

```
$ git clone https://github.com/mtianyan/Mxonline3.git
$ cd Mxonline3
$ pip install -r requirements.txt
$ python manage.py runserver
```

use the address: http://127.0.0.1:8000/

## Contents：

对应教程已开通简书连载文集: https://www.jianshu.com/nb/21010157

**欢迎大家关注订阅，点赞！！！**

## Background:

- 最近重装了系统，所以从环境配置开始,我都做到尽可能从零开始，对初学者友好。
- 自己已经学习Python一年了，最近对于Python相关开始进行一个较全面复习。
- 希望可以帮到那些对于Python，对Django有兴趣的同学少走弯路。

[项目线上演示地址](http://mxonline.mtianyan.cn)
[原版视频课程地址:](https://coding.imooc.com/learn/list/78.html)

>一次性的一个完整项目代码很难被学习，所以我采用commit记录源码快照 + 阶段性教程结合的形式。类似关卡式学习概念。

- 每节教程前面会写明对应的上节commit：开始某一节教程的前置条件。
- 每节教程后面会写明对应的已结束commit: 方便本节出错参考。

希望可以对Django初学者，Python爱好者有所帮助。

## About me
[简书](https://www.jianshu.com/u/db9a7a0daa1f) && [mtianyan's blog](http://blog.mtianyan.cn/)

有趣的Python群：619417153

欢迎关注简书，star项目！谢谢！

你的关注支持是我继续分享前进的动力。

## 求打赏鼓励

很高兴我写的文章（或我的项目代码）对你有帮助，请我吃包辣条吧！

微信打赏:

![mark](http://myphoto.mtianyan.cn/blog/180302/i52eHgilfD.png?imageslim)

支付宝打赏:

![mark](http://myphoto.mtianyan.cn/blog/180302/gDlBGemI60.jpg?imageslim)
