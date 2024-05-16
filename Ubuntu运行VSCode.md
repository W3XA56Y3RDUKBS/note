# Ubuntu运行VSCode

### **1. 下载 OpenVSCode Server**

打开终端并运行以下命令，下载 OpenVSCode Server：

```bash
wget https://github.com/gitpod-io/openvscode-server/releases/download/openvscode-server-v1.89.1/openvscode-server-v1.89.1-linux-x64.tar.gz
```

### **2. 解压文件**

下载完成后，使用以下命令解压文件：

```bash
tar -xzf openvscode-server-v1.89.1-linux-x64.tar.gz
```

### **3. 重命名文件夹**

使用 **`mv`** 命令将文件夹重命名。将 **`openvscode-server-v1.89.1-linux-x64`** 文件夹改名为 **`1.89.1`**：

```bash
mv /home/warp/vscode/openvscode-server-v1.89.1-linux-x64 /home/warp/vscode/1.89.1
```

### **4. 创建 systemd 服务**

要让 OpenVSCode Server 作为系统服务运行，请按照以下步骤操作：

### **4.1 创建新的服务文件**

使用以下命令创建一个新的服务文件：

```bash
sudo nano /etc/systemd/system/openvscode.service
```

### **4.2 添加服务配置**

将以下内容粘贴到打开的文件中：

```makefile
[Unit]
Description=OpenVSCode Server
After=network.target

[Service]
ExecStart=/home/warp/vscode/1.89.1/bin/openvscode-server --host 0.0.0.0 --connection-token <你的密码>
Restart=always
User=<你的用户名>

[Install]
WantedBy=multi-user.target
```

> 注意： 将 /home/warp/vscode/1.89.1/bin/openvscode-server 替换为你实际的二进制文件路径，将 <你的密码> 替换为你设置的密码，并将 <你的用户名> 替换为你用于运行服务的用户名。
> 

### **4.3 保存并关闭文件**

按 **`Ctrl + O`** 保存文件，按 **`Enter`** 确认，然后按 **`Ctrl + X`** 关闭文件。

### **4.4 重新加载 systemd 配置**

运行以下命令重新加载 systemd 配置：

```bash
sudo systemctl daemon-reload
```

### **4.5 启动服务**

启动 OpenVSCode 服务：

```bash
sudo systemctl start openvscode
```

### **4.6 检查服务状态**

检查服务是否正常运行：

```bash
sudo systemctl status openvscode
```

### **4.7 启用开机自启动**

如果一切正常，启用服务以便在系统启动时自动启动：

```bash
sudo systemctl enable openvscode
```

### **5. 管理服务**

### **停止服务**

如果你想停止服务，运行以下命令：

```bash
sudo systemctl stop openvscode
```

### **重启服务**

如果你想重启服务，运行以下命令：

```bash
sudo systemctl restart openvscode
```

### **禁用开机自启动**

如果你想禁用服务，使其不在系统启动时自动启动，运行以下命令：

```bash
sudo systemctl disable openvscode
```

现在，你已经成功配置了 OpenVSCode Server 作为 systemd 服务，即使你退出 SSH 会话，服务也会继续运行。