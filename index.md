---
---

@import "minima/skins/dark", "minima/initialize";

/* Page title */
.page-title {
  color: #79c0ff;
  border-bottom: 2px solid #79c0ff;
  padding-bottom: 0.5rem;
}

/* Make inline code pop */
code {
  background-color: #1c2128;
  color: #7ee787;
  padding: 0.2em 0.45em;
  border-radius: 4px;
  font-size: 0.88em;
  font-weight: 500;
  border: 1px solid #30363d;
}

/* Code blocks */
pre {
  background-color: #0d1117 !important;
  border: 1px solid #30363d;
  border-radius: 8px;
  padding: 1.2em;
  overflow-x: auto;
}

pre code {
  background-color: transparent;
  border: none;
  padding: 0;
  color: #c9d1d9;
  font-size: 0.9em;
}

/* Tables */
table {
  width: 100%;
  border-collapse: collapse;
  margin: 1.5em 0;
}

th {
  background-color: #161b22;
  color: #79c0ff;
  text-align: left;
  padding: 0.75em 1em;
  border-bottom: 2px solid #30363d;
  font-weight: 600;
}

td {
  padding: 0.65em 1em;
  border-bottom: 1px solid #21262d;
}

tr:hover {
  background-color: #161b22;
}

/* Table inline code — brighter */
td code {
  color: #7ee787;
  background-color: #0d1117;
  font-weight: 600;
}

/* Section headers */
h2 {
  color: #d2a8ff;
  margin-top: 2.5em;
  padding-bottom: 0.3em;
  border-bottom: 1px solid #21262d;
}

h3 {
  color: #79c0ff;
  margin-top: 1.8em;
}

/* Strong/bold text — used for warnings */
strong {
  color: #ffa657;
}

/* Blockquotes for notes */
blockquote {
  border-left: 4px solid #ffa657;
  background-color: #161b22;
  padding: 0.8em 1.2em;
  margin: 1.5em 0;
  border-radius: 0 6px 6px 0;
}

/* Horizontal rules */
hr {
  border: none;
  border-top: 1px solid #30363d;
  margin: 3em 0;
}

/* Ordered and unordered lists */
li {
  margin-bottom: 0.4em;
}

/* Body adjustments */
body {
  font-size: 16px;
  line-height: 1.7;
}

/* Smooth scrolling */
html {
  scroll-behavior: smooth;
}
| `dir -Force` | Windows | Show hidden files |
| `Get-ChildItem -Recurse` | Windows | List files in all subdirectories |

```bash
$ ls -la
total 24
drwxr-xr-x  5 tyrell staff  160 May 25 10:30 .
drwxr-xr-x  8 tyrell staff  256 May 25 09:15 ..
-rw-r--r--  1 tyrell staff   45 May 25 10:30 .gitignore
-rw-r--r--  1 tyrell staff  890 May 25 10:28 main.py
drwxr-xr-x  3 tyrell staff   96 May 25 10:25 src
```

---

## File & Folder Creation

### Creating Folders

| Command | Platform | What It Does |
| --- | --- | --- |
| `mkdir foldername` | Both | Make Directory — creates a new folder |
| `mkdir -p path/to/nested/folder` | Mac | Creates the entire path, including parents that don't exist |
| `mkdir path/to/nested/folder -Force` | Windows | Same idea in PowerShell |
| `mkdir folder1 folder2 folder3` | Both | Create multiple folders at once |

```bash
$ mkdir -p my-app/src/components
$ mkdir -p my-app/tests
$ mkdir -p my-app/docs
```

### Creating Files

| Command | Platform | What It Does |
| --- | --- | --- |
| `touch filename` | Mac | Creates an empty file (or updates timestamp if it exists) |
| `touch file1.py file2.py file3.py` | Mac | Create multiple empty files at once |
| `New-Item filename` | Windows | Creates a new empty file |
| `ni filename` | Windows | Shorthand alias for New-Item |

```bash
$ touch index.html style.css app.js
```

---

## Writing & Reading Files

### Writing to Files

| Command | Platform | What It Does |
| --- | --- | --- |
| `echo "text" > file.txt` | Mac | Write text to a file — **overwrites everything** |
| `echo "text" >> file.txt` | Mac | Append text to the end — keeps existing content |
| `"text" > file.txt` | Windows | Overwrite |
| `"text" >> file.txt` | Windows | Append |
| `Set-Content file.txt "text"` | Windows | Another way to write (overwrites) |
| `Add-Content file.txt "text"` | Windows | Another way to append |

**The difference between `>` and `>>` matters:**

- `>` = OVERWRITE — existing content is gone permanently
- `>>` = APPEND — adds to the end, existing content is safe

