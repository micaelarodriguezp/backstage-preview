# [Backstage](https://backstage.io)

This is your newly scaffolded Backstage App, Good Luck!

To start the app locally:

```sh
yarn install
yarn dev
```

To start the app using docker:

```sh
docker image build . -f packages/backend/Dockerfile --tag backstage
docker run -it -p 7007:7007 backstage
```

## How this project was built

Execute the following commands to have a local backstage project

1. npx @backstage/create-app
2. cd backstage-preview/
3. yarn add --cwd packages/backend @backstage/plugin-techdocs-backend
4. yarn add --cwd packages/app backstage-plugin-techdocs-addon-mermaid

5. Enable the addon in the techdocs viewer inside App.tsx (packages/app/src/App.tsx) and EntityPage.tsx (packages/app/src/components/catalog/EntityPage.tsx)
   import { Mermaid } from 'backstage-plugin-techdocs-addon-mermaid';
   { techDocsPage}
   <TechDocsAddons>
   {/*...*/}
   <Mermaid config={{ theme: 'dark'}}} />
   </TechDocsAddons>

6. Inside the examples folder (the only component so far of this project) which is where our static documents that we want to display are located. We modified the entities.yml file adding inside metadata the following lines:
   annotations:
   backstage.io/techdocs-ref: dir:.

7. After that we added the docs folder where you can find all our documents that we have inside the documentation related to the example component.