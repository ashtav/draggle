<template>
  <div draggable="true" @transitionStart="transitionStart" @transitionEnd="transitionEnd"
    @dragover.prevent.stop="onDragOver" @dragstart.stop="onDragStart" @dragend.stop="onDragEnd" @dragenter.prevent
    ref="draggableItemEl" :class="{ isDragging }">
    <slot></slot>
  </div>
</template>

<script lang="ts">
import { toRefs } from "vue";
import { useDraggleItem } from "../composables/draggle";

export default {
  name: "DraggleItem",
  props: {
    item: Object,
    items: Array<any>,
    position: Number,
    containerId: Number
  },
  setup(props, context) {
    const { item, items, position, containerId } = toRefs<any>(props);
    const {
      draggableItemEl,
      isDragging,
      onDragStart,
      onDragOver,
      onDragEnd,
      transitionStart,
      transitionEnd
    } = useDraggleItem(item, items, position, containerId, context);

    return {
      draggableItemEl,
      isDragging,
      onDragStart,
      onDragOver,
      onDragEnd,
      transitionStart,
      transitionEnd
    };
  }
};
</script>

<style scoped>
.isDragging {
  opacity: 0.4;
}
</style>
