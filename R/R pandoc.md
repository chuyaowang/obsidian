# R pandoc error

If you're encountering an error stating that `pandoc` is not installed during the installation of the `SHAPforxgboost` package, despite having `pandoc` accessible via the command line (`pandoc --version`), the issue may stem from R not recognizing the `pandoc` installation. Here's how you can address this:

### 1. Verify R's Awareness of Pandoc

R, particularly through RStudio, typically uses its own bundled version of `pandoc`. To check if R recognizes `pandoc`, run the following in your R session:

```r
rmarkdown::find_pandoc()
```

This function will display the version and path of `pandoc` that R is using. If it returns `NULL` or an unexpected path, R might not be detecting your system's `pandoc`.

### 2. Set the `RSTUDIO_PANDOC` Environment Variable

If R isn't detecting `pandoc`, you can manually set the `RSTUDIO_PANDOC` environment variable to point to your `pandoc` installation. First, determine the path to your `pandoc` executable. In a terminal, run:

```bash
which pandoc
```

This will return the path to the `pandoc` executable, such as `/usr/local/bin/pandoc`. Then, in your R session, set the environment variable:

```r
Sys.setenv(RSTUDIO_PANDOC = "/usr/local/bin")
```

Replace `/usr/local/bin` with the directory containing your `pandoc` executable. After setting this, try installing the package again.

### 3. Install Pandoc via RStudio (If Applicable)

If you're using RStudio, it comes with its own version of `pandoc`. Ensure that RStudio's `pandoc` is properly installed and recognized. You can check RStudio's `pandoc` path by running:

```r
Sys.getenv("RSTUDIO_PANDOC")
```

If this returns an empty string, RStudio might not have `pandoc` installed correctly. In that case, consider reinstalling RStudio or manually installing `pandoc` and setting the `RSTUDIO_PANDOC` environment variable as described above.

### 4. Install `ggExtra` Separately

Since the error mentions `ggExtra` requiring `pandoc`, try installing `ggExtra` separately to isolate the issue:

```r
install.packages("ggExtra")
```

If this installation succeeds, then proceed to install `SHAPforxgboost`:

```r
install.packages("SHAPforxgboost")
```

This step-by-step installation can help identify which package is causing the issue.

### 5. Check for System Package Requirements

Some R packages require system-level dependencies. Ensure that your system's package manager has all necessary dependencies installed. For example, on Debian-based systems, you can run:

```bash
sudo apt-get install pandoc
```

This ensures that `pandoc` is available system-wide.

If you've tried these steps and the issue persists, please provide additional details about your operating system and R environment so I can offer more targeted assistance.