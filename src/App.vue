<template>
  <div id="app">
    <div class="content">
      <div class="flex justify-center mb-12">
        <input
          class="w-full px-4 py-2 rounded-full"
          type="text"
          v-model="task.label"
        />
        <button
          @click="createTask"
          class="px-4 py-2 text-green-100 bg-green-600 rounded-full ml-2 outline-none"
        >
          Adicionar
        </button>
      </div>
      <div class="list">
        <ul>
          <li
            v-for="item in list"
            :key="item.id"
            class="flex items-center justify-between bg-gray-50 px-4 py-2 rounded-full"
          >
            <div class="flex items-center flex-1">
              <input
                type="checkbox"
                name="done"
                :id="item.id"
                :checked="item.done"
                @change="(e) => (item.done = e.target.checked)"
              />
              <p class="ml-4">
                {{ item.label }}
              </p>
            </div>

            <button
              @click="deleteTask(item.id)"
              class="w-8 h-8 rounded-full bg-red-400 flex justify-center items-center"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5 text-white"
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
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      task: {
        label: "",
        done: false,
      },
      list: [],
    };
  },
  methods: {
    createTask() {
      this.list.push({
        id: new Date(),
        label: this.task.label,
        done: this.task.done,
      });
    },
    deleteTask(id) {
      this.list = this.list.filter((item) => item.id !== id);
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
  justify-content: center;
  align-items: center;
}

div.content {
  width: 500px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
}
</style>
