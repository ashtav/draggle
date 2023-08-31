<template>
  <div class="container my-5">
    <div class="row">
      <div class="col-lg-4">
        <div class="card">
          <div class="card-header">
            <h3 class="card-title">Daily Tasks</h3>
          </div>
          <draggle v-model="todos" transition="100" parent-class="list-group list-group-flush" @change="onChange"
            child-class="list-group-item list-group-item-action cursor-pointer">
            <template v-slot:item="{ item }">
              {{ item.title }}
            </template>
          </draggle>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Draggle from "./components/DraggleContainer.vue";

export default {
  name: "App",
  components: {
    Draggle
  },

  data() {
    return {
      todos: [
        { id: 1, title: "Do the dishes" },
        { id: 2, title: "Take out the trash" },
        { id: 3, title: "Mow the lawn" },
        { id: 4, title: "Clean the house" },
        { id: 5, title: "Wash the car" }
      ]
    };
  },

  methods: {
    onChange(data: any) {
      console.log(data);
    }
  }
};
</script>