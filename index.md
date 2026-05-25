# Terminal & PowerShell Command Reference - Code in Place

> Your go-to reference for terminal commands. Covers both Mac Terminal (Bash/Zsh) and Windows PowerShell. Bookmark this page and come back to it whenever you forget a command.
> 

---

# 🧭 Navigation Commands

These are the commands you'll use the most. If you only memorize a handful of commands, make it these.

## Where Am I?

| Command | Platform | What It Does |
| --- | --- | --- |
| `pwd` | Mac | **Print Working Directory**  • shows the full path to where you currently are in the file system |
| `pwd` | Windows | Works the same way (PowerShell aliases it to `Get-Location`) |
| `Get-Location` | Windows | The "official" PowerShell version of pwd |

**When to use it:** Before doing literally anything. If you're about to create a file, delete something, or run a script, pwd first. You'd be surprised how often you're not where you think you are.

**Example:**

```
$ pwd
/Users/tyrell/projects/my-app
```

## Moving Around

| Command | Platform | What It Does |
| --- | --- | --- |
| `cd foldername` | Both | **Change Directory**  • move into a folder |
| `cd ..` | Both | Go back (up) one level |
| `cd ../..` | Both | Go back two levels |
| `cd ~` | Both | Jump straight to your home directory |
| `cd /` | Both | Jump to the root of your filesystem |
| `cd -` | Mac | Go back to the previous directory you were in (like an undo) |
| `cd $HOME` | Mac | Another way to go home |
| `Set-Location foldername` | Windows | The "official" PowerShell version of cd |

**When to use it:** Every single time you need to work in a different folder. You'll chain this with other commands constantly.

**Pro tip:** Use `cd` + Tab to auto-complete folder names. Start typing the first few letters and hit Tab. If there are multiple matches, hit Tab twice to see all options.

**Example:**

```
$ cd ~/projects/my-app
$ cd ..          # now in ~/projects
$ cd -           # back in ~/projects/my-app
```

## Listing Contents

| Command | Platform | What It Does |
| --- | --- | --- |
| `ls` | Mac | **List**  • shows files and folders in current directory |
| `ls -l` | Mac | Long format - shows permissions, size, dates |
| `ls -a` | Mac | Shows ALL files, including hidden ones (starting with .) |
| `ls -la` | Mac | Combo - long format + hidden files. The one you'll use most. |
| `ls -lh` | Mac | Long format with human-readable file sizes (KB, MB, GB) |
| `ls *.py` | Mac | List only Python files (or any pattern you want) |
| `dir` | Windows | **Directory listing**  • shows files and folders |
| `Get-ChildItem` | Windows | The "official" PowerShell version |
| `dir -Force` | Windows | Shows hidden files too |
| `ls -Force` | Windows | Same thing (PowerShell aliases ls to Get-ChildItem) |
| `Get-ChildItem -Recurse` | Windows | Lists files in all subdirectories too |

**When to use it:** Before creating files (to see what's already there), before deleting (to confirm you're targeting the right stuff), or just to orient yourself.

**Example:**

```
$ ls -la
total 24
drwxr-xr-x  5 tyrell staff  160 May 25 10:30 .
drwxr-xr-x  8 tyrell staff  256 May 25 09:15 ..
-rw-r--r--  1 tyrell staff   45 May 25 10:30 .gitignore
-rw-r--r--  1 tyrell staff  890 May 25 10:28 main.py
drwxr-xr-x  3 tyrell staff   96 May 25 10:25 src
```

---

# 📁 File & Folder Creation

Building your project structure from the terminal is fast once you get the hang of it.

## Creating Folders

| Command | Platform | What It Does |
| --- | --- | --- |
| `mkdir foldername` | Both | **Make Directory**  • creates a new folder |
| `mkdir -p path/to/nested/folder` | Mac | Creates the entire path, including parent folders that don't exist yet |
| `mkdir path/to/nested/folder -Force` | Windows | Same idea in PowerShell |
| `mkdir folder1 folder2 folder3` | Both | Creates multiple folders at once |
| `New-Item -ItemType Directory -Name foldername` | Windows | The verbose PowerShell way (mkdir is easier) |

**When to use it:** Setting up project structures, creating directories for organizing files, scaffolding a new project.

**Example:**

```
$ mkdir -p my-app/src/components
$ mkdir -p my-app/tests
$ mkdir -p my-app/docs
# Creates the full tree in three commands
```

## Creating Files

