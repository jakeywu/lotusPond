---
title: python
tags:
---

```
    e = {
        "ＢaseException": {
            "Exception": {
                "StandardError": {
                    "ArithmeticError": {
                        "FloatingPointError": None,
                        "OverflowError": None,
                        "ZeroDivisionError": None
                    },
                    "AssertionError": None, 
                    "AttributeError": None,
                    "BufferError": None,
                    "MemoryError": None,
                    "ValueError": {
                        "UnicodeError": {
                            "UnicodeDecodeError": None,
                            "UnicodeEncodeError": None,
                            "UnicodeTranslateError": None
                        },
                    },
                    "NameError": {
                        "UnboundLocalError": None
                    },
                    "ReferenceError": None,
                    "SystemError": None,
                    "TypeError": None,
                    "RuntimeError": {
                        "NotImplementedError": None,
                    },
                    "EnvironmentError": {
                        "IOError": None,
                        "OSError": None
                    },
                    "EOFError": None,
                    "ImportError": None,
                    "LookupError": {
                        "IndexError": None,
                        "KeyError": None
                    },
                    "SyntaxError": {
                        "IndentationError": None,
                        "TabError": None
                    },
                },
                "Warning": {
                    "BytesWarning": None,
                    "DeprecationWarning": None, 
                    "FutureWarning": None, 
                    "ImportWarning": None,
                    "PendingDeprecationWarning": None,
                    "RuntimeWarning": None,
                    "SyntaxWarning": None,
                    "UnicodeWarning": None,
                    "UserWarning": None
                },
                "StopIteration": None,
            },
            "GeneratorExit": None,
            "KeyboardInterrupt": None,
            "SystemExit": None
        }
    }

```

```
Mounting
	constructor()
	componentWillMount()
	render()
	componentDidMount()

Updating
	componentWillReceiveProps()
	shouldComponentUpdate()
	componentWillUpdate()
	render()
	componentDidUpdate()

Unmounting
	componentWillUnmount()
```


方式一(01)：在URL上面区分 /api/v2
https://haveibeenpwned.com/api/v2/breachedaccount/foo

方式一(02) URL里面添加
https://haveibeenpwned.com/api/breachedaccount/foo?v=2

  
方式二：利用用户自定义的request header
HTTP GET:  
https://haveibeenpwned.com/api/breachedaccount/foo  
api-version: 2


方式三(01)：利用content type
HTTP GET:  
https://haveibeenpwned.com/api/breachedaccount/foo  
Accept: application/vnd.haveibeenpwned.v2+json


方式三(02)：利用content type
HTTP GET:  
https://haveibeenpwned.com/api/breachedaccount/foo  
Accept: application/vnd.haveibeenpwned+json; version=2.0  

