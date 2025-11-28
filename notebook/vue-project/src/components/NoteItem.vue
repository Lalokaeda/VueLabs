<template>
  <li :class="{ active: active }" @click="$emit('select')">
    <span>{{ note.title }}</span>
    <button class="delete" @click.stop="$emit('remove')">
      <img src="@/assets/icons/trash.svg" width="15" height="15"/>
    </button>
  </li>
</template>

<script>
export default {
  props: {
    note: {
      type: Object,
      required: true
    },
    active: {
      type: Boolean,
      required: true
    }
  }
}
</script>

<style scoped>
li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 8px;
  margin: 6px 0;
  border-radius: 8px;
  cursor: pointer;
  color: #60143f;
}

li:hover {
  background: #fab4dc;
}

li.active {
  background: #fab4dc;
  font-weight: bold;
}

button.delete {
  background: #ff6666;
  border: none;
  border-radius: 6px;
  color: white;
  padding: 4px 8px;
  cursor: pointer;
}

button.delete:hover {
  background: #ff4d4d;
}
</style>
