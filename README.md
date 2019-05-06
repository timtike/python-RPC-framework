实现思路



    tcp server tcp client
    tcp server bind accept recv parse call
    tcp client connect send data

1.客户端调用rpc方法

    client
    c.foo(1, 2, 3)





2.解析、发送数据格式

函数名， 参数（args，kwargs）

    通过 __getattr__ pack， 解析出 function name function args function kwargs
    
    send json
    {
        'function_name':'foo',
        'function_args':(1,2,3),
        'function_kwargs':{}
    }
    
    



3.server socket接收json，调用getattr执行对应方法， 返回数据

    server
    
    1. recv json
    {
      'function_name':'foo',
      'function_args':(1,2,3),
      'function_kwargs':{}
    }
    
    getattr(self, 'foo')
    getattr(self, 'foo')(*args, **kwargs)
    



