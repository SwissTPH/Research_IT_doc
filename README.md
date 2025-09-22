# Auto-remove Jupyter Outputs before committing

Jupyter notebooks are great for interactive work, but by default, they also store all cell outputs (e.g., figures, tables, and logs) together with the .ipynb file.
When you commit to Git, this can make diffs large and messy — often you only want the code, not the saved outputs.

---
## Manually clear outputs

When committing changes, we only want to keep the script itself and see the changes in the script. Thus, we need to remove outputs from Jupyter Notebook. This can be manually done using:
* If you can find **Cell** in the Toolbar (< Version 7): Click **Cell** - **All Output** - **Clear**. This will clear the output of all cells without deleting any of your scripts
* If you cannot find **Cell** in the Toolbar (> Version 7): right click on any cell - **Clear Outputs of All Cells**. This will do the same thing.

---
## Automatically clear outputs

To avoid clearing outputs manually before every commit, you can configure Git to remove them automatically:

Install nbstripout:
```bash
pip install nbstripout nbconvert
nbstripout --install --attributes .gitattributes
```
What this does:

* Installs nbstripout in your environment.
* Adds a Git filter and clean rule to .gitattributes so that, whenever you git add a notebook, its outputs are stripped before being written to the repository.
Note that: Your local copy keeps its outputs, but the committed version is clean.

To double-check whether nbstripout is working, use
```bash
cat .git/config
```
and check whether you see this in the file:
```bash
[filter "nbstripout"]
```

---
## Clear outputs from code

If you only need to clear the output of the current cell during execution, you can call:

```python
from IPython.display import clear_output
clear_output(wait=True)
```