There is no undo. If you use `>` when you meant `>>`, that data is gone.

```bash
$ echo "Hello World" > greeting.txt     # File contains: Hello World
$ echo "How are you?" >> greeting.txt   # File contains both lines
$ echo "Oops" > greeting.txt            # File now ONLY contains: Oops
```

### Reading Files

| Command | Platform | What It Does |
| --- | --- | --- |
| `cat file.txt` | Both | Dumps the entire file contents to your screen |
| `less file.txt` | Mac | Opens a scrollable viewer (press `q` to quit) |
| `more file.txt` | Both | Simpler scrollable viewer |
| `head file.txt` | Mac | Shows the first 10 lines |
| `head -n 20 file.txt` | Mac | Shows the first 20 lines |
| `tail file.txt` | Mac | Shows the last 10 lines |
| `tail -f file.txt` | Mac | Follows the file in real-time (useful for logs) |
| `Get-Content file.txt` | Windows | Full PowerShell cmdlet for reading files |
| `Get-Content file.txt -Head 10` | Windows | First 10 lines |
| `Get-Content file.txt -Tail 10` | Windows | Last 10 lines |
| `Get-Content file.txt -Wait` | Windows | Follow in real-time |

---

## Copying, Moving & Renaming

### Copying

| Command | Platform | What It Does |
| --- | --- | --- |
| `cp source.txt destination.txt` | Mac | Copy a file |
| `cp -r sourcefolder/ destfolder/` | Mac | Copy a folder and everything inside it |
| `Copy-Item source.txt destination.txt` | Windows | Copy a file |
| `Copy-Item sourcefolder/ destfolder/ -Recurse` | Windows | Copy a folder recursively |

### Moving & Renaming

| Command | Platform | What It Does |
| --- | --- | --- |
| `mv oldname.txt newname.txt` | Mac | Move or rename — same directory = rename |
| `mv file.txt ../` | Mac | Move file up one directory |
| `mv file.txt ~/Desktop/` | Mac | Move file to Desktop |
| `Move-Item oldname.txt newname.txt` | Windows | Move or rename |
| `Rename-Item oldname.txt newname.txt` | Windows | Explicitly rename without moving |
| `mv *.py scripts/` | Mac | Move all Python files into the scripts folder |

On Mac, `mv` handles both moving and renaming. If the destination is a directory, it moves. If it's a filename, it renames.

---

## Deletion

Terminal deletion is permanent. There is no trash can.

### Deleting Files

| Command | Platform | What It Does |
| --- | --- | --- |
| `rm file.txt` | Mac | Delete a file permanently |
| `rm file1.txt file2.txt` | Mac | Delete multiple files |
| `rm *.log` | Mac | Delete all .log files in current directory |
| `rm -i file.txt` | Mac | Interactive — asks for confirmation before deleting |
| `Remove-Item file.txt` | Windows | Delete a file |
| `Remove-Item file.txt -Confirm` | Windows | Asks for confirmation |

### Deleting Folders

| Command | Platform | What It Does |
| --- | --- | --- |
| `rmdir foldername` | Both | Remove an empty directory only |
| `rm -r foldername` | Mac | Recursive delete — folder and everything inside |
| `rm -ri foldername` | Mac | Recursive + interactive (asks before each file) |
| `Remove-Item foldername -Recurse` | Windows | Recursive delete |

### Dangerous Commands

| Command | Platform | What It Does |
| --- | --- | --- |
| `rm -rf foldername` | Mac | Force-deletes everything recursively. No confirmation. |
| `rm -rf /` | Mac | Deletes your entire filesystem. Never run this. |
| `rm -rf *` | Mac | Deletes everything in the current directory |
| `Remove-Item / -Recurse -Force` | Windows | PowerShell equivalent of rm -rf / |

**Rules for deletion:**

1. There is no trash can. Terminal deletion bypasses Recycle Bin / Trash.
2. Always `ls` first. Look at what you're about to delete.
3. Never use `-f` (force) unless you know exactly what you're targeting.
4. Never copy-paste `rm` commands from the internet without reading them.
5. Use `-i` (interactive) when you're unsure.
6. When in doubt, move it instead of deleting: `mv file.txt ~/trash-staging/`

---

## Searching & Finding

