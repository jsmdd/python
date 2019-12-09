## Python3之requests模块

### requests 是使用 Apache2 Licensed 许可证的 基于Python开发的HTTP 库，其在Python内置模块的基础上进行了高度的封装

- requests.get(url, params=None, **kwargs)

- requests.post(url, data=None, json=None, **kwargs)

- requests.put(url, data=None, **kwargs)

- requests.head(url, **kwargs)

- requests.delete(url, **kwargs)

- requests.patch(url, data=None, **kwargs)

- requests.options(url, **kwargs)


### post请求
```python
import requests
import sys

url="http://my.edu.wanfangdata.com.cn/Account/SendMessageCode"
data = {"MobilePhone": "%s"%(sys.argv[1]),"Type":"register"}
headers={"user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.90 Safari/537.36"}
request = requests.post(url,data=data,headers=headers)
print(request.status_code)   ## 此处将Response对象返回状态码
print(request.text)
```
requests模块的返回对象是一个Response对象，可以从这个对象中获取需要的信息。下面 r 代表Response对象。
1. r.text         文本响应内容
2. r.context      二进制响应内容
3. r.json()       JSON响应内容
4. r.raw          原始相应内容
5. r.status_code  响应状态码
6. r.headers      响应头部
7. r.cookies      Cookie
8. r.url          url

.................

> 参考文章：https://www.cnblogs.com/wang-yc/p/5623711.html
