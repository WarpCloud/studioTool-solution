环境：开安全 - 不开安全 

  1.全部是用workflow调度 ：sql，脚本这2种任务类型
  2.sql任务类型，要注意，认证方式  分为开安全和不开安全
  3.脚本任务类型，要注意，脚本内容里面有source TDH-clite，需要把TDH-clite.tar 添加到/var/lib/workflow{id}/ 目录下
    并重启workflow服务，才能source TDH-clite 成功
	
	
	如果一个环境开安全，一个没有开
	需要在开安全的环境需要添加参数 
	-Dipc.client.fallback-to-simple-auth-allowed=true
	discp命令 hadoop distcp  -Dipc.client.fallback-to-simple-auth-allowed=true hdfs://node089:8020/sql_hbase hdfs://172.26.5.39:8020/test_data



1.hbase_hbase_table_only.json  跨租户表文件互导   
  源端为开安全， 目标端为不开安全
  
  wf内容:通过workflow 选取sql任务，添加创建hbase表，导入数据，导出数据等sql内容，再通过脚本执行distcp 拷贝数据到
         目标端hdfs，然后选取sql内容，再目标端创建hbase表，并把拷贝过来的数据导入到表中  来实现跨租户表文件互导的功能
		
  
2.hbase_hbase_table_many.json   跨租户多表文件互导 
	 源端为开安全， 目标端为不开安全
	
	 wf内容:通过workflow 选取sql任务，添加创建多张hbase表，导入数据，导出数据等sql内容，再通过脚本执行distcp 拷贝文件夹到
         目标端hdfs，然后选取sql内容，再目标端创建多张hbase表，并把拷贝过来的数据导入到表中  来实现跨租户表文件互导的功能