# Create template react app
```
npx create-react-app
```

# Modify folder structure
```
react-componentX
├── package.json
├── package-lock.json
├── public
│   ├── favicon.ico
│   ├── index.html
│   └── manifest.json
├── README.md
└── src
    ├── index.js
    └── lib
        └── ComponentX.js
```

# Modify package.json
```
{
  "name": "_____",
  "version": "0.1.0",
  "description": "...",
  "eslintConfig": {
    "extends": "react-app"
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/___/___.git"
  },
  "author": "_____",
  "license": "GPL-3.0",
  "bugs": {
    "url": "https://github.com/___/___/issues"
  },
  "dependencies": {
    "____": "_____"
  },
  "peerDependencies": {
    "prop-types": "^15.7.2",
    "react": "^16.8.6"
  },
  "devDependencies": {
    "babel-cli": "^6.26.0",
    "babel-preset-env": "^1.7.0",
    "babel-preset-react": "^6.24.1",
    "babel-preset-stage-0": "^6.24.1",
    "gh-pages": "^2.0.1",
    "prop-types": "^15.7.2",
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
    "react-router-dom": "^5.0.0",
    "react-scripts": "^2.1.8"
  },
  "babel": {
    "presets": [
      "react",
      "env",
      "stage-0"
    ]
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "dist": "export NODE_ENV=production && rm -rf dist && mkdir dist && npx babel src/lib --out-dir dist --copy-files",
    "test": "react-scripts build",
    "eject": "react-scripts eject",
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build"
  },
  "main": "dist/index.js",
  "module": "dist/index.js",
  "homepage": "https://___.github.io/___"
}
```

To further highlight the changes we made from default template created by `create-react-app`, here we go again:

## Change in dependencies:
* From
```
  "dependencies": {
    "react": "^16.8.6",
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
    "react-router-dom": "^5.0.0",
    "react-scripts": "^2.1.8"
  },
```
* To
```
  "dependencies": {
    "____": "_____"
  },
  "peerDependencies": {
    "proptypes": "^1.1.0",
    "react": "^16.8.6"
  },
  "devDependencies": {
    "babel-cli": "^6.26.0",
    "babel-preset-env": "^1.7.0",
    "babel-preset-react": "^6.24.1",
    "babel-preset-stage-0": "^6.24.1",
    "gh-pages": "^2.0.1",
    "prop-types": "^15.7.2",
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
    "react-router-dom": "^5.0.0",
    "react-scripts": "^2.1.8"
  },
```

This change reflect that:
1) We are no longer creating a stand-alone react app. Instead, we are creating a module that work in a parent react application, and hence part of the dependencies have been moved to `peerDependencies`.
2) However, during development, we still need to fire up a test web application and hence much of the original dependencies are now also moved to `devDependencies`.
3) Additional tools, such as babel is installed for transpiling; `gh-pages` is installed for building github pages.

## Add npm script
Add the following lines to 
```
    "dist": "export NODE_ENV=production && rm -rf dist && mkdir dist && npx babel src/lib --out-dir dist --copy-files",
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build"
```
These settings provide the following commands for the project:
```
npm run dist     # Build `/dist` folder for distribution
npm run predeploy   # Equivalent to `npm run build`
npm run deploy   # Use gh-pages to push a second github.io branch to the repository
```
As you can probably tell, everything in `src/lib` is transpiled and moved to `dist` folder for distribution. Therefore, you should write you components in `src/lib`, but still you can write react app outside of `src/lib`. The react app can import components from `src/lib` and run as usual using `npm start` and deploy as usual using `npm deploy`.

TODO: Can we replace build script with our dist script?

## Set up babel
```
  "babel": {
    "presets": [
      "react",
      "env",
      "stage-0"
    ]
  },
```
Non-standard js languages, such as jsx, or the latest ES 20xx may not be supported widely.

## Writing the component(s)
Well, have fun developing your components. You can still 

## Deploying on github
Simply:
```
npm deploy
```
