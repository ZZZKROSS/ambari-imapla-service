An Ambari Service for Impala
====

## Support Version
- Impala 2.6 +
- Hadoop 2.6 +

## Install Impala two ways:

### 1. To download the Impala service folder, run below    

```
VERSION=`hdp-select status hadoop-client | sed 's/hadoop-client - \([0-9]\.[0-9]\).*/\1/'`
sudo git clone https://github.com/cas-bigdatalab/ambari-impala-service.git /var/lib/ambari-server/resources/stacks/HDP/$VERSION/services/IMPALA        
```

### 2. MPACK 
```
ambari-server install-mpack --mpack=ambari-impala-mpack-2.6.0-0816.tar.gz -v
```

## local repository
Make your local repository.Download software from https://archive.cloudera.com/cdh5/redhat/6/x86_64/cdh/5.8.0/

software list as below:
```
avro-doc-1.7.6+cdh5.8.0+112-1.cdh5.8.0.p0.74.el6.noarch.rpm
avro-libs-1.7.6+cdh5.8.0+112-1.cdh5.8.0.p0.74.el6.noarch.rpm
avro-tools-1.7.6+cdh5.8.0+112-1.cdh5.8.0.p0.74.el6.noarch.rpm
bigtop-jsvc-0.6.0+cdh5.8.0+847-1.cdh5.8.0.p0.74.el6.x86_64.rpm
bigtop-jsvc-debuginfo-0.6.0+cdh5.8.0+847-1.cdh5.8.0.p0.74.el6.x86_64.rpm
bigtop-utils-0.7.0+cdh5.8.0+0-1.cdh5.8.0.p0.72.el6.noarch.rpm
hbase-1.2.0+cdh5.8.0+160-1.cdh5.8.0.p0.80.el6.x86_64.rpm
hbase-doc-1.2.0+cdh5.8.0+160-1.cdh5.8.0.p0.80.el6.x86_64.rpm
hbase-master-1.2.0+cdh5.8.0+160-1.cdh5.8.0.p0.80.el6.x86_64.rpm
hbase-regionserver-1.2.0+cdh5.8.0+160-1.cdh5.8.0.p0.80.el6.x86_64.rpm
hbase-rest-1.2.0+cdh5.8.0+160-1.cdh5.8.0.p0.80.el6.x86_64.rpm
hbase-thrift-1.2.0+cdh5.8.0+160-1.cdh5.8.0.p0.80.el6.x86_64.rpm
hive-1.1.0+cdh5.8.0+610-1.cdh5.8.0.p0.77.el6.noarch.rpm
hive-hbase-1.1.0+cdh5.8.0+610-1.cdh5.8.0.p0.77.el6.noarch.rpm
hive-hcatalog-1.1.0+cdh5.8.0+610-1.cdh5.8.0.p0.77.el6.noarch.rpm
hive-jdbc-1.1.0+cdh5.8.0+610-1.cdh5.8.0.p0.77.el6.noarch.rpm
hive-metastore-1.1.0+cdh5.8.0+610-1.cdh5.8.0.p0.77.el6.noarch.rpm
hive-server-1.1.0+cdh5.8.0+610-1.cdh5.8.0.p0.77.el6.noarch.rpm
hive-server2-1.1.0+cdh5.8.0+610-1.cdh5.8.0.p0.77.el6.noarch.rpm
hive-webhcat-1.1.0+cdh5.8.0+610-1.cdh5.8.0.p0.77.el6.noarch.rpm
hive-webhcat-server-1.1.0+cdh5.8.0+610-1.cdh5.8.0.p0.77.el6.noarch.rpm
impala-2.6.0+cdh5.8.0+0-1.cdh5.8.0.p0.111.el6.x86_64.rpm
impala-catalog-2.6.0+cdh5.8.0+0-1.cdh5.8.0.p0.111.el6.x86_64.rpm
impala-debuginfo-2.6.0+cdh5.8.0+0-1.cdh5.8.0.p0.111.el6.x86_64.rpm
impala-server-2.6.0+cdh5.8.0+0-1.cdh5.8.0.p0.111.el6.x86_64.rpm
impala-shell-2.6.0+cdh5.8.0+0-1.cdh5.8.0.p0.111.el6.x86_64.rpm
impala-state-store-2.6.0+cdh5.8.0+0-1.cdh5.8.0.p0.111.el6.x86_64.rpm
impala-udf-devel-2.6.0+cdh5.8.0+0-1.cdh5.8.0.p0.111.el6.x86_64.rpm
parquet-1.5.0+cdh5.8.0+174-1.cdh5.8.0.p0.71.el6.noarch.rpm
parquet-format-2.1.0+cdh5.8.0+12-1.cdh5.8.0.p0.70.el6.noarch.rpm
sentry-1.5.1+cdh5.8.0+244-1.cdh5.8.0.p0.83.el6.noarch.rpm
sentry-hdfs-plugin-1.5.1+cdh5.8.0+244-1.cdh5.8.0.p0.83.el6.noarch.rpm
sentry-store-1.5.1+cdh5.8.0+244-1.cdh5.8.0.p0.83.el6.noarch.rpm
solr-4.10.3+cdh5.8.0+423-1.cdh5.8.0.p0.79.el6.noarch.rpm
solr-crunch-1.0.0+cdh5.8.0+0-1.cdh5.8.0.p0.75.el6.noarch.rpm
```

## Restart Ambari  
sudo service ambari-server restart


## HDFS config
we need add below config to /etc/hadoop/conf/core-site.xml
```
<property>
    <name>dfs.client.read.shortcircuit</name> 
   <value>true</value>
</property>

<property>
    <name>dfs.client.read.shortcircuit.skip.checksum</name>
        <value>false</value>
</property>

<property> 
    <name>dfs.datanode.hdfs-blocks-metadata.enabled</name> 
    <value>true</value>
</property>
```
we need add below config to /etc/hadoop/conf/hdfs-site.xml
```
<property>
    <name>dfs.datanode.hdfs-blocks-metadata.enabled</name> 
    <value>true</value>
</property>
<property> 
    <name>dfs.block.local-path-access.user</name> 
    <value>impala</value>
</property>
<property>
    <name>dfs.client.file-block-storage-locations.timeout.millis</name>
    <value>60000</value>
</property>
```
add config info through webui

![Image](../master/screenshots/core-site.png?raw=true)
![Image](../master/screenshots/hdfs-site.png?raw=true)

restart hadoop and restart impala

## SUMMARY
![Image](../master/screenshots/summary.png?raw=true)

## NOTICE
- make sure your hive server normally
- hdfs and hive conf file is sync to /etc/impala/conf

## Some error note:
- NoSuchMethodError:setCaching
![Image](../master/screenshots/impala-error.jpg?raw=true)
Impala rely on Cloudrea Hbase Jar ,please use relevant jar.
