

# Remote Calls #

**Note**:

  * To allow XML-RPC, you must activate it. This is done in the config file.

## Version 3.4 ##

### XML-RPC(s) in PHP ###

The snippet for 3.2 series works well for 3.4 series too.


## Version 3.2 ##

### JSON-RPC in Python ###

#### Example 1 ####

```
from jsonrpclib import Server as ServerProxy

URI = 'http://localhost:8000/DATABASE'
USER = 'admin'
PASSWORD = 'admin'

server = ServerProxy(URI, verbose=0)
user, session = server.common.server.login(USER, PASSWORD)
pref = server.model.res.user.get_preferences(
        user, session, True, {})
# search all modules; return a list(dict)
modules = server.model.ir.module.module.search_read(
            user, session, [], pref)
```

#### Example 2 ####

```
from jsonrpclib import Server as ServerProxy
import jsonrpclib
import json

HOST = 'http://yourhost'
PORT = '8000'
DB = 'database'
USER = 'admin'
PASSWORD = 'sigrid'


class Tryton(object):

    def __init__(self, url):
        self.server = ServerProxy(url, verbose=0)
        self.user, self.cookie = self.server.common.server.login(
            USER,
            PASSWORD)
        self.pref = self.server.model.res.user.get_preferences(
            self.user,
            self.cookie, True, {})

    def execute(self, method, *args):
        args += (self.pref,)
        try:
            return getattr(self.server, method)(self.user, self.cookie, *args)
        except TypeError:
            a = json.loads(jsonrpclib.history.response)
            raise TypeError('%s: %s' % (a['error'][0], a['error'][1]))

if __name__ == "__main__":
    a = Tryton("%s:%s/%s" % (HOST, PORT, DB))
    # Nice
    print a.execute('model.party.party.read', [20])
    # Error
    print a.execute('model.party.party.readx', [20])
```

An example to create new records related with many2one and many2many fields:

```
party = 1 # ID party
bank = 1 # ID bank
bank_accounts = a.execute('model.bank.account.create', [{
    'bank': bank,
    'numbers': [('create', [{'type': 'other', 'number': '123456'}]),],
    'owners': [('add', [party]),],
    }])
```

### JSON-RPC in PHP ###

This example use the customized version of jsonRPCClient.php class that you can find [here](jsonRPCClient_php.md).

It (seems that) doesn't suport SSL.

```
<?php
require_once 'jsonRPCClient.php'; 

$user = 'username';
$password = 'password';

$debug = true;
$rpcClient = new jsonRPCClient('http://localhost:8000/database', $debug); 

$session = $rpcClient->cl('common.db.login', array($user, $password));
$context = $rpcClient->cl('model.res.user.get_preferences',array($session[0], $session[1], true, array(1=>1))); 

$products = $rpcClient->cl('model.product.product.search_read', array($session[0], $session[1], array('template.type', '=', 'service'), 0, 10, false, array('id', 'template.name'), $context)); 

echo "Print search read result:\n";
foreach ($products as $product) {
    echo " - Product: " . $product['template.name'] . " (" . $product['id'] . ")\n";
}
?>
```


### XML-RPC(s) in PHP ###

Based on Pierre-Louis Bonicoli example: https://groups.google.com/d/msg/tryton-dev/0FhTZRC0LN0/kw3rLC3yLikJ

