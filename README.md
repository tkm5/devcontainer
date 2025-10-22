# Devcontainer Practice

This is a template repository for developing web applications using Python (FastAPI) and Node.js within a Devcontainer.

## Features

- **Reproducible Development Environment**: Builds a consistent development environment using Devcontainer.
- **Backend**: Python 3.13 with [FastAPI](https://fastapi.tiangolo.com/).
- **Frontend**: Node.js 22 environment.
- **Pre-installed Tools**: Comes with useful tools like Zsh, Git, and Gemini-CLI.

## Getting Started

### Prerequisites

- [Visual Studio Code](https://code.visualstudio.com/)
- [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Usage

1.  Clone this repository to your local machine.
2.  Open the cloned repository folder with Visual Studio Code.
3.  When prompted, click on "**Reopen in Container**" to build and start the dev container.
4.  Placeholder files have already been created to allow Git to track the `backend/src` and `frontend` directories.

## Directory Structure

```
.
├── .devcontainer/   # Devcontainer configuration files
├── backend/         # Backend application (FastAPI)
│   └── src/
└── frontend/        # Frontend application (Node.js)
```

> **Note**
> The `backend/src` and `frontend` directories are empty by default. You will need to create your FastAPI and Node.js applications within these respective directories to get started.

## Managing `.gitkeep`

The `.gitkeep` files are placeholders. Their only purpose is to make sure Git tracks the `backend/src` and `frontend` directories while they are empty.

Once you add any other file to a directory (e.g., `main.py` or `index.js`), the `.gitkeep` file is no longer needed and can be safely deleted.
