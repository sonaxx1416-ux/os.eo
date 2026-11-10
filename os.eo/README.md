# os.eo

Files and folders from eo, with a log of every operation. It's written in eo, with no changes to the language.

```eo
from os {OsS}

var sys @OsS = OsS()
sys.remove "test.txt"
print sys.log[0]        # [20:01:05] remove test.txt → ok
```

You can also use `import os` with `var sys = os.OsS()`.

## Methods

Each method writes a line to `sys.log` and returns `true` or `false`. If it fails, the reason is in `sys.error`.

| Method | What it does |
|---|---|
| `sys.exists(path)` | Checks whether a file or folder exists |
| `sys.isdir(path)` | Checks whether a path is a folder |
| `sys.remove(path)` | Deletes a file |
| `sys.rmdir(path)` | Deletes an empty folder |
| `sys.rmdir(path, true)` | Deletes a folder and everything in it |
| `sys.copy(src, dst)` | Copies a file or a whole folder. If `dst` is a folder, it copies into it |
| `sys.rename(old, new)` | Renames or moves a file or folder. It won't overwrite something that already exists |
| `sys.system(cmd)` | Not supported yet. Returns `-1` and logs the reason |

## The log

```eo
print sys.log[0]          # the first line
print sys.last()          # the latest line
sys.show_log              # prints every line
sys.save_log "os.log"     # appends the log to a file
sys.clear_log
sys.echo = true           # prints each line as it happens
sys.max_log = 100         # keeps only the latest 100 lines
```

A line looks like this:

```
[20:01:05] copy a.png → backup → ok
[20:01:06] remove x.txt → failed: the file does not exist
```

## Notes

- Relative paths start from the folder of your main `.eo` file.
- `rename` copies then deletes, so it's slower on very large files.
- `system` needs a new builtin in eo to run commands. Until then it always fails.
