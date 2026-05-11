# Delta Deploy

Delta Deploy is a desktop deployment manager for syncing local project files to remote servers over SSH. It helps teams review file changes, deploy selectively, manage environment/config differences, and keep a local deployment history with backup and rollback support.

## Website

```text
https://sintakaridina.github.io/delta-deploy-site/
```

## Features

- SSH server connection management
- Project management per server
- Local vs remote file comparison before deployment
- Selective deployment for new, modified, and deleted files
- Dedicated env/config comparison flow
- Backup and rollback support
- Deployment history per project
- Collapsible server sidebar for a wider deployment workspace
- Local JSON storage, no external database required

## Download

Download the latest Windows release from:

```text
https://github.com/sintakaridina/delta-deploy-site/releases
```

Then:

1. Download the Windows ZIP package.
2. Extract the ZIP.
3. Run `DeltaDeploy.exe`.

## Basic Workflow

1. Add an SSH connection.
2. Connect to the server.
3. Add a project under the connected server.
4. Configure the local path, remote path, exclusions, and env-managed files.
5. Select the project to open the deployment workspace.
6. Refresh the comparison.
7. Review the detected changes.
8. Deploy selected files.
9. Use History for previous deployments and rollback.

## Run From Source

Install dependencies:

```bash
pip install -r requirements.txt
```

Start the desktop app:

```bash
python launcher.py
```

For development, the browser-based local server script is still available:

```bash
run.bat
```

Then open:

```text
http://localhost:8000
```

## Build for Windows

Install dependencies and build:

```bash
pip install -r requirements.txt
build.bat
```

Or run PyInstaller directly:

```bash
pyinstaller delta_deploy.spec
```

Build output:

```text
dist/DeltaDeploy.exe
```

If the executable is locked during rebuild, close the app or run:

```powershell
Stop-Process -Name DeltaDeploy -Force
```

## Create a Release ZIP

After building:

```powershell
Compress-Archive -Path dist\DeltaDeploy.exe, README.md, QUICKSTART.md -DestinationPath DeltaDeploy-windows.zip -Force
```

Upload the ZIP file to GitHub Releases.

## Project Structure

```text
automation-deploy/
├── backend/
│   ├── app.py
│   ├── config.py
│   ├── storage.py
│   ├── routes/
│   └── services/
├── frontend/
├── build.bat
├── delta_deploy.spec
├── launcher.py
├── requirements.txt
├── QUICKSTART.md
└── README.md
```

## Technology

- Backend: FastAPI, Uvicorn, Paramiko
- Desktop shell: pywebview
- Frontend: HTML, CSS, Vanilla JavaScript
- Storage: local JSON file at `~/.delta-deploy/data.json`
- Packaging: PyInstaller

## API Overview

### Auth / Servers

- `POST /api/auth/servers`
- `GET /api/auth/servers`
- `GET /api/auth/servers/{server_id}`
- `PUT /api/auth/servers/{server_id}`
- `DELETE /api/auth/servers/{server_id}`
- `POST /api/auth/test-connection/{server_id}`

### Projects

- `POST /api/projects/`
- `GET /api/projects/server/{server_id}`
- `GET /api/projects/by-id/{project_id}`
- `PUT /api/projects/{project_id}`
- `DELETE /api/projects/{project_id}`

### Deploy

- `POST /api/deploy/check`
- `POST /api/deploy/execute/start`
- `GET /api/deploy/execute/progress/{task_id}`
- `GET /api/deploy/history/{project_id}`
- `POST /api/deploy/rollback/{sync_log_id}`

## Security Notes

- SSH passwords are currently stored in local plaintext storage.
- For production usage, credential encryption or SSH key-based authentication is recommended.
