Development container (dev container)讓使用者可以用容器當成是完整的開發環境。Development container定義了一個開發環境，讓開發者在交付前開發。然而交付和開發用的容器可能很相似，但在交付用的image中不會想包裝開發用的工具進去。</br>
[<img alt="dev container V.S. production container" src="https://containers.dev/img/dev-container-stages.png" />](https://containers.dev/img/dev-container-stages.png)

# Developing inside a Container
[<img alt="devcontainers architecture" width="720px" src="https://code.visualstudio.com/assets/docs/devcontainers/containers/architecture-containers.png" />](https://code.visualstudio.com/assets/docs/devcontainers/containers/architecture-containers.png)

Visual Studio Code Dev Containers extension讓你用Docker當成全功能的完整開發環境。其做法是將開發用的目錄掛載到docker container中，container中則包含了整個的VSCode開發環境。在你的專案中會有一支devcontainer.json檔，裡面描述development container的產生方式，執行程式，以及開發工具的安裝等等。

## 系統需求
- Docker daemon,以及其它的Docker相容CLI (docker, Docker Desktop for Windows, kubernetes, podman ...etc)
- 安裝VS Code `Dev Containers` extension (用VS Code當成開發工具)
[<img alt="Dev Containers extension on VS Code Market" src="https://code.visualstudio.com/assets/docs/devcontainers/tutorial/dev-containers-extension.png" />](https://code.visualstudio.com/assets/docs/devcontainers/tutorial/dev-containers-extension.png)
- Dev Containers執行後，在最下方Status bar的最左側會出現Remote Status bar item<br/>
[<img alt="remote-status-bar" src="https://code.visualstudio.com/assets/docs/devcontainers/tutorial/remote-status-bar.png" />](https://code.visualstudio.com/assets/docs/devcontainers/tutorial/remote-status-bar.png)
- 按下Remote Statue bar icon，會在Command Palette中顯示出可用的Dev Containers命令
[<img src="https://code.visualstudio.com/assets/docs/devcontainers/tutorial/dev-containers-commands-simple.png" alt="Dev Containers commands on Command Palette" />](https://code.visualstudio.com/assets/docs/devcontainers/tutorial/dev-containers-commands-simple.png)

## Dev Containers extension如何運作
Dev Containers extension使用在.devcontainer資料夾中的數個檔案，名稱為devcontainer.json，和一個選擇性的檔案，Dockerfile或docker-compose.yml，以產出dev containers。
首先，container的image檔會從devcontainer.json中提供的Dockfile或image名稱中產生。再來的話會依image產出container，然後用json檔中的設定啟動container。最後，VS Code的環境(含extensions)會依json檔中的設定安裝到container裡。
當之前的啟動程序結束後，你在local端VS Code會連結到新產生的dev container中正執行Visual Studio Code Server。
[<img src="https://code.visualstudio.com/assets/docs/remote/remote-overview/architecture.png" alt="Dev Container Architecture" />](https://code.visualstudio.com/assets/docs/remote/remote-overview/architecture.png)

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

- Always forwarding a port : 在devcontainer.json檔中，加入*forwardPorts* property，語法為`"fowardPorts":[3000:3001]`
- Temporarily forwarding a port : 從VSCode的Command Palette (F1)中，執行**Forward a Port** Command
- Publishing a port : Docker has the concept of "publishing" ports when the container is created.
  - Use the appPort property : devcontainer.json檔中，加入"appPort": \[ 3000, "8921:5000" \]
  - Use the Docker Compose ports mapping : docker-compose.yml檔中，加入</br>
    ports:</br>
    \- "3000" </br>
    \- "8921:5000" </br>

