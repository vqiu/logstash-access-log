# logstash-access-log
### 常见错误
1. 使用systemd无法启动
- 版本: logstash-5.6.4

解决： 打开 ${LS_HOME}/config/startup.options 文件，
查看 LS_USER 与 LS_GROUP所对应的用户名[Default: logstash] ,建立对应的用户，再使用systemd 启动即可。
```
# groupadd logstash
# useradd logstash -g logstash -M -s /sbin/nologin
```
2. kibana 生成地图时提示“The "xx*" index pattern does not contain any of the following field types: geo_point”
出现该现象为 template 的geoip字段中的`location` type 非为`geo_point`，这里可以有两种方法：
- 将 location 的type 改为`geo_point`
- template 使用`logstash-*` 开头名称

> https://discuss.elastic.co/t/geo-point-missing/77506/3
> https://github.com/logstash-plugins/logstash-output-elasticsearch/blob/master/lib/logstash/outputs/elasticsearch/elasticsearch-template-es5x.json

