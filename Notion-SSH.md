# SSH

# 1. 建立公私鑰

開啟powersell

```powershell
# 在本機建立公私鑰
ssh-keygen
```

C:\User\[使用者名稱]\.ssh 會新增鑰匙

# 2. server 建立使用者

```powershell
# 連線到 server
ssh [server帳號]@[server IP 位置]

# 切換 root 權限，輸入密碼
su

# 新增使用者
useradd [使用者名稱]

# 設定使用者的密碼
passwd [使用者密碼]

# 登出 server
Ctrl+D
```

# 3. 交換公私鑰

```powershell
ssh [使用者名稱]@[server IP 位置]

### 查看是否有 .ssh
ls -al
```

若無.ssh

```powershell
# 建立公私鑰
ssh-keygen

# 編輯文本(使用vim編輯器)將本機公鑰(步驟1.)輸入
vim authorized_keys

# 更改權限
chmod 744 authorized_keys
```

若有.ssh

```powershell
# 編輯文本(使用vim編輯器)將本機公鑰(步驟1.)輸入
vim authorized_keys
```

# 4. 建立連線 config

於本機.ssh資料夾建立config檔案

```powershell
Host [任意命名]
  HostName [server IP 位置]
  port 22
  User [使用者名稱]
  IdentityFile ~/.ssh/[本機公鑰.pub結尾之檔案名稱]
```

> **之後可以直接 ssh [任意命名] 而不需輸入 server 密碼**
> 

# 5. vim編輯器操作說明

1. 輸入模式 Insert Mode
2. 命令模式 Command Mode
3. 命令行模式 Command Line Mode

常用命令指令

- i     → 切換到輸入模式
- x    → 刪除當前光標所在處的字符
- :     → 切換到底線命令模式，已在最底一行輸入命令
- dd → 剪切當前行
- yy  → 複製當前行
- u    → 撤銷上一次操作
- Crtl+R  → 重作上一次撤銷的操作

常用底線命令指令

- :w   → 保存文件
- :q    → 退出 vim 編輯器
- :wq → 組合技
- :q! → 強制退出 vim 編輯器

> **vim [filename] 進入編輯器(命令模式)**
> 

> **輸入 i a o 進入輸入模式
Esc鍵 回到命令模式**
> 

> **輸入:進入底線命令模式
Enter鍵結束運行
輸入:wq退出編輯器**
>