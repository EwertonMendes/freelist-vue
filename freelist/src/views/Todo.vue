<template>
  <div class="home">
    <v-text-field v-model="newTaskTitle" @click:append="addTask" @keyup.enter="addTask" clearable label="New task" append-icon="mdi-plus" class="pa-3" hide-details>

    </v-text-field>
    <v-list two-line flat class="pt-0">
      <div v-for="task in tasks" :key="task.id">
        <v-list-item @click="doneTask(task.id)" :class="{'blue lighten-4': task.done}">
          <v-list-item-action>
            <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title :class="{'text-decoration-line-through' : task.done}">
              {{task.title}}
            </v-list-item-title>
            <v-list-item-subtitle>{{task.description}}</v-list-item-subtitle>
          </v-list-item-content>
          <v-list-item-action>
            <v-btn icon>
              <v-icon color="red lighten-1" @click.stop="deleteTask(task.id)">mdi-delete</v-icon>
            </v-btn>
          </v-list-item-action>
        </v-list-item>
        <v-divider></v-divider>
      </div>


    </v-list>
  </div>
</template>

<script>
  export default {
    name: 'Home',
    data() {
      return {
        newTaskTitle: '',
        tasks: []
      }
    },
    methods: {
      doneTask(id) {
        let task = this.tasks.filter(task => task.id === id)[0]
        task.done = !task.done
      },
      deleteTask(id) {
        this.tasks = this.tasks.filter(task => task.id !== id)
      },
      addTask(){
        let newTask = {
          id: Date.now(),
          title: this.newTaskTitle,
          done: false
        }
        this.tasks.push(newTask)
        this.newTaskTitle = ''
      }
    }
  }
</script>