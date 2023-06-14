# Poetry

## Pypi test
Poetry still use the legacy API:  
`poetry config repositories.testpypi https://test.pypi.org/legacy/`

## Publish
Build and publish in one command:  
`poetry publish --build --repository testpy --username __token__ --password TOKEN`
