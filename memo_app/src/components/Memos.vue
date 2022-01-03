<template>
  <div class="container">
    <h1>My Memos</h1>
      <ul class="memo-list">
        <li class="memo" v-for="(memo,index) in memoList" :key="memo.id">
          <div class="view">
            <label @click="editMemo(memo, index)">{{ memoTitle(memo.content) }}</label>
          </div>
        </li>
      </ul>
     <button class="add-button" @click="showAddForm">＋</button>
    <div v-if="showFormToggle">
      <div v-if="formMode === 'add'">
        <h2>Add Memo</h2>
          <textarea v-model="tempMemo" required></textarea>
          <div class="form-button">
            <button class="common-button" @click="addMemo">save</button>
            <button class="common-button" @click="cancelAdd">remove</button>
          </div>
      </div>
      <div v-else-if="formMode === 'edit'">
        <h2>Edit Memo</h2>
        <textarea v-model="editedMemo"></textarea>
        <div class="form-button">
          <button class="common-button" @click="doneEdit(editIndex)">update</button>
          <button class="common-button" @click="removeMemo(editIndex)">remove</button>
        </div>
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
  },
  computed: {
    memoTitle: () => (content) => {
      return content.split('\n')[0]
  }
}
}
</script>

<style>
.container{
  font-family: cursive;
  color: #73586F;
}

textarea {
  width: 250px;
  height: 7em;
  color: #73586F;
  background-color: #FFF9EE;
  border-radius: 5px;
  border: 2px solid #b1b5e6;
  font-family: cursive;
  font-weight: bold;
}

.form-button {
  text-align:center;
}

.common-button {
  border: none;
  background-color:#cccff3;
  margin-top: 10px;
  margin-right: 10px;
  border-radius: 5px;
  font-family: cursive;
  font-size: 17px;
  padding :3px 15px;;
}

.add-button {
  border: none;
  background-color:#F0C0C3;
  border-radius: 5px;
  padding: 5px 10px;
  font-family: cursive;
}

h1 {
  color: #EF858C;
}

h2 {
  color: #8D93C8;
}

.memo-list{
  list-style: none;
  padding-left: 0px;
  font-size: 20px;

}


.memo:hover {
  font-weight: bold;
  font-size: 23px;
}
</style>
