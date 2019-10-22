我的學習筆記
待釐清關鍵字：
Load Balancer
什麼是負載平衡器（Load Balancer）？
負載平衡器提供了類似是路由器的功能，能幫你自動分配新進來的請求要導到哪一台 Server。
為什麼你需要它？
假設你原本只有開單台機器運行一個網站，可是某一天你的服務突然撐不住了，這時候你可以重買一台規格比較好的（Scale Up），也可以買一台比較便宜差不多的然後兩台分散（Scale Out）。
可是若是你要開多台分散，就會遇到一個問題，你的網站只有一個網址，要怎麼自動分散導到這兩台呢？
這個時候通常你就需要負載平衡器（Load Balancer）了！

常見的產品有：F5 Networks BIG-IP platforms、A10 Application Delivery & Load Balancer... (key word:load balancer vender)

AWS(Amazon) + Wordpress 


自己發問：什麼是大數據？
流程圖、簡報

# Python
學習資源：
https://www.w3schools.com/python/default.asp
http://www.runoob.com/python3/python3-tutorial.html
https://python-graph-gallery.com/ (Python 畫圖！)

design pattern...

dict[x]後串接list()
1. 在要新增一筆資料的時候檢查是否已經被初始化為list
d = {}
d[key] = list()
d[key].append(value)

2. 初始化後就可以使用.append()當成list用了
if key not in d:
   d[key] = list()
d[key].append(value)


print dictionary ->
for k, v in d.items():
    print(k, v)


關於datetime的計算
How would I compute exactly 30 days into the past with Python (down to the minute)?
You want to use a datetime object instead of just a date object:

start_date = datetime.datetime.now() + datetime.timedelta(-30)
date just stores a date and time just a time. datetime is a date with a time.


dataframe
Adding new column to existing DataFrame in Pandas
Method #1: By declaring a new list as a column.
Method #2: By using DataFrame.insert()
Method #3: Using Dataframe.assign() method
Method #4: By using a dictionary
連結：https://www.geeksforgeeks.org/adding-new-column-to-existing-dataframe-in-pandas/

dataframe 選取特定欄位
df = DataFrame({'A':[5,6,3,4], 'B':[1,2,3,5]})
df[df['A']==5] or df[df['A'].isin([3,6])]
df.groupby('A').count() or df['A'].value_counts()



待研究項目：
python unit test：用 Mock 來做 python unit test
python virtualenv：使用方式與情境



# Pyspark
Filter Pyspark dataframe column with None value
1. Column.isNull / Column.isNotNull
2. If you want to simply drop NULL values you can use na.drop with subset argument:
   df.na.drop(subset=["column"])
3. sqlContext.sql("SELECT NULL = NULL").show()
   sqlContext.sql("SELECT NULL != NULL").show()
The only valid method to compare value with NULL is IS / IS NOT 
which are equivalent to the isNull / isNotNull method calls.

連結：https://stackoverflow.com/questions/37262762/filter-pyspark-dataframe-column-with-none-value


PySpark: multiple conditions in when clause
Python has no && operator. 
It has and and & where the latter one is the correct choice to create boolean expressions on Column 
(| for a logical disjunction and ~ for logical negation).

Condition you created is also invalid because it doesn't consider operator precedence. 
& in Python has a higher precedence than == so expression has to be parenthesized.


1. (col("Age") == "") & (col("Survived") == "0")
## Column<b'((Age = ) AND (Survived = 0))'>

2. On a side note when function is equivalent to case expression not WHEN clause. Still the same rules apply. 
Conjunction: df.where((col("foo") > 0) & (col("bar") < 0))
Disjunction: df.where((col("foo") > 0) | (col("bar") < 0))

3. You can of course define conditions separately to avoid brackets:
cond1 = col("Age") == "" 
cond2 = col("Survived") == "0"

cond1 & cond2
連結：https://stackoverflow.com/questions/37707305/pyspark-multiple-conditions-in-when-clause



