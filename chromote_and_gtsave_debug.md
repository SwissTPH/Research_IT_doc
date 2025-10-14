# Debugging `chromote`/headless browser issues for `gtsave`

When [`gt::gtsave`](https://gt.rstudio.com/reference/gtsave.html) writes a PDF, it first renders HTML and then converts it to PDF via a headless Chromium-based browser. That external dependency can be different across systems. Two ways to fix this:

1. **Configure the browser for `chromote`** (recommended);
2. **Bypass the browser**: render to LaTeX (`.tex`) and compile to PDF.

Below are debugging snippets for Windows system + Edge browser:

## Option A: Configure the headless browser

```R
# browser config

edge_paths <- c(
  "C:/Program Files/Microsoft/Edge/Application/msedge.exe",
  "C:/Program Files (x86)/Microsoft/Edge/Application/msedge.exe"
) # paths for 64- and 32-bit systems (only one of these paths exists)
edge_paths[file.exists(edge_paths)]
Sys.setenv(CHROMOTE_CHROME = edge_paths[file.exists(edge_paths)][1]) # use the first existing path

# This line is just for double-check
file.exists(Sys.getenv("CHROMOTE_CHROME"))

# make sure there is a path for a temporary “user data directory” used by the headless browser
ud <- file.path(tempdir(), "chromote-profile")
dir.create(ud, showWarnings = FALSE, recursive = TRUE)
Sys.setenv(CHROMOTE_USER_DATA_DIR = ud)

# this ensures chromote picks a free port automatically
Sys.unsetenv("CHROMOTE_PORT")
Sys.setenv(CHROMOTE_ARGS = "--no-sandbox --disable-gpu --disable-dev-shm-usage")

# then load the libraries again:
library(chromote)
library(tinytex)
library(gt)

# another double-check line:
chromote::chromote_info()

```



## Option B:  Render `gt` tables to LaTeX and compile to PDF (browser-free)

```R
# Format tables before rendering to tex (this function can be case-dependent)
make_wrapped <- function(tbl,
                         first_col_pct = 55,
                         other_col_pct = 15,
                         pad_px       = 2,
                         soft_wrap    = TRUE) {
  sw <- function(x) {
    x <- gsub(",",  ",\u200B", x, fixed = TRUE)
    x <- gsub("/",  "/\u200B", x, fixed = TRUE)
    x <- gsub("\\(", "\u200B(", x)
    x
  }

  out <- tbl |>
    gt::tab_options(table.width = gt::pct(100),
                    data_row.padding = gt::px(pad_px)) |>
    gt::cols_width(
      1  ~ gt::pct(first_col_pct),
      -1 ~ gt::pct(other_col_pct)
    ) |>
    gt::cols_align("left",  columns = 1) |>
    gt::cols_align("right", columns = -1)

  if (soft_wrap) {
    out <- out |>
      gt::text_transform(
        locations = gt::cells_body(columns = 1),
        fn = sw
      )
  }
  out
}

# apply wrapping function and save as tex (add more files if needed):
Table1 <- make_wrapped(Table1)

# make sure the output "PDF" folder exists
dir.create("PDF", showWarnings = FALSE, recursive = TRUE)

# save as tex (add more files if needed)
gt::gtsave(Table1, "PDF/table1.tex")


# Patch the generated .tex and compile
# gt’s LaTeX output is a tabular environment, not a full document. The helper below wraps it into a minimal LaTeX document and ensures the compiling progress

fix_tex_file <- function(path, out = path) {
  lines <- readLines(path, warn = FALSE)

  has_docclass <- any(grepl("^\\\\documentclass", lines))

  i_begin <- which(grepl("^\\\\begin\\{tabular\\*?\\}", lines))
  i_end   <- which(grepl("^\\\\end\\{tabular\\*?\\}",   lines))
  if (length(i_begin) == 1L && length(i_end) == 1L) {
    lines[i_begin] <- paste0("\\begin{adjustbox}{width=\\textwidth}\n", lines[i_begin])
    lines[i_end]   <- paste0(lines[i_end], "\n\\end{adjustbox}")
  }

  if (!has_docclass) {
    header <- c(
      "\\documentclass{article}",
      "\\usepackage[margin=1in]{geometry}",
      "\\usepackage{booktabs}",
      "\\usepackage{array}",
      "\\usepackage{longtable}",
      "\\usepackage{graphicx}",
      "\\usepackage{adjustbox}",
      "\\usepackage{caption}",
      "\\begin{document}"
    )
    footer <- "\\end{document}"
    lines  <- c(header, lines, footer)
  }

  writeLines(lines, out)
  invisible(out)
}

# apply the fix function to the tables (add more files if needed)
tex_files <- c("PDF/table1.tex") 
invisible(lapply(tex_files, fix_tex_file))


# creates PDF/table1.pdf next to the .tex
tinytex::latexmk("PDF/table1.tex")

```



Notes:

1. If LaTeX compilation fails the first time due to missing packages, run:

```R
tinytex::tlmgr_update(); tinytex::tlmgr_install(c("adjustbox","booktabs","caption","graphics","geometry","array","longtable"))

```

2. For very wide tables, consider switching to `\\begin{adjustbox}{max width=\\textwidth}` and/or reducing font size with `\\small` before the table block.

3. If you later switch back to browser-based PDF (HTML → PDF), keep the `chromote` environment block at the top of your script.
