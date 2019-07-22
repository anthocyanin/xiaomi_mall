# xiaomi_mall
这个项目是网易云课堂图灵学院python习题课的结课项目，基本上就是拿过来把它跑通了，因为这个项目不是一个能运行的项目，为了让总共40多个url每个都能同跑通
也是一个一个测试，
- 有的问题是前端页面加载时出现各种问题以及表单input命名混乱导致的问题，
- 有的是后端视图函数写的不对导致渲染不出来页面或者直接崩溃，
- 有的是路由里面根本没有相应的url，导致页面reverse相应url时报错，或者直接返回客户端错误404。
- 有的是model里面的的表定义不全面，导致视图函数直接直接调用时相应的类函数时找不着。
总之最终是把所有页面都给跑通了。
其中也记录一些bug：
- 15. 症状：首页点击家电类目，报错如下：Reverse for 'list' not found. 'list' is not a valid view function or pattern name.
  16. 检查base.html发现家电类目tag的href属性，需要加载 list函数
  17. 于是urls里添加list函数
  18. 再次点击家电类目，仍然报错Reverse for 'detail' not found. 'detail' is not a valid view function or pattern name.
  19. 于是base.html 里面找detail，没找到。
  20. 最终发现在list.html里有tag需要加载detail函数
  21. 于是urls里添加detail函数。最后解决问题
- 22. 
  22. 问题：明明用户存在，密码正确，验证码正确，但就是点击登陆按钮，总是提示用户不存在，
  23. 排查发现视图模块里的dologin函数有问题，它在这样做了request.session['user'] = user.dePosit()。但实际上Users表里面没有 dePosit()
  24. 于是models.py里添加函数，但是又️报错说不可序列化
  25. 于是把两个时间字段拿下，解决问题。
- 26. 
  26. 问题：购物车列表点击增加数量总是报错，keyerror，
  27. 排查好久发现问题是Models里面的Goods表dePosit()函数的返回值里面返回的是typeid，这是类目ID，而购物车里需要的是具体每个商品的id，改过来即
- 28. 问题：订单确认页面， 点击支付，报错：keyerror
  29. 排查好久发现问题是Models里面的Users表dePosit()函数的返回值里面没有返回id，所以request.session里索引id找不到。
- 30. 问题：indent.html页面加载{% load dealwithtime %}报错：Templates syntaxError. 'dealwithtime' is not a registered tag library.
  31. 网上有说重启电脑即可，但试了也没用，setting也按照部分答案设置了，仍然不行。实在解决不了只好，删掉这个自定义的tag,然后绕过问题吧
