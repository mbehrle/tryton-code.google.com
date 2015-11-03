# Introduction #

When running a POS system reliability is the most important thing to pay attention to. Failures caused by network or other problems can be mostly ignored when the POS-Terminals synchronize with a master server.

There are two directions that have to be handled, getting product information from the server via pulling and writing the transaction data back to the server via pushing.

To solve those problems a generic synchronize module into which existing models can be added configured with GUI was written. To prevent that all records would be synchronized, for each model and its fields can be individually configured if the records should simply be created or if should be tried to determine the records by matching the fields values. This is for example useful with the UOM models. If a record can not be determined by matching it will be created.

When a new model is added to the synchronize module it will be recursively scanned for its dependencies that also will be added into the tree. Then the user has to check the fields that he wants to be synchronized. After setting up a remote server connection the connection has to be configured into the root record of the model.

With the "Synchronize with server" wizard a synchronization can be initiated. The wizard will ask if it should be a pull or a push operation.

# Realization #

The whole idea of the synhronize algorithm is to compare timestamps between the last synch and the time of synching. Each synch is added into a model named synchronize.history.

The whole synch operation a connection set with the two connections to synch between is used. It stores the direction and the source and target connection. The connection objects used for synching can be extended by extending the synchronize.server model which will create all the connection objects. With this it is possible to implement the ConnectionInterface for other systems maybe for migration. It should also be possible to synch in both directions with it.
The connection to the remote Trytond-Server uses [NET-RPC](http://code.google.com/p/tryton/wiki/RemoteCalls#NET-RPC_in_Python) for communication.
Because of the same interface for all connections it is possible to change the direction of synching by easy exchanging of the two connections.

When a new synch operation is started, the synchronize.model class will traverse the dependency tree of the desired model. The leafs will be created first because of the reference constraints. If the current model contains fields that are marked with the match\_field flag, it will be tried to get the records by matching otherwise they will be created. When a new record is created, its foreign primary key is added into the synchronize.translation model so that it later can be translated back.

The idea is to provide modules which will provide preconfigured datasets for models so that the user does not have to think about it in depth.

### Synchronize module ###
The synchronize module is available at:
https://bitbucket.org/pokereichlich/synchronize

### Synchronize Product Module ###
A module that configures product.product ready to use is available at:
https://bitbucket.org/pokereichlich/synchronize_product
Only a server connection has to be added and set into the product.product root entry.

### Other related repositories ###
https://bitbucket.org/pokereichlich/synchronize_mysql

https://bitbucket.org/pokereichlich/pos_cash

https://bitbucket.org/pokereichlich/pos_client

https://bitbucket.org/pokereichlich/pos_price_label

The modules are still under development and a kind of experimental.