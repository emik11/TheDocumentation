---
authors: Emil Andrzejewski
date: 19.03.2025
weight: 0
---

### Package manager
``` title="List Python modules"
pip list
pip freeze
```

``` title="Install specific module & version"
pip install pwntools==4.5.1
```

``` title="Install required modules"
pip install -r requirements.txt
```

### Virtual environments
``` title="Preparation"
pip install virtualenv
mkdir virtual && cd virtual
python3 -m venv env
source env/bin/activate
```