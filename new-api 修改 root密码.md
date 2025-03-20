# MySQL root密码修改指南

## 1. 进入Docker容器
```bash
docker exec -it mysql bash
```

## 2. 连接MySQL数据库
```bash
mysql -u root -p
```

## 3. 数据库操作
```sql
-- 查看所有数据库
SHOW DATABASES;

-- 切换到目标数据库
USE new-api;

-- 获取现有用户密码
SET @pwd = (SELECT password FROM users WHERE username = 'weishi');

-- 更新root密码
UPDATE users SET password = @pwd WHERE username = 'root';

-- 退出MySQL
EXIT;
```

## 4. 完成操作
```bash
# 退出Docker容器
exit
```

## 注意事项
1. 操作前请确认：
   - 当前Docker容器名称确实是"mysql"
   - 目标数据库名称正确（示例中使用new-api）
   - 源用户（示例中weishi）确实存在

2. SQL语句结尾必须带分号
3. 密码更新后建议重启相关服务