**����**  
Ӧ��ͨ��log4j�����־��mongodb���ݿ��У����繷��ʱ���нű�������־�����ɼ�����ߺ͸澯����Ҫ�ŵ��ǲ�Ӱ��ҵ����룬ֻ����뼸��jar�����޸�log4j�����ļ����ܽ��롣
## 
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
![screenshot](https://github.com/downloads/flash-dog/flash-dog/image-flash-dog-1.jpg)
 2. �����Լ�����Ŀ�������繷
* ��[flash-dog-api-log4j](https://github.com/flash-dog/flash-dog/downloads)���ؿͻ��˵�lib�⣬���ߴ�flash-dog-server�ļ���libĿ¼�¿���log4mongo-java ,flash-dog-api-log4j �� mongo-java-driver ����Ŀ��lib���£�ע�⻹��Ҫlog4j 1.2.15���ϵİ汾
* �޸����Լ���log4j.properties�����ļ�
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


 4. ʹ��logback
* ���ذ�װ [logback-mongodb](https://github.com/flash-dog/logback-mongodb)
        <pre><code>
            mvn clean install
        </code></pre>

* ����slf4j �� logback ������

		<dependency>
			<groupId>org.slf4j</groupId>
			<artifactId>slf4j-api</artifactId>
			<version>1.6.5</version>
		</dependency>

        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-core</artifactId>
            <version>1.0.6</version>
        </dependency>
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.0.6</version>
        </dependency>

        <dependency>
            <groupId>logback.mongodb</groupId>
            <artifactId>logback.mongodb</artifactId>
            <version>1.0.2</version>
        </dependency>


* logback������

        <appender name="MONGO" class="logback.mongodb.MongoDBAppender">
            <connectionSource class="logback.mongodb.MongoDBConnectionSource">
                <uri>mongodb://172.16.3.47:27017</uri>
                <db>ugglog</db>
                <collection>paylog</collection>
            </connectionSource>
        </appender>

        <appender name="ASYNCMONGO" class="ch.qos.logback.classic.AsyncAppender">
            <appender-ref ref="MONGO" />
        </appender>

        <logger name="currency" additivity="false" level="warn">
            <appender-ref ref="MONGO"/>
        </logger>


* ��logback�п���ʹ��MDC����������ӵ��ֶ�
        <pre><code class="java">
                MDC.clear();
                MDC.put("mob", mob.name());
                MDC.put("value", value + "");
                MDC.put("currency", type.name());
                MDC.put("reason", reason);
                MDC.put("saveAtOnce", saveAtOnce + "");
                mongoLogger.info("{}:{} {} {} {} {}", new Object[]{logPre, mob.name(), value, type, reason, saveAtOnce});
        </code></pre>

* ������mongodb��collection�б����scheme��������Щ�ֶ�:
        <pre><code>
           {
              mob: '',
              value: '',
              currency: '',
              reason: '',
              saveAtOnce: ''
           }
        </code></pre>
