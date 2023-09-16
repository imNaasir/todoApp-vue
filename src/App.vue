<template>
  <div class="flex flex-col  items-center my-10 min-h-screen w-screen">
    <h1 class="text-3xl">Welcome to todo app</h1>
    <div class="md:w-1/2 w-full max-md:p-4">
      <form action="" @submit.prevent="addTodo" class="my-4 w-full flex flex-col gap-5">
        <input type="text" placeholder="add something" v-model="newTodo" name="newTodo"
          class="w-full py-2 border-2 border-gray-400 rounded-md px-2">
        <button type="submit" class="w-full bg-gray-200 py-2 rounded-md">Add</button>
      </form>

      <button v-if="all_Done" type="submit" @click="allDone" class=" w-full bg-gray-200 py-2 rounded-md mb-6">All
        Done</button>

      <ul v-for="todo in todos" :key="todo.title" class="my-2">

        <li class="flex flex-col  gap-2 text-2xl">
          <div class="flex items-center justify-between gap-2">
            <span class="flex items-center gap-2">
              <input type="checkbox" name="" id="" v-model="todo.done" class="w-5 h-5">
              <span :class="{ 'line-through': todo.done }">{{ todo.title }}</span>
            </span>
            <span>
              <button @click="remove(todo)" class="w-auto px-4 text-sm bg-gray-200 py-1 rounded-md">remove</button>
            </span>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      all_Done: false,
      newTodo: '',
      todos: [],

    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.length === 0) {
        this.all_Done = false;
        return
      } else {
        this.all_Done = true
        this.todos.push({
          title: this.newTodo,
          done: false
        });
        this.newTodo = null
        // console.log(this.todos);
      }
    },
    remove(todo) {
      const todoIndex = this.todos.indexOf(todo);

      this.todos.splice(todoIndex, 1)
    },
    allDone() {
      this.todos.forEach(todo => {
        todo.done = true;
      });
    }
  },
}
</script>

<style lang="scss" scoped></style>