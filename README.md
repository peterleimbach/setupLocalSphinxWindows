# simple setup Sphinx on local Windows Environment

## Command Files and reason for them

### 1. 0-setupEnvironment.cmd
This script sets some environment variables needed to individualize the setup on the Windows PC of the user

``` script
set HOME=C:/Users/lei
rem echo %HOME%

PATH=%HOME%;%HOME%/AppData/Local/Programs/Python/Python312;%PATH%
echo %PATH%


set AAPS=%HOME%/aaps
echo %AAPS%

set AndroidAPSDocs=%AAPS%/AndroidAPSDocs
echo %AndroidAPSDocs%
```

### 1-activateVirtualPythonEnvironment.cmd
Here environment variables for the virtual python environment are set.

This script is generate by the installSphinxInVirtualEnvironment.cmd.

``` script
%AAPS%\.venv\Scripts\activate.bat
```

### buildHTML.cmd
Generates HTML code from the markdown code the documenation is written in.

``` script
python -m sphinx -T -E -b html -d %AAPS%/_build/doctrees -D language=en %AndroidAPSDocs%/docs/EN %AAPS%/html
```

### createVirtualPythonEnvironment.cmd
Creates a virtual Python environment for this "project". It's better to seperate such environments as otherwise the central environment gets messed up with maybe incompatible versions of python packages.

``` script
python -m venv %AAPS%/.venv

%AAPS%\.venv\Scripts\activate.bat
```

### installSphinxInVirtualEnvironment.cmd
This script just installs Sphinx and the necessary submodules which are listed in requirements.txt in the AndroidAPSDocs root directory.

``` script
python -m pip install -r %AndroidAPSDocs%/requirements.txt
```

### serveHTML.cmd
This script starts a simple python web server to serve the HTML files on your local machine. It's only for development and testing useful.

``` script
cd %AAPS%/html
python -m http.server 
```
