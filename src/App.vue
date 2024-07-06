<template>
  <div class="markdown-body" v-html="html"></div>
</template>

<script lang="ts" setup>
import MarkdownIt from "markdown-it";
import Hello from "./md/Hello.md?raw";
const md = new MarkdownIt({});
const html = md.render(Hello);
</script>

<style lang="scss">
.markdown-body {
  h1 {
    color: #fc5c65;
  }

  h2 {
    color: #fd9644;
  }

  h3 {
    color: #26de81;
  }

  p {
    color: #2bcbba;
  }

  blockquote p {
    color: #546de5;
  }

  ul li {
    color: #a55eea;
  }

  pre {
    code.language-js {
      color: #45aaf2;
    }
    code.language-java {
      color: #f7b731;
    }
  }
}
</style>
