<template>
  <div class="container">
    <div v-for="user in users" :key="user.id">{{user.id}}.{{user.name}}</div>
  </div>
</template>

<script>
import axios from "axios";
//テスト用のwebAPI
const url = "https://jsonplaceholder.typicode.com/users";

export default {
  //Nuxtの非同期通信メソッド。コンポーネントの初期化、ページ遷移、SSR時に実行
  asyncData({ params, error }) {
    return axios
      .get(url)
      .then(res => {
        return { users: res.data };
      })
      .catch(e => {
        //Nuxtのエラーメソッド。エラーページを表示。引数に渡すオブジェクトのプロパティはHTTPのステータスコードもしくはエラーメッセージ
        error({ users: e.response.status, message: e.message });
      });
  }
};
</script>

<style>
</style>
