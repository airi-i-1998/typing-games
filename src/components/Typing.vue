<script setup>
import { ref, onMounted } from 'vue';

const RANDOM_SENTENCE_URL_API = "https://api.quotable.io/random";

onMounted(() => {
  const typeDisplay = document.getElementById("typeDisplay");
  console.log(document.getElementById("typeDisplay"));
});

/* 非同期でランダムな文章を取得　*/
// データをAPIで取得する際は、データ取得までに時間がかかるため、非同期処理で行う！
function getRandomSentence(){

  // fetch関数：Web APIかつHTTPリクエストを行うための機能を提供。また、非同期処理を行う関数→fetch自体がPromiseオブジェクトを返す。
  return fetch(RANDOM_SENTENCE_URL_API)

  // then.()：Promiseパターンにおいて非同期操作が完了した後に実行されるコールバック関数を指定するメソッド。
  .then((response) => response.json())
  .then((data) => data.content);
}

/* ランダムな文章を取得して表示する　*/
// 非同期処理のデータを取得する際　async ~ await
async function renderNextSentence(){
  const sentence = await getRandomSentence();
  typeDisplay.innerText = sentence;
}

renderNextSentence();


</script>

<template>
  <div class="container">
    <div class="type-display" id="typeDisplay"></div>
    <textarea class="type-input" autofocus id="typeInput">type</textarea>
  </div>
</template>

<style scoped>
.container {
  background-color: #33CCFF;
  /* rem(root em):HTML要素のフォントサイズに対する倍率のこと。 */
  /* 通常ブラウザはデフォルトで16pxを使用している。
  その場合、font-size: 2.4rem; は 2.4 * 16px = 38.4px に相当 */
  font-size: 2.4rem;
  font-weight: 600;
  padding: 4rem;
  border-radius: 0.5rem;
  width: 1000px;
  min-height: 600px;
  max-width: 90%;
  box-shadow: 1px 5px 6px rgb(80, 80, 80);
}

.container,
.type-input {
  margin-top: 4rem;
  font-size: 3rem;
}

.type-display {
  margin-bottom: 1rem;
  margin-left: 1rem;
}

.type-input {
  /* 背景を透明にする */
  background: transparent;
  border: 2px solid;
  /* 余白無効化 */
  outline: none;
  width: 100%;
  height: 14rem;
  /* margin: auto; */
  resize: none;
  padding: 0.5rem 1rem;
  border-radius: 0.5rem;
  font-size: 40px;
}

.type-input:focus {
  border: 4px solid white;
}
</style>
