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
Antes de qualquer coisa atualize seu pip:  
`pip install --upgrade pip`  

## Build
Instale o pacote responsável por construir pacotes:  
`pip install build`  

Construa seu pacote com:  
`python -m build`  
Ao executar note que ele criou os pacotes na pasta `dist`, um pacote em `tar.gz` (formato antigo) e outro em `whl` (formato novo). Você pode especificar se deseja criar apenas no formato novo ou velho com:  
Velho: `python -m build --sdist`  
Novo: `python -m build --wheel`  
Se não especificar ele irá criar ambos.  

## Installing
Estando na pasta do projeto, basta instalar com:  
`pip install .`  

A desvantagem de instalar da maneira acima é que se você quiser atualizar o pacote que está usando, precisa instalar novamente. Para evitar isso basta instalar no modo editável.  
`pip install -e .`  
Agora qualquer mudança no pacote irá refletir na hora nos seus testes.  

## Upload  
Biblioteca responsável por fazer upload no Pypi:  
`pip install twine`  
Você não precisa fazer upload lá. Uma biblioteca muitas vezes pode ser baixada diretamente de um VCS, por exemplo, baixada de um repositório do Github.  

Para fazer o upload execute:  
`twine upload dist/*`  
Fará o upload de todos os pacotes naquela pasta.  


# References
https://packaging.python.org/en/latest/tutorials/packaging-projects/  
https://betterscientificsoftware.github.io/python-for-hpc/tutorials/python-pypi-packaging/#creating-a-python-package  
https://packaging.python.org/en/latest/guides/distributing-packages-using-setuptools/#requirements-for-packaging-and-distributing
