<template>
  <div class="wrapper">
    <div class="menu">
      <h2>Заметки</h2>

      <button class="add-btn" @click="createNote">+ Создать запись</button>

      <ul>
        <NoteItem
          v-for="(note, index) in notes"
          :key="index"
          :note="note"
          :active="selectedNoteIndex === index"
          @select="selectNote(index)"
          @remove="removeNote(index)"
        />
      </ul>
    </div>

    <div class="editor">
      <textarea
        v-model="currentText"
        placeholder="Выберите запись или создайте новую..."
        @input="updateNote"
      ></textarea>
    </div>
  </div>
</template>

<script>
import NoteItem from './components/NoteItem.vue'

export default {
  components: { NoteItem },

  data() {
    return {
      notes: [],              
      selectedNoteIndex: null, 
      currentText: ''         
    }
  },

  methods: {
    createNote() {
      this.notes.push({
        title: 'Новая запись',
        text: ''
      })
      this.selectNote(this.notes.length - 1)
    },

    selectNote(index) {
      this.selectedNoteIndex = index
      this.currentText = this.notes[index].text
    },

    updateNote() {
      if (this.selectedNoteIndex !== null) {
        this.notes[this.selectedNoteIndex].text = this.currentText
        this.notes[this.selectedNoteIndex].title =
          this.currentText.split('\n')[0] || 'Без названия'
      }
    },

    removeNote(index) {
      this.notes.splice(index, 1)

      if (this.selectedNoteIndex === index) {
        this.selectedNoteIndex = null
        this.currentText = ''
      }
    }
  }
}
</script>

<style scoped>
.wrapper {
  display: flex;
  width: 100%;
  height: 90vh;
  box-shadow: 0 3px 8px #60143f;
  border-radius: 12px;
  overflow: hidden;
}

.menu {
  width: 30%;
  background: #fbdeef;
  padding: 20px;
  color: #60143f;
  border-right: 2px solid #fab4dc;
}

h2 {
  text-align: center;
  margin-top: 0;
  color: #60143f;
}

.add-btn {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: none;
  border-radius: 8px;
  background: #fab4dc;
  color: #60143f;
  font-weight: bold;
  cursor: pointer;
}

.add-btn:hover {
  background: #f7c2e3;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.editor {
  flex-grow: 1;
  background: #fff0f8;
  padding: 20px;
}

textarea {
  width: 100%;
  height: 100%;
  resize: none;
  border: none;
  outline: none;
  padding: 10px;
  border-radius: 8px;
  background: #ffffff;
  box-shadow: 0 3px 8px #fab4dc;
  color: #60143f;
  font-size: 16px;
}
</style>
