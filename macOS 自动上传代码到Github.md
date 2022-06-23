# macOS 自动上传代码到Github

1. Github创建私有仓库
2. 在本地终端中初始化本地仓库
    
    ```bash
    git init
    ```
    
3. 输出Github公钥
    
    ```bash
    ssh-keygen -t rsa -C "youremail@example.com"
    ```
    
4. 进入`.ssh`目录复制公钥 `id_rsa.pub`
    
    ```bash
    cd .ssh
    vim id_rsa.pub
    ```
    
5. 登录[Github](https://github.com/settings/keys)复制公钥
    
    ![Untitled](Untitled.png)
    
6. 关联本地仓库和Github仓库
    
    ```bash
    git remote add origin git@github.com:waynesparrow123/xxx.git
    ```
    
7. 从远程仓库同步到本地仓库
    
    ```bash
    git pull --rebase origin main
    ```
    
8. 同步本地文件夹, 命令参考：[https://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html](https://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)
    
    ```bash
    # 将所有文件添加到暂存区
    git add . 
    
    # 提交暂存区文件到仓库区
    git commit -m "From Macmini - Time:$(date +%Y-%m-%d-%H-%M-%S)" 
    
    # 上传文件到远程仓库
    git push -u origin main
    ```
    
9. 创建`.sh`脚本
    
    ```bash
    cd /Users/zhangweishi/xxx
    cd PD\ Code
    git add .
    git commit -a -m "From Macmini - Time:$(date +%Y-%m-%d-%H-%M-%S)"
    git push origin main
    ```
    
10. 给脚本添加权限
    
    ```bash
    chmod 777 autoGit.sh
    ```
    
11. 创建定时运行脚本
    
    ```bash
    crontab -e
    ```
    
12. 编辑定时运行脚本，命令参考：[https://qqe2.com/cron#p_min](https://qqe2.com/cron#p_min)
    
    ```bash
    * * * * * /Users/zhangweishi/autoGit.sh > ~/log.txt 2>&1 &
    ```
    
13. 查看定时运行脚本
    
    ```bash
    crontab -l
    ```
    
14. 定时脚本命令
    
    ```bash
    #开启：
    sudo /usr/sbin/cron start
    #重启：
    sudo /usr/sbin/cron restart
    #停止：
    sudo /usr/sbin/cron stop
    #编写crontab：
    crontab -e
    #查看crontab：
    crontab -l
    ```
    
15. 打开权限
    
    ` Apple menu` → `System Preference` → `Security & Privacy` → `Privacy` → `Full Disk Access` → `锁头🔒` → click the `+` button → hit `⌘⇧G` → input `/usr/sbin` → double click the `cron` file
    

---

参考资料：

[本地文件自动同步到GitHub](https://cloud.tencent.com/developer/article/1575314)

[https://cloud.tencent.com/developer/article/1575314](https://cloud.tencent.com/developer/article/1575314)

[本地文件自动同步到GitHub](https://mp.weixin.qq.com/s?__biz=MzI4Njg5MDA5NA==&mid=2247486515&idx=1&sn=584fa08c4569c3fb5cad0ad9861af0a7&token=1963867963&lang=zh_CN#rd)

[](https://onns.xyz/blog/2020/06/10/fix-crontab-operation-not-permitted-on-mac/)

[Crontab Operation not permitted](https://apple.stackexchange.com/questions/378553/crontab-operation-not-permitted)