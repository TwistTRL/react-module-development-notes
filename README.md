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
  "main": "dist/index.js",
  "module": "dist/index.js",
  "eslintConfig": {
    "extends": "react-app"
  },
  "dependencies": {
    "____": "_____"
  },
  "peerDependencies": {
    "prop-types": "^15.7.2",
    "react": "^16.8.6"
  },
  "devDependencies": {
    "@babel/cli": "^7.4.4",
    "@babel/core": "^7.4.5",
    "@babel/preset-env": "^7.4.5",
    "@babel/preset-react": "^7.0.0",
    "gh-pages": "^2.0.1",
    "prop-types": "^15.7.2",
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
    "react-router-dom": "^5.0.0",
    "react-scripts": "^3.0.1"
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
  "babel": {
    "presets": [
      "@babel/preset-react",
      "@babel/preset-env"
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
  "homepage": "https://___.github.io/___",
  "repository": {
    "type": "git",
    "url": "git+https://github.com/___/___.git"
  },
  "author": "_____",
  "license": "GPL-3.0",
  "bugs": {
    "url": "https://github.com/___/___/issues"
  }
}
```

To further highlight the changes we made from default template created by `create-react-app`, here we go again:

## Change in dependencies:
* From
```
  "dependencies": {
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
    "react-router-dom": "^5.0.0",
    "react-scripts": "^3.0.1"
  },
```
* To
```
  "dependencies": {
    "____": "_____"
  },
  "peerDependencies": {
    "prop-types": "^15.7.2",
    "react": "^16.8.6"
  },
  "devDependencies": {
    "@babel/cli": "^7.4.4",
    "@babel/core": "^7.4.5",
    "@babel/preset-env": "^7.4.5",
    "@babel/preset-react": "^7.0.0",
    "gh-pages": "^2.0.1",
    "prop-types": "^15.7.2",
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
    "react-router-dom": "^5.0.0",
    "react-scripts": "^3.0.1"
  },
```

This change reflect that:
1) We are no longer creating a stand-alone react app. Instead, we are creating a module that work in a parent react application, and hence part of the dependencies have been moved to `peerDependencies`.
2) However, during development, we still need to fire up a test web application and hence much of the original dependencies are now also moved to `devDependencies`.
3) Additional tools, such as babel is installed for transpiling; `gh-pages` is installed for building github pages.
* Note: babel dependencies changed from the older v6.x to v7.x. State presets has been removed. Use appropriate babel setting if your project requires. This settting with only `preset-env` and `preset-react`, should be able to accomodate most use cases.

## Add npm script
Add the following lines to 
```
    "dist": "export NODE_ENV=production && rm -rf dist && mkdir dist && npx babel src/lib --out-dir dist --copy-files",
~~    "install": "npm run dist",~~
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build"
```
These settings provide the following commands for the project:
```
npm run dist     # Build `/dist` folder for distribution
npm run predeploy   # Equivalent to `npm run build`
npm run deploy   # Use gh-pages to push a second github.io branch to the repository
```
~~In addition `npm install` is now hooked with `npm run dist`. You can count on the dist script to run when you run `npm install` inside the package, or when you install this package from another project. In other word, the dist script automatically transpiles your package when installed.~~ (Turns out, install script is a bad idea. In my own experience, install script puts additional requirement on parent project: whoever that is going to install this package, will require installing @babel v7.x. It is better to transpile the `src` into `dist` and simply distribute that.)
As you can probably tell, everything in `src/lib` is transpiled and moved to `dist` folder for distribution. Therefore, you should write you components in `src/lib`, but still you can write react app outside of `src/lib`. The react app can import components from `src/lib` and run as usual using `npm start` and deploy as usual using `npm deploy`.

## Set up babel
```
  "babel": {
    "presets": [
      "@babel/preset-react",
      "@babel/preset-env"
    ]
  },
```
Non-standard js languages, such as jsx, or the latest ES 20xx may not be supported widely. These babel setting support transpiling jsx and ES2015 (as of 2019, ES2015 transpiling is enabled by preset-env).
* Note, unlike babel v6.x, babel v7.x deprecated state-x. This is likely because writing state-0 JS code is no longer a "cool" thing. So, stop writing state-0 JS code if possible.

## Writing the component(s)
Well, have fun developing your components. You can still test your react component by `npm start`.

## Deploying on github
Simply:
```
npm deploy
```
