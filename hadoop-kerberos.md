# hadoop-kerberos

Hadoop uses a number of configuration files to control its behavior, including core-site.xml, hdfs-site.xml, and mapred-site.xml. When using Kerberos for authentication, there are additional configuration settings that need to be added to these files.

Here's an example of what the `core-site.xml` file might look like when using Kerberos:

```xml
<configuration>
  <property>
    <name>hadoop.security.authentication</name>
    <value>kerberos</value>
  </property>
  <property>
    <name>hadoop.security.authorization</name>
    <value>true</value>
  </property>
  <property>
    <name>hadoop.security.auth_to_local</name>
    <value>RULE:[2:$1@$0](.*@EXAMPLE.COM)s/@.*//</value>
  </property>
  <property>
    <name>hadoop.security.auth_to_local.backing.file</name>
    <value>/etc/krb5.conf</value>
  </property>
  <property>
    <name>hadoop.security.auth_to_local.backing.program</name>
    <value>/usr/local/bin/auth_to_local.sh</value>
  </property>
  <property>
    <name>hadoop.security.auth_to_local.backing.provider</name>
    <value>com.example.AuthToLocalProvider</value>
  </property>
</configuration>
```

Here is an example of what the `hdfs-site.xml` file might look like:

```xml
<configuration>
  <property>
    <name>dfs.namenode.kerberos.principal</name>
    <value>nn/_HOST@EXAMPLE.COM</value>
  </property>
  <property>
    <name>dfs.namenode.keytab.file</name>
    <value>/etc/hadoop/conf/nn.keytab</value>
  </property>
  <property>
    <name>dfs.datanode.kerberos.principal</name>
    <value>dn/_HOST@EXAMPLE.COM</value>
  </property>
  <property>
    <name>dfs.datanode.keytab.file</name>
    <value>/etc/hadoop/conf/dn.keytab</value>
  </property>
  <property>
    <name>dfs.web.authentication.kerberos.principal</name>
    <value>HTTP/_HOST@EXAMPLE.COM</value>
  </property>
  <property>
    <name>dfs.web.authentication.kerberos.keytab</name>
    <value>/etc/hadoop/conf/http.keytab</value>
  </property>
  <property>
    <name>dfs.web.authentication.kerberos.name.rules</name>
    <value>DEFAULT</value>
  </property>
```
