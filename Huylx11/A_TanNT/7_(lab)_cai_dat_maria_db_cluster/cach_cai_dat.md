# Maria DB cluster
- Tên là `maria DB galera cluster`, cơ chế đồng bộ dữ liệu cho `multi-master mariadb`

# Multi master?

[cách hoạt động của multi master](https://arpitbhayani.me/blogs/multi-master-replication/#:~:text=A%20Multi-Master%20setup%20has%20multiple%20nodes%20of%20a,request%2C%20it%20accepts%20it%20and%20applies%20the%20changes.)

- trong một cụm hình thành ra vài sub-cluster, mỗi sub-cluster chứa thêm một master

# setup - systemd

Trong trường hợp cần doc của maria, [mariadb galera installation](https://mariadb.com/kb/en/getting-started-with-mariadb-galera-cluster/#installing-mariadb-galera-cluster)

[Hướng dẫn cài đặt MariaDB Galera Cluster](https://www.atlantic.net/vps-hosting/how-to-install-and-configure-mariadb-galera-cluster-on-ubuntu-18-04/#:~:text=How%20to%20Install%20and%20Configure%20MariaDB%20Galera%20Cluster,Step%204%20%E2%80%93%20Test%20Galera%20Cluster%20Replication%20)

1. Cài 3 VMs và cài đặt docker package trên đó: `sudo apt install docker.io -y`
2. Cài 3 VM vào chung cluster (chọn 1 máy là master)
  - Thêm mỗi VM vào group docker: `sudo usermod -aG docker h`
  - Nên đặt tên cho các node: `hostnamectl set-hostname <worker-name>`
  - `sudo -i` để chuyển sang root với tên host mới
3. vào master, `docker swarm init` để sinh token cho các worker cùng join vào cluster
4. Cài đặt mariadb 
  -  `apt install mariadb-server mariadb-client`
  - Với các bản mariadb-server 10.1 trở lên, mariadb galera server sẽ được đi kèm với mariadb-server
5. Thiết lập mật khẩu trong mariadb: (Yes hết)
4. Cài đặt các gói sau:
  - `install git wget vim`
  - `apt install galera-4`
  - `apt-get install galera-arbitrator-4`
  - `apt install rsync`
  - `apt-get install python3-pymysql`
5. disable firewall and selinux (default là disable, check để biết có enable 2 cái này không)
6. Follow tiếp các bước test để xem galera cluster có hoạt động hay không

# setup - docker
1. Kéo image galera trên dockerhub: `docker pull bitnami/mariadb-galera:latest`
2. Tạo container từ image:
  docker run --name mariadb-galera-0 `
  -e MARIADB_GALERA_CLUSTER_BOOTSTRAP=yes `
  -e MARIADB_GALERA_CLUSTER_NAME=my_galera `
  -e MARIADB_GALERA_MARIABACKUP_USER=my_mariabackup_user `
  -e MARIADB_GALERA_MARIABACKUP_PASSWORD=my_mariabackup_password `
  -e MARIADB_ROOT_PASSWORD=my_root_password `
  -e MARIADB_USER=my_user `
  -e MARIADB_PASSWORD=my_password `
  -e MARIADB_DATABASE=my_database `
  bitnami/mariadb-galera:latest

------------------------------------

https://www.youtube.com/watch?v=7EBqw5FPsvw&t=307s

docker pull bitnami/mariadb-galera:latest

> Step 1: Bootstrap the cluster

docker run --name mariadb-galera-0 \
  -e MARIADB_GALERA_CLUSTER_BOOTSTRAP=yes \
  -e MARIADB_GALERA_CLUSTER_NAME=my_galera \
  -e MARIADB_GALERA_MARIABACKUP_USER=my_mariabackup_user \
  -e MARIADB_GALERA_MARIABACKUP_PASSWORD=my_mariabackup_password \
  -e MARIADB_ROOT_PASSWORD=my_root_password \
  -e MARIADB_USER=my_user \
  -e MARIADB_PASSWORD=my_password \
  -e MARIADB_DATABASE=my_database \
  bitnami/mariadb-galera:latest


> Step 2: Add nodes to the cluster

docker run --name mariadb-galera-1 --link mariadb-galera-0:mariadb-galera \
  -e MARIADB_GALERA_CLUSTER_NAME=my_galera \
  -e MARIADB_GALERA_CLUSTER_ADDRESS=gcomm://mariadb-galera \
  -e MARIADB_GALERA_MARIABACKUP_USER=my_mariabackup_user \
  -e MARIADB_GALERA_MARIABACKUP_PASSWORD=my_mariabackup_password \
  bitnami/mariadb-galera:latest


docker exec -it mariadb-galera-0 /bin/bash
docker exec -it mariadb-galera-1 /bin/bash

ip a

ps -ef | grep mysql

mysql -u my_user -p -h 172.17.0.3
passworrd: my_password

SHOW STATUS LIKE '%cluster%';

show databases;

CREATE TABLE example ( id smallint unsigned not null auto_increment, name varchar(20) not null, constraint pk_example primary key (id) );
INSERT INTO example ( id, name ) VALUES ( null, 'Sample data 1' );
INSERT INTO example ( id, name ) VALUES ( null, 'Sample data 2' );

GRANT ALL PRIVILEGES ON . TO 'username'@'localhost' IDENTIFIED BY 'password';
SELECT user FROM mysql.user GROUP BY user;

docker stop mariadb-galera-0
docker stop mariadb-galera-1