| Command | Platform | What It Does |
| --- | --- | --- |
| `find . -name "*.py"` | Mac | Find all Python files in current directory and subdirectories |
| `find . -name "*.py" -type f` | Mac | Find only files (not directories) |
| `find . -size +10M` | Mac | Find files larger than 10MB |
| `find . -mtime -7` | Mac | Find files modified in the last 7 days |
| `grep "search term" file.txt` | Mac | Search for text inside a file |
| `grep -r "search term" .` | Mac | Search for text in all files recursively |
| `grep -rn "search term" .` | Mac | Same but with line numbers |
| `grep -ri "search term" .` | Mac | Case-insensitive recursive search |
| `Get-ChildItem -Recurse -Filter *.py` | Windows | Find all Python files recursively |
| `Select-String "search term" file.txt` | Windows | Search for text in a file |
| `which command` | Mac | Find where a program is installed |
| `where command` | Windows | Find where a program is installed |

---

## Process & System Commands

| Command | Platform | What It Does |
| --- | --- | --- |
| `clear` | Mac | Clear the terminal screen |
| `cls` | Windows | Clear the terminal screen |
| `history` | Mac | Show your command history |
| `Get-History` | Windows | Show your command history |
| `!!` | Mac | Re-run the last command |
| `Ctrl + C` | Both | Stop/kill the currently running command |
| `Ctrl + D` | Mac | Exit the terminal session |
| `exit` | Both | Exit the terminal session |
| `top` | Mac | Show running processes (q to quit) |
| `Get-Process` | Windows | Show running processes |
| `kill PID` | Mac | Kill a process by its Process ID |
| `Stop-Process -Id PID` | Windows | Kill a process by its Process ID |
| `sudo command` | Mac | Run a command as administrator (asks for password) |

About `sudo`: this gives you root access. Use it only when you actually need elevated permissions. If a tutorial tells you to sudo something and you don't understand why, pause and look into it first.

---

## Piping & Redirection

This is where the terminal gets powerful. You can chain commands together.

| Command | Platform | What It Does |
| --- | --- | --- |
| `command1 \| command2` | Both | Pipe — send the output of command1 into command2 |
| `command > file.txt` | Both | Redirect output to a file (overwrites) |
| `command >> file.txt` | Both | Redirect output to a file (appends) |
| `command 2> errors.txt` | Mac | Redirect error messages to a file |
| `command &> all.txt` | Mac | Redirect both output and errors to a file |
| `command1 && command2` | Both | Run command2 only if command1 succeeds |
| `command1 \|\| command2` | Both | Run command2 only if command1 fails |
| `command1 ; command2` | Mac | Run both commands regardless of success/failure |

```bash
$ ls -la | grep ".py"              # List files, filter for Python files
$ cat file.txt | wc -l              # Count lines in a file
$ history | grep "git"              # Find git commands in your history
```

---

## Virtual Environments (Python)

Virtual environments are isolated Python installations. Each project gets its own set of packages so they don't conflict.

### Why you need them

Your system Python is shared across everything. Installing packages globally can break other projects. Different projects may need different versions of the same package. Virtual environments keep each project's dependencies isolated.

### Mac / Linux

| Step | Command |
| --- | --- |
| Create | `python3 -m venv myenv` |
| Activate | `source myenv/bin/activate` |
| Verify | `which python` (should show a path inside myenv/) |
| Install packages | `pip install numpy pandas` |
| Save dependencies | `pip freeze > requirements.txt` |
| Install from file | `pip install -r requirements.txt` |
| Deactivate | `deactivate` |
| Delete venv | `rm -rf myenv/` |

### Windows (PowerShell)

| Step | Command |
| --- | --- |
| Create | `python -m venv myenv` |
| Activate | `.\myenv\Scripts\Activate` |
| Verify | `Get-Command python` (should show path inside myenv/) |
| Install packages | `pip install numpy pandas` |
| Save dependencies | `pip freeze > requirements.txt` |
| Install from file | `pip install -r requirements.txt` |
| Deactivate | `deactivate` |
| Delete venv | `Remove-Item myenv -Recurse` |

**Windows note:** if you get an error about script execution when activating, run this once:

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

### Best practices

- One venv per project. Always.
- Create it inside your project folder.
- Add the venv folder to `.gitignore`.
- Use `requirements.txt` so others can recreate the environment.
- If something breaks, delete the venv and recreate it. They're disposable.
- Check your prompt — `(myenv)` at the beginning means you're in the venv. No prefix = system Python.

---

## Package Management

| Command | Platform | What It Does |
| --- | --- | --- |
| `pip install package` | Both | Install a Python package |
| `pip install package==1.2.3` | Both | Install a specific version |
| `pip uninstall package` | Both | Uninstall a package |
| `pip list` | Both | Show all installed packages |
| `pip freeze` | Both | Show installed packages in requirements format |
| `pip freeze > requirements.txt` | Both | Save dependencies to a file |
| `pip install -r requirements.txt` | Both | Install all packages from a requirements file |
| `python --version` | Both | Check Python version |
| `which python` | Mac | Show path to current Python |
| `Get-Command python` | Windows | Show which Python executable is being used |

