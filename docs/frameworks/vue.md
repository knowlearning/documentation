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

## Embedded Content Component

You can embed other sites backed by @knowlearning/agents like so:

```html
<template>
  <div>
    <vueContentComponent
      :id="id"
      @state="handleState"
      @mutate="handleMutate"
    />
  </div>
</template>

<script>
  import { vueContentComponent } from '@knowlearning/agents'

  export default {
    components: {
      vueContentComponent
    },
    data() {
      return {
        id: "some-uuid-reference"
      }
    },
    methods: {
      handleState(event) {
        // event will contain the id that the embedded content called Agent.state(id) on
      },
      handleMutate(event) {
        // event will contain the id for a state that the embedded content has updated
      }
    }
  }
</script>
```