# Vue+TypeScript Cheatsheets

Cheatsheets for experienced Vue developers getting started with TypeScript

# Section 1: Setup

## Prerequisites

1. A good understanding of [Vue.js](https://vuejs.org/)
2. Read the TypeScript support section in the Vue docs [2.x](https://vuejs.org/v2/guide/typescript.html) | [3.x](https://v3.vuejs.org/guide/typescript-support.html#typescript-support)

## React + TypeScript Starter Kits

1. Using the [Vue CLI](https://vuejs.org/v2/guide/installation.html#CLI) , you can select the [TypeScript plugin](https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-typescript) to be setup in a new a Vue project. 

  ```bash
  # 1. Install Vue CLI, if it's not already installed
  npm install --global @vue/cli

  # 2. Create a new project, then choose the "Manually select features" option
  vue create my-project-name
  ```

2. [Vite](https://github.com/vitejs/vite) is a new build tool by Evan You. Which current only works with Vue 3.x but works with TypeScript out-of-the-box.

  > ⚠ Current in beta. Don't use in production.

  ```bash
  npm init vite-app <project-name>
  cd <project-name>
  npm install
  npm run dev
  ```

# Section 2: Getting Started

## Recommended `ts.config` setup

note: `strict:true` stricter inference for data properties on `this`. If you do not use it, `this` will always be treated as `any`
```json
// tsconfig.json
{
  "compilerOptions": {
    "target": "esnext",
    "module": "esnext",
    "strict": true,
    "moduleResolution": "node"
  }
}
```

## Usage in `.vue` files
Add `lang="ts"` to the script tag to declare TS as the `lang` used.
```vue
<script lang="ts">
  ...
</script>
```

In Vue 2.x you need  to define components with `Vue.component` or `Vue.extend`:

```vue
<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "HelloWorld",
  props: {
    msg: String
  }
});
</script>
```

In Vue 3.x you can use `defineComponent` to get type inference in Vue component options

```vue
import { defineComponent } from 'vue'

const Component = defineComponent({
  // type inference enabled
})
```

# Other Vue + TypeScript resources
- Views on Vue podcast - https://devchat.tv/views-on-vue/vov-076-typescript-tell-all-with-jack-koppa/
