<template>
  <div class="container">
     <ul class="memo-list">
       <!-- メモ一覧 -->
     </ul>
    <button @click="toggleEditForm">＋</button>

    <div v-if="showEditForm">
      <EditForm />
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
      showEditForm: false
    }
  },
  methods: {
    toggleEditForm() {
      this.showEditForm = !this.showEditForm
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
