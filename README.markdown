* ����
Ӧ��ͨ��log4j�����־��mongodb���ݿ��У����繷��ʱ���нű�������־�����ɼ�����ߺ͸澯����Ҫ�ŵ��ǲ�Ӱ��ҵ����룬ֻ����뼸��jar�����޸�log4j�����ļ����ܽ��롣

 1. ��װ
* ��װ[mongodb](http://www.mongodb.org/downloads),��ѹ�������������ݱ���·������������ 
* ����[flash-dog-server](http://github.com/mongodb/mongo-java-driver/downloads)
* �޸�flash-dog-server�ļ����µ�log4j.properties�ļ����޸�log4j.appender.MongoDB��hostname��portָ���㲿���mongodb��ַ�Ͷ˿ڣ�  
	log4j.appender.MongoDB.hostname=172.16.3.47  
	log4j.appender.MongoDB.port=27017  
* �޸�conf/develop/app.properties��Ҳָ��ղŲ����mongodb  
	mongo.uri=mongodb://172.16.3.47:27017/monitor_test  


* ����bin�£�����start.sh develop����start-dev.bat  
 ����������http://localhost:8080/flash-dog/projects �����û�����admin ���� 123456 ���㽫����һ�������繷����Ŀ��������Ϊ���繷�����Լ���wwo  

