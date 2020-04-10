---
layout: post
title: "python编码"
categories:
tags:
---

# str

默认ascii编码，若代码中有中文则会报错

```python
s = 'hello'  # ascii str
s = '中文'  # SyntaxError: Non-ASCII character
```

文件头部指定编码

```python
# -*- coding: utf-8 -*-

s = '中文'  # utf-8 str
```

# unicode

```python
# -*- coding: utf-8 -*-

s = u'中文'
s = unicode('中文', 'utf-8')
```

# str与unicode转换

```python
# -*- coding: utf-8 -*-

# str解码unicode: decode解码
s = '中文'.decode('utf-8')

# unicode编码str: encode编码
s = u'中文'.encode('utf-8')
```
