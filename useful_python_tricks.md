# 🔦Useful Tricks for Python Scripts

## 🧑‍💻Formatting

Please refer to [PEP-8](https://peps.python.org/pep-0008/) style guide for consistent, readable, and maintainable code.
 Use `this_is_a_function()` for functions and `ThisIsAClass` for classes. Keep lines under 79 characters and add one blank line between functions.



## 🌱Environment Management

Create a dedicated **Conda environment** for each project to avoid version conflicts between packages.

```bash
conda create -n myproject python=3.12
conda activate myproject
```



Use `pip install` instead of `conda install` - it minimises the risk of altering other package versions in your environment.

```bash
pip install your_package
```



## 💬 Comments and Type Hints

Use clear, concise comments to explain logic and context - not just what the code does, e.g.:

```
def greet(name: str) -> str:
    """Return a polite greeting."""
    return f"Hello, {name}!"
```



- Comment as much as possible.
- Use hints (`-> str`) to clarify expected input and output.
