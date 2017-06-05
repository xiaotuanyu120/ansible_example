# ansbile示例：线上服务器服务安装roles
各位大哥，只要在前期配置了组变量中的server_type，并完善相应的主机变量，此roles就会根据指定的服务类型来安装配套的软件和环境

---

### 1. group_vars 配置示例
``` yaml
---
##################
# server config
##################
# server_type:
# {
#   nginx:
#     yaml_file: "{{ service_conf.nginx.yaml_file }}" 
#   webserver:
#     ext: "{{ service_conf.webserver.ext }}"
#     yaml_file: "{{ service_conf.webserver.yaml_file }}"
#   webservice:
#     ext: "{{ service_conf.webservice.ext }}"
#     yaml_file: "{{ service_conf.webservice.yaml_file }}"
#   middleservice:
#     ext: "{{ service_conf.middleservice.ext }}"
#     yaml_file: "{{ service_conf.middleservice.yaml_file }}"
#   redis:
#     yaml_file: "{{ service_conf.redis.yaml_file }}" 
#   zookeeper:
#     yaml_file: "{{ service_conf.zookeeper.yaml_file }}" 
# }
server_type:
  redis:
    yaml_file: "{{ service_conf.redis.yaml_file }}" 
##################
# jdk config
##################
# jdk version type:
# {
#   "{{ jdk6 }}"
#   "{{ jdk7 }}"
#   "{{ jdk8 }}"
# }
jdk_version:
  - "{{ jdk6 }}"
  - "{{ jdk7 }}"
  - "{{ jdk8 }}"
```
> 指定service type，可指定多个，指定了对应的service type之后，会安装该service的相应软件  
另外配置jdk的版本，当指定webserver,webservice,middleservice service type时，会安装jdk，在这里指定需要安装的jdk版本

> 另外值得注意的是，需要配置一个all的组变量文件
``` yaml
# ssh config
ansible_ssh_private_key_file: /root/.ssh/id_rsa
ansible_ssh_pass: 123456
ansible_user: gsmcupdate
```
配置一个全局变量

---

### 2. host_vars 配置示例
``` yaml
---
################
# brand
################
brand:
    name: testBrand
################
# redis
################
# redis_pass default: pass123
redis_pass: pass123
# redis_port default: 6379
redis_port: 6379
```
> brand变量主要是影响代码目录的名称  
redis的相应配置可以配置在主机变量或者组变量中
