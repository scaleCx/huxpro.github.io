---
layout: post
title:  "自动提交GitHub脚本"
date:   2021-08-07 16:12:40
catalog:  true
tags:
  - Shell
  - Linux
  - Git
---

出于想使用 Vnote + GitHub 记录工作笔记的原因,网上找脚本修改下...
```shell
#!/bin/bash

git_push(){
    echo "开始push"

    cd ${1}
    echo "-------切换目录------"
    echo `pwd`
    echo "---------------------"
    if [ -n "$(git status -s)" ];
    then
        echo "${1} 文件夹 有变化，正在准备push..."
        date=`date "+%Y-%m-%d %H:%M:%S"`
        git add .
        git commit -m "automatic push @$(date)"
        echo "git fetch origin master"
        git fetch origin master

        echo "git merge origin/master"
        git merge origin/master

        echo "git push origin master:master"
        git push origin master:master

    fi
}

git_push ~/IdeaProjects/20210729/src/ttt
```
脚本主要参考文章[ubuntu自动push到github脚本](https://cloud.tencent.com/developer/article/1179839),文中定时任务使用cron服务实现,我这里就直接贴过来了(#^.^#)   

```
编辑定时任务文件
(https://blog.csdn.net/xiyuan1999/article/details/8160998) <- linux定时任务的设置 crontab 配置指南
crontab  -e
在文件的末尾添加：

30 5 * * * /home/mianhk/shell/auto_push.sh  表示在每天的 5.30执行
启动服务
/etc/init.d/cron start
```

---
坑:
1. `stat -c %Y ${1}`Mac 上无法使用,没有-c 的选项

参考:  
[ubuntu自动push到github脚本](https://cloud.tencent.com/developer/article/1179839)  
[linux shell:判断git工作文件夹是否干净(clean)](https://cloud.tencent.com/developer/article/1508321)  

