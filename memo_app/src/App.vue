<template>
  <div class="container">
     <ul class="memo-list">
        <li class="memo" v-for="memo in memoList" :key="memo.id">
          <div class="view">
            <label>{{memo.title}}</label>
          </div>
        </li>
     </ul>
    <button @click="toggleEditForm">＋</button>

    <div v-if="showEditForm">
      <EditForm @parentMethod="getMemoList" />
    </div>

  </div>
</template>

<script>
import EditForm from './components/EditForm.vue'

export default {
  name: 'App',
  components: { EditForm },
  data() {
    return {
      showEditForm: false,
      memoList: ''
    }
  },
  methods: {
    toggleEditForm() {
      this.showEditForm = !this.showEditForm
    },
    getMemoList(memoList) {
      this.memoList = memoList
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
