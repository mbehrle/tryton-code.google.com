# Introduction #

[Pyramid](http://www.pylonsproject.org/projects/pyramid/about) is an very general web development framework for Python. This howto will show how Tryton could be used with it.


## Minimal Application ##

This example is based on TrytonFlask and the Pyramid [HelloWorld](http://pyramid.readthedocs.org/en/latest/narr/firstapp.html) example:

```
from wsgiref.simple_server import make_server
from pyramid.config import Configurator
from pyramid.response import Response
from trytond.transaction import Transaction
from trytond.pool import Pool

def get_tryton_pool(request):
    Transaction().start('test', 0)
    pool = Pool()
    
    def _cleanup(request):
        Transaction().stop()
    request.add_finished_callback(_cleanup)
    return pool

def hello_world(request):
    pool = request.tryton_pool
    user_obj = pool.get('res.user')
    user = user_obj.browse(0)
    return Response("%s, Hello World!" % user.name)

if __name__ == '__main__':
    config = Configurator()
    Pool.start()
    Pool('test').init()
    config.set_request_property(get_tryton_pool, 'tryton_pool', reify=True)
    config.add_route('hello', '/')
    config.add_view(hello_world, route_name='hello')
    app = config.make_wsgi_app()
    server = make_server('0.0.0.0', 8080, app)
    server.serve_forever()
```

Just save it as hello\_pyramid.py (or something similar) and run it with your Python interpreter.

```
$ python hello_pyramid.py
```

Now head over to http://127.0.0.1:8080/, and you should see your hello world greeting.


For more information about Pyramid head on over to http://docs.pylonsproject.org