<template>
  <section class="jumbotron">
    <h3 class="jumbotron-heading">Search Github Users</h3>
    <div>
      <input type="text" placeholder="enter the name" v-model="keyWord"/>&nbsp;<button @click="searchUsers">Search</button>
    </div>
  </section>
</template>

<script>
  import axios from "axios";
  export default {
    name: "ComSearch",
    data() {
      return {
        keyWord: ''
      }
    },
    methods: {
      searchUsers() {
        // 請求前更新List數據
        this.$bus.$emit('updateListData',{isFirst: false, isLoading: true, errMsg: '', users: []})
        axios.get(`https://api.github.com/search/users?q=${this.keyWord}`).then(
          (response) => {
            // 請求成功更新List數據
            this.$bus.$emit('updateListData',{isLoading: false, errMsg: '', users: response.data.items})
          },
          (error) => {
            console.log('請求失敗', error.message);
            // 請求失敗更新List數據
            this.$bus.$emit('updateListData',{isLoading: false,errMsg: error.message, users: []})
          }
        );
      },
    }
  }
</script>

<style scoped>
  .jumbotron{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
</style>