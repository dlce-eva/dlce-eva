# Reproducible research - above the coding level

We'll leave aside the reproducibility vs. replicability debate for this
intro, and simply define reproducibility as

"running the same code, reaching the same results - twice"


## The baby step: Running your code twice (a.k.a testing)

Ensuring reproducibility already requires
- a way to figure out you're using the same code (version control!)
  - versioned data!
- a way to figure out you reached the same result (random seed, etc.)

Your code isn't static, neither are the results (a.k.a. revise and resubmit):
- automatic assessment of results should be versioned with your code
  (as tests or assert statements)
- your code should explain how and which results are obtained
  (This is where many of the coding best practices come in: Basically,
  make your code understable/workable over a longer period of time.)


## The giant leap: Running your code somewhere else (a.k.a. portability)

e.g. moving your code to the cluster

- how to move? -> version control software
- controling the environment
  - recording the environment
  - narrowing down the required environment
    - how to run? Target the command line for deployment of your code!
  - inputs: is data acquisition reproducible? (Know your file-system requirements!)
  - outputs: Are visualizations the output? Or can you get away with creating
    a dataset as output from which visualizations can be built with standard
    software?


Portability in Java, Python, R:

- Java: "write once run anywhere" somewhat true. The JRE replaces many OS dependencies
  for Java code
- Python: Not quite a JRE, but comes with "batteries included". Portability between
  MacOS and Linux mostly good. C extensions can be problematic.
- R: Portability between MacOS and Linux made more difficult by the default of
  using binaries on MacOS, compiling from source on Linux. Thus, what seems easy
  on MacOS may turn out to be problematic on Linux (due to OS-level dependencies)
- For both, Python and R there is a tension between OS/distribution versions of
  packages and custom environments.


General considerations for good portability:
- Try to stick with stable, released versions of packages, which can be
  installed from standard package sources (PyPI, CRAN, OS distribution)
- "First make it work, then make it fast": performance tuning is often highly
  platform-specific - abstain from it until necessary and the deployment target
  is fixed.


## The next step: Having someone else run your code

e.g. a reviewer

- document the environment
  - specify "known good" platforms (i.e. OS+version, e.g. "Ubuntu 20.04")
- document the execution
  - specify whether internet access is necessary (e.g. to fetch data)

While "make" is fairly common and a good wrapper format to tie the steps of an
analysis together, it introduces yet another dependency. So either have a human
readable Makefile which makes it possibly to simply cut&paste the steps to the
command line, or list the commands in a README in addition.

