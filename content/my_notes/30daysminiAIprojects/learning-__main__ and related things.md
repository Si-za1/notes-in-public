---
title: learning-__main__ and related things
draft: false
tags: []
---

i remember the first few times i saw `if __name__ == "__main__":`, i just accepted it blindly because every tutorial used it. like okay, fine, paste this here and somehow things will work. but then i messed up. i used it inside a function. i put some code above it and expected it to run automatically when i imported the file somewhere else. it didn’t. or worse, it ran twice. i felt stupid. but the more i messed up, the more curious i became.

so i started reading. and i found out that `__name__` is just a built-in variable in python. every file or script that runs has this variable. and when you run a file _directly_, python sets `__name__` to `"__main__"`. if you're _importing_ that same file into another file as a module, then `__name__` becomes the file’s name instead.

so basically, that line

```python
if __name__ == "__main__":
    do_something()
```

means: “only run `do_something()` if this script is being run directly, not when it’s being imported somewhere else.”  
and suddenly a lot of weird behavior started making sense. like why some scripts ran automatically, and others didn’t, depending on how i used them.

yeah, once i got the basic idea of `__name__` and `__main__`, i realized i still didn’t really know **when** i was supposed to use it, or how to structure my scripts properly. like, should i always use it? can i skip it? and what’s the cleanest way?

so i started breaking it down further.

first, `__name__` is always a string. when you run a file directly like:

```bash
python my_script.py
```

python sets `__name__` to `"__main__"` **just for that file**. but if you import that file somewhere else, like:

```python
import my_script
```

then `__name__` becomes `"my_script"` — the actual filename (without `.py`). this is what lets python know whether to run a chunk of code or not when the file is imported.

so when you write:

```python
if __name__ == "__main__":
    do_something()
```

you’re telling python: "only run this part if this is the main file being executed." it’s kind of like the "entry point" for the script.

but i also saw people do things like:

```python
def main():
    # actual logic
    do_something()

if __name__ == "__main__":
    main()
```

and that made the structure super readable. like, now i know where the program starts, and i can reuse `main()` if i want to call it from somewhere else. it also keeps the global space cleaner.

some people even skip the `main()` function and write:

```python
if __name__ == "__main__":
    print("Running script...")
```

which is okay for tiny scripts, but in bigger ones, having that `main()` function helps organize things.

then i came across something like:

```python
print("loaded module")

if __name__ == "__main__":
    print("running script")
```

and i started to _really_ get it. when i ran the script, both lines would print. but if i imported it somewhere else, only `"loaded module"` would show. so whatever goes **outside** the `if __name__ == "__main__":` block runs **even when imported**. anything **inside** it runs **only when executed directly**.

so, small things i picked up along the way:

- **Always use `if __name__ == "__main__"` when your script is meant to be both reusable and executable.** like utility files, experiments, scripts that can be run as CLI tools _and_ imported somewhere else.
    
- **Don’t use just `if __name__:`** — that works but doesn’t check for `"__main__"` specifically. better to be explicit.
    
- **Never put heavy logic outside the `if` block** if you might reuse the file as a module. otherwise it runs even when you don’t want it to.
    
- **Use a `main()` function** if the script is doing more than just 1-2 lines. it’s cleaner and easier to test later.
    
- if you’re creating a **library**, then that file should just contain definitions (functions, classes), and no code that runs at the top level unless guarded by the `if __name__ == "__main__"` block.
    

it was only after all these small “a-ha” moments that the full picture clicked. python’s trying to be helpful: it lets you write code that works both as a script _and_ as a reusable module. but only if you understand how and when to control what runs — and that all comes down to understanding `__name__` and `"__main__"`.


and then, i ran into `__init__.py`. that was during a time i was trying to structure my code into folders and make it less messy. i had folders like `utils`, `models`, `data`, and i kept getting import errors. something like `ModuleNotFoundError`. frustrating.

eventually, i learned that `__init__.py` tells python: “this folder is a package, you can import from it.” earlier, if there was no `__init__.py`, python wouldn’t recognize it as a valid module. that’s changing with newer versions, but still—adding an empty `__init__.py` file made my imports work. and when i put actual code inside it—like default imports or setup logic—it helped clean up the interface of the module. i could import stuff from the folder directly without diving deep into files.

so i started playing with it. i’d define classes and functions in individual files, like `math_utils.py` and `text_utils.py`, and then in `__init__.py` i’d write:

```python
from .math_utils import add, subtract
from .text_utils import clean_text
```

so that when someone did:

```python
from utils import add, clean_text
```

they didn’t need to know which file had what. it felt clean and elegant, and it helped a lot in building reusable code.

it was like one thing led to another. i wanted to know why my script didn’t run → learned about `__name__ == "__main__"` → tried splitting code into modules → ran into import issues → discovered `__init__.py` → realized how python treats packages and modules.

and through all that confusion and error messages and reading documentation i didn’t fully understand the first time, i finally got it. slowly. with lots of mistakes. and honestly, that’s how it sticks.