```
<?php 
<?php 

/* 
 * XML-RPC calls to trytond using https://github.com/gggeek/phpxmlrpc/ 
 */ 

set_include_path(get_include_path() . PATH_SEPARATOR . 
    './phpxmlrpc/lib'); 
require_once 'xmlrpc.inc' ; 
require_once 'xmlrpcs.inc' ; 
require_once 'xmlrpc_wrappers.inc' ;

function getVersion($url, $user, $pass, $ssl_verify) { 
    $server = new xmlrpc_client($url);
    if (! $ssl_verify) {
        $server->setSSLVerifyPeer(false);
        $server->setSSLVerifyHost(false);
    }
    $message = new xmlrpcmsg( 
        'common.server.version', 
        array(new xmlrpcval(0, 'int'), new xmlrpcval(0, 'int')) 
    ); 
    $message = new xmlrpcmsg('common.server.version'); 
    // With XML-RPC, authentication is mandatory, see 
    // https://bugs.tryton.org/issue4148 
    $server->setCredentials($user, $pass); 

    $server->return_type = 'phpvals'; 
    $result = $server->send($message); 
    print "\nTrytond version: " . $result->value() . "\n"; 
} 


function readModel($url, $user, $pass, $ssl_verify) { 
    $server = new xmlrpc_client($url);
    if (! $ssl_verify) {
        $server->setSSLVerifyPeer(false);
        $server->setSSLVerifyHost(false);
    }
    $server->setCredentials($user, $pass); 
    $message = new xmlrpcmsg( 
        // method 
        'model.ir.model.read', 
        // parameters 
        array( 
            new xmlrpcval( 
                // ids 
                array( 
                    new xmlrpcval(1, 'int'), 
                    new xmlrpcval(2, 'int')), 
                'array' 
            ), 
            new xmlrpcval( 
                // fields 
                array( 
                    new xmlrpcval('info', 'string'), 
                    new xmlrpcval('model', 'string'), 
                    new xmlrpcval('name', 'string'), 
                    new xmlrpcval('module', 'string')), 
                'array' 
            ), 
            // context 
            new xmlrpcval([], 'struct') 
        ) 
    ); 
    $server->return_type = 'xml'; 
    $result = $server->send($message); 
    print "\nRead call returns: \n" . $result->value() . "\n"; 
} 

function readProduct($url, $user, $pass, $ssl_verify) { 
    $server = new xmlrpc_client($url);
    if (! $ssl_verify) {
        $server->setSSLVerifyPeer(false);
        $server->setSSLVerifyHost(false);
    }
    $server->setCredentials($user, $pass); 
    $message = new xmlrpcmsg( 
        // method 
        'model.product.product.read', 
        // parameters 
        array( 
            new xmlrpcval( 
                // ids 
                array(
                        new xmlrpcval(71, 'int'), 
                        new xmlrpcval(72, 'int')), 
                'array' 
            ), 
            new xmlrpcval( 
                // fields 
                array( 
                    new xmlrpcval('id', 'string'), 
                    new xmlrpcval('template.name', 'string')), 
                'array' 
            ), 
            // context 
            new xmlrpcval(array(
                "language" => new xmlrpcval("en_US"),
                ), 'struct') 
        ) 
    );
    $server->return_type = 'phpvals'; 
    $result = $server->send($message); 
    echo "Read Products getting vals as phpvals:\n";
    foreach ($result->value() as $product) {
        echo " - Product: " . $product['template.name'] . " (" . $product['id'] . ")\n";
    }
} 

function searchReadProduct($url, $user, $pass, $ssl_verify) { 
    $server = new xmlrpc_client($url);
    if (! $ssl_verify) {
        $server->setSSLVerifyPeer(false);
        $server->setSSLVerifyHost(false);
    }
    $server->setCredentials($user, $pass);
    $message = new xmlrpcmsg( 
        // method 
        'model.product.product.search_read',
        // parameters
        array(
            // Domain
            new xmlrpcval(array(
                    new xmlrpcval('template.type', 'string'), 
                    new xmlrpcval('=', 'string'), 
                    new xmlrpcval('service', 'string')), 
                'array'),
            // offset
            new xmlrpcval(0, 'int'),  
            // limit
            new xmlrpcval(10, 'int'), 
            // order
            new xmlrpcval(array(), 'array'), 
            // fields 
            new xmlrpcval(array( 
                    new xmlrpcval('id', 'string'), 
                    new xmlrpcval('template.name', 'string')), 
                'array'), 
            // context 
            new xmlrpcval(array(
                "language" => new xmlrpcval("en_US"),
                ), 'struct') 
        ) 
    );
    $server->return_type = 'phpvals'; 
    $result = $server->send($message);
    echo "Search Read Service Products getting vals as phpvals:\n";
    foreach ($result->value() as $product) {
        echo " - Product: " . $product['template.name'] . " (" . $product['id'] . ")\n";
    }
}

// To access to a Tryton server with ssl_xmlrpc param to True, use this URL
// $url = 'https://localhost:8069/';
$url = 'http://localhost:8069/';

// If you don't use a self signed certificate you may can allow ssl_verify
// Try to do this call and see what it returns:
// $ wget https://localhost:8069/
$ssl_verify = false;

$db = 'database'; 
$user = 'user'; 
$pass = 'password'; 

getVersion($url . $db, $user, $pass, $ssl_verify); 
readModel($url . $db, $user, $pass, $ssl_verify);
readProduct($url . $db, $user, $pass, $ssl_verify);
searchReadProduct($url . $db, $user, $pass, $ssl_verify);
?> 
```


## Version 1.6 ##

### XML-RPC in Python ###

```
import xmlrpclib

PASSWORD = 'admin'
USER = "admin"

# Get user_id and session
s = xmlrpclib.ServerProxy ('http://%s:%s@localhost:8069/try' % (USER, PASSWORD))

# Get the user context
context = s.model.res.user.get_preferences(True, {})

# Print all methods (introspection)
print s.system.listMethods()

# Search parties and print rec_name
party_ids = s.model.party.party.search(
        [], # search clause
        0,  # offset
        10, # limit
        False, # order
        context)  # context

print s.model.party.party.read(
        party_ids, # party ids
        ['rec_name'], # list of fields
        context) # context

# Execute report
type, data, _ = s.report.party.label.execute(
        party_ids, # party ids
        {}, # data
        context) # context
```

