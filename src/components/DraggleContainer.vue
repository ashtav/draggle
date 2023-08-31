<template>
  <transition-group name="draggle-item-list" :tag="tag" :class="parentClass" @dragover.prevent.stop="onDragOver">
    <draggle-item v-for="(item, index) in items" :key="item.id" :item="item" :items="items" :containerId="id"
      :position="index" :tagChild="tagChild" :class="childClass" @itemDragOver="onItemDragOver" @dragenter.prevent
      @change="onItemChange">
      <slot name="item" :item="item.data" :i="index"></slot>
    </draggle-item>
  </transition-group>
</template>

<script lang="ts">
import { toRefs } from "vue";
import { useDraggleContainer } from "../composables/draggle";
import DraggleItem from "./DraggleItem.vue";

export default {
  name: "Draggle",
  components: {
    DraggleItem
  },

  props: {
    modelValue: Array,

    transition: {
      default: "0",
      type: String
    },

    tag: {
      default: "div",
      type: String
    },

    tagChild: {
      default: "div",
      type: String
    },

    parentClass: {
      default: "",
      type: String
    },

    childClass: {
      default: "",
      type: String
    }
  },

  setup(props, context) {
    const { modelValue } = toRefs<any>(props);
    const {
      id,
      items,
      onDragOver,
      onItemDragOver,
    } = useDraggleContainer(modelValue, context);

    return { id, items, onDragOver, onItemDragOver };
  },

  computed: {
    transitionStyle() {
      return `transform ${this.transition}ms`;
    }
  },

  methods: {
    onItemChange(data: any) {
      this.$emit('change', data)
    }
  }
};
</script>

<style scoped>
.draggle-item-list-move {
  transition: v-bind(transitionStyle);
}
</style>
