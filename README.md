# Project structure

## Modules
* project_folder
  * `foo.py`
  * `bar.py`
  * `setup.py`

## Package
* project_folder
  * package_folder
    * `foo.py`
    * `bar.py`
  * `setup.py`

## Package with multiple directories
* project_folder
  * package_folder
    * another_folder
      * `foobar.py`
    * `foo.py`
    * `bar.py`
  * `setup.py`

# Setup file
Criação desse pacote vai ser minimalista.  
Minha intenção é ser capaz de utiliza-lo em outros projetos próprios (não publica-lo no PIP).  

## Modules
Nesse caso seu pacote é composto de poucos arquivos.  
Passe uma lista com o nome desses arquivos para `py_modules`.  

```python
from setuptools import setup

setup(
  name='my_package',      # name used when pip installing
  version='0.0.1',
  author='thiagola92',
  py_modules=['foo', 'bar']
)
```

### Usage
Os módulos selecionados vão ser acessados diretamente pelos nomes.  
`from foo import say_foo`  

## Package
Nesse caso se seu pacote é composto de multiplos pacotes/diretórios/pasta.  
Passe uma lista com as pastas do projeto para `packages`.  

Por exemplo, neste caso eu passei a raiz do projeto (project_folder).  
Isto torna tudo na pasta raiz do projeto parte do pacote.  
```python
from setuptools import setup

setup(
  name='my_package',
  version='0.0.1',
  author='thiagola92',
  packages=['']
)
```

Em pacotes, você normalmente deseja passar a pasta do pacote.  
```python
from setuptools import setup

setup(
  name='my_package',
  version='0.0.1',
  author='thiagola92',
  packages=['package_folder']
)
```

### Usage
Utilize o nome do pacote para referênciar os arquivos dentro dele
`from package_folder.foo import say_foo`  

## Package with multiple directories
Pastas dentro da pasta do pacote funcionam normalmente.  
```python
from setuptools import setup

setup(
  name='my_package',
  version='0.0.1',
  author='thiagola92',
  packages=[
    'package_folder',
    'package_folder.another_folder'
  ]
)
```

### Usage
Se for um script externo usando seu pacote, ele deve utilizar normalmente  
`from package_folder.another_folder.foobar import say_foobar`  

Se dentro do seu pacote você quiser referênciar outras pastas dentro dele, tem duas opções  
`from package_folder.fast_folder.fast import say_fast`  
`from .fast_folder.fast import say_fast`  

# Create package

## Requirements
`pip install wheel`  
(only the first time)  

## Create package
`python setup.py bdist_wheel`  

## Installing locally
`pip install -e .`  

# References
https://betterscientificsoftware.github.io/python-for-hpc/tutorials/python-pypi-packaging/#creating-a-python-package
