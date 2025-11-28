<template>
  <li :class="{ done: task.done }">
    <template v-if="task.editing">
      <input
        v-model="task.text"
        @keyup.enter="$emit('save')"
        @blur="$emit('save')"
        autofocus
      />
      <button class="save" @click="$emit('save')">
        <img src="@/assets/icons/disketa.svg" width="15" height="15"/>
      </button>
    </template>
    <template v-else>
      <span @click="$emit('toggle')">{{ task.text }}</span>
      <div>
        <button class="edit" @click="$emit('edit')">
          <img src="@/assets/icons/pencil.svg" width="15" height="15"/>
        </button>
        <button class="delete" @click="$emit('remove')">
          <img src="@/assets/icons/trash.svg" width="15" height="15"/>
        </button>
      </div>
    </template>
  </li>
</template>

<script>
export default{
  props: {
    task:{
      type: Object,
      required: true
    },
    key: {
      type: Number,
      required: true
    }
  }
}
</script>

<style scoped>
li {
  display: flex;
  justify-content: space-between;
  align-items: left;
  padding: 8px;
  margin: 8px;
  border-radius: 8px;
  /* border-bottom: 1px solid #fab4dc; */
  color: #60143f;
  text-align: left;
}

li:hover {
  border-bottom: 1px solid #fab4dc;
  color: #60143f;
  background: #fab4dc;
}

li.done span {
  text-decoration: line-through;
  color: gray;
}
span {
  flex-grow: 1;
  cursor: pointer;
}
button {
  margin-left: 5px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  padding: 4px 8px;
  color: white;
}
button.delete {
  background: #ff6666;
}
button.edit {
  background: #4a90e2;
}
button.save {
  background: #34c759;
}
input {
  background: transparent;
  width: 100%;
  border-radius: 8px;
  border: 0;
  outline: none;
  color: #60143f;
}
</style>
