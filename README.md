# Vue 3 + Vite + Vuetify

In this readme I show you the steps I have follow to config this proyect, in case you wish toknow how setup yours.

If you don't feel confident yet, nevermind. Clone this repo, copy your code carefully into it and then run it.

## Step 1: [Vite + Vue](https://vitejs.dev/guide/)

First, execute this command:

```
npm create vite@latest
```

Terminal ask to us to install vite, then we type 'Y' (yes). At this point we choose the following configuration:

- Project name --> [your proyect name]
- Select a framework --> Vue
- Select a variant --> Javascript
  After setup finish, we need to enter in the folder proyect and install npm dependencies, so write this:

```
  cd [your proyect name]
  npm install
  npm run dev
```

Now we had installed our Vite + Vue proyect.

## Step 2: [Vuetify](https://vuetifyjs.com/en/getting-started/installation/)

Vuetify consist in a built-in component gallery. For example, we can use pre-built cards, navbars and many more.

So we need to configure this in or existing Vite + Vue proyect.

First, install the npm depency:

```
npm i vite-plugin-vuetify
```

Great, now we only need to apply a couple changes to configure it:

Open vite.config.js located in your root directory, and add the lines I specify you below:

```javascript
//vite.config.js
import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";
import vuetify from "vite-plugin-vuetify"; //ADD

export default defineConfig({
  plugins: [vue(), vuetify({ autoImport: true })], // ADD
});
```

```javascript
//main.js
import { createApp } from "vue";
import "./style.css";
import App from "./App.vue";

// ADD FROM THIS LINE
import "vuetify/styles";
import { createVuetify } from "vuetify";
import * as components from "vuetify/components";
import * as directives from "vuetify/directives";

const vuetify = createVuetify({
  components,
  directives,
});

createApp(App).use(vuetify).mount("#app");
// TO THIS

// AND COMMENT OLD MOUNT:
// createApp(App).mount('#app')
```

And that's all. Happy coding!