fetch more than 20 rows and display full value of column in spark-shell
For pyspark, you'll need to specify the argument name : maxDF.show(truncate = False)
連結：https://stackoverflow.com/questions/37741841/fetch-more-than-20-rows-and-display-full-value-of-column-in-spark-shell



PySpark - Sum a column in dataframe and return results as int
df.groupBy().sum().collect()

will return a list. In your example:
In [1]: df.groupBy().sum().collect()[0][0]
Out[1]: 130


PySpark rename 的方法：

連結



Python pandas 和 Pyspark 可以混著用嗎？
pandas通常都是用在較小的資料集上，Pyspark則反之。
pandas return 結果快於 pyspark ? (待確認)
所以我們可以根據資料大小和記憶體大小來轉換這兩個工具，如果計算資料時所需的記憶體不足時，use pyspark。
連結：https://www.quora.com/Does-it-make-sense-to-use-pandas-in-pyspark


pandas vs pyspark

1. load csv
2. view dataframe (head)
3. columns name and data types
4. rename columns
5. drop columns or rows
6. filtering
7. add columns
8. fill nulls
9. aggregation
...
連結：https://www.youtube.com/watch?v=XrpSRCwISdk




# D3.js
學習資源：
https://www.tutorialsteacher.com/d3js

範例：
https://github.com/d3/d3/wiki/Gallery
https://observablehq.com/@d3


資料視覺化
https://www.informationisbeautifulawards.com/

node.js 安裝：brew install node


# Design Principles


# Cassandra

工具：Datastax DevCenter
學習資源：
https://www.tutorialspoint.com/cassandra/index.htm
https://datastax.github.io/python-driver/getting_started.html
https://yiibai.com/cassandra

啟動服務：
systemctl start cassandra
Start : - $service cassandra start
Stop  : - $service cassandra stop
Starting Cassandra as a service
Start the Cassandra Java server process for packaged installations. 
Startup scripts are provided in /etc/init.d. The service runs as the cassandra user.

使用文件執行CQL
bin/cqlsh -f select.cql
使用指令執行CQL
bin/cqlsh -e'SELECT video_id,title FROM stackoverflow.videos' > output.txt

問題：有時Cassandra要重啟時沒有確實關閉，如修改參數後須重啟。
-有時Cassandra會無法啟動，可能是參數沒設定好或是硬碟空間不足
解決辦法：
If it's only a process and not a service you could do something like

$ ps auwx | grep cassandra
$ sudo kill <pid>  
where <pid> is what you get from ps auwx | grep cassandra

This will stop the process. Then you have to start it again

$ cd <install_location>
$ bin/cassandra
where <install_location> is where you have installed cassandra

if is a service: service cassandra restart
連結：https://stackoverflow.com/questions/21433802/how-do-i-restart-apache-cassandra-2-0-4


問題：cassandra copy导入数据时batch too large错误
調整 /etc/cassandra/cassandra.yaml 文件中的參數
batch_size_fail_threshold_in_kb

cassandra.yaml 參數配置
文件位置：/etc/cassandra/conf/
連結：https://docs.datastax.com/en/dse/6.0/dse-dev/datastax_enterprise/config/configCassandra_yaml.html


建立表格：
CREATE TABLE keyspace.table ( id UUID PRIMARY KEY, lastname text, birthday timestamp, nationality text, weight text, height text );
CREATE TABLE keyspace.table ( id UUID PRIMARY KEY, lastname text, cyclist_teams set<text>, events list<text>, teams map<int,text> );
CREATE TABLE keyspace.table (race_id int, race_name text, lat_long tuple<text, tuple<float,float>>, PRIMARY KEY (race_id, point_id));
CQL 語法 ->
連結：http://cassandra.apache.org/doc/latest/cql/dml.html
其他->
連結：https://docs.datastax.com/en/archived/cql/3.3/cql/cql_using/useCreateTable.html (Create)
連結：https://www.guru99.com/cassandra-collections-tutorial-set-list-map.html
連結：https://docs.datastax.com/en/archived/cql/3.3/cql/cql_reference/cqlUpdate.html (Update)


