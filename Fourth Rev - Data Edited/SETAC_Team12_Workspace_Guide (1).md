# Working together on the SETAC project

## Why I set this up

I have put our project on GitHub so we can share the code and data in one organised place, see what has changed, and run the analysis on our own computers. This should make it easier to combine the retention and engagement work without repeatedly sending notebooks around or wondering which version is current.

We can keep using the Jupyter notebooks we know from the course. VS Code opens the same `.ipynb` files and lets us write Python cells, add Markdown observations, run code and see tables and charts underneath it. We are changing where we open the notebook, not learning a different programming language or rewriting everything as scripts.

GitHub gives us a shared project and a record of changes. GitHub Desktop gives us buttons for downloading and uploading those changes. VS Code is where we edit and run the notebooks. Python is what actually executes the code on each laptop.

Our repository is [SETAC-Team-12](https://github.com/joeladuba16-ship-it/SETAC-Team-12). Our data folder is called **`Fourth Rev - Data Edited`**. Please keep that spelling, spacing and capitalisation unless we agree a change together.

This guide follows our project folder structure. The setup steps below are recommendations for the team; they have not been installed or tested on each member's computer.

## Before we start: repository access

Because the repository contains the employer-project datasets, Joel should check that it is set to **Private**, unless SETAC/FourthRev has explicitly approved public distribution. Anonymised data is not automatically intended for public sharing.

For Joel: on the repository website, open **Settings → General**, scroll to **Danger Zone**, choose **Change repository visibility**, select **Private**, and complete GitHub's confirmation. Making it private restricts future access to the repository; it does not recall copies already downloaded or make existing public forks private.

Then invite the team through the repository's **Settings → Collaborators / Manage access** area. Each person should accept the invitation using the GitHub account they will use in GitHub Desktop. The exact access-menu label can vary.

Members need permission to contribute to this repository. If GitHub Desktop suggests creating a fork when you try to upload, stop and ask Joel to check your access. We want everyone contributing to the same team repository.

## 1. What each application does

| Application or term | What it means for us |
|---|---|
| GitHub website | The online project, shared file history, discussions and review of proposed changes. It does not run our local Python code. |
| GitHub Desktop | The app we use to copy the repository onto our laptop and exchange updates. |
| VS Code | The app where we open the whole project folder and work on notebooks and scripts. Download **Visual Studio Code**, not the separate product called Visual Studio. |
| Python | The programming language and software that executes our analysis. Installing VS Code does not install Python itself. |
| Python/Jupyter extensions | Add-ons inside VS Code that enable Python support and the notebook interface. |
| Kernel | The Python process running a notebook. Choosing the correct kernel makes the notebook use the packages installed for this project. |
| Repository | The project folder plus its tracked history. Each person has a local copy connected to the shared online repository. |

We do not need GitHub Codespaces, a paid AI subscription or a cloud computer for this workflow. GitHub Desktop can handle the Git operations described here without using Git commands in a terminal. If VS Code separately asks for command-line Git, it is optional for this guide: continue using Desktop for sharing.

## 2. Install the applications

### Everyone: create or sign into a GitHub account

1. Visit [github.com](https://github.com/) and create an account if needed.
2. Send Joel your username so he can invite the right account.
3. Accept the repository invitation. You do not need to create a new repository yourself.

### Windows

1. Download [GitHub Desktop](https://desktop.github.com/), run the installer and sign in to your GitHub account. Complete the browser authorisation if prompted.
2. Download [VS Code](https://code.visualstudio.com/download). The Windows **User Installer** is the usual choice. Run it, follow the prompts, then open the application.
3. Install Python if you do not already have the agreed version. For this guide, the proposed common version is **Python 3.13**. Use the official [Python downloads](https://www.python.org/downloads/windows/) page. If you install the Python Install Manager, open a terminal and run `py install 3.13`. If you use a conventional installer instead, choose the build appropriate to your computer and enable the launcher/PATH options if offered.
4. Close and reopen VS Code after installing Python. In **Terminal → New Terminal**, run:

   ```powershell
   py -3.13 --version
   ```

You should see a Python 3.13 version. If `py` is not recognised, check that the install finished and reopen the application. Do not uninstall your existing course/Anaconda setup to make this work.

### Mac

1. Download [GitHub Desktop](https://desktop.github.com/) for Mac. Open the download, install the app as prompted, and sign in to GitHub.
2. Download [VS Code](https://code.visualstudio.com/download). Choose Apple silicon for an M-series Mac or Intel for an Intel Mac; the Universal build also covers both. Open the download and move the app to **Applications** as prompted.
3. If needed, install Python 3.13 using the macOS installer on the official [Python 3.13.16 release page](https://www.python.org/downloads/release/python-31316/). Use a normal installer build, not an experimental/free-threaded build. You do not need Homebrew for this route.
4. Close and reopen VS Code. In **Terminal → New Terminal**, run:

   ```bash
   python3.13 --version
   ```

You should see a Python 3.13 version. Do not rely on a macOS system Python or remove your existing Anaconda installation.

If you already have a working course environment, we can use it once the team agrees the Python version and confirms the required imports work. The separate project environment below avoids changing packages used by your other assignments. The proposed 3.13 setup is a starting convention, not a claim about what everyone currently has installed.

### Both systems: install the VS Code extensions

1. Open **Extensions**, the icon with small blocks in VS Code's left sidebar.
2. Search for **Python** and install the extension published by **Microsoft** (`ms-python.python`).
3. Search for **Jupyter** and install the extension published by **Microsoft** (`ms-toolsai.jupyter`).

The extensions are separate from Python packages. For example, installing the Jupyter extension is not the same as installing `ipykernel` into Python; we do both below.

## 3. Download the connected project copy

In GitHub Desktop:

1. Select **File → Clone Repository**.
2. Select the **URL** tab and paste:

   ```text
   https://github.com/joeladuba16-ship-it/SETAC-Team-12
   ```

3. Choose a local folder. Use an ordinary local location outside Google Drive, OneDrive, Dropbox and iCloud syncing. Check carefully: Documents and Desktop can themselves be cloud-synced. A dedicated folder under your user account, such as `Projects`, is a reasonable choice if it is not synced.
4. Click **Clone** and wait for the download to finish.
5. If you already cloned this repository, select that existing copy instead. You do not need a new clone every day.

Cloning downloads the tracked folder structure, files and history, and connects your local copy to GitHub. Do not use **Download ZIP** for the normal team workflow: a ZIP is a disconnected snapshot. Do not fork the project for this workflow either.

The repository already contains the extracted data folder and the original ZIP. Use the extracted **`Fourth Rev - Data Edited`** folder for analysis. You do not need to extract the ZIP again or copy a second data folder into the repository.

## 4. Open the project in VS Code

1. In VS Code, choose **File → Open Folder**.
2. Open the outer **`SETAC-Team-12`** folder that GitHub Desktop just cloned.
3. Check that the Explorer sidebar shows the README and **`Fourth Rev - Data Edited`** folder.
4. Expand that data folder and open **`Joel_test.ipynb`**.
5. If asked about Workspace Trust, trust the project only after confirming it is our expected repository and you are comfortable running its code.

Open the whole repository, not an old copy of a notebook from Downloads or the original Desktop folder. VS Code and GitHub Desktop should be pointing to the same local repository.

## 5. Set up Python and the packages

A project environment is a separate collection of Python packages for this project. Each person creates their own `.venv` folder. It stays on their computer; we share the package list, not the environment folder itself.

Use **Terminal → New Terminal** in VS Code. Make sure the terminal is in the outer `SETAC-Team-12` folder. The commands below call the environment's Python directly, so you do not need to activate it or change PowerShell security settings.

### Windows: run these lines one at a time in PowerShell

```powershell
py -3.13 -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install pandas numpy openpyxl xlrd ipykernel matplotlib seaborn scipy statsmodels scikit-learn
```

### Mac: run these lines one at a time

```bash
python3.13 -m venv .venv
./.venv/bin/python -m pip install --upgrade pip
./.venv/bin/python -m pip install pandas numpy openpyxl xlrd ipykernel matplotlib seaborn scipy statsmodels scikit-learn
```

The packages cover the planned workflow:

| Package | Why we use it |
|---|---|
| `pandas` | Load, clean, combine and summarise datasets. |
| `numpy` | Numerical operations used throughout the analysis. |
| `openpyxl` | Read and write `.xlsx` workbooks. |
| `xlrd` | Read the older `.xls` Annual Meeting file. |
| `ipykernel` | Run our Python environment as a notebook kernel in VS Code. |
| `matplotlib`, `seaborn` | Charts and visualisations. |
| `scipy`, `statsmodels` | Statistical tests and models where needed. |
| `scikit-learn` | Preprocessing, clustering or predictive analysis if agreed and justified. In Python, import it as `sklearn`. |

We do not need all these imports in every notebook. The first five packages are enough for the initial data-access and cleaning checks; the rest prepare us for the planned analysis. Installing a modelling package does not mean we have committed to using a model.

`pathlib`, `sqlite3`, `json` and `os` are included with Python. Do not try to install them with pip. If we use a PostgreSQL server later, we can add `sqlalchemy` and an appropriate PostgreSQL driver then; those are not required just to read the supplied files.

### Select the project environment

1. Open the Command Palette: **Ctrl+Shift+P** on Windows or **Cmd+Shift+P** on Mac.
2. Run **Python: Select Interpreter** and select the environment inside this repository's `.venv` folder.
3. In the open notebook, click **Select Kernel** at the top right.
4. If needed, choose **Select Another Kernel → Python Environments**, then select that same `.venv` environment.

Run this notebook cell to check:

```python
import sys
import pandas as pd
import numpy as np
import openpyxl
import xlrd
import matplotlib
import seaborn
import scipy
import statsmodels.api as sm
import sklearn

print("Python executable:", sys.executable)
print("Python version:", sys.version.split()[0])
print("pandas version:", pd.__version__)
print("All project imports worked.")
```

The executable path should contain our repository's `.venv` folder. A successful terminal installation will not help a notebook using a different kernel.

### Keep a shared package list

Joel or the data engineer should add a `requirements.txt` file at the repository root once, with the agreed packages, and share it through the normal review process. The starting contents would be:

```text
pandas
numpy
openpyxl
xlrd
ipykernel
matplotlib
seaborn
scipy
statsmodels
scikit-learn
```

Once that file exists, install from it instead of repeating the long package command:

Windows:

```powershell
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

Mac:

```bash
./.venv/bin/python -m pip install -r requirements.txt
```

This starting list does not pin exact versions, so it does not guarantee identical installations on different dates. Once the team has a working setup, record and agree the tested versions, then pin them in this shared file. Do not replace it with an export of an unrelated Anaconda/base environment.

## 6. What will feel familiar from Jupyter?

Open a notebook and you will still see code and Markdown cells. Use the triangle next to a cell to run it, or **Shift+Enter** to run and move on. Results appear beneath the cell. Use **+ Code** and **+ Markdown** to add cells and the notebook toolbar to run all cells or restart the kernel.

Save with **Ctrl+S** on Windows or **Cmd+S** on Mac. If a variable is missing after restarting, rerun the earlier cells in order. Before handing over a notebook, restart its kernel and run all cells from top to bottom. This checks that the saved analysis does not depend on an old variable left in memory.

You can still open the same `.ipynb` file in browser-based Jupyter if that is more comfortable. Use the notebook inside the cloned repository, select the right environment, and close it in one editor before editing it in another. GitHub Desktop will see saved changes regardless of which editor you used.

The optional browser-Jupyter package is `notebook`; install it into the same environment if needed. From a terminal in the repository root, launch it with `.\.venv\Scripts\python.exe -m notebook` on Windows or `./.venv/bin/python -m notebook` on Mac. Do not type these terminal commands into a Python code cell.

## 7. Where code and data should sit

For now, keep our notebooks alongside the main Excel files inside **`Fourth Rev - Data Edited`**. Keep event, group and newsletter files in their existing subfolders. Save cleaned outputs in a **`Cleaned`** subfolder at that same level. If it is absent after cloning, the code can create it: Git does not track empty folders.

| Path relative to the repository root | Purpose |
|---|---|
| `README.md` | Project introduction and instructions. |
| `requirements.txt` | Agreed package list, to be added by the team. |
| `.venv/` | Your local Python environment; not uploaded. |
| `Fourth Rev - Data Edited/Joel_test.ipynb` | Existing access-test notebook. |
| `Fourth Rev - Data Edited/01_data_preparation.ipynb` | Example proposed preparation notebook. |
| `Fourth Rev - Data Edited/02_retention_analysis.ipynb` | Example proposed Theme 1 notebook. |
| `Fourth Rev - Data Edited/03_engagement_analysis.ipynb` | Example proposed Theme 3 notebook. |
| `Fourth Rev - Data Edited/Country list.xlsx` | Original country lookup. |
| `Fourth Rev - Data Edited/Individual Contacts.xlsx` | Original contact profiles. |
| `Fourth Rev - Data Edited/Subscriptions Europe.xlsx` | Original Europe subscriptions. |
| `Fourth Rev - Data Edited/Events/` | Existing event subfolders and source files. |
| `Fourth Rev - Data Edited/Groups/` | Existing group subfolders and source files. |
| `Fourth Rev - Data Edited/Newsletters and Website Resources/` | Existing communication/content data. |
| `Fourth Rev - Data Edited/Cleaned/` | Generated cleaned datasets. |

The numbered analysis notebooks are suggested names for the team to agree. Agree ownership before creating them. Do not rename existing source files or move folders individually, as this can break other people's code.

The overall location can differ between computers. Your clone might be under `C:\Users\YourName\Projects` on Windows or `/Users/YourName/Projects` on Mac. What matters is that the structure **inside** the repository stays consistent.

### A first cell that finds the data folder

The working directory can vary depending on how VS Code or Jupyter starts the notebook. Use this setup cell rather than assuming `Path.cwd()` always means the notebook's own folder:

```python
from pathlib import Path

current = Path.cwd().resolve()
project_root = next(
    (location for location in [current, *current.parents]
     if (location / ".git").exists()),
    None
)

if project_root is None:
    raise RuntimeError(
        "Open the cloned SETAC-Team-12 project in VS Code, "
        "then start the notebook from that project."
    )

data_dir = project_root / "Fourth Rev - Data Edited"

if not (data_dir / "Country list.xlsx").is_file():
    raise FileNotFoundError(
        f"Expected source file not found in: {data_dir}. "
        "Check the folder name and that your clone has finished downloading."
    )

cleaned_dir = data_dir / "Cleaned"
cleaned_dir.mkdir(exist_ok=True)

print("Project:", project_root)
print("Source data:", data_dir)
print("Cleaned outputs:", cleaned_dir)
```

This searches the current directory and its parents for the Git project, then uses the agreed data-folder name. It works when the notebook starts at the repository root or inside one of its subfolders. It deliberately stops if the notebook was launched somewhere unrelated.

### Read and save using those paths

```python
import pandas as pd

countries = pd.read_excel(data_dir / "Country list.xlsx")
display(countries.head())

# Small cleaning example: keep the source unchanged.
countries_cleaned = countries.copy()
countries_cleaned.columns = countries_cleaned.columns.str.strip()

for column in countries_cleaned.select_dtypes(include="object").columns:
    countries_cleaned[column] = countries_cleaned[column].map(
        lambda value: value.strip() if isinstance(value, str) else value
    )

output_path = cleaned_dir / "Country_list_cleaned.xlsx"
countries_cleaned.to_excel(output_path, index=False)
print("Saved:", output_path)
```

This reads the full file, not just a five-row sample. It only trims spaces; it is not complete data validation. Rerunning it replaces the generated cleaned file. It never writes over `Country list.xlsx`.

To read a nested file, extend the same path, for example:

```python
students = pd.read_excel(
    data_dir / "Groups" / "Affinity Groups" / "Europe Students.xlsx"
)
```

Avoid personal absolute paths such as `/Users/Joel/Desktop/...`, and avoid manually typed Windows backslashes inside data-loading code. `Path` joins work on both systems.

## 8. How sharing actually works

We each work on our own local copy. Saving a notebook changes the file on your laptop. It does not immediately change everyone else's copy, and another person's running notebook will not change while they are using it.

| Action | Meaning |
|---|---|
| Save | Write your changes to the local file. |
| Commit | Record a named version of selected changes locally. |
| Push | Upload your commits to GitHub. |
| Fetch | Check for updates on GitHub without applying them to your working files. |
| Pull | Bring the selected branch's remote updates into your local copy. |
| Branch | A separate tracked line of work within this repository. |
| Pull request | A proposal to review and merge a branch into another branch, usually `main`. It is different from clicking Pull. |
| Merge | Combine an agreed set of changes into the destination branch. |

We are sharing the files and code history, not each person's Python memory or installed packages. Someone receiving a notebook still needs to select their local environment and run it.

All tracked changes can be shared: notebooks, scripts, data, documentation, and file deletions or moves. Review the changed-file list before committing. Accidental changes to a source spreadsheet should not be included just because they appear in that list.

## 9. Our recommended day-to-day workflow

### Before starting a new task

1. Open GitHub Desktop and select **SETAC-Team-12**.
2. Make sure any unfinished local work is saved and safely committed on its own branch. Do not discard work simply to make the Changes list empty.
3. Switch **Current Branch** to **main**.
4. Click **Fetch origin**. If offered, click **Pull origin**.
5. Use **Current Branch → New Branch** to create a branch for your task, such as `christelle/retention-baseline` or `joel/dictionary-notes`. Create it from the updated `main`.
6. Open the project in VS Code and work on the agreed notebook or script.

If you are continuing an existing task branch, switch to that branch and fetch/pull its updates. Updates to `main` are not automatically merged into an older task branch. When needed, first update local `main`, switch back to your saved/committed task branch, open **Current Branch → Choose a branch to merge into [your branch]**, select `main`, and confirm the merge. Ask for help if conflicts appear.

### When your work is ready to share

1. Run the notebook from a fresh kernel, check the results, then save it.
2. Return to GitHub Desktop and check **Current Branch** is your intended task branch.
3. Review **Changes**. Select only the files belonging to the task. Check for unexpected source-data changes, huge outputs or personal files.
4. Enter a clear summary, for example `Add renewal checks and document unmatched contact IDs`.
5. Click **Commit to [your branch]**.
6. Click **Publish branch** for a new branch, or **Push origin** for one already published.
7. Use **Preview Pull Request / Create Pull Request** to propose merging your branch into **main**. Check that the base branch is `main` and the comparison branch is yours.
8. Explain what changed, why, which files you used, how you checked it and any unresolved assumptions. Ask the relevant team member to review it.

Pushing makes your branch available online. It does not automatically put those changes into `main`. The reviewer should read the proposed changes and, for code changes, check out the branch and run the relevant notebook. Once the team is happy, Joel or the agreed person with merge access can open the pull request on GitHub, check that it targets `main`, choose **Merge pull request**, and confirm. If GitHub reports a conflict or a failed required check, resolve that first rather than bypassing it.

After review and merge, everyone can switch to `main`, fetch/pull, and reopen or reload the changed notebook. A teammate can also check out your published branch to inspect it before merging, but should coordinate before editing it.

**Example:** Christelle works on the retention notebook on her branch, pushes it, and requests review. Once that change is merged into `main`, Katherine pulls the updated `main` and can run it locally. Merely saving or committing the notebook on Christelle's laptop would not share it.

If a push is rejected because remote changes exist, do not force-push. Preserve your local commits, fetch/pull as appropriate, and ask for help resolving any conflict.

## 10. A few agreements that will make this easier

- Give each notebook a main owner. Branches help organise changes, but do not make simultaneous edits to the same notebook effortless to combine.
- Keep different workstreams in separate notebooks. Agree shared preparation functions and metric definitions together rather than creating competing versions silently.
- Keep original data unchanged. Put transformations in code and save derived datasets in `Cleaned`.
- Agree who generates shared cleaned files. Two people producing different versions of the same Excel file can cause conflicts; it is often better to regenerate it from reviewed code.
- Keep useful charts, tables and observations in notebooks, but avoid printing thousands of contact-level rows. Clear unnecessarily large outputs before sharing.
- Use descriptive notebook and commit names. Avoid a chain of files named `final`, `final2` and `final_really_final`; Git already records versions.
- Do not upload passwords, access tokens, local environments or unrelated personal files.
- After pulling changes, reload an open notebook only after saving or otherwise preserving your own work. If asked whether to overwrite an externally changed file, pause and check which version you need.
- If Git reports a conflict, preserve both versions and ask the relevant author to resolve it with you. Do not click Discard Changes or choose one side without checking what would be lost.

### Files we should ignore

Joel/data engineering should check the existing `.gitignore` and add the following entries if absent. Add to the existing file rather than replacing it:

```gitignore
.venv/
__pycache__/
*.py[cod]
.ipynb_checkpoints/
.DS_Store
._*
~$*
.env
```

Do not add a blanket `*.xlsx` or `*.csv` rule for our current arrangement, because the team is deliberately tracking the project data. The `.gitattributes` file also controls how Git handles some files; leave it unchanged unless we agree a reason to edit it.

Some `.DS_Store` files are already tracked in the repository. Adding an ignore rule prevents new untracked ones from being added; it does not remove files already in Git's history. Joel can make a separate, reviewed cleanup later. This is housekeeping, not a prerequisite for running the analysis.

## 11. Common problems

| What you see | What to check |
|---|---|
| Repository not found or permission denied | Sign into the invited GitHub account, accept the invitation, and check the URL. |
| Desktop offers to create a fork | Ask Joel to confirm write access to the shared repository. |
| No kernel available | Confirm the Microsoft Python and Jupyter extensions are installed, then choose the `.venv` environment in Select Kernel. |
| `ModuleNotFoundError` | Run the import-check cell and inspect `sys.executable`. Install into that environment, not a different Python. |
| `openpyxl` or `xlrd` missing | Install the package into the notebook's selected environment, then restart the kernel if needed. |
| File not found | Run the path-setup cell; check `Fourth Rev - Data Edited` is spelled exactly and the file exists in the clone. |
| A file is visible on GitHub but missing locally | Fetch/pull the right branch; check you are opening the correct local clone. |
| You cannot see a teammate's change | Check they pushed it, which branch it is on, whether it has merged, and whether you pulled that branch. |
| A notebook works only after running cells out of order | Restart and run all cells from the top; fix missing setup steps. |
| Lots of changes appear unexpectedly | Inspect the list before committing. Running a notebook can change outputs, execution counts and metadata. |
| A notebook opens as JSON text | Use **Reopen Editor With → Jupyter Notebook**, and check the Jupyter extension is installed. |
| `Cleaned` is absent after cloning | Empty folders are not tracked; run the setup cell to create it. |
| Windows says script execution is disabled | The installation commands above call `python.exe` directly, so activation is unnecessary. Do not change security settings just for this setup. |

## 12. First-session checklist

You are ready when you can:

1. Open the cloned **SETAC-Team-12** repository in both GitHub Desktop and VS Code.
2. Select your own project Python environment and pass the import-check cell.
3. Read `Country list.xlsx` using the shared path setup.
4. Save the example output into `Cleaned` without altering the source file.
5. Make a small change on your own branch, commit it, publish/push it, and see that branch on GitHub.
6. Open a pull request for review and, after merging, retrieve the agreed version from `main`.

For daily work, the habit is: get the latest agreed version, work on your task branch, test and save, commit and push, then request review. Keep Google Drive for the shared documents and presentation work we already manage there; use this repository as the agreed home for the coding project and tracked data.

## Official help and downloads

These instructions were checked against official documentation on 21 October 2026. Button labels may change slightly between app versions.

- [VS Code downloads](https://code.visualstudio.com/download), [Windows installation](https://code.visualstudio.com/docs/setup/windows) and [Mac installation](https://code.visualstudio.com/docs/setup/mac).
- [Python 3.13.16 downloads](https://www.python.org/downloads/release/python-31316/) and [Python for Windows](https://www.python.org/downloads/windows/).
- [Python environments in VS Code](https://code.visualstudio.com/docs/python/environments).
- [Jupyter notebooks in VS Code](https://code.visualstudio.com/docs/datascience/jupyter-notebooks) and [choosing a notebook kernel](https://code.visualstudio.com/docs/datascience/jupyter-kernel-management).
- [GitHub Desktop setup](https://docs.github.com/en/desktop/installing-and-authenticating-to-github-desktop/setting-up-github-desktop).
- [Cloning with GitHub Desktop](https://docs.github.com/en/desktop/adding-and-cloning-repositories/cloning-and-forking-repositories-from-github-desktop).
- [Committing changes](https://docs.github.com/en/desktop/making-changes-in-a-branch/committing-and-reviewing-changes-to-your-project-in-github-desktop).
- [Syncing branches](https://docs.github.com/en/desktop/working-with-your-remote-repository-on-github-or-github-enterprise/syncing-your-branch-in-github-desktop).
- [Creating pull requests in Desktop](https://docs.github.com/en/desktop/working-with-your-remote-repository-on-github-or-github-enterprise/creating-an-issue-or-pull-request-from-github-desktop).
- [Changing repository visibility](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings/setting-repository-visibility).
