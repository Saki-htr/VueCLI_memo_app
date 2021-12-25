fetchStorage()
<template>
  <div class="form">
    <textarea class="edit-memo" v-model="tempMemo" required></textarea>
    <button @click="addMemo">保存</button>
    <button>削除</button>

    <!-- デバッグ用 -->
    <p>memoList: {{ memoList }}</p>
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
    this.memoList = JSON.parse(localStorage.getItem(this.STORAGE_KEY) || '[]')
    this.$emit('giveMemoList',this.memoList)
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
      this.memoList.push({ id: Math.random().toString(),title: this.tempMemo.split('\n')[0], content: this.tempMemo })
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
