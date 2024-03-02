<template>
  <div class="container">
    <div class="type-display" id="typeDisplay">type</div>
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
