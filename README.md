Based on https://github.com/isemenko/impala-jdbc-kerberos, modified to connect to Cloudera Impala CDH5.10.0 secure cluster.


/***************Copy description from base***************/

To run this, do the following:

- Export keytab of the local principal, using 'hdfs' principal in this example
  kadmin.local
  xst -k hdfs.keytab hdfs/test.com@TEST.COM
- Edit gss-jaas.conf to have the correct principal and path to keytab of that principal.
- Edit the krb5.conf with the correct values or copy one of your own over it.
-- Alternatively you may just refer to /etc/krb5.conf
- Make sure you are using oracle's JDK in your path.
- Compile the project with Maven3
  mvn clean install
  
  --------------------------Impala case---------------------------
- /usr/java/default/bin/java -cp target/hiveserver2-jdbc-1.0-jar-with-dependencies.jar  com.test.ImpalaJDBC "jdbc:hive2://impala-host:21050/;principal=impala/test.com@TEST.COM" /etc/krb5.conf

Notice that we are using local principal "hdfs@TEST.COM" to connect to impala using service principal impala/test.com@TEST.COM

  --------------------------Hive2 case----------------------------
- /usr/java/default/bin/java -cp target/hiveserver2-jdbc-1.0-jar-with-dependencies.jar  com.test.ImpalaJDBC "jdbc:hive2://hive2-host:10000/;principal=hive/test.com@TEST.COM" /etc/krb5.conf

Notice that we are using local principal "hive/test.com@TEST.COM" to connect to hive2 using service principal hive/test.com@TEST.COM
