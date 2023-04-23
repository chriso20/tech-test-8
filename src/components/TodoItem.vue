<template>
  <div @click="toggleCompleted">
    <input type="checkbox" v-model="completed" @change="toggleCompleted">
    <span :class="{ completed }">{{ todo.title }}</span>
  </div>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      completed: this.todo.completed,
    };
  },
  methods: {
    toggleCompleted() {
      this.completed = !this.completed
      this.$emit('toggleCompleted', this.todo.id);
    },
  },
};
</script>