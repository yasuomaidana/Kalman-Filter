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
## DataSpell Configuration
Restart DataSpell: If you had it open, a restart helps it refresh the available Jupyter kernels.

Select Kernel: Open your .ipynb file. In the top-right corner, click the kernel name and select Octave.

Environment Sync: Ensure that the Python Interpreter selected for your DataSpell project is the same one where you just ran the uv pip install.

## Troubleshooting the Path
If you run a cell and get an error saying octave is not found, you need to tell the kernel exactly where your Octave installation lives.

Find the path to your Octave executable (e.g., C:\Program Files\GNU Octave\...\bin\octave-cli.exe on Windows or /usr/bin/octave on macOS/Linux) and set it as an environment variable:

Variable Name: OCTAVE_EXECUTABLE

Value: [Your Path to Octave]

You can set this in your OS environment variables or directly within DataSpell’s Run/Debug Configurations.
