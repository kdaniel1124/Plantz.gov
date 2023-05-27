# Purpose
The purpose of this document is to list instructions for how to install and run this app. Packages in Node change very frequently and it is important to stay on top of vulnerabilities as much as possible. When building the app, `npm` will mention vulnerabilities if it finds them. Oftentimes there will be some workaround to resolve them, but it will take some Googling and a lot of patience. As we encounter errors, read them carefully as to not break something that has core functionality to the app.

# References
- [Creating a React app in AWS](https://aws.amazon.com/getting-started/hands-on/build-react-app-amplify-graphql/module-one/?e=gs2020&p=build-a-react-app-intro)
- [MERN Stack Tutorial](https://www.mongodb.com/languages/mern-stack-tutorial)

# Install
### Create the app (don't need to do this again)
#npx create-react-app amplifyapp

## 1. Install dependencies
```
# MERN stack
npm install mongodb express cors dotenv

# Navbar functionality
npm install react-router-dom
npm install --save styled-components
npm install react-icons
```

## 2. Fix vulnerabilities
For react-scripts, npm audit says to downgrade -- but according to [this thread](https://github.com/facebook/create-react-app/issues/12132), you can install a non-vulnerable version of an upstream dependency (@svgr/webpack) 

#### npm audit before making changes
```
jack@Jacks-MacBook-Pro plantapp % npm audit
# npm audit report

nth-check  <2.0.1
Severity: high
Inefficient Regular Expression Complexity in nth-check - https://github.com/advisories/GHSA-rp65-9cf3-cjxr
fix available via `npm audit fix --force`
Will install react-scripts@2.1.3, which is a breaking change
node_modules/svgo/node_modules/nth-check
  css-select  <=3.1.0
  Depends on vulnerable versions of nth-check
  node_modules/svgo/node_modules/css-select
    svgo  1.0.0 - 1.3.2
    Depends on vulnerable versions of css-select
    node_modules/svgo
      @svgr/plugin-svgo  <=5.5.0
      Depends on vulnerable versions of svgo
      node_modules/@svgr/plugin-svgo
        @svgr/webpack  4.0.0 - 5.5.0
        Depends on vulnerable versions of @svgr/plugin-svgo
        node_modules/@svgr/webpack
          react-scripts  >=2.1.4
          Depends on vulnerable versions of @svgr/webpack
          node_modules/react-scripts

6 high severity vulnerabilities

To address all issues (including breaking changes), run:
  npm audit fix --force
```

When fixing this vulnerability, a version conflict occurs with the `typescript` module. At the time of writing, set version to `4.9.5` to resolve this (see below).

#### Add the following to `package.json`
```
...

"devDependencies": {
    "@svgr/webpack": "^6.2.1",
    "typescript": "4.9.5"
  },
  "overrides": {
    "@svgr/webpack": "$@svgr/webpack"
  },
...

```

#### Remove `package.lock` and `node_modules`, then run `npm install` again
```
npm install
```

## 3. Run app
```
cd <app folder>
npm start
```

