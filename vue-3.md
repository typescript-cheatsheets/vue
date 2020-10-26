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

## Composition API

### Refs

Vue can infer the type of your `ref`'s but if you need to represent some more complex types you can do so with generics:

```ts
import {ref} from "vue"

interface PersonInfo { 
  firstName: string,
  surname: string,
  age: number
}

const people = ref<PersonInfo[]>([])

```

Alternatively you can use casting with `as`. This should be used if the type is unknown. Consider this example where we create a composition wrapper function around `fetch` and we dont know the data structure that will be returned.

```ts

import { ref, Ref } from "vue";

type ApiRequest = () => Promise<void>;

// When using this function we can supply the type via generics
export function useAPI<T>(url: RequestInfo, options?: RequestInit) {
  
  const response = ref() as Ref<T>;  // 👈 note we're typing our ref using `as`

  const request: ApiRequest = async () => {
    const resp = await fetch(url, options);
    const data = await resp.json();
    response.value = data;
  };

  return { response, request };
}

```