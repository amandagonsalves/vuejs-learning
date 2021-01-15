<template>
  <div>
    <h1>Lista de tarefas</h1>
    <button @click="handleShowHideList">Ver lista</button>
    <input v-focus v-model="state.currentTask" @keyup.enter="handleAdd" />
    <button @click="handleAdd">Adicionar</button>

    <table v-if="state.showList">
      <thead>
        <tr>
          <th>Título</th>
          <th>Feita</th>
        </tr>
      </thead>

      <tbody>
        <tr
          v-for="(task, index) in state.tasks"
          :key="`${task}-${index}`"
          @dblclick="complete(task)"
          class="task-item"
        >
          <td
            :class="{
              line: task.isDone,
            }"
          >
            {{ task.title }}
          </td>

          <td>{{ task.isDone ? "Sim" : "Não" }}</td>
          <button @click="handleRemove(task)">&times;</button>
        </tr>
      </tbody>
    </table>

    <p v-else>Lista de tarefas escondida</p>
  </div>
</template>

<script>
import { reactive } from "vue";

const focus = {
  inserted: (el) => {
    el.focus();
  },
};

// VUE 3
export default {
  directives: {
    focus,
  },
  setup() {
    const state = reactive({
      currentTask: "",
      showList: false,
      tasks: [
        {
          title: "Fazer um curso",
          isDone: true,
        },
        {
          title: "Fazer comida",
          isDone: false,
        },
      ],
    });

    function handleAdd() {
      state.tasks.push({
        title: state.currentTask,
        isDone: false,
      });

      state.currentTask = "";
    }

    function handleShowHideList() {
      state.showList = !state.showList;
    }

    function complete(task) {
      state.tasks = state.tasks.map((t) => {
        if (t.title === task.title) {
          console.log(t.title);
          return { ...t, isDone: !t.isDone };
        }

        return { ...t };
      });

      console.log(state.tasks);
    }

    function handleRemove(task) {
      state.tasks = state.tasks.filter((t) => t.title != task.title);
    }

    return {
      state,
      handleAdd,
      handleShowHideList,
      handleRemove,
      complete
    };
  },
};

// VUE 2
// export default {
//   directives: {
//     focus,
//   },
//   data: () => ({
//     currentTask: "",
//     showList: false,
//     tasks: [
//       {
//         title: "Fazer um curso",
//         isDone: true,
//       },
//       {
//         title: "Fazer comida",
//         isDone: false,
//       },
//     ],
//   }),
//   methods: {
//     handleAdd() {
//       this.tasks.push({
//         title: this.currentTask,
//         isDone: false,
//       });

//       this.currentTask = "";
//     },
//     handleShowHideList() {
//       this.showList = !this.showList;
//     },
//     complete(task) {
//       this.tasks = this.tasks.map((t) => {
//         if (t.title === task.title) {
//           console.log(t.title);
//           return { ...t, isDone: !t.isDone };
//         }

//         return { ...t };
//       });

//       console.log(this.tasks);
//     },
//     handleRemove(task) {
//       this.tasks = this.tasks.filter((t) => t.title != task.title);
//     },
//   },
// };
</script>

<style scoped>
table {
  text-align: center;
  width: 100%;
}

td,
th {
  padding: 0.3rem;
}

.line {
  text-decoration: line-through;
}

.task-item {
  cursor: pointer;
}
</style>