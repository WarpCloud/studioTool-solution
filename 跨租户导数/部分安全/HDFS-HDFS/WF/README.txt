
1.hdfs_hdfs_smail.json  跨租户的hdfs的小文件互导   文件大小771 KB  5千条数据量

  wf内容：通过脚本任务 执行distcp 命令 拷贝文件 到目标集群 实现跨租户的hdfs的小文件互导
  
2.hdfs_hdfs_big.json 跨租户的hdfs的大文件文件互导  文件大小2G   1千w数据量

  wf内容：通过脚本任务 执行distcp 命令 拷贝文件 到目标集群 实现跨租户的hdfs的大文件互导
  
3.hdfs_hdfs_table_only.json  跨租户表文件互导  表数据5000条
  
  wf内容：通过sql任务，在源端创建orc表，导入数据，并导出数据至hdfs目录，再通过脚本任务，执行distcp命令
          拷贝文件到目标端hdfs，然后用sql任务，在目标端创建orc表，并把拷贝的数据导入到orc表
		  
4.hdfs_hdfs_table_many.json  跨租户多表文件互导  3张orc表，数据为5000

  wf内容: 通过sql任务，在源端创建多张orc表，导入数据，并导出数据至hdfs目录，再通过脚本任务，执行distcp命令
          拷贝文件夹到目标端hdfs，然后用sql任务，在目标端创建多张orc表，并把拷贝的数据导入到orc表
          

 WF 参数解析：
${hostname_inceptor_A} 填写源端inceptor ip
${hostname_inceptor_B} 填写目标端inceptor ip
${hostname_distcp_A} 填写源端namenode hdfs ip
${hostname_distcp_B} 填写目标端namenode hdfs ip
${guardian_token} 填写源端inceptor guardian token
注意：
如果试用wf的脚本任务，但是同时需要调用hdfs等客户端，可以试用tdhclient，具体操作可详见workflow的操作文档，下面简单描述：
1 需要把TDH-client.tar 添加到/var/lib/workflow{id}/ 目录下
2 并重启workflow服务，才能source TDH-client 成功

只支持从安全到不开安全的distcp,不支持不开安全到开安全的，执行distcp 添加的参数：
-Dipc.client.fallback-to-simple-auth-allowed=true  这个参数不支持 源端和目标端都不开安全的环境，或者源端和目标端都开安全的环境
例如:hadoop distcp  -Dipc.client.fallback-to-simple-auth-allowed=true hdfs://node089:8020/sql_hbase hdfs://172.26.5.39:8020/test_data
	
