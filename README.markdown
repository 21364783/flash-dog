* ����
Ӧ��ͨ��log4j�����־��mongodb���ݿ��У����繷��ʱ���нű�������־�����ɼ�����ߺ͸澯����Ҫ�ŵ��ǲ�Ӱ��ҵ����룬ֻ����뼸��jar�����޸�log4j�����ļ����ܽ��롣

 1. ��װ
* ��װ[mongodb](http://www.mongodb.org/downloads),��ѹ�������������ݱ���·������������ 
* ����[flash-dog-server](https://github.com/flash-dog/flash-dog/downloads)
* �޸�flash-dog-server�ļ����µ�log4j.properties�ļ����޸�log4j.appender.MongoDB��hostname��portָ���㲿���mongodb��ַ�Ͷ˿ڣ�  
    log4j.appender.MongoDB.hostname=172.16.3.47  
    log4j.appender.MongoDB.port=27017  
* �޸�conf/develop/app.properties��Ҳָ��ղŲ����mongodb  
    mongo.uri=mongodb://172.16.3.47:27017/monitor_test  
* ����bin�£�����start.sh develop����start-dev.bat  
 ����������http://localhost:8080/flash-dog/projects �����û�����admin ���� 123456 ���㽫����һ�������繷����Ŀ��������Ϊ���繷Ҳ�����Լ���wow

 2. �����Լ�����Ŀ�������繷
* ��flash-dog-server�ļ���libĿ¼�¿���log4mongo-java ,flash-dog-api-log4j �� mongo-java-driver-2.7.0.jar ����Ŀ��lib���£�ע�⻹��Ҫlog4j 1.2.15���ϵİ汾
* ����flash-dog-server�����log4j.properties�޸����Լ���log4j.properties�����ļ�
* ����������Ŀ
* ����http://localhost:8080/flash-dog/projects ,�½���Ŀ�����������ȷ���㽫�ڡ���־��������Ŀ�в�ѯ��������־��enjoy your self��

 3. ����˵��
* log4j.properties
<pre><code>
log4j.appender.MongoDB=org.log4mongo.AsynMongoDbLayoutAppender
log4j.appender.MongoDB.layout=org.log4mongo.contrib.HostInfoPatternLayout
#pid��ʾ���̺ţ�ipΪ��ǰ������ip
log4j.appender.MongoDB.layout.ConversionPattern={"timestamp":"%d","level":"%p","className":"%c","message":"%m","pid":"%V","ip":"%I"}
#��̨������־ʹ�õ��߳���
log4j.appender.MongoDB.threadCount=2
#�Ƿ��Զ���ӡjvm��Ϣ����cpu��memory��threadcount��
log4j.appender.MongoDB.jvmMonitor=true
log4j.appender.MongoDB.databaseName=test
log4j.appender.MongoDB.collectionName=flash_dog_log
log4j.appender.MongoDB.hostname=172.16.3.47
log4j.appender.MongoDB.port=27017 
log4j.rootLogger=info,stdout,logfile,MongoDB
</code></pre>