SELECT List:?
UPDATE List:
https://docs.datastax.com/en/archived/cql/3.3/cql/cql_using/useInsertList.html
https://docs.datastax.com/en/dse/5.1/cql/cql/cql_using/useInsertList.html
SELECT Set:?
UPDATE Set: 使用 {}


表格備份：可以使用COPY指令
匯出資料：COPY source_adobe_table (adobeid,updatetime,behavior,company) TO 'source_adobe_table_backup.csv';
匯入資料：COPY source_adobe_table_backup (adobeid,updatetime,behavior,company) FROM 'source_adobe_table_backup.csv';


Cassandra如果要update，where條件必須要包含全部的 private key，否則不會通過 (Cassandra 沒有 subquery)
連結：https://stackoverflow.com/questions/27295679/how-update-rows-in-cassandra-using-only-partition-key


問題：How to get the size of a table in Cassandra?
解決辦法：
nodetool cfstats -- <keyspace>.<table>
nodetool tablestats <keyspace>.<table>
will give you the 'Space used' by a table.

連結：https://stackoverflow.com/questions/27702883/how-to-get-the-size-of-a-table-in-cassandra
連結：https://docs.datastax.com/en/archived/cassandra/3.0/cassandra/tools/toolsTablestats.html


Cassandra Backup and Restore Methods
連結：https://8kmiles.com/blog/cassandra-backup-and-restore-methods/



問題：Cassandra 空間不斷地增長
commitlog_total_space_in_mb：限制 commit log 大小，防止硬碟使用空間暴增
連結：https://stackoverflow.com/questions/38360311/if-auto-snapshot-is-enabled-in-cassandra-yaml-when-these-snapshots-will-be-dele
解決辦法：Cassandra 會在執行 drop 或 truncate 時將資料備份，以免重要資料被刪除，
在測試階段時，有可能有非常多份被快照起來
連結：https://stackoverflow.com/questions/38360311/if-auto-snapshot-is-enabled-in-cassandra-yaml-when-these-snapshots-will-be-dele
清除快照->
連結：https://docs.datastax.com/en/dse/6.7/dse-admin/datastax_enterprise/tools/nodetool/toolsClearSnapShot.html
新增快照->
連結：https://docs.datastax.com/en/dse/6.7/dse-admin/datastax_enterprise/operations/opsBackupTakesSnapshot.html
連結：https://www.vskills.in/certification/tutorial/big-data/apache-cassandra/snapshot-management/
清除特定快照->
連結：https://cassandra.apache.org/doc/latest/tools/nodetool/clearsnapshot.html
cd /var/lib/cassandra/data/dmp/table_name-xxxx/snapshot/
snapshot 底下會有多個版本
$nodetool clearsnapshot -t table_snapshot_version


常修改參數：https://www.jianshu.com/p/5bacb06e334b
Cassandra中有三个非常重要的数据结构：记录在内存中的Memtable，以及保存在磁盘中的Commit Log和SSTable
缓存主要目的通过运用内存改善读的性能，良好的配置也能极大改善写的性能。其缓存类型包括：Key Cache 、Row Cache和Counter Cache。
(1)部署調整
cluster_name: xxxxx
authenticator: PasswordAuthenticator (是否需要密碼)
data_file_directories:/home/tbs/dev/cassandra/cassdata/cassdata1 (資料文件位置)
commitlog_directory: /home/tbs/dev/cassandra/casscomm/casscomm1 (日誌文件位置)
saved_caches_directory: /home/tbs/dev/cassandra/applogs/saved_caches/1 ( Key Cache 和 Row Cache 暫存文件對應地址)

