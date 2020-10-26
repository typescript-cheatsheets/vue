# Vue+TypeScript Cheatsheets

Cheatsheets for experienced Vue developers getting started with TypeScript.

-   [Vue 3 specifics](vue-3.md)
-   [Class Components & Decorators](class-components.md)

# Section 1: Setup

## Prerequisites

1. A good understanding of [Vue.js](https://vuejs.org/)
2. Read the TypeScript support section in the Vue docs [2.x](https://vuejs.org/v2/guide/typescript.html) | [3.x](https://v3.vuejs.org/guide/typescript-support.html#typescript-support)

## Vue + TypeScript Starter Kits

1. Using the [Vue CLI](https://vuejs.org/v2/guide/installation.html#CLI) , you can select the [TypeScript plugin](https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-typescript) to be setup in a new a Vue project.

```bash
# 1. Install Vue CLI, if it's not already installed
npm install --global @vue/cli

# 2. Create a new project, then choose the "Manually select features" option
vue create <my-project-name>
```

2. [Vite](https://github.com/vitejs/vite) is a new build tool by Evan You. It currently only works with Vue 3.x but supports TypeScript out-of-the-box.

> ⚠ Currently in beta. Do not use in production.

```bash
npm init vite-app <project-name>
cd <project-name>
npm install
npm run dev
```

# Section 2: Getting Started

## Recommended `ts.config` setup

> note: `strict:true` stricter inference for data properties on `this`. If you do not use it, `this` will always be treated as `any`

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

```js
<script lang='ts'>...</script>
```

In Vue 2.x you need to define components with `Vue.component` or `Vue.extend`:

```js
<script lang="ts">
import Vue from "vue";

export default Vue.extend({

  // type inference enabled
  name: "HelloWorld",
  props: {
    msg: String
  }
});
</script>
```

In Vue 3.x you can use `defineComponent` to get type inference in Vue component options

```js
import { defineComponent } from 'vue';

const Component = defineComponent({
    // type inference enabled
});
```

## Props

`PropType` can be used to annotate props with a particular object shape.

```vue
import Vue, { PropType } from 'vue'

<script lang="ts">
import Vue from "vue";

interface PersonInfo { 
  firstName: string,
  surname: string,
  age: number
}

export default Vue.extend({
  
  name: "InfoCard",
  props: {
    info: {
      type: Object as PropType<PersonInfo>,
      required: true
    }
  }
});
</script>
```

Alternatively, you can also annote your prop types with an anonymous function:

```vue
import Vue from 'vue'

<script lang="ts">
import Vue from "vue";

interface PersonInfo { 
  firstName: string,
  surname: string,
  age: number
}

export default Vue.extend({
  
  name: "InfoCard",
  props: {
    info: {
      type: Object as () => PersonInfo,
      required: true
    }
  }
});
</script>
```

## Data Properties (Options API)

You can enforce types on Vue data properties by annotating the return data object:

```ts
interface Post {
  title: string;
  contents: string;
  likes: number;
}

export default Vue.extend({
  data(): { newPost: Post } {
    return {
      newPost: {
        title: "",
        contents: "",
        likes: 0
      }
    };
  }
});
```

It might be tempting to annotate your Vue data properties using `as` like this:

```ts
interface Post {
  title: string;
  contents: string;
  likes: number;
}

export default Vue.extend({
  data() {
    return {
      newPost: {
        title: "",
        contents: "",
        likes: 0
      } as Post // ❌ Avoid doing this
    };
  }
});
```
Note that [type assertion](https://www.typescriptlang.org/docs/handbook/basic-types.html#type-assertions) like this does not provide any type safety. If for example, the `contents` property was missing in `newPost`, TypeScript would not catch this error. 

## Computed Properties (Options API)

Typing the return type for your computed properties is important especially when `this` is involved as TypeScript sometimes has trouble infering the type. 

```ts

export default Vue.extend({
  data() {
    return {
      name: 'World',
    }
  },
  computed: {
    greet(): string {  //👈 Remember to annotate your computed properties like so. 
      return 'Hello ' + this.name
    },
  }
})

```

> 


# Other Vue + TypeScript resources
- Views on Vue podcast - https://devchat.tv/views-on-vue/vov-076-typescript-tell-all-with-jack-koppa/
- Focuses a lot on class components and vue-property-decorator - https://blog.logrocket.com/how-to-write-a-vue-js-app-completely-in-typescript/
- Vue 3 Hooks and Type Safety with TypeScript - https://www.youtube.com/watch?v=aJdi-uEKYAc
