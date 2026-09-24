# Komari

![komari](https://socialify.git.ci/kadidalax/komari-classic/image?description=1&font=Inter&forks=1&issues=1&language=1&logo=https%3A%2F%2Fraw.githubusercontent.com%2Fkomari-monitor%2Fkomari-web%2Fd54ce1288df41ead08aa19f8700186e68028a889%2Fpublic%2Ffavicon.png&name=1&owner=1&pattern=Plus&pulls=1&stargazers=1&theme=Auto)

[简体中文](./docs/README_zh.md) | [繁體中文](./docs/README_zh-TW.md) | [日本語](./docs/README_ja.md)

Komari is a lightweight, self-hosted server monitoring tool designed to provide a simple and efficient solution for monitoring server performance. It supports viewing server status through a web interface and collects data through a lightweight agent.

> [!WARNING]
> Komari is a self-hosted monitoring and control program intended only for systems you own or are authorized to administer. Do not weaponize Komari, deploy it without consent, or use it for unauthorized access, persistence, command execution, or other abusive activity. For context on real-world abuse risks, see Huntress' analysis: [Komari C2 agent abuse](https://www.huntress.com/blog/komari-c2-agent-abuse).
> Users are solely responsible for how they deploy and operate Komari. The developers do not accept responsibility for unauthorized or abusive use, or for any resulting consequences.
> On Windows, when remote control is enabled, the client displays a Windows notification at each user login to remind the user that Komari is remote control software.

[Documentation](https://komari-document.pages.dev/) | [文档(镜像站 By Geekertao)](https://www.komari.wiki)

## Features

- **Lightweight and Efficient**: Low resource consumption, suitable for servers of all sizes.
- **Self-hosted**: Complete control over data privacy, easy to deploy.
- **Web Interface**: Intuitive monitoring dashboard, easy to use.

## Quick Start

### 1. Use the One-click Install Script

Suitable for distributions using systemd (Ubuntu, Debian...).

```bash
curl -fsSL https://raw.githubusercontent.com/kadidalax/komari-classic/main/install-komari.sh -o install-komari.sh
chmod +x install-komari.sh
sudo ./install-komari.sh
```

### 2. Docker Deployment

1. Create a data directory:
   ```bash
   mkdir -p ./data
   ```
2. Run the Docker container:
   ```bash
   docker run -d \
     -p 25774:25774 \
     -v $(pwd)/data:/app/data \
     --name komari \
     ghcr.io/kadidalax/komari-classic:latest
   ```
3. View the default username and password:
   ```bash
   docker logs komari
   ```
4. Access `http://<your_server_ip>:25774` in your browser.

> [!NOTE]
> You can also customize the initial username and password through the environment variables `ADMIN_USERNAME` and `ADMIN_PASSWORD`.

### 3. Binary File Deployment

1. Visit Komari's [GitHub Release page](https://github.com/kadidalax/komari-classic/releases) to download the latest binary for your operating system.
2. Run Komari:
   ```bash
   ./komari server -l 0.0.0.0:25774
   ```
3. Access `http://<your_server_ip>:25774` in your browser. The default port is `25774`.
4. The default username and password can be found in the startup logs or set via the environment variables `ADMIN_USERNAME` and `ADMIN_PASSWORD`.

> [!NOTE]
> Ensure the binary has execute permissions (`chmod +x komari`). Data will be saved in the `data` folder in the running directory.

### Manual Build

#### Dependencies

- Go 1.18+ and Node.js 20+ (for manual build)

1. Build the frontend static files:
   ```bash
   git clone https://github.com/kadidalax/komari-web-1.2.5-fix2
   cd komari-web
   npm install
   npm run build
   ```
2. Build the backend:
   ```bash
   git clone https://github.com/kadidalax/komari-classic
   cd komari
   ```
   Copy the static files generated in step 1 to the `/web/public/defaultTheme/dist` folder in the root of the `komari` project, and copy `komari-theme.json` + `preview.png`/`perview.png` to `/web/public/defaultTheme`.
   ```bash
   go build -o komari
   ```
3. Run:
   ```bash
   ./komari server -l 0.0.0.0:25774
   ```
   The default listening port is `25774`. Access `http://localhost:25774`.

## Frontend Development Guide

[Komari Theme Development Guide | Komari](https://komari-document.pages.dev/dev/theme.html)

## Client Agent Development Guide

[Komari Agent Information Reporting and Event Handling Documentation](https://komari-document.pages.dev/dev/agent.html)

## Contributing

Issues and Pull Requests are welcome!

## Acknowledgements

### The open source software community

All the developers who submitted PRs and created themes

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=kadidalax/komari-classic&type=Date)](https://www.star-history.com/#kadidalax/komari-classic&Date)
