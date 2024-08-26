# 数据解析
# re解析 bs4解析 xpath解析

# 正则表达式
# . 匹配除换行符以外的任意字符
# \w 匹配字母或数字或下划线
# \s 匹配任意的空白符
# \d 匹配数字
# \n 匹配一个换行符
# \t 匹配一个制表符
# ^ 开始 $ 结束

```py
# re模块的使用
import re

# # findall 匹配字符串中所有的符合正则的内容
# ls = re.findall(r"\d+", "prind09102")
# print(ls)
#
# # finditer 匹配字符串中所有的内容[返回的是迭代器]
#
# it = re.finditer(r"\d+", "prind09102")
# for i in it:
#     print(i.group())

# search返回的结果是match对象，找到一个结果就返回
# s = re.search(r"\d+", "prind09102")
# print(s.group())

# match从头开始匹配
# s = re.match(r"\d+", "prind09102")

# 预加载正则表达式
# obj = re.compile(r"\d+")
#
# res = obj.finditer("prind09102")
# for r in res:
#     print(r.group())

s = """
<div class='lb'><span id='1'>李白</span></div>
<div class='df'><span id='2'>杜甫</span></div>
<div class='bjy'><span id='3'>白居易</span></div>
"""
# (?P<分组名>正则)
obj = re.compile(r"<div class='(?P<id>.*?)'><span id='\d+'>(?P<name>.*?)</span></div>", re.S)  # re.S 让.能匹配换行符

res = obj.finditer(s)
for i in res:
    print(i.group("id"))


import requests
import re
import csv
url = 'https://movie.douban.com/top250'

headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36"
}
# 请求拿到页面源代码

res = requests.get(url, headers=headers)
strHtml = res.text
# 使用正则获取到想要的数据
obj = re.compile(r'<li>.*?<div class="item">.*?<span class="title">(?P<name>.*?)</span>.*?<p class="">.*?<br>(?P<year>.*?)&nbsp', re.S)
res1 = obj.finditer(strHtml)
f = open("data.csv", mode="w", encoding="utf-8")
csvWriter = csv.writer(f)
for s in res1:
    # print(s.group("name"))
    # print(s.group("year").strip())
    dic = s.groupdict()
    dic['year'] = dic['year'].strip()
    csvWriter.writerow(dic.values())
res.close()
print("over!")
```
