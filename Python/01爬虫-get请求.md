# 需求： 用浏览器模拟浏览器。输入一个网址，从该网址中获取到资源或者内容

``` py
# 导入库
from urllib.request import urlopen

url = "http://www.baidu.com"
resp = urlopen(url)

with open("mybaidu.html", mode="w", encoding="utf-8") as f:
    f.write(resp.read().decode("utf-8"))  # 读取页面的源代码
print("over!")

resp.close()
```
