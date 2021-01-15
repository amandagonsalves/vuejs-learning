<template>
  <div>
    <h1>Lista de tarefas</h1>
    <button @click="handleShowHideList">Ver lista</button>
    <input v-focus>
    <table v-if="showList">
      <thead>
        <tr>
          <th>Título</th>
          <th>Feita</th>
        </tr>
      </thead>

      <tbody>
        <tr 
          v-for="(task, index) in tasks" 
          :key="`${task}-${index}`"
          @dblclick="complete(task)">

          <td 
          :class="{
            'line': task.isDone
          }">
            {{ task.title }}
          </td>
          
          <td>{{ task.isDone ? 'Sim' : 'Não' }}</td>
          <button @click="handleRemove(task)">&times;</button>
        </tr>
      </tbody>

    </table>

    <p v-else>Lista de tarefas escondida</p>
  </div>
</template>

<script>
const focus = {
  inserted: (el) => {
    el.focus();
  }
}

export default {
  directives: {
    focus
  },
  data: () => ({
    showList: false,
    tasks:[
      {
        title: 'Fazer um curso',
        isDone: true
      },
      {
        title: 'Fazer comida',
        isDone: false
      }
    ]
  }),
  methods: {
    handleShowHideList() {
      this.showList = !this.showList;
    },
    complete(task) {
      this.tasks = this.tasks.map(t => {
        if (t.title === task.title) {
          console.log(t.title)
          return { ...t, isDone: !t.isDone }
        }

        return { ...t };
      })

      console.log(this.tasks)
    },
    handleRemove(task) {
      this.tasks = this.tasks.filter(t => t.title != task.title);
    }
  }
}
</script>

<style scoped>
  table {
    text-align: center;
    width:100%
  }

  td, th {
    padding: .3rem;
  }

  .line {
    text-decoration: line-through;
  }
</style>