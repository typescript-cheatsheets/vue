# Class Components

## Overview

[Vue Class Components](https://class-component.vuejs.org/) offers an alternative class-style syntax for Vue components which integrates well with TypeScript.

To have consistent support for decorators in your Vue components, it's also recommended to install [vue-property-decorator](https://github.com/kaorun343/vue-property-decorator).


To get started with both libraries in your existing Vue project, run: 
```
npm install vue-class-component vue-property-decorator
```

You only need to import `vue-property-decorator` into your `.vue` file as it extends `vue-class-component`. 

You can now write TS in your components like this:

```vue
<template>
  <div>
    {{ count }}
    <button v-on:click="increment">+</button>
    <button v-on:click="decrement">-</button>
    {{ computedValue }}
  </div>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";

@Component
export default class Hello extends Vue {

  count: number = 0
  vue: string = "vue"
  ts: string = "ts"

  // Lifecycle methods can be accessed like this
  mounted() {
    console.log('component mounted')
  }

  // Method are component methods
  increment(): void {
    this.count++
  }

  decrement(): void {
    this.count--
  }

  // Computed values are getters
  get computedValue(): string {
    return `${vue} and ${ts} rocks!`
  }
}
</script>
```
See the [full guide for Vue Class Components](https://class-component.vuejs.org/guide/class-component.html#data).

> _Class components should not confused with the now abandoned [Class API proposal](https://github.com/vuejs/rfcs/pull/17#issuecomment-494242121)._

## Props
You can use the `Prop` decorator to annoate your prop types like so:

```ts
<script lang="ts">
import { Vue, Component, Prop } from "vue-property-decorator";

interface PersonInfo { 
  firstName: string,
  surname: string,
  age: number
}

@Component
export default class InfoCard extends Vue {
  @Prop() readonly info!: PersonInfo;
  @Prop({ default: false }) readonly admin?: boolean;
}
</script>
```
Is equivalent to:

```ts
import Vue from "vue-property-decorator";
import Vue, { PropType } from 'vue'

interface PersonInfo {
  firstName: string,
  surname: string,
  age: number
}
export default {
  props: {
    info: {
      type: Object as PropType<PersonInfo>,
      required: true
    },
    admin: {
      type: Boolean,
      default: false
    }
  },
}

```