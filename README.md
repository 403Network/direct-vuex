# direct-vuex

Just Vuex with typing. Compatible with the Vue 3 composition API.

## How to use

### Install

First, add `direct-vuex` to a Vue application:

    npm install direct-vuex

### Create the store

The store is implemented in the same way as usual (ie. without typing).

A minor details anyway: It is necessary to append `as const` at the end of store and module implementation objects. It will help direct-vuex to better infer types.

Then, create the store:

    import Vue from "vue"
    import Vuex from "vuex"
    import { createDirectStore } from "direct-vuex"

    Vue.use(Vuex)

    export default createDirectStore({
      // … store implementation here …
    } as const)

The classic Vuex store is still accessible through the `store.original` property. We need it to initialize the Vue application:

    import Vue from "vue"
    import store from "./store"

    new Vue({
      store: store.original, // Inject the classic Vuex store
      // …
    }).$mount("#app")

### Use typed wrappers from outside the store

From a component, import the store.

    import store from "./store"

Then, the old way to call an action:

    store.dispatch("myModule/myAction", myPayload)

… is replaced by the following wrapper:

    store.dispatch.myModule.myAction(myPayload)

… which is fully typed.

Typed getters and mutations are accessible the same way:

    store.getters.myModule.myGetter;
    store.commit.myModule.myMutation(myPayload);

Notice: The underlying Vuex store can be used simultaneously if you wish, through the injected `this.$store` or `store.original`.

## Limitations

- Actions can't be declared with the object alternative syntax.

## Contribute

With VS Code, our recommanded plugin is:

- **TSLint** from Microsoft (`ms-vscode.vscode-typescript-tslint-plugin`)
