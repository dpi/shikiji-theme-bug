<script setup>
// Common
import {onMounted, ref } from "vue";
const foo = ref()

// Shiki Implementation.
import {getHighlighter, setCDN} from 'shiki'
import githubDark from "shiki/themes/github-dark.json";

onMounted(async () => {
  setCDN("https://unpkg.com/shiki/");

  const highlighter = await getHighlighter({
    themes: [githubDark],
    langs: ['php']
  })

  const codeBlocks = foo.value.querySelectorAll("pre > code");
  codeBlocks.forEach((codeBlock) => {
    codeBlock.parentNode.parentNode.innerHTML = highlighter.codeToHtml(codeBlock.innerText, {
      // ‼️ Notice: Shiki does not require 'theme' here.
      lang: "php",
    });
  });
})

// // Shikiji Implementation.
// import {getHighlighter} from 'shikiji'
// import githubDark from "shikiji/themes/github-dark.mjs";
//
// onMounted(async () => {
//   const highlighter = await getHighlighter({
//     themes: [githubDark],
//     langs: [
//       import('shikiji/langs/php.mjs'),
//     ],
//   })
//
//   const codeBlocks = foo.value.querySelectorAll("pre > code");
//   codeBlocks.forEach((codeBlock) => {
//     const code = highlighter.codeToHtml(codeBlock.innerText, {
//       lang: "php",
//       // ‼️ Notice: Shikiji requires 'theme' here.
//       // Otherwise 'Uncaught (in promise) Error: [shikiji] Invalid options, either `theme` or `themes` must be provided'
//       theme: 'github-dark'
//     });
//     if (codeBlock.parentNode.parentNode) {
//       codeBlock.parentNode.parentNode.innerHTML = code;
//     }
//   });
// })
</script>
<template>
<div class="text-left" ref="foo">
  Test
  <pre>
  <code>
echo "Foo bar";
$gen = (static function () {
  foreach (['a', 'b'] as $l) {
    yield $l;
  }
})();
print_r(iterator_to_array($gen));
  </code>
  </pre>
</div>
</template>
