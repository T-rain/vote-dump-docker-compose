# vote-dump-docker-compose

docker compose 和 postgresql 配置檔

共有以下幾個檔案
* docker-compose.yml
* local_db.dump
* scripts資料夾


## docker-compose.yml

> docker-compose的設定檔

docker-compose的安裝教學

* How to Install and Use Docker on Ubuntu 18.04  
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04
* How To Install Docker Compose on Ubuntu 18.04  
https://www.digitalocean.com/community/tutorials/how-to-install-docker-compose-on-ubuntu-18-04

修改完相關的 port,password,volume位置，就可以啟動了 volume中 dump 是接下來要restore會用到的  
scripts是要放一些自己寫的scripts會用到，可不用配置

## local_db.dump
從 https://github.com/g0v/councilor-voter-guide/
專案中 voter_guide 資料夾裡頭的local_db.dump複製過來  
時間: 2018/10/09

# Usage Steps

1. 配置完後，使用以下指令啟動：

```shell
docker-compose up -d
```

2. 進入containter，並restore dump，密碼就跟docker-compose.yml 設定的一樣

```shell
docker-compose exec db bin/bash
#建立資料庫 vote
createdb -U postgres vote
# restore dump 進 vote 資料庫
pg_restore -U postgres -W -d vote -v local_db.dump
```

Ref:  
https://www.postgresql.org/docs/current/static/app-pgrestore.html


3.最後開始進行連線吧