集群種子節點設定，同一個集群的每個節點的種子節點必須一致，設定2-3个種子就可以了
seed_provider:  
    - class_name: org.apache.cassandra.locator.SimpleSeedProvider
    parameters:          
        - seeds: "xxx.xxx.xxx.xxx,xxx.xxx.xxx.xxx"

本地IP和端口
native_transport_port: 9042
listen_address: xxx.xxx.xxx.xxx
rpc_address: xxx.xxx.xxx.xxx

#网关设置时间，保持一致
request_timeout_in_ms: 30000

#集群拓扑结构感知方式
endpoint_snitch: GossipingPropertyFileSnitch
dynamic_snitch_update_interval_in_ms: 100
dynamic_snitch_reset_interval_in_ms: 10000
dynamic_snitch_badness_threshold: 0.1

(2)資料結構
#批量数据大小超过5M则报警，增加该值可能引起节点不稳定
batch_size_warn_threshold_in_kb: 5000

#批量数据大小超过100M则批量操作失败
batch_size_fail_threshold_in_kb: 100000

#提交日志相关优化
#行情是周期性很强的应用，所以为了保证数据能够异步持久化到磁盘上，并减少损失，使用1s间隔刷新，避免因为batch导致写阻塞block
commitlog_sync: periodic
commitlog_sync_period_in_ms: 1000
#每个commit log 32M
commitlog_segment_size_in_mb: 32
#全部commit log大小 4G，促使memtable刷入sstable
commitlog_total_space_in_mb: 4096

batchlog_replay_throttle_in_kb: 32768

#结合业务特点，大量写，尽快进行压缩
compaction_throughput_mb_per_sec: 256

(3)線程優化
#处理CQL的最大线程数          
native_transport_max_threads: 4092

#刷盘线程
memtable_flush_writers: 2

#压缩线程
concurrent_compactors: 8

#并发读线程
concurrent_reads: 512

#并发写线程
concurrent_writes: 256

#并发计数器线程
concurrent_counter_writes: 512


(4)記憶體優化
#确保CDC配置关闭
cdc_enabled: false

#调整key cache占用heap大小，设置为0，关闭key cache
key_cache_size_in_mb: 0

#调整row cache，使用操作系统物理内存
row_cache_size_in_mb: 32768

#定时将缓存刷入磁盘，启动时预热缓存，优化读性能
row_cache_save_period: 1000

#设置缓存的key数量，根据业务场景分析，可以保存所有key值
row_cache_keys_to_save: 0

#实现类
row_cache_class_name: org.apache.cassandra.cache.OHCProvider

#通过Java NIO操作非堆，如果允许，配置成offheap_objects
memtable_allocation_type: offheap_buffers
memtable_offheap_space_in_mb: 32768
#memtable_heap_space_in_mb: 4096


#SSTable读缓存大小
file_cache_size_in_mb: 8192

#当SSTable读缓存耗尽，不分配heap作为读缓存
buffer_pool_use_heap_if_exhausted: false

#数据回传机制的同步带宽 260MB/s
hinted_handoff_throttle_in_kb: 262144

hints_flush_period_in_ms: 1000
max_hints_file_size_in_mb: 256

#索引内存大小
index_summary_capacity_in_mb: 1024


待解決問題：
Cassandra在insert大量資料時會相當慢，該如何加速
思考 Cassandra -> Kafka or Kafka -> Cassandra

Cassandra是一個強大的nosql(在特定集群下資料的throughput可是mongo db的10幾倍)?
nosql強調的是資料寫入、查詢的效能，但是為了突顯其效能，nosql有其內部的運作方式，因此有些使用上的特性必須去滿足他或是盡量要照著他的查詢規則，例如…cql的語法裡面，你的where條件必須一定要有partition key，而且還要照順序作條件，下update語法時，更新的條件，你一定要包含partition key，也只能使用=運算子，無法像sql那樣，批次大量地去異動資料(如果有錯，歡迎糾正)，而且不是關鍵式資料庫特性，不需要正規化的那麼全面，甚至就是橫向的長下去也沒關系



# Kafka



