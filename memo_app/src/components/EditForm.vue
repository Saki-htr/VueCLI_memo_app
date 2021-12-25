<template>
  <div class="form">
    <textarea class="edit-memo" v-model="tempMemo" required></textarea>
    <button @click="addMemo">保存</button>
    <button>削除</button>

    <!-- デバッグ用 -->
    <p>tempMemo: {{ tempMemo }}</p>
  </div>

</template>

<script>
export default {
  data() {
    return{
      tempMemo: '',
      STORAGE_KEY: 'memos-vuejs-3.0',
      memoList: []
    }
  },
  mounted() {
    this.memoList = JSON.parse(localStorage.getItem('items') || '[]')
  },
  methods: {
    saveList() {
      localStorage.setItem('memoList', JSON.stringify(this.memoList))
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
    }
  }
  // watch: {
  //   memoList: {
  //     deep: true,
  //     handler: this.saveList()
  //   }
  // }
}
</script>

<style>
textarea {
  width: 200px;
  height: 5em;
}

</style>