| Command | Platform | What It Does |
| --- | --- | --- |
| `touch filename` | Mac | Creates an empty file (or updates the timestamp if it already exists) |
| `touch file1.py file2.py file3.py` | Mac | Creates multiple empty files at once |
| `New-Item filename` | Windows | Creates a new empty file |
| `ni filename` | Windows | Shorthand alias for New-Item |
| `New-Item filename -ItemType File` | Windows | Explicitly creates a file (not a directory) |
| `> filename` | Mac | Creates an empty file (redirect nothing into it) |
| `$null > filename` | Windows | PowerShell equivalent of creating an empty file |

**When to use it:** Starting new scripts, creating config files, setting up project boilerplate.

**Example:**

```
$ touch index.html style.css app.js
# Creates all three files in one shot
```

---

# ✏️ Writing & Reading Files

You don't always need to open an editor to put text in a file or see what's in one.

## Writing to Files

| Command | Platform | What It Does |
| --- | --- | --- |
| `echo "text" > file.txt` | Mac | **Writes text to a file. OVERWRITES everything.** |
| `echo "text" >> file.txt` | Mac | **Appends text to the end of a file. Keeps existing content.** |
| `"text" \ | Out-File file.txt` | Windows |
| `"text" \ | Out-File file.txt -Append` | Windows |
| `"text" > file.txt` | Windows | Shorthand overwrite |
| `"text" >> file.txt` | Windows | Shorthand append |
| `cat > file.txt` | Mac | Opens interactive mode - type content, then Ctrl+D to save |
| `Set-Content file.txt "text"` | Windows | Another way to write (overwrites) |
| `Add-Content file.txt "text"` | Windows | Another way to append |

**⚠️ CRITICAL:** The difference between `>` and `>>` is everything.

- `>` = **OVERWRITE** (destructive - existing content is gone forever)
- `>>` = **APPEND** (safe - adds to the end)

If you accidentally use `>` when you meant `>>`, that data is gone. No undo. Double-check every time.

**Example:**

```
$ echo "Hello World" > greeting.txt     # File now contains: Hello World
$ echo "How are you?" >> greeting.txt   # File now contains: Hello World\nHow are you?
$ echo "Oops" > greeting.txt            # File now ONLY contains: Oops (everything else is gone)
```

## Reading Files

| Command | Platform | What It Does |
| --- | --- | --- |
| `cat file.txt` | Both | **Concatenate**  • dumps the entire file contents to your screen |
| `less file.txt` | Mac | Opens a scrollable viewer (press q to quit) |
| `more file.txt` | Both | Similar to less but simpler |
| `head file.txt` | Mac | Shows the first 10 lines |
| `head -n 20 file.txt` | Mac | Shows the first 20 lines |
| `tail file.txt` | Mac | Shows the last 10 lines |
| `tail -n 20 file.txt` | Mac | Shows the last 20 lines |
| `tail -f file.txt` | Mac | Follows the file in real-time (great for logs) |
| `Get-Content file.txt` | Windows | The "official" PowerShell command for reading files |
| `Get-Content file.txt -Head 10` | Windows | First 10 lines |
| `Get-Content file.txt -Tail 10` | Windows | Last 10 lines |
| `Get-Content file.txt -Wait` | Windows | Follow in real-time (like tail -f) |

**When to use it:** Quick checks on file contents, debugging, reading logs, verifying that your write commands worked.

---

# 📋 Copying, Moving & Renaming

## Copying

| Command | Platform | What It Does |
| --- | --- | --- |
| `cp source.txt destination.txt` | Mac | **Copy** a file |
| `cp -r sourcefolder/ destfolder/` | Mac | Copy a folder and everything inside it (recursive) |
| `Copy-Item source.txt destination.txt` | Windows | Copy a file |
| `Copy-Item sourcefolder/ destfolder/ -Recurse` | Windows | Copy a folder recursively |
| `cp source.txt .` | Mac | Copy a file to the current directory |

## Moving & Renaming

