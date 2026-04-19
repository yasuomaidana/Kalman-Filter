# Configuring Octave Kernel

## Install the Kernel via uv
Open your terminal and run the following command. This will install the octave_kernel into your current environment:

Bash
uv pip install octave_kernel
Note: If you prefer not to "pollute" your global Python environment, you can use uv tool run to register the kernel, but standard pip install via uv is generally more reliable for DataSpell detection.

## Register the Kernel with Jupyter
Even after installing the package, you need to make sure the Jupyter ecosystem (which DataSpell uses) knows where to find Octave. Run this command:

Bash
python -m octave_kernel install --user
To verify it worked, ask uv to list the available kernels:

Bash
uv run jupyter kernelspec list
## Code Completion and Documentation
To get IDE-like features (as-you-type completion, documentation hovers) in JupyterLab or DataSpell, you can use the native Octave kernel features.

### For JupyterLab (Automatic in Docker)
The Docker setup now includes **Continuous Hinting** (as-you-type completion) and **texinfo** (for built-in documentation). 
1.  **Autocomplete:** Simply start typing a function name (e.g., `ss` or `lsim`) and suggestions will appear automatically.
2.  **Documentation:** Press `Shift + Tab` while your cursor is on a function name to see its signature and documentation.

### For Local Setup (DataSpell / Local Jupyter)
If you are running outside of Docker, follow these steps:

1.  **Enable Continuous Hinting:**
    - Go to **Settings** > **Settings Editor**.
    - Search for **Code Completion**.
    - Check **Continuous Hinting**.
    - This will make completions appear without pressing `Tab`.

2.  **Documentation Support:**
    Ensure you have `texinfo` installed on your system (e.g., `brew install texinfo` on macOS or `sudo apt install texinfo` on Linux). This allows the Octave kernel to provide helpful tooltips when you press `Shift+Tab`.

3.  **DataSpell Configuration:**
    DataSpell has built-in support for Octave highlighting. Ensure that your Python interpreter is the same one where you installed `octave_kernel`.

## Troubleshooting the Path
If you run a cell and get an error saying octave is not found, you need to tell the kernel exactly where your Octave installation lives.

Find the path to your Octave executable (e.g., C:\Program Files\GNU Octave\...\bin\octave-cli.exe on Windows or /usr/bin/octave on macOS/Linux) and set it as an environment variable:

Variable Name: OCTAVE_EXECUTABLE

Value: [Your Path to Octave]

You can set this in your OS environment variables or directly within DataSpell’s Run/Debug Configurations.
