About Kwitter:
---------------------
Kwitter (Kundera + Twitter) is a basic web-based application that allows users to view and save tweets.
It uses Cassandra as backend for storing data and Kundera as a high-level client for operations on it.
It demonstrates powerful JTA support in Kundera. All operations on database are JTA managed.  


How to use:
-------------------------
* Start cassandra and create column-families by running bellow commands on cassandra-cli:

```
drop keyspace kwitter;
create keyspace kwitter;
use kwitter;
create column family USER with column_type=Super and comparator=UTF8Type and default_validation_class=UTF8Type and key_validation_class=UTF8Type;
create column family USER_INVRTD_IDX with comparator=UTF8Type and default_validation_class=UTF8Type and key_validation_class=UTF8Type;
create column family PREFERENCE;
create column family EXTERNAL_LINK with comparator=UTF8Type and default_validation_class=UTF8Type and key_validation_class=UTF8Type and column_metadata=[{column_name: USER_ID, validation_class:UTF8Type, index_type: KEYS}];
describe kwitter;
```

* Create war file of application by running below maven command:

```
mvn clean install
```

kwitter.war will be created into target folder. Copy this to webapps folder under tomcat home.

* Copy kundera-core-x.x.x.jar into lib folder under tomcat

Kundera uses its own UserTransaction and UserTransactionFactory implementation for JTA. That are needed at server startup time. So copy this file into tomcat lib folder.

* Start tomcat and hit below URL, and you are ready to go:

```
http://<your host>:<port>/kwitter/xhtml/login/login.jsf
```
