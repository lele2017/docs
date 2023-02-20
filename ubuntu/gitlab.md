## gitlab使用教程

##### 默认repositories目录

> /var/opt/gitlab/git-data/repositories/

##### 服务器IP修改后，项目克隆地址仍是原IP地址的修改方法

> sudo vi /opt/gitlab/embedded/service/gitlab-rails/config/gitlab.yml        //修改host值即可
>
> sudo gitlab -ctl restart

