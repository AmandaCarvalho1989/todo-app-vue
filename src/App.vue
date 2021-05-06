<template>
  <div id="app">
    <div class="w-full flex-col justify-center items-center px-32 py-24">
      <h1 class="my-4 text-2xl font-bold">Tasks: {{ list.length }}</h1>
      <div class="flex justify-center mb-6">
        <input
          class="w-full px-4 py-2 rounded-lg"
          type="text"
          v-model="task.label"
        />
        <button
          @click="createTask"
          class="px-4 py-2 text-primaryLight bg-green rounded-lg ml-2 outline-none"
        >
          Adicionar
        </button>
      </div>
      <div class="list">
        <ul>
          <li
            v-for="item in list"
            :key="item.label"
            class="flex items-center justify-between bg-gray-50 px-4 py-2 rounded-lg my-4"
          >
            <div class="flex items-center flex-1">
              <input
                type="checkbox"
                name="done"
                :id="item.id"
                :checked="item.done"
                @change="(e) => (item.done = e.target.checked)"
                class="border-1 border-gray rounded-sm"
              />
              <p class="ml-4">
                {{ item.label }}
              </p>
            </div>

            <button
              class="w-8 h-8 rounded-lg bg-red-400 flex justify-center items-center hover:bg-white "
              @click="deleteTask(item.id)"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5 text-white hover:text-red-400"
                viewBox="0 0 20 20"
                fill="currentColor"
              >
                <path
                  fill-rule="evenodd"
                  d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z"
                  clip-rule="evenodd"
                />
              </svg>
            </button>
          </li>
        </ul>
      </div>
    </div>
    <aside class="w-3/5 h-full bg-primaryLight px-32 py-16">
      <div class="h-1/2 w-full">
        <h1 class="text-xl font-bold">
          Tarefas a fazer: {{ incompletedTasks.length }}
        </h1>
        <ul>
          <li v-for="item in incompletedTasks" :key="item.label">
            {{ item.label }}
          </li>
        </ul>
      </div>
      <div class="h-1/2 w-full">
        <h1 class="text-xl font-bold">
          Tarefas feitas: {{ completedTasks.length }}
        </h1>
        <ul>
          <li v-for="item in completedTasks" :key="item.label">
            {{ item.label }}
          </li>
        </ul>
      </div>
    </aside>
  </div>
</template>

<script lang='ts'>
export default {
  name: "App",
  data() {
    return {
      task: {
        label: "",
        done: false,
      },
      hasError: false,
      list: [],
    };
  },
  methods: {
    createTask() {
      if (!this.list.find((task) => task.label === this.task.label)) {
        this.list.push({
          id: new Date(),
          label: this.task.label,
          done: this.task.done,
        });
        return (this.hasError = true);
      }
    },
    deleteTask(id) {
      console.log({ id });
      return (this.list = this.list.filter((item) => item.id !== id));
    },
  },
  computed: {
    completedTasks() {
      return this.list.filter((task) => task.done);
    },
    incompletedTasks() {
      return this.list.filter((task) => !task.done);
    },
  },
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  background-color: #f3f0ef;
  width: 100vw;
  height: 100vh;
  display: flex;
}

div.content {
}
</style>