## Version 1.2, 1.4 ##

### XML-RPC in Python ###

```
import xmlrpclib

PASSWORD = 'admin'
USER = "admin"

# Get user_id and session
s = xmlrpclib.ServerProxy ('http://localhost:8069/try')
user_id, session = s.common.db.login(USER, PASSWORD)

# Get the user context
context = s.model.res.user.get_preferences(user_id, session, True, {})

# Print all methods (introspection)
print s.system.listMethods()

# Search parties and print rec_name
party_ids = s.model.party.party.search(user_id, session,
                                   [], # search clause
                                   0,  # offset
                                   10, # limit
                                   False, # order
                                   context)  # context

print s.model.party.party.read(user_id, session,
                             party_ids, # party ids
                             ['rec_name'], # list of fields
                             context) # context

# Execute report
type, data, _ = s.report.party.label.execute(user_id, session,
                             party_ids, # party ids
                             {}, # data
                             context) # context
```

### NET-RPC in Python ###

```
from trytond import pysocket

PASSWORD = 'admin'
DB = "try"
USER = "admin"

sock = pysocket.PySocket()
sock.connect('127.0.0.1', '8070')

# Get user_id and session
sock.send((DB, USER, PASSWORD, 'common', 'db', 'login'))
user_id, session = sock.receive()

# Get the user context
sock.send((DB, user_id, session, 'model', 'res.user', 'get_preferences',
               True, {}))
context = sock.receive()

# Search parties and print rec_name
sock.send((DB, user_id, session, 'model', 'party.party', 'search',
               [],  # search clause
               0,   # offset
               10,  # limit
               False, # order
               {}))  # context

party_ids = sock.receive()

sock.send((DB, user_id, session, 'model', 'party.party', 'read',
               party_ids, # party ids
               ['rec_name'], # list of fields
               context)) #context
print sock.receive()

# Execute report
sock.send((DB, user_id, session, 'report', 'party.label', 'execute',
               party_ids, # party ids
               {}, # data
               context)) # context
type, data, _ = sock.receive()

# Logout, disconnect, cleanup
sock.send((DB, USER, PASSWORD, 'common', 'db', 'logout'))
_ = sock.receive()
sock.disconnect()
del sock
```

## Version 1.0 ##

### XML-RPC in Python ###

```
import xmlrpclib

PASSWORD = 'admin'
DB = "try"
USER = "admin"

# Get user_id and session
common = xmlrpclib.ServerProxy ('http://localhost:8069/xmlrpc/common')
user_id, session = common.login(DB, USER, PASSWORD)

object = xmlrpclib.ServerProxy('http://localhost:8069/xmlrpc/object')

party_ids = object.execute(DB, user_id, session, 'party.party', 'search',
                           [], # search clause
                           0,  # offset
                           10, # limit
                           {})  # context

print object.execute(DB, user_id, session, 'party.party', 'name_get',
                     party_ids)

```

### XML-RPC in Ruby ###

```
require 'xmlrpc/client'
require 'pp'

PASSWORD = 'admin'
DB = "try"
USER = "admin"

# Get user_id and session
common = XMLRPC::Client.new2("http://localhost:8069/xmlrpc/common")
user_id, session = common.call('login', DB, USER, PASSWORD)

object = XMLRPC::Client.new2("http://localhost:8069/xmlrpc/object")

party_ids = object.call('execute', DB, user_id, session, 'party.party', 'search',
                        [],  # search clause
                        0,   # offset
                        10,  # limit
                        {})  # context
pp object.call('execute', DB, user_id, session,  'party.party', 'name_get',
               party_ids)

```

  * NET-RPC is only available with Python since it uses [pickle](http://docs.python.org/library/pickle.html) to serialize data. The data sent over the network are more compact than with XML-RPC, hence speeding up the requests.

### NET-RPC in Python ###

```
from trytond import pysocket

PASSWORD = 'admin'
DB = "try"
USER = "admin"

sock = pysocket.PySocket()
sock.connect('127.0.0.1', '8070')

# Get user_id and session
sock.send(('common', 'login', DB, USER, PASSWORD))
user_id, session = sock.receive()

sock.send(('object', 'execute', DB, user_id, session, 'party.party', 'search',
           [],  # search clause
           0,   # offset
           10,  # limit
           {}))  # context

party_ids = sock.receive()

sock.send(('object', 'execute', DB, user_id, session, 'party.party', 'name_get',
           party_ids))
print sock.receive()
```