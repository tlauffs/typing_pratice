<script setup lang="ts">
import snippets from "../assets/snippets.json";
import { ref } from "vue";
import hljs from "highlight.js";
import "highlight.js/styles/base16/gruvbox-dark-hard.min.css";
import { computed } from "@vue/reactivity";

const snippet = snippets.array.twosum;
const nonTypedCode = ref(snippet.languages.js);

const typedCode = computed(
  () =>
    hljs.highlight("", {
      language: "javascript",
    }).value
);

addEventListener("keydown", (event) => {
  const key = event.key;

  console.log(JSON.stringify(key))
  const nextKey = nonTypedCode.value[0];
  if (nextKey !== key) {
    console.log('error: ', nextKey);
    return;
  }
  nonTypedCode.value = nonTypedCode.value.slice(1);
});

</script>

<template>
  <div class="code-wrapper" >
    <pre class="grayed-out">{{ nonTypedCode }}</pre>
    <pre v-html="typedCode"></pre>
  </div>
</template>

<style scoped>
pre {
  white-space: pre-wrap;
}

.code-wrapper {
  margin: 4rem;
  background-color: #1d2021;
  font-size: 1.1rem;
  padding: 2rem;
  border-radius: 1rem;
}

.grayed-out {
  color: rgb(184, 184, 184);
  opacity: 0.8;
}
</style>
