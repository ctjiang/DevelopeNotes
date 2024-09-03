[<img alt="devcontainers architecture" width="720px" src="https://code.visualstudio.com/assets/docs/devcontainers/containers/architecture-containers.png" />](https://code.visualstudio.com/assets/docs/devcontainers/containers/architecture-containers.png)

Visual Studio Code Dev Containers extension讓你用Docker當成全功能的完整開發環境。其做法是將開發用的目錄掛載到docker container中，container中則包含了整個的VSCode開發環境。在你的專案中會有一支devcontainer.json檔，裡面描述development container的產生方式，執行程式，以及開發工具的安裝等等。

**幾種使用devcontainer的使用情境：**
- [Quick start: Try a development container](https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-try-a-development-container)
- [Quick start: Open an existing folder in a container](https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-an-existing-folder-in-a-container)
  - [Open a WSL 2 folder in a container on Windows](https://code.visualstudio.com/docs/devcontainers/containers#_open-a-wsl-2-folder-in-a-container-on-windows)
  - [Open a folder on a remote SSH host in a container](https://code.visualstudio.com/docs/devcontainers/containers#_open-a-folder-on-a-remote-ssh-host-in-a-container)
  - [Open a folder on a remote Tunnel host in a container](https://code.visualstudio.com/docs/devcontainers/containers#_open-a-folder-on-a-remote-tunnel-host-in-a-container)
  - [Open an existing workspace in a container](https://code.visualstudio.com/docs/devcontainers/containers#_open-an-existing-workspace-in-a-container)
- [Quick start: Open a Git repository or GitHub PR in an isolated container volume](https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-a-git-repository-or-github-pr-in-an-isolated-container-volume)

[**Create a devcontainer.json file**](https://code.visualstudio.com/docs/devcontainers/containers#_create-a-devcontainerjson-file)

**Forwarding or publishing a port**
- Always forwarding a port : 在devcontainer.json檔中，加入*forwardPorts* property，語法為```"fowardPorts":[3000:3001]```
- Temporarily forwarding a port : 從VSCode的Command Palette (F1)中，執行 **Forward a Port** Command
- Publishing a port : Docker has the concept of "publishing" ports when the container is created.
  - Use the appPort property : devcontainer.json檔中，加入"appPort": \[ 3000, "8921:5000" \]
  - Use the Docker Compose ports mapping : docker-compose.yml檔中，加入</br>
    ports: </br>
    \- "3000" </br>
    \- "8921:5000" </br>
    