# Git
學習資源：
https://blog.techbridge.cc/2018/01/17/learning-programming-and-coding-with-python-git-and-github-tutorial/


查看git版本
$git --version 

Github 無法上傳程式？發現以下訊息：
Branch 'master' set up to track remote branch 'master' from 'origin'.
Everything up-to-date

解決辦法：
加入本地端repository
git add .
git add file_name

添加提交描述
git commit -m '修改內容描述'

提交前先從 Github repo 主分支中取得最新版本
git pull origin master

把本地端repo程式提交到 Github
git push -u origin master


# Linux
資料分析會使用到的指令：

$sudo du -h --max-depth=1 /var
$sudo du -h /var/ | sort -rh | head -5
磁碟空間大小：https://linuxize.com/post/how-get-size-of-file-directory-linux/

cronjob : https://dotblogs.com.tw/jason_wang/2016/10/27/crontab


Linux 查看記憶體 (RAM) 使用狀況及規格
free 指令
free 指令可以顯示實體記憶體和 SWAP 的大小及使用狀況
以 MB 作為單位顯示記憶體使用狀況:$ free -m
以 GB 作為單位顯示記憶體使用狀況:$ free -g
檔案 /proc/meminfo
/proc/meminfo 檔案儲存了有關記憶體用量的資訊, 用 cat 擷取便以可看到:$ cat /proc/meminfo

top 指令
執行 top 指令後, 可以從 “Mem:” 及 “Swap:” 兩行看到記憶體及 SWAP 的使用狀況。



# vim


# Docker


# SQL
數字，日期連續範圍如何計算：
連續資料有個特性是一組連續範圍數值 - 有順序的值  結果是一樣的！
＊利用(num - RK)  可以得到分組的資料
相關連結：
https://dotblogs.com.tw/daniel/2018/03/27/180710
http://jengting.blogspot.com/2013/01/sql.html


ERD

連結：https://www.visual-paradigm.com/cn/guide/data-modeling/what-is-entity-relationship-diagram/


# Netezza
1. 如何在兩個整數相除，得到小數位的數值
When dividing both integers, it will perform integer division, which returns an integer. To perform floating point division, you must either cast one or both of the operands to float/decimal/double.
SELECT cast(12 as float)/8
SELECT 12/cast(8 as float)
SELECT cast(12 as float)/cast(8 as float)
SELECT cast(12/8 as float)
Note that the last query is different since the integer division is performed first before casting to float,that is why the decimal value was already lost.

2. 如何增加欄位
  ALTER TABLE REGION2 ADD r_col1 char(8);
https://stackoverflow.com/questions/10791332/netezza-how-to-add-a-column-to-a-table

3. 新增資料
 Insert into table_name (‘’,’’,’’,’’,) values (‘’,’’,’’,’’,’’,’’,’’)
可以按右鍵看 insert 格式


# Posgre SQL 
Postgre SQL 在使用 in 時，效能會非常不好  
連結：https://stackoverflow.com/questions/17037508/sql-when-it-comes-to-not-in-and-not-equal-to-which-is-more-efficient-and-why/17038097#17038097

Streaming Replication (wal replication)  
串流複寫（ Streaming Replication ）是 PostgreSQL 的資料複寫（ Replication ）的功能。  
這功能是用來備份資料到別台機器上，並且在主要資料庫所在的主機發生異常時，利用備份機頂替主要資料庫。  
連結：https://ravenonhill.blogspot.com/2016/03/streaming-replication.html
連結：https://scalegrid.io/blog/getting-started-with-postgresql-streaming-replication/

# DB2

日期轉字串  
SELECT VARCHAR_FORMAT(MYDATE, 'YYYY/MM/DD') FROM MYCALENDAR;  
https://stackoverflow.com/questions/9083121/format-date-to-string
https://www.ibm.com/support/knowledgecenter/SSEPGG_11.5.0/com.ibm.db2.luw.sql.ref.doc/doc/r0007110.html
