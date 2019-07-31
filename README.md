### Vuetify and SCSS

Vue CLI 3.9.3

Vuetify 2.0.3

### Solution

The solution is the highest rated answer to this [stackoverflow question](https://stackoverflow.com/questions/32236443/mocha-testing-failed-due-to-css-in-webpack):

```
npm install --save-dev ignore-styles
```   

and then edit package.json:

```
"test:unit": "vue-cli-service test:unit mocha --require ignore-styles"
```

Unit tests fail with errors similar to this one:

```
Error in ./node_modules/vuetify/src/components/VResponsive/VResponsive.sass

  Module build failed (from ./node_modules/sass-loader/lib/loader.js):
  Expected ";".
    ╷
  1 │ @import './settings/_index'
    │                            ^
    ╵
    Users/Ken/Projects/vue-scss/node_modules/vuetify/src/styles/styles.sass 1:28  @import
    Users/Ken/Projects/vue-scss/src/sass/main.scss 1:9                            @import
    stdin 1:9                                                                     root stylesheet
        in http:/localhost/Users/Ken/Projects/vue-scss/node_modules/vuetify/src/styles/styles.sass (line 1, column 28)

```

### Steps to Reproduce Errors

```
git clone https://github.com/kensiprell/vuetify-scss.git  

npm install

npm run test:unit
```   

### Steps to Create App 

I created a new Vue CLI (v3.9.3) app using this preset:

```
"useConfigFiles": true,
"plugins": {
  "@vue/cli-plugin-typescript": {
    "classComponent": true,
    "tsLint": true,
    "lintOn": []
  },
  "@vue/cli-plugin-unit-mocha": {},
  "@vue/cli-plugin-e2e-cypress": {}
},
"router": true,
"routerHistoryMode": true,
"vuex": true,
"cssPreprocessor": "node-sass"
```

Then I followed these [instructions](https://vuetifyjs.com/en/customization/sass-variables) to add support for SASS/SCSS.


