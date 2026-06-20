# Local Setup

## Prerequisites

The following must be available before setting up the project locally:

- GitHub account
- Git installed on your machine
- Terminal (Command Prompt, PowerShell, or any terminal emulator)
- VS Code
- Live Server extension installed in VS Code
- Web browser (Chrome recommended)
- Internet connection

## Step-by-step guide

**1. Open a terminal.**

**2. Navigate to your preferred directory:**

cd ~

**3. Clone the repository:**
git clone https://github.com/Douglasebhoman/douglasebhoman.github.io.git

**4. Move into the project folder:**
cd douglasebhoman.github.io

**5. Open the project in VS Code:**
code .

> **Note:** This requires VS Code to be added to PATH during installation.
> If it does not work, open VS Code manually and use File, then Open Folder.

**6. In the VS Code file explorer, click `index.html` to open it.**

**7. Right-click `index.html` and select Open with Live Server.**

**8. Your default browser will open the site at `http://127.0.0.1:5500`**

## Previewing other pages locally

Live Server serves the entire repository, not just `index.html`. Any page
can be previewed by navigating to its path in the browser after Live Server
is running:

| Page | Local URL |
| --- | --- |
| Homepage | `http://127.0.0.1:5500` |
| Work | `http://127.0.0.1:5500/work/` |
| Services | `http://127.0.0.1:5500/services/` |
| Audit | `http://127.0.0.1:5500/audit/` |
| Blog index | `http://127.0.0.1:5500/blog/` |
| Blog post | `http://127.0.0.1:5500/blog/posts/post-slug/` |
| 404 | `http://127.0.0.1:5500/404.html` |

## Notes

- Changes saved in VS Code update the browser preview automatically while
  Live Server is running
- The MailerLite newsletter form and Giscus comments require an internet
  connection to load
- The documentation audit widget runs entirely client-side and works
  without an internet connection