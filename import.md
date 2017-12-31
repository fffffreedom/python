import datetime是引入整个datetime包，如果使用datetime包中的datetime类,需要加上模块名的限定。
```
import datetime
print datetime.datetime.now()
```
如果不加模块名限定会出现错误：TypeError: 'module' object is not callable \ AttributeError: 'module' object has no attribute 'now'
```
from datetime import datetime 是只引入datetime包里的datetime类,在使用时无需添加模块名的限定
from datetime import datetime
print datetime.now()
```
总结：Python导入模块的方法有两种：import module 和 from module import，区别是前者所有导入的东西使用时需加上模块名的限定，而后者不需要。

https://www.cnblogs.com/xxoome/p/5880693.html