---

## Common Workflows

### Starting a New Python Project

```bash
mkdir my-project
cd my-project
python3 -m venv venv
source venv/bin/activate   # Mac
.\venv\Scripts\Activate    # Windows
pip install numpy pandas
pip freeze > requirements.txt
touch main.py              # Mac
New-Item main.py           # Windows
```

### Cloning and Setting Up Someone Else's Project

```bash
git clone https://github.com/user/project.git
cd project
python3 -m venv venv
source venv/bin/activate   # Mac
.\venv\Scripts\Activate    # Windows
pip install -r requirements.txt
python main.py
```

### Quick File Exploration

```bash
pwd                    # Where am I?
ls -la                 # What's here?
cd src                 # Go into src
ls                     # What's in src?
cat config.py          # Quick look at a file
cd ..                  # Back up
```

### Finding Something in Your Code

```bash
grep -rn "def my_function" .           # Mac: find a function definition
Get-ChildItem -Recurse | Select-String "def my_function"  # Windows
find . -name "*.py" -exec grep -l "import pandas" {} \;   # Find which files import pandas
```

---

## Common Pitfalls

**"Command not found" / "not recognized"**
The tool isn't installed, or it's not in your PATH. For Python on Mac, try `python3` instead of `python`.

**"Permission denied"**
You don't have permission to access that file or run that command. Mac: prefix with `sudo`. Windows: run PowerShell as Administrator.

**"No such file or directory"**
Typo in the path, wrong directory, or case sensitivity issue. Run `pwd` and `ls` to confirm where you are and what's available.

**Files created in the wrong place**
You were in a different directory than you thought. Always `pwd` before creating or modifying files.

**Hidden files not showing up**
Files starting with `.` are hidden by default. Mac: `ls -a`. Windows: `dir -Force`.

**Spaces in file/folder names causing issues**
The terminal interprets spaces as argument separators. Wrap the name in quotes: `cd "My Documents"` or escape with backslash: `cd My\ Documents`

**Accidentally overwrote a file with >**
You used `>` (overwrite) instead of `>>` (append). There's no undo. The data is gone.

**"pip: command not found" inside a virtual environment**
The venv might not be activated. Check if you see `(venv)` in your prompt. If not, activate the environment first.

---

## Keyboard Shortcuts

| Shortcut | What It Does |
| --- | --- |
| `Tab` | Auto-complete file/folder names |
| `Tab Tab` | Show all possible completions |
| `↑ / ↓` | Cycle through command history |
| `Ctrl + C` | Kill the current running command |
| `Ctrl + D` | Exit the terminal |
| `Ctrl + L` | Clear the screen |
| `Ctrl + A` | Jump to beginning of line |
| `Ctrl + E` | Jump to end of line |
| `Ctrl + W` | Delete the word before cursor |
| `Ctrl + U` | Delete everything before cursor |
| `Ctrl + R` | Search through command history (Mac) |

---

## Quick Reference

| Action | Mac Terminal | Windows PowerShell |
| --- | --- | --- |
| Where am I? | `pwd` | `pwd` / `Get-Location` |
| List files | `ls` / `ls -la` | `dir` / `Get-ChildItem` |
| Change directory | `cd folder` | `cd folder` |
| Go back one level | `cd ..` | `cd ..` |
| Go home | `cd ~` | `cd ~` |
| Make folder | `mkdir name` | `mkdir name` |
| Make file | `touch file` | `New-Item file` |
| Write to file | `echo "text" > file` | `"text" > file` |
| Append to file | `echo "text" >> file` | `"text" >> file` |
| Read file | `cat file` | `Get-Content file` |
| Copy file | `cp src dest` | `Copy-Item src dest` |
| Move/Rename | `mv old new` | `Move-Item old new` |
| Delete file | `rm file` | `Remove-Item file` |
| Delete folder | `rm -r folder` | `Remove-Item folder -Recurse` |
| Find files | `find . -name "*.py"` | `Get-ChildItem -Recurse -Filter *.py` |
| Search in files | `grep "text" file` | `Select-String "text" file` |
| Clear screen | `clear` | `cls` |
| Kill process | `Ctrl + C` | `Ctrl + C` |
| Create venv | `python3 -m venv env` | `python -m venv env` |
| Activate venv | `source env/bin/activate` | `.\env\Scripts\Activate` |
| Deactivate venv | `deactivate` | `deactivate` |

---

*Code in Place — Terminal Teaching Session. Tyrell Baker.*
