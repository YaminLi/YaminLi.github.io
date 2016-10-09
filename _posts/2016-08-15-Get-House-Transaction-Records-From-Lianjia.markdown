---
layout:     post
title:      "Want to Analysis the Housing Price Trends in China? Get the Data First"  
subtitle:   "Get House Transaction Records From Lianjia"
date:       2016-08-15 12:00:00
author:     "Michael"
header-img: "img/in-post/2016-08-15/post-bg2.jpg"
tags:
  - Web Crawler
  - Python
---

## #Tools Used  
<p></p>

#### Python ####

Web service applications mostly are client-server programing. We are using the python library 'urllib' to send the request to the server and get the response.

A __URL__ or _Universal Resource Locator_ can be automatically translated to the __IP__ address by __DNS__ servers. So we can reach our destination simply using the __URL__ without knowing the specific ip address. Python's urllib library can use the url to locate the server and send a request to it. Simply like this.

````
// python 3.5.2
import urllib.request

url = 'https://google.com'
req = urllib.request.Request(url)
content = urllib.request.urlopen(req).read()
// print(content)
````

----
#### Regular Expression ####

To grab the useful information, we need some tool to just extract what we want from the complicated contents received from the server. We can use the __BeautifulSoup__ library or __Regular Expression__.

> regular expressions are text matching patterns described with a formal syntax. The patterns are interpreted as a set of instructions, which are then executed with a string as input to produce a matching subset or modified version of the original.

Regular Expression Tutorial can be found in [Regular Expression HOWTO](https://docs.python.org/3/howto/regex.html).


## #To Start
<p></p>

#### Log in Lianjia ####

````
import re
import requests
import urllib.request

def login(username, password):
    s = requests.session()

    home_url = 'http://bj.lianjia.com/'
    auth_url = 'https://passport.lianjia.com/cas/login?service=http%3A%2F%2Fbj.lianjia.com%2F'

    headers = {
        'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8',
        'Accept-Encoding': 'gzip, deflate, sdch',
        'Accept-Language': 'zh-CN,zh;q=0.8',
        'Cache-Control': 'no-cache',
        'Connection': 'keep-alive',
        'Content-Type': 'application/x-www-form-urlencoded',
        'Host': 'passport.lianjia.com',
        'Pragma': 'no-cache',
        'Upgrade-Insecure-Requests': '1',
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/47.0.2526.111 Safari/537.36'
    }

    s.get(home_url)
    res = s.get(auth_url, headers=headers)
    # print(res.content)
    # print(res.headers)

    # r=re.compile(r'Set-Cookie: JSESSIONID=(.+?);')
    set_cookie = res.headers['Set-Cookie']
    idx = set_cookie.find(';')
    jsesseionid = set_cookie[11:idx]
    # print(jsesseionid)

    pattern = re.compile(r'value=\"(LT-.+?)\"')
    lt = pattern.findall(res.content.decode('utf-8'))[0]
    # print(lt)

    pattern = re.compile(r'name="execution" value="(.+?)"')
    execution = pattern.findall(res.content.decode('utf-8'))[0]
    # print(execution)

    data = {
        'username': 'username',
        'password': 'password',
        'execution': execution,
        '_eventId': 'submit',
        'lt': lt,
        'verifyCode': '',
        'redirect': '',
    }

    res=s.post(auth_url, data)
    print(res)

    return s
````
----

#### Get the Transaction List ####

----

#### Data Frame ####
![img](/img/in-post/2016-08-15/trans-list.png)
<!-- <h2 class="section-heading">The Final Frontier</h2> -->

<!-- <span class="caption text-muted">To go places and do things that have never been done before – that’s what living is all about.</span> -->
