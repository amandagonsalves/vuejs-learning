<template>
  <div>
    <h1>Lista de tarefas</h1>
    <button @click="() => showList = !showList">Ver lista</button>
    <input v-focus>
    <table v-if="showList">
      <thead>
        <tr>
          <th>Título</th>
          <th>Feita</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="(task, index) in tasks" :key="`${task}-${index}`">
          <td>{{ task.title }}</td>
          <td>{{ task.isDone ? 'Sim' : 'Não' }}</td>
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
  })
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
</style>