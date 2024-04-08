## 环境配置

下载chrome浏览器对应版本的chromedriver，并将其放在python环境的目录中。如将`chromedriver.exe`放到`.\Python39`中

## 环境引入

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
```

## 代码示例

```python
#初始化实例
driver = webdriver.Chrome()

#根据url打开网页
driver.get("https://www.bilibili.com")

#找到输入框元素，并输入英雄联盟
driver.find_element(By.CLASS_NAME, "nav-search-input").send_keys("英雄联盟")

#关闭浏览器
driver.close()
```

## 源码分析

![image-20240408151304603](./selenium_note.assets/image-20240408151304603.png)

编程语言的客户端发送一个http请求发送个Server，也就是`Chromedriver。exe`。然后它会对浏览器做出相应操作。

## 元素定位

![image-20240408151847109](./selenium_note.assets/image-20240408151847109.png)

### ID元素定位

id在html中是唯一的，因此使用id定位可以确保找到页面上唯一的元素，提高了定位的效率

```python
driver = webdriver.Chrome()
driver.maximize_window()#窗口最大化
driver.get("https://www.baidu.com")
element = driver.find_element(By.ID, "kw")
element.send_keys("lol")
driver.find_element(By.ID, "su").click()
```

### CLASS_NAME定位

当有多个相同名字的CLASS时，他会选择第一个。

如果想同时定位多个，则使用`driver.find_elements()`

```python
driver = webdriver.Chrome()
driver.maximize_window()#窗口最大化
driver.get("https://www.bilibili.com")
elements = driver.find_elements(By.CLASS_NAME, "channel-link")#此时的elements为一个数组
```

 当一个元素同时有多个CLASS时，则无法使用

### TAG_NAME定位

```python
driver = webdriver.Chrome()

driver.get("https://www.bilibili.com")
driver.find_element(By.TAG_NAME, "input").send_keys("lol")
```

当有多个元素时，同上

### NAME定位

name属性一般在表单元素中

### LINK_TEXT定位

可点击链接定位

### PARTIAL_LINK_TEXT定位

部分包含即可。比如`新闻`用LINK_TEXT，则只有完全匹配才能够定位。而PARTIAL_LINK_TEXT则进行部分匹配

