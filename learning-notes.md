我的學習筆記


-- Python



-- Cassandra

問題：How to get the size of a table in Cassandra?
解決辦法：
nodetool cfstats -- <keyspace>.<table>
will give you the 'Space used' by a table.

連結：https://stackoverflow.com/questions/27702883/how-to-get-the-size-of-a-table-in-cassandra


-- Git
學習相關資源：
https://blog.techbridge.cc/2018/01/17/learning-programming-and-coding-with-python-git-and-github-tutorial/


查看git版本
$git --version 

Github 無法上傳程式？發現以下訊息：
Branch 'master' set up to track remote branch 'master' from 'origin'.
Everything up-to-date

解決辦法：
加入本地端repository
git add .

添加提交描述
git commit -m '修改內容描述'

提交前先從 Github repo 主分支中取得最新版本
git pull origin master

把本地端repo程式提交到 Github
git push -u origin master


-- vim
