# Ubuntu挂载webdav

### **使用`davfs2`挂载WebDAV**

1. **安装davfs2**
    
    首先，安装**`davfs2`**工具：
    
    ```bash
    sudo apt update
    sudo apt install davfs2
    ```
    
2. **创建挂载点**
    
    创建一个目录作为WebDAV的挂载点：
    
    ```bash
    sudo mkdir /mnt/webdav
    ```
    
3. **挂载WebDAV**
    
    使用**`mount`**命令来挂载WebDAV：
    
    ```bash
    sudo mount -t davfs https://example.com/webdav /mnt/webdav
    ```
    
    如果需要输入用户名和密码，可以在命令行中指定：
    
    ```bash
    sudo mount -t davfs https://example.com/webdav /mnt/webdav -o username=your_username,password=your_password
    ```
    
4. **自动挂载**
    
    如果你希望在系统启动时自动挂载WebDAV，可以编辑**`/etc/fstab`**文件：
    
    ```bash
    sudo nano /etc/fstab
    ```
    
    添加以下行，不指定具体的用户名和用户组：
    
    ```
    # https://example.com/webdav /mnt/webdav davfs user,rw,uid=your_username,gid=your_group 0 0
    
    https://example.com/webdav /mnt/webdav davfs _netdev,auto,user 0 0
    ```
    
    请将**`your_username`**和**`your_group`**替换为实际的用户名和用户组。
    
5. **配置凭据文件**
    
    为了避免每次挂载时输入用户名和密码，可以在**`/etc/davfs2/secrets`**文件中保存凭据：
    
    ```bash
    sudo nano /etc/davfs2/secrets
    ```
    
    添加以下内容：
    
    ```
    https://example.com/webdav your_username your_password
    ```
    
    确保该文件的权限设置为仅限root用户访问：
    
    ```bash
    sudo chmod 600 /etc/davfs2/secrets
    ```
    
6. **检查配置**
    1. **手动挂载测试**
        
        在配置完成后，可以手动测试挂载是否成功：
        
        ```bash
        sudo systemctl daemon-reload
        sudo mount /mnt/webdav
        ```
        
        检查挂载点是否可访问：
        
        ```bash
        ls /mnt/webdav
        ```
        
    2. **重启系统**
        
        重启系统以确保WebDAV在开机时自动挂载：
        
        ```bash
        sudo reboot
        ```
        
        重启后，检查挂载点：
        
        ```bash
        ls /mnt/webdav
        ```
