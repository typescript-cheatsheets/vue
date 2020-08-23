# This document is for Vue-3 _specific_ syntax

### Setup Template Attribute Syntax

⚠️ This feature is still a WIP, and is an active RFC. [Follow the conversation](https://github.com/vuejs/rfcs/pull/182) to stay up to date with the lifecycle.

This provides a better DX when using the setup function in Vue SFCs.
Type inference still works, and you don't need to use `defineComponent`..
It's important to note that this is just **syntactic sugar**, and still get's compiled down to a component
using `defineComponent` and the `setup` function.

```vue
<script setup lang="ts">
import { ref } from 'vue';

export const welcome = ref('Welcome to Vue 3 with TS!');
</script>
```

`props` and the `context` object work as well.
For TS inference, declare them using TS syntax.

```vue
<script setup="props, ctx" lang="ts">
import { computed } from 'vue'

declare const props: {
    name: string
}

export const welcome = computed(() => `Welcome, ${props.name}!`)
```
