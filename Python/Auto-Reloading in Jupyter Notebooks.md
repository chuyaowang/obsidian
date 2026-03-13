# Auto-Reloading in Jupyter Notebooks

By default, Jupyter imports a library once and keeps it in memory. If you edit the source code of that library locally, Jupyter won't see the changes until you restart the kernel. The **IPython Autoreload extension** solves this by automatically detecting changes and refreshing the code.

## 1. The Engine: What is IPython?

Before using the commands, it helps to know where they come from.

- **Python** is the programming language.
    
- **Jupyter** is the visual interface (the web page).
    
- **IPython (Interactive Python)** is the _kernel_—the backend process that actually executes your code.
    

The commands used for autoreloading are **"Magic Commands"** (prefixed with `%`). These are special instructions for the IPython kernel, not standard Python syntax.

---

## 2. Basic Setup (Local Configuration)

To enable autoreloading for a specific notebook, run these commands in the very first cell:

Python

```
# 1. Load the extension
%load_ext autoreload

# 2. Set the mode (Mode 2 is the most common)
%autoreload 2
```

---

## 3. The Three Modes of Autoreload

You can control _how aggressive_ the reloading is by changing the number after `%autoreload`.

### `%autoreload 0` (Disable)

- **Behavior:** Auto-reloading is turned off.
    
- **Use Case:** Production runs where stability is key and code is not changing.
    

### `%autoreload 2` (Reload Everything)

- **Behavior:** Reloads **all** modules (except those explicitly excluded) every time you execute a cell.
    
- **Use Case:** The default for development. It ensures your notebook always reflects the latest version of your code.
    
- **Pros:** "Set it and forget it."
    
- **Cons:** Can be slightly slower if you have massive libraries imported.
    

### `%autoreload 1` (Selective Reloading)

- **Behavior:** Only reloads modules that you have explicitly selected using `%aimport`.
    
- **Use Case:** Performance optimization. If you have 50 libraries but are only editing one specific helper file, use this to tell IPython to ignore the other 49.
    

---

## 4. Fine-Tuning with `%aimport`

The `%aimport` command works differently depending on which mode you are in.

### Scenario A: The Whitelist (Using Mode 1)

When using `%autoreload 1`, nothing reloads by default. You use `%aimport` to add libraries to the "watch list."

Python

```
%autoreload 1

# Standard import (won't auto-reload)
import pandas as pd 

# Watched import (will auto-reload on changes)
%aimport my_custom_module
```

### Scenario B: The Blacklist (Using Mode 2)

When using `%autoreload 2`, everything reloads by default. You use `%aimport` with a **minus sign (`-`)** to exclude libraries that are causing errors or slowness.

Python

```
%autoreload 2

# Reload everything EXCEPT 'heavy_library'
%aimport -heavy_library
```

---

## 5. Global Configuration (Permanent Setup)

If you don't want to type these commands in every new notebook, you can configure IPython to run them automatically at startup.

### Step 1: Find your startup profile

Locate the `.ipython` folder on your machine:

- **Linux/Mac:** `~/.ipython/profile_default/startup/`
    
- **Windows:** `%USERPROFILE%\.ipython\profile_default\startup\`
    

### Step 2: Create the script

Create a file named `00-autoreload.ipy` in that folder. (The number `00` ensures it runs first).

### Step 3: Add the content

Paste the magic commands exactly as you would in a notebook:

Python

```
%load_ext autoreload
%autoreload 2
```

_Now, every time you launch Jupyter, autoreload will be active globally._

---

## Summary Cheatsheet

|**Goal**|**Command Sequence**|
|---|---|
|**Standard Dev (Recommended)**|`%load_ext autoreload`<br><br>  <br><br>`%autoreload 2`|
|**Performance Dev**|`%load_ext autoreload`<br><br>  <br><br>`%autoreload 1`<br><br>  <br><br>`%aimport my_lib`|
|**Exclude a library**|`%autoreload 2`<br><br>  <br><br>`%aimport -problematic_lib`|
|**Check watched modules**|`%aimport` (no arguments)|

### ⚠️ Important Limitations

1. **C-Extensions:** Modules written in C (like NumPy or parts of PyTorch) often cannot be reloaded without crashing. You must restart the kernel.
    
2. **Object Definitions:** If you modify a class `__init__`, existing instances of that class in your notebook will keep the _old_ structure until they are re-instantiated.