# pycode_similar-master
pycode_similar-master/
├── .gitignore
├── CHANGES.md
├── LICENSE
├── MANIFEST.in
├── README.rst
├── setup.cfg
├── setup.py
├── pycode_similar/
│   ├── __init__.py
│   ├── pycode_similar.py
│   └── tests/
│       ├── empty.py
│       ├── original_version.py
│       └── test_cases.py
└── plagiarism_data/                (extra data in your archive)
    ├── users.json
    └── uploaded_files/             (pdf/docx sample uploads)
Similarity method (algorithm) — how pycode_similar works
pycode_similar is an AST-based plagiarism/similarity detector for Python:

Parse Python code into AST

Normalize the AST (so irrelevant differences are reduced; optional to keep/remove print nodes) 
GitHub

Compare code at function level (AST level) using one of two methods: 
GitHub

UnifiedDiff (default): converts normalized function AST to line strings and uses a line-based diff (difflib). Fast and practical. 
GitHub

TreeDiff (optional): tree edit distance on AST (slower; depends on zss). 
GitHub

Output “plagiarism percentage” defined as:
how much of the reference code is plagiarized by the candidate (directional; swapping ref/candidate can change the result). 
GitHub

✅ Perfect README.md (based on real code)
Create a file named README.md in the project root and paste:

md
Copy code
# pycode_similar (Python Code Similarity / Plagiarism Detector)

`pycode_similar` is a lightweight plagiarism detection tool for Python code.
It normalizes Python **AST** (Abstract Syntax Tree) and then uses diff methods to measure how much
**reference code structure** is plagiarized by **candidate code**.

> Note: The plagiarism score is **directional**:
> “How much of reference is plagiarized by candidate.”
> Swapping reference/candidate can produce different results.

---

## How it works (Similarity Method)

1. Parse files into Python AST
2. Normalize the AST (reduce superficial differences; optional to keep `print` nodes)
3. Compare at **function AST level**
4. Produce similarity/plagiarism percentage

### Diff methods

- **UnifiedDiff (default, recommended)**  
  Line-based diff of normalized function-AST strings (fast + good in practice)

- **TreeDiff (optional)**  
  Tree edit distance diff on AST (slower; requires `zss`)

---

## Project Structure

pycode_similar-master/
├── pycode_similar/
│ ├── init.py
│ ├── pycode_similar.py
│ └── tests/
│ ├── empty.py
│ ├── original_version.py
│ └── test_cases.py
├── setup.py
├── setup.cfg
└── README.rst

yaml
Copy code

---

## Installation

### Option A: Install via pip (recommended)
```bash
pip install pycode_similar
Option B: Run from source
Clone/download the repo and run from the folder:

bash
Copy code
python setup.py install
Usage (Command Line)
After installing:

bash
Copy code
pycode_similar <reference_file.py> <candidate_file.py> [more_candidate_files.py...]
Common flags
-l L Output function-level details only if AST lines >= L (default 4)

-p P Output details only if plagiarism percentage >= P (default 0.5)

-k, --keep-prints Keep print nodes (otherwise prints are normalized away)

-m, --module-level Process module-level nodes too

-c, --continue-on-error Continue on AST parsing errors for candidate files

Example:

bash
Copy code
pycode_similar -l 4 -p 0.5 pycode_similar/tests/original_version.py pycode_similar/pycode_similar.py
Usage (Python Library)
python
Copy code
import pycode_similar

results = pycode_similar.detect(
    [reference_code_str, candidate_code_str1, candidate_code_str2],
    diff_method=pycode_similar.UnifiedDiff,  # default
    keep_prints=False,
    module_level=False
)
print(results)
To use TreeDiff:

python
Copy code
import pycode_similar
results = pycode_similar.detect(
    [ref, cand],
    diff_method=pycode_similar.TreeDiff
)
TreeDiff requires the zss package.

Running Tests
bash
Copy code
python pycode_similar/tests/test_cases.py
Dependencies
Core: No third-party dependencies for UnifiedDiff

Optional: zss if you use TreeDiff

Limitations
Works best for Python code that can be parsed into AST

Directional score (reference → candidate)

Not a full replacement for enterprise tools (e.g., Moss/JPlag), but great for quick checks

License
MIT License

yaml
Copy code

---

## If you want me to *literally* read every `.py` file in your RAR
Upload the project as **`.zip`** (or extracted folder). Then I can open and read each script and tailor the README to *your exact* implementation (including dependencies from `requirements.txt`, entrypoints, CLI wrappers, etc.).

If you want, tell me which one you’ll upload:
- `pycode_similar-master.zip` ✅
- extracted folder ✅
::contentReference[oaicite:6]{index=6}
