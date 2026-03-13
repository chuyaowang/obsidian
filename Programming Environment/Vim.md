# Vim

## Yank and paste to new file

To yank and paste lines into a new file in Vim, you can use one of these methods:

### Method 1: Yank and Paste (Standard)

1.  **Yank:** Move to the line and press `yy` (or `5yy` for 5 lines). Alternatively, use `V` to select lines visually and press `y`.
2.  **Open New File:** Type `:e newfile.txt` (or `:tabnew` / `:vnew` for a split).
3.  **Paste:** Press `p`.

### Method 2: Direct Write (Fastest)

1.  **Select:** Press `V` and highlight the lines you want.
2.  **Write:** Type `:w newfile.txt` and press `Enter`. (Vim will automatically fill in `:'<,'>w newfile.txt`).

### Method 3: Using a Register

1.  **Yank to register `a`:** `"ayy`.
2.  **Paste from register `a`:** In the new file, type `"ap`.