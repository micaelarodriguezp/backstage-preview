# [Backstage](https://backstage.io)

This is your newly scaffolded Backstage App, Good Luck!

### To start the app locally:

Prerequisite: Before building this image, be sure to run the following commands in the repo root:
```sh
brew install python@3.11
python3.11 -m pip install --upgrade pip
pip3 install mkdocs
pip3 install mkdocs-mermaid2-plugin
pip3 install mkdocs-material-extensions
pip3 install mkdocs-material
pip3 install mkdocs-techdocs-core
mkdocs --version // confirms that all of the above was done correctly
```

```sh
yarn install
yarn dev
```

### To start the app using docker:

Prerequisite: Before building this image, be sure to run the following commands in the repo root:
```sh
 yarn install
 yarn tsc
 yarn build:backend
```

```sh
docker image build . -f packages/backend/Dockerfile --tag backstage
docker run -it -p 7007:7007 backstage
```