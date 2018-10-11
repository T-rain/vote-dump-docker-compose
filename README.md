# vote-dump-docker-compose
docker compose 和 postgresql 配置檔

共有以下幾個檔案
* docker-compose.yml
* local_db.dump
* scripts資料夾

## docker-compose.yml

docker-compose的設定檔

修改完相關的 port,password,volume位置，就可以啟動了 volume中 dump 是接下來要restore會用到的  
scripts是要放一些自己寫的scripts會用到，可不用配置

## local_db.dump

從 https://github.com/g0v/councilor-voter-guide/  
專案中 voter_guide 資料夾裡頭的local_db.dump複製過來  
時間: 2018/10/09

## Usage Steps

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
# 會需要輸入剛剛docker-compsoe中設定的密碼，這邊是設your_password
```

Ref:  
https://www.postgresql.org/docs/current/static/app-pgrestore.html


3. 最後開始進行連線吧
```
host: your_host/ip/localhost
port: docker-compose裡頭設定的，這邊是設5432
user: postgres
password: docker-compose裡頭設定的，這邊是設your_password
dbname: vote(上個步驟建立的)
```

## 附錄: 
各系統軟體安裝

### Windows
非使用docker，與以上步驟不同，只會使用到資料夾中的 local_db.dump 來 restore
1. 安裝 postgresql
https://www.openscg.com/bigsql/postgresql/installers.jsp/

2. restore from dump(資料夾裡頭的local_db.dump)
https://www.youtube.com/watch?v=TsLTDttthRw

3. 開始使用吧

### Mac
* Get started with Docker for Mac  
https://docs.docker.com/docker-for-mac/  

照以上步驟做就可安裝完 docker 與 docker-compose

### Linux
* How to Install and Use Docker on Ubuntu 18.04  
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04
* How To Install Docker Compose on Ubuntu 18.04  
https://www.digitalocean.com/community/tutorials/how-to-install-docker-compose-on-ubuntu-18-04

照以上步驟做就可安裝完 docker 與 docker-compose
