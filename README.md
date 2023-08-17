# oracle-12c-12.2.0.1

用来在Docker内部安装Oracle 12c

##用法
1. 先要去Oracle官网下载对应的linux安装压缩包
2. 解压到/tmp/oracle目录下
3. 挂载 /tmp/oracle 到容器的 /install
4. 启动docker，等待安装
5. 如果安装失败，可能是由于docker的内存太小

 ##使用docker stack部署的示例
 ```yml
version: '3.2'
  oracle12cR2:
    image: ivancondori/oracle-12c-12.2.0.1:latest
    ports:
      - "1521:1521"
    volumes:
      - /home/oracle/database/data:/u01/app/oracle
      - /home/temp:/install
    networks:
      - portainer_agent_network
    deploy: 
      replicas: 1
      restart_policy:
        condition: on-failure

networks:
  portainer_agent_network:
    external: true
```
