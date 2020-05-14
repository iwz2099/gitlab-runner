# deploy gitlab-runner


#### Docker方式启动Gitlab-runner

```
docker-compose up -d 
```

#### 注册Runner
```
docker exec -it gitlabrunner_gitlab-runner-platform_1  gitlab-runner register \
--non-interactive \
--executor "docker" \
--docker-image registry.test.cn/platform/ci-base:1 \ #runner默认基础镜像
--url "https://code.test.cn/" \
--registration-token "hzUzz3a2Zhdkmvgs-Zy3" \  #这里可以到gitlab仓库或者族CICD配置那里获取
--description "gitlab-runner-platform" \
--tag-list "platform,infra" \ #以逗号分割，定义tag,gitlab CI构建时使用
--locked="false" \
--docker-volumes="/cache" \
--docker-volumes="/var/run/docker.sock:/var/run/docker.sock" \
--docker-extra-hosts="github.com:192.30.253.113" \
--docker-dns "172.20.10.210"  #配置内部dns，防止无法解析内网服务。
```