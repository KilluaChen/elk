###  ELK

1. Install Dcoker
    - Docker
        - centos 7
            ```bash
            $ sudo yum install -y yum-utils
            $ sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
            $ sudo yum install docker-ce docker-ce-cli containerd.io
            ```
        - centos 8 缺少 `containerd.io` 时执行
            ```bash
            $ yum install -y https://mirrors.aliyun.com/docker-ce/linux/centos/7/x86_64/edge/Packages/containerd.io-1.2.13-3.2.el7.x86_64.rpm
            ```
        - [Other systems](https://docs.docker.com/engine/install/)
    - Docker-compose
        - centos
            ```
            $ curl -L https://get.daocloud.io/docker/compose/releases/download/1.26.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
            $ sudo chmod +x /usr/local/bin/docker-compose
            # append to ~/.bashrc
            alias docker-compose="/usr/local/bin/docker-compose"
            
            $ source ~/.bashrc
            ```
        - [Other systems](https://docs.docker.com/compose/install/)

2. Start Docker Service (centos)
    ```
   $ sudo systemctl start docker
   $ sudo systemctl enable docker
   ```
3. Clone project
    - Git  `git clone https://github.com/KilluaChen/elk.git`
    - [Download](https://github.com/KilluaChen/elk/archive/master.zip)
    
1. Setting ES Account
    ```
    $ docker-compose up es1
    $ docker exec -it es1 /bin/bash
    $ elasticsearch-setup-passwords interactive
    ```
5. Command
    ```bash
   # Run
   $ docker-compose up

   # Start single service
   $ docker-compose up es1
   
   # Run Daemon
   $ docker-compose up -d
   
   # Stop
   $ docker-compose stop˙
   
   # Delete
   $ docker-compose down
   ```
1. zsh alias
    ```bash
    alias dis="docker images"
    alias dps="docker ps"
    alias dc="docker-compose"
    ```
7. PS
    - 查看宿主机ip 让容器内访问
         ```
         ip addr show docker0
         ```
    - 下载`Docker 镜像`过慢可以使用阿里的[容器镜像服务](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors) 
        ```
       sudo mkdir -p /etc/docker
       sudo tee /etc/docker/daemon.json <<-'EOF'
       {
         "registry-mirrors": ["https://c9uxfqpy.mirror.aliyuncs.com"]
       }
       EOF
       sudo systemctl daemon-reload
       sudo systemctl restart docker
       ```
    - 更多设置参考 [https://github.com/nanoninja/docker-nginx-php-mysql](https://github.com/nanoninja/docker-nginx-php-mysql)
    
     
    
