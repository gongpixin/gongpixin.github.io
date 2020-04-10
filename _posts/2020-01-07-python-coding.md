---
layout: post
title: "python编码"
categories:
tags:
---

python默认ascii编码，若代码中有中文则会报错

```python
s = 'hello'  # ascii str
s = '中文'  # Non-ASCII character error
```

可在文件头部指定编码

```python
# -*- coding: utf-8 -*-
s = '中文'
```

unicode

```python
# -*- coding: utf-8 -*-
s = u'中文'
s = unicode('中文', 'utf-8')
```

str与unicode转换

decode: str转unicode

encode: unicode转str

```python
# -*- coding: utf-8 -*-
s = '中文'.decode('utf-8')
s = u'中文'.encode('utf-8')
```
