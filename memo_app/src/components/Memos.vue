<template>
  <div class="container">
    <h1>My Memos</h1>
      <ul class="memo-list">
        <li class="memo" v-for="(memo,index) in memoList" :key="memo.id">
          <div class="view">
            <label @click="editMemo(memo, index)">{{memo.content.split('\n')[0]}}</label>
          </div>
        </li>
      </ul>
     <button @click="showAddForm">＋</button>

    <div v-if="showFormToggle">
      <div v-if="formMode === 'add'">
        <h2>Add Memo</h2>
        <textarea v-model="tempMemo" required></textarea>
        <button @click="addMemo">save</button>
        <button @click="cancelAdd">remove</button>
      </div>
      <div v-else-if="formMode === 'edit'">
        <h2>Edit Memo</h2>
        <textarea v-model="editedMemo"></textarea>
        <button @click="doneEdit(editIndex)">update</button>
        <button @click="removeMemo(editIndex)">remove</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return{
      tempMemo: '',
      STORAGE_KEY: 'memos-vuejs-3.0',
      memoList: [],
      showFormToggle: false,
      formMode: null,
      editedMemo: null,
      editIndex: null
    }
  },
  mounted() {
    this.memoList = JSON.parse(localStorage.getItem(this.STORAGE_KEY) || '[]')
  },
  methods: {
    saveList() {
      localStorage.setItem(this.STORAGE_KEY, JSON.stringify(this.memoList))
    },
    addMemo() {
      const value = this.tempMemo && this.tempMemo.trim()
      if (!value) {
        return
      }
      this.memoList.push({ id: Math.random().toString(), content: this.tempMemo })
      console.log(this.memoList)
      this.tempMemo = ''
      this.saveList();
      this.showFormToggle = false
    },
    showAddForm() {
      this.showFormToggle = !this.showFormToggle
      this.formMode = 'add'
    },
    editMemo(memo, index){
      this.showFormToggle = !this.showFormToggle
      this.formMode = 'edit'
      this.editIndex = index
      this.editedMemo = memo.content
    },
    doneEdit(index){
      this.memoList[index].content = this.editedMemo
      this.saveList()
      this.editedMemo = ''
      this.editedIndex = ''
      this.showFormToggle = !this.showFormToggle
    },
    removeMemo (index){
      this.memoList.splice(index,1)
      this.saveList()
      this.showFormToggle = !this.showFormToggle
    },
    cancelAdd() {
      this.tempMemo = ''
      this.showFormToggle = false
    }
  }
}
</script>

<style>
textarea {
  /* width: 200px;
  height: 5em; */
}

ul {
  list-style: none;
}

</style>
