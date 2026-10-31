# Container Podman-常用指令

# 常用指令

```bash
# 查看當前所有的container
podman ps -a
```

```bash
# 暫停container
podman stop [container name]

# 移除container
podman rm [container name]
```

```bash
# 監控 container 當前執行狀態 (例如是否有被API呼叫並成功執行)
podman logs -f [container name]
```

# 啟動Container (.sh)

```bash
podman run -itd --rm --name \
-- privileged=true \
-v /home/[工號]/VScode-extensions/[工號]/.vscode-server:/root/.vscode-server \
-v /home/[工號]/workspace:/home[工號]/workspace \
-w /home/[工號]/workspace/[欲執行.py所在目錄資料夾] \ #移至某工作目錄，類似cd
-p 5002:5000 \ #通道：port
xx.xx.xx.xxx:xxxx/ibdi_py311:latest \ #image gitlab位置
python [腳本名稱].py
```

# VScode 啟動 server 上的 container 流程

step1. 連線到 server 的 使用者帳號

```powershell
# 若有事先建立 config
ssh [Host]
```

step2. 透過 image 啟動 container

```powershell
podman run -id --rm --name [工號] --privileged=true \
xx.xx.xxx:xxxx/ibdi_py311:latest

```

> ***image 來源為 gitlab***
> 

step3. VScode extensions 安裝 Dev Container 與 Remote Explorer

step4. 去 VScode setting 將 Dev Containe 的 Docker 修改為 podman

step5. VScode Remote(Tunnels/SSH) → 連線到step1.的 Host →開啟step2.已啟動的 container

step6. 至 Host ~/VScode_extensions 新增自己的工號資料夾

```powershell
mkdir -p ~/VScode_extensions/[工號]
```

step7. 在VScode container 的環境下安裝 Python 與 Jupyter extensions

step8. 把 container 的 .vscode-server 複製到 step6.新增的資料夾，完成 container 初始化

```powershell
podman cp [工號]:/root/.vscode-server ~/VScode_extensions/[工號]
```

step9. 刪除原本的 container

```powershell
podman stop [工號]
podman rm -f [工號]
```

step10. 新增/home/[工號]/workspace，並撰寫啟動Container腳本 (.sh)於此

```powershell
mkdir -p ~/VScode_extensions/[工號]

cd ~/VScode_extensions/[工號]

. [啟動Container腳本 ].sh
```