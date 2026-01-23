# How to use Stata on our server？

## 1. Access Requirement

Before using Stata, you **must apply for access** via the [Google Form link](https://forms.gle/ghY9dEvQY1548kmK7).

⚠️ If you have not been approved:

* Running `stata-mp` in the terminal will show:

  ```
  stata-mp: command not found
  ```
* Opening a Stata notebook (`nbstata`) will show an error such as:

  ```
  Specified stata_dir, "/mnt/disk5/software/stata19", is not Stata's installation path
  ```

If you see either of these, it means you do not yet have access. Please submit the form.

---

## 2. Two Ways to Use Stata

### Option 1: Jupyter Notebook with Stata Kernel (`nbstata`)

* In JupyterLab, click **Stata (nbstata)** under “Notebook”.
* Write Stata commands in cells and run them with **Shift + Enter**.
* Example:

  ```stata
  sysuse auto
  summarize
  ```

### Option 2: Terminal (Command Line `stata-mp`)

* Open a terminal.
* To start interactive Stata:

  ```bash
  stata-mp
  ```
* To run a `.do` file in batch mode:

  ```bash
  stata-mp -b do your_script.do
  ```

---
