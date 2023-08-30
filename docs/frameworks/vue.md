# Vue

## Persistent Components

### Application Root Components

You can create a vue application who's root component's state is automatically bound to a scope you specify:

```js
import { vuePeristentComponent } from '@knowlearning/agents'
import myComponent from './my-component-file.vue'

const id = 'uuid-or-name-of-scope-to-bind-to-component-data'
const root = vuePersistentComponent(myComponent, id)

const app = createApp(root)
app.mount()
```

Now all state updates to that component will be persisted, and the most recent state will be re-attached to on every reload.

### Child Components

A persistent component does not have to be used as the application root. You are free to make any component in your app a persistent component:

Now you are free to use that component in your template as usual:

```html
<template>
  <div>
    <h1>Cool persistent component!</h1>
    <anyNameForMyPersistentComponent :importantProp="42">
  </div>
</template>

<script>
  import { vuePeristentComponent } from '@knowlearning/agents'
  import myComponent from './my-component-file.vue'

  const id = 'uuid-or-name-of-scope-to-bind-to-component-data'
  export default {
    components: {
      anyNameForMyPersistentComponent: vuePeristentComponent(myComponent, id)
    }
  }
</script>
```