| Command | Platform | What It Does |
| --- | --- | --- |
| `mv oldname.txt newname.txt` | Mac | **Move/Rename**  • if same directory, it renames |
| `mv file.txt ../` | Mac | Moves file up one directory |
| `mv file.txt ~/Desktop/` | Mac | Moves file to Desktop |
| `Move-Item oldname.txt newname.txt` | Windows | Move or rename |
| `Rename-Item oldname.txt newname.txt` | Windows | Explicitly rename (doesn't move) |
| `mv *.py scripts/` | Mac | Move all Python files into the scripts folder |

**Pro tip:** `mv` doubles as both move AND rename on Mac. If the destination is a directory, it moves. If it's a filename, it renames.

---

# 🗑️ Deletion

This is the section where you need to pay the most attention. Terminal deletion is permanent.

## Deleting Files

| Command | Platform | What It Does |
| --- | --- | --- |
| `rm file.txt` | Mac | **Remove**  • deletes a file permanently |
| `rm file1.txt file2.txt` | Mac | Delete multiple files |
| `rm *.log` | Mac | Delete all .log files in current directory |
| `rm -i file.txt` | Mac | **Interactive**  • asks "are you sure?" before deleting |
| `Remove-Item file.txt` | Windows | Delete a file |
| `Remove-Item file.txt -Confirm` | Windows | Asks for confirmation first |
| `del file.txt` | Windows | Shorthand alias |

## Deleting Folders

| Command | Platform | What It Does |
| --- | --- | --- |
| `rmdir foldername` | Both | Removes an empty directory only |
| `rm -r foldername` | Mac | **Recursive delete**  • removes folder AND everything inside |
| `rm -ri foldername` | Mac | Recursive + interactive (asks before each file) |
| `Remove-Item foldername -Recurse` | Windows | Recursive delete |
| `Remove-Item foldername -Recurse -Confirm` | Windows | Recursive with confirmation |

## ☠️ The Dangerous Commands

| Command | Platform | Why It's Dangerous |
| --- | --- | --- |
| `rm -rf foldername` | Mac | Force-deletes everything recursively. No confirmation. No mercy. |
| `rm -rf /` | Mac | **DELETES YOUR ENTIRE FILESYSTEM.** Never. Ever. Run. This. |
| `rm -rf *` | Mac | Deletes everything in the current directory without asking |
| `rm -rf ~` | Mac | Deletes your entire home directory |
| `Remove-Item / -Recurse -Force` | Windows | The PowerShell equivalent of rm -rf / |

**⚠️ THE GOLDEN RULES OF DELETION:**

1. **There is no trash can.** Terminal deletion bypasses the Recycle Bin / Trash. It's gone.
2. **Always `ls` first.** Look at what you're about to delete before you delete it.
3. **Never use `-f` (force) unless you absolutely know what you're doing.**
4. **Never copy-paste `rm` commands from the internet** without reading them first.
5. **Use `-i` (interactive) when you're unsure.** It'll ask you file by file.
6. **When in doubt, move it instead of deleting.** `mv file.txt ~/trash-staging/`

---

# 🔍 Searching & Finding

| Command | Platform | What It Does |
| --- | --- | --- |
| `find . -name "*.py"` | Mac | Find all Python files in current directory and subdirectories |
| `find . -name "*.py" -type f` | Mac | Find only files (not directories) |
| `find . -size +10M` | Mac | Find files larger than 10MB |
| `find . -mtime -7` | Mac | Find files modified in the last 7 days |
| `grep "search term" file.txt` | Mac | Search for text inside a file |
| `grep -r "search term" .` | Mac | Search for text in all files in current directory (recursive) |
| `grep -rn "search term" .` | Mac | Same but shows line numbers |
| `grep -ri "search term" .` | Mac | Case-insensitive recursive search |
| `Get-ChildItem -Recurse -Filter *.py` | Windows | Find all Python files recursively |
| `Select-String "search term" file.txt` | Windows | Search for text in a file |
| `Get-ChildItem -Recurse \ | Select-String "term"` | Windows |
| `where command` | Windows | Find where a program is installed |
| `which command` | Mac | Find where a program is installed |

**When to use it:** Hunting down a specific file, searching for a function across your codebase, finding large files eating up disk space.

---

# ⚡ Process & System Commands

| Command | Platform | What It Does |
| --- | --- | --- |
| `clear` | Mac | Clears the terminal screen |
| `cls` | Windows | Clears the terminal screen |
| `Clear-Host` | Windows | The "official" PowerShell version |
| `history` | Mac | Shows your command history |
| `Get-History` | Windows | Shows your command history |
| `!!` | Mac | Re-runs the last command (useful with sudo) |
| `Ctrl + C` | Both | **Stops/kills the currently running command** |
| `Ctrl + D` | Mac | Exit the terminal session |
| `exit` | Both | Exit the terminal session |
| `top` | Mac | Shows running processes (press q to quit) |
| `htop` | Mac | Prettier version of top (may need to install) |
| `Get-Process` | Windows | Shows running processes |
| `kill PID` | Mac | Kill a process by its Process ID |
| `Stop-Process -Id PID` | Windows | Kill a process by its Process ID |
| `sudo command` | Mac | Run a command as administrator (will ask for password) |
| `Start-Process powershell -Verb runAs` | Windows | Opens a new admin PowerShell window |

**⚠️ About `sudo`:** This gives you root (administrator) access. It's like the master key to your computer. Use it only when you actually need elevated permissions. If a tutorial tells you to `sudo` something and you don't understand why, be cautious.

---

# 🔗 Piping & Redirection

This is where the terminal starts getting really powerful. You can chain commands together.

| Command | Platform | What It Does |
| --- | --- | --- |
| `command1 \ | command2` | Both |
| `command > file.txt` | Both | Redirect output to a file (overwrites) |
| `command >> file.txt` | Both | Redirect output to a file (appends) |
| `command 2> errors.txt` | Mac | Redirect error messages to a file |
| `command &> all.txt` | Mac | Redirect both output and errors to a file |
| `command 2>&1` | Mac | Merge error stream into output stream |
| `command1 && command2` | Both | Run command2 only if command1 succeeds |
| `command1 \ | \ | command2` |
| `command1 ; command2` | Mac | Run both commands regardless of success/failure |

**Example:**

```
$ ls -la | grep ".py"              # List files, then filter for Python files only
$ cat file.txt | wc -l              # Count the number of lines in a file
$ history | grep "git"              # Find all git commands you've run
$ echo "done" >> log.txt && echo "Logged!"  # Append to log, then confirm
```

---

# 🐍 Virtual Environments (Python)

Virtual environments are isolated Python installations. Each project gets its own set of packages so they don't conflict with each other.

## Why You Need Them

- Your system Python is shared across everything. Installing packages globally can break other projects.
- Different projects may need different versions of the same package.
- Virtual environments keep each project's dependencies contained in a bubble.
- You can delete a venv and start fresh without affecting anything else.

## Setting Up Virtual Environments

### Mac / Linux

| Step | Command | What Happens |
| --- | --- | --- |
| Create | `python3 -m venv myenv` | Creates a `myenv/` folder with an isolated Python |
| Activate | `source myenv/bin/activate` | Switches your shell to use this Python |
| Verify | `which python` | Should show a path inside myenv/ |
| Install packages | `pip install numpy pandas` | Installs only inside this environment |
| Save dependencies | `pip freeze > requirements.txt` | Creates a list of all installed packages |
| Install from file | `pip install -r requirements.txt` | Installs everything from the list |
| Deactivate | `deactivate` | Returns to your system Python |
| Delete venv | `rm -rf myenv/` | Removes the entire virtual environment |

### Windows (PowerShell)

| Step | Command | What Happens |
| --- | --- | --- |
| Create | `python -m venv myenv` | Creates a `myenv/` folder with an isolated Python |
| Activate | `.\myenv\Scripts\Activate` | Switches your shell to use this Python |
| Verify | `Get-Command python` | Should show a path inside myenv/ |
| Install packages | `pip install numpy pandas` | Installs only inside this environment |
| Save dependencies | `pip freeze > requirements.txt` | Creates a list of all installed packages |
| Install from file | `pip install -r requirements.txt` | Installs everything from the list |
| Deactivate | `deactivate` | Returns to your system Python |
| Delete venv | `Remove-Item myenv -Recurse` | Removes the entire virtual environment |

### Windows Gotcha

If you get an error about script execution when trying to activate, run this first:

```
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

This allows PowerShell to run local scripts. You only need to do this once.

## Virtual Environment Best Practices

- **One venv per project. Always.** Don't share environments between projects.
- **Create the venv inside your project folder** so everything stays organized.
- **Add `myenv/` to `.gitignore`** so you don't commit it to version control.
- **Use `requirements.txt`** so other people (or future you) can recreate the environment.
- **If something's broken, delete the venv and recreate it.** They're disposable by design.
- **Check your prompt.** If you see `(myenv)` at the beginning, you're in the venv. No prefix = system Python.

---

# 🛠️ Package & Environment Management

| Command | Platform | What It Does |
| --- | --- | --- |
| `pip install package` | Both | Install a Python package |
| `pip install package==1.2.3` | Both | Install a specific version |
| `pip uninstall package` | Both | Uninstall a package |
| `pip list` | Both | Show all installed packages |
| `pip freeze` | Both | Show installed packages in requirements format |
| `pip freeze > requirements.txt` | Both | Save dependencies to a file |
| `pip install -r requirements.txt` | Both | Install all packages from a requirements file |
| `python --version` | Both | Check which Python version you're running |
| `python3 --version` | Mac | Check Python 3 specifically (Mac often has both 2 and 3) |
| `pip --version` | Both | Check pip version and which Python it's tied to |
| `which python` | Mac | Shows the path to the Python you're currently using |
| `Get-Command python` | Windows | Shows which Python executable is being used |

---

# 🏗️ Common Workflows

Here are some real-world patterns you'll use all the time.

## Starting a New Python Project

```
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

## Cloning and Setting Up Someone Else's Project

```
git clone https://github.com/user/project.git
cd project
python3 -m venv venv
source venv/bin/activate   # Mac
.\venv\Scripts\Activate    # Windows
pip install -r requirements.txt
python main.py
```

## Quick File Exploration

```
pwd                    # Where am I?
ls -la                 # What's here?
cd src                 # Go into src
ls                     # What's in src?
cat config.py          # Quick look at a file
cd ..                  # Go back
```

## Finding Something in Your Code

```
grep -rn "def my_function" .           # Mac: find a function definition
Get-ChildItem -Recurse | Select-String "def my_function"  # Windows
find . -name "*.py" -exec grep -l "import pandas" {} \;   # Mac: find which files import pandas
```

---

# ⚠️ Common Pitfalls & How to Fix Them

## "Command not found" / "not recognized"

**What happened:** The tool isn't installed, or it's not in your PATH.

**Fix:** Make sure the tool is installed. For Python: try `python3` instead of `python` on Mac.

## "Permission denied"

**What happened:** You don't have permission to access that file or run that command.

**Fix:** Mac: prefix with `sudo` (carefully). Windows: Run PowerShell as Administrator.

## "No such file or directory"

**What happened:** Typo in the path, wrong directory, or case sensitivity (Mac is case-sensitive!).

**Fix:** Run `pwd` and `ls` to confirm where you are and what's available.

## Files created in the wrong place

**What happened:** You were in a different directory than you thought.

**Fix:** Always `pwd` before creating or modifying files. Every time.

## Hidden files not showing up

**What happened:** Files starting with `.` (like `.gitignore`, `.env`) are hidden by default.

**Fix:** Mac: `ls -a`. Windows: `dir -Force`.

## Spaces in file/folder names causing issues

**What happened:** The terminal interprets spaces as argument separators.

**Fix:** Wrap the name in quotes: `cd "My Documents"` or escape with backslash: `cd My\ Documents`

## Accidentally overwrote a file with >

**What happened:** You used `>` (overwrite) instead of `>>` (append).

**Fix:** There's no fix. The data is gone. This is why you should be careful with `>`.

## "pip: command not found" inside a virtual environment

**What happened:** The venv might not be activated, or pip isn't installed in it.

**Fix:** Check if you see `(venv)` in your prompt. If not, activate the environment first.

---

# 🎯 Keyboard Shortcuts

These work in most terminals and will speed you up significantly.

| Shortcut | What It Does |
| --- | --- |
| `Tab` | Auto-complete file/folder names |
| `Tab Tab` | Show all possible completions |
| `↑ / ↓` | Cycle through command history |
| `Ctrl + C` | Kill the current running command |
| `Ctrl + D` | Exit the terminal |
| `Ctrl + L` | Clear the screen (same as `clear`) |
| `Ctrl + A` | Jump to the beginning of the line |
| `Ctrl + E` | Jump to the end of the line |
| `Ctrl + W` | Delete the word before the cursor |
| `Ctrl + U` | Delete everything before the cursor |
| `Ctrl + R` | Search through command history (Mac) |
| `Ctrl + Shift + C` | Copy selected text (Linux terminals) |
| `Ctrl + Shift + V` | Paste text (Linux terminals) |

---

# 📚 Quick Reference Card

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
| Read file | `cat file` | `cat file` / `Get-Content file` |
| Copy file | `cp src dest` | `Copy-Item src dest` |
| Move/Rename | `mv old new` | `Move-Item old new` |
| Delete file | `rm file` | `Remove-Item file` |
| Delete folder | `rm -r folder` | `Remove-Item folder -Recurse` |
| Find files | `find . -name "*.py"` | `Get-ChildItem -Recurse -Filter *.py` |
| Search in files | `grep "text" file` | `Select-String "text" file` |
| Clear screen | `clear` | `cls` |
| Command history | `history` | `Get-History` |
| Kill process | `Ctrl + C` | `Ctrl + C` |
| Create venv | `python3 -m venv env` | `python -m venv env` |
| Activate venv | `source env/bin/activate` | `.\env\Scripts\Activate` |
| Deactivate venv | `deactivate` | `deactivate` |

---

*Built for the Code in Place terminal teaching session by Tyrell Baker. When in doubt, `pwd` first.*
