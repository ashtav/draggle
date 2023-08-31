# Draggle

Draggle is a powerful Vue 3 plugin that extends the capabilities of the popular vue3-draggable package, enhancing your drag-and-drop experience with a variety of additional features and customizations. With Draggle, you can effortlessly integrate advanced drag-and-drop functionality into your Vue 3 applications while benefiting from the added flexibility and control it offers.

# Features

- support v-model
- support transition
- customizable draggable component

Nested usage is currently not supported

# Installation

```
npm i draggle
```

# Try Sample

```bash
git clone https://github.com/ashtav/draggle.git

npm i
npm run serve
```

# Usage

import component:

```javascript
import Draggable from "draggle";

export default {
  components: {
    Draggable,
  },

  data(){
      return {
         todos: [ {id: 1, title: 'Learn something...'} ]
      }
  }
};
```

template:

```vue
<draggable v-model="todos" transition="100" tag="div" parent-class="list-group list-group-flush" child-class="list-group-item list-group-item-action cursor-pointer">
   <template v-slot:item="{ item }">
      {{ item.title }}
   </template>
</draggable>
```

This componet is implemented based on [v-slot](https://v3.vuejs.org/guide/component-slots.html#slots)

### Props

| Name       | Required | Type   | Description                      |
| :--------- | :------- | :----- | :------------------------------- |
| modelValue | REQUIRED | ARRAY  | v-model value, items to be bound |
| transition | OPTIONAL | STRING | transition delay in ms           |
| tag        | OPTIONAL | STRING | The HTML tag to wrap the draggable items. Default is a "div" tag.           |
| parentClass | OPTIONAL | STRING | Additional CSS classes for the parent container of the draggable items.           |
| childClass | OPTIONAL | STRING | Additional CSS classes for each individual draggable item.           |

### Events

| Name       | Data | Description                      |
| :--------- | :------- | :------------------------------- |
| change | { item: Object, from: Number, to: Number } | Emitted when the order of draggable items changes. Data includes the dragged item, its original index, and new index.
