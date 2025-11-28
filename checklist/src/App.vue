<template>
  <div class="container">
    <h2>Список дел</h2>
    <input
      v-model="newTask"
      @keyup.enter="addTask()"
      placeholder="Добавьте задачу и нажмите Enter"
    />
    <ul>
      <TodoItem
        v-for="(task, index) in tasks"
        :key="index"
        :task="task"
        @toggle="toggleTask(task)"
        @remove="removeTask(index)"
        @edit="editTask(task)"
        @save="saveTask(task)"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from './components/ToDoItem.vue'

export default{
  components: {TodoItem},
  data(){
    return{
      tasks: [],
      newTask: '',
      text: ''
      // done: Boolean,
      // editing: Boolean
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.tasks.push({
        text: this.newTask.trim(),
        done: false,
        editing: false
        })
    newTask.value = ''
      }
    },
  removeTask(index) {
    this.tasks.splice(index, 1)
  },
    editTask(task) {
    task.editing = true
    },
    saveTask(task) {
  task.text = task.text.trim()
  task.editing = false
  },
  toggleTask(task) {
  task.done = !task.done
  }
  }
}

const addTask = () => {
  if (newTask.value.trim()) {
    tasks.value.push({
      text: newTask.value.trim(),
      done: false,
      editing: false
    })
    newTask.value = ''
  }
}

const toggleTask = (task) => {
  task.done = !task.done
}

const removeTask = (index) => {
  tasks.value.splice(index, 1)
}

const editTask = (task) => {
  task.editing = true
}

const saveTask = (task) => {
  task.text = task.text.trim()
  task.editing = false
}
</script>

<style scoped>
.container {
  background: #fbdeef;
  padding: 20px;
  border-bottom-left-radius: 12px;
  border-bottom-right-radius: 12px;
  /* width: 340px; */
  box-shadow: 0 3px 8px #60143f;
  text-align: center;
}
.container input {
  background: transparent;
  width: 100%;
  padding: 8px;
  border-radius: 8px;
  margin: 1px;
  margin-bottom: 10px;
  border: 0;
  outline: none;
  color: #60143f;
}

.container input:focus {
 border-bottom: 2px solid #fab4dc;
}

::placeholder {
  color: #60143f82;
  font-style: italic;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
h2{
  text-align: center;
  color: #60143f;
  font-size: 30px;
}

</style>
