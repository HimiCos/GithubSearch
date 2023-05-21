<template>
  <div class="row">
    <!-- 展示用戶列表 -->
    <div v-show="info.users.length" class="card" v-for="u in info.users" :key="u.id">
      <a :href="u.html_url" target="_blank">
        <img :src="u.avatar_url" style='width: 100px'/>
      </a>
      <p class="card-text">{{u.login}}</p>
    </div>
    <!-- 展示歡迎詞 -->
    <h1 v-show="info.isFirst">歡迎使用～</h1>
    <!-- 正在搜索 -->
    <h1 v-show="info.isLoading">加載中....</h1>
    <!-- 搜索出錯 -->
    <h1 v-show="info.errMsg">{{info.errMsg}}</h1>
  </div>
</template>

<script>
  export default {
    name: "ComList",
    data() {
      return {
        info:{
          isFirst: true,
          isLoading: false,
          errMsg: '',
          users: []
        }
      }
    },
    mounted() {
      this.$bus.$on('updateListData', (dataObj) => {
        this.info = {...this.info, ...dataObj}
      })
    },
  }
</script>

<style scoped>
  .album {
    min-height: 50rem; /* Can be removed; just added for demo purposes */
    padding-top: 3rem;
    padding-bottom: 3rem;
    background-color: #f7f7f7;
  }
  .card {
    float: left;
    width: 32%;
    padding: 0.75rem;
    border: 1px solid #efefef;
    text-align: center;
    border-radius: 20px;
    margin: 4px auto;
  }
  img {
    margin-bottom: .75rem;
    border-radius: 100px;
  }
  .card-text {
    font-size: 85%;
  }
</style>