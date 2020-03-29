
1.hbase_hbase_table_only.json  跨租户表文件互导   
  源端为开安全， 目标端为不开安全
   
  wf内:通过workflow 选取sql任务，添加创建hbase表，通过TDT 创建数据流，导入数据，并通过workflow选取数据流调度，
       再用TDT数据流导出数据，到hdfs上 然后再使用脚本内容，distcp 拷贝数据到目标hdfs，通过源端TDT，
	   选取连接都为目标端，创建数据流，导入数据   使用wf+tdt来实现跨租户表文件互导
   
  
2.hbase_hbase_table_many.json   跨租户多表文件互导 
	 源端为开安全， 目标端为不开安全
	
  wf内:通过workflow 选取sql任务，添加创建多张hbase表，通过TDT 创建数据流，导入数据，并通过workflow选取数据流调度，
       再用TDT数据流导出数据，到hdfs上 然后再使用脚本内容，distcp 拷贝文件夹到目标hdfs，通过源端TDT，
	   选取连接都为目标端，创建数据流，导入数据   使用wf+tdt来实现跨租户多表文件互导
	   
	   
  图片：hbase_hbase_many_tdt_1.PNG,hbase_hbase_many_tdt_2.PNG,hbase_hbase_many_tdt_3.PNG 记载的是 tdt reader端导入数据到hbase表 步骤
  
        hbase_hbase_many_tdt_4.PNG,hbase_hbase_many_tdt_5.PNG 记载的是 tdt wirter端导出数据到源端 hdfs 步骤
		
		
  TDT_json:
       1.tdt_hbase_hbase_only_json  文件夹  里面是TDT数据流json文件    跨租户表文件互导 TDT数据流
	   
	   1.hbase_location_data_table_89.json   导入数据，到89的hbase表
	   2.hbase_location_data_hdfs_89.json   通过inceptor 已有的hbase表，导出数据到89的hdfs上
	   3.hbase_location_data_table_38.json  通过538hdfs连接，获取到distcp 拷贝到38的数据，导入到38inceptor hbase中
	   
	   
	   2.tdt_hbase_hbase_many_json 文件夹   里面是TDT数据流json文件   跨租户多表文件互导  TDT数据流
	   
	   1.hbase_loaction_data_table_89_1.json       3个json，是tdt通过csv获取89hdfs上路径文件，分别导入数据到89 hbase表
	     hbase_loaction_data_table_89_2.json
		 hbase_loaction_data_table_89_3.json
	   
	   2.hbase_loaction_data_hdfs_89_1.json        3个json 通过inceptor 已有的3张hbase表，导出数据到89的hdfs上
	     hbase_loaction_data_hdfs_89_2.json
		 hbase_loaction_data_hdfs_89_3.json
		 
	   3.hbase_loaction_data_table_38_1.json       3个json 通过538hdfs连接，获取到distcp 拷贝到38的数据，导入到38inceptor hbase中
	     hbase_loaction_data_table_38_2.json
		 hbase_loaction_data_table_38_3.json