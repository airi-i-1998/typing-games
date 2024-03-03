<script setup>
import { ref, onMounted } from "vue";

const RANDOM_SENTENCE_URL_API = "https://api.quotable.io/random";

onMounted(() => {
  const typeDisplay = document.getElementById("typeDisplay");
  const typeInput = document.getElementById("typeInput");
  /* 入力されたテキストが表示テキストと一致しているのか判定 */

  // typeInputにイベントを追加、入力されるinput要素を監視
  typeInput.addEventListener("input", () => {
    //sentenceArray変数：typeDisplay内のすべての<span>要素を取得
    const sentenceArray = typeDisplay.querySelectorAll("span");
    // 入力されたテキストを1文字ずつ取得
    const arrayValue = typeInput.value.split("");

    // characterSpan：<span> 要素そのもの
      // character.innerText：<span> 要素内のテキストコンテンツを取得
    sentenceArray.forEach((characterSpan, index) => {
      if (arrayValue[index] == null) {
        characterSpan.classList.remove("correct");
        characterSpan.classList.remove("incorrect");
        // characterSpanのテキストがarrayValue配列の[index]番目の要素と等しいかどうかを比較
      } else if (characterSpan.innerText == arrayValue[index]) {
        characterSpan.classList.add("correct");
        characterSpan.classList.remove("incorrect");
      } else {
        characterSpan.classList.add("incorrect");
        characterSpan.classList.remove("correct");
      }
    });
  });
});

/* 非同期でランダムな文章を取得　*/
// データをAPIで取得する際は、データ取得までに時間がかかるため、非同期処理で行う！
function getRandomSentence() {
  // fetch関数：Web APIかつHTTPリクエストを行うための機能を提供。また、非同期処理を行う関数→fetch自体がPromiseオブジェクトを返す。
  return (
    fetch(RANDOM_SENTENCE_URL_API)
      // then.()：Promiseパターンにおいて非同期操作が完了した後に実行されるコールバック関数を指定するメソッド。
      .then((response) => response.json())
      .then((data) => data.content)
  );
}

/* ランダムな文章を取得して表示する　*/
// 非同期処理のデータを取得する際　async ~ await
async function renderNextSentence() {
  const sentence = await getRandomSentence();
  typeDisplay.innerText = "";

  // 文章を一文字ずる分解して<span>を生成
  let oneText = sentence.split("");

  // forEachメソッド：配列内の各要素に対して指定された関数を実行するメソッド
  // character：forEachメソッドの仮引数
  oneText.forEach((character) => {
    // 新しい span 要素を作成
    const characterSpan = document.createElement("span");
    // 仮引数に入っている各要素をinnerTextでspan要素に代入
    characterSpan.innerText = character;
    // 既存の親要素（typeDisplay）に新しい要素（characterSpan）を追加
    typeDisplay.appendChild(characterSpan);
  });

  // テキストとボックスの中身を消す
  typeInput.innerText = "";
}

renderNextSentence();
</script>

<template>
  <div class="container">
    <div class="type-display" id="typeDisplay"></div>
    <textarea class="type-input" autofocus id="typeInput"></textarea>
  </div>
</template>

<style>
.container {
  background-color: #33ccff;
  /* rem(root em):HTML要素のフォントサイズに対する倍率のこと。 */
  /* 通常ブラウザはデフォルトで16pxを使用している。
  その場合、font-size: 2.4rem; は 2.4 * 16px = 38.4px に相当 */
  font-size: 2.4rem;
  font-weight: 600;
  padding: 2.5rem;
  border-radius: 0.5rem;
  width: 1024px;
  min-height: 600px;
  max-width: 90%;
  box-shadow: 1px 5px 6px rgb(80, 80, 80);
}

.container,
.type-input {
  margin-top: 4rem;
  font-size: 2rem;
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
  margin: auto;
  resize: none;
  padding: 0.5rem 1rem;
  border-radius: 0.5rem;
}

.type-input:focus {
  border: 4px solid white;
}

.correct {
  color: green;
}

.incorrect {
  color: red;
  text-decoration: underline;
}
</style>
