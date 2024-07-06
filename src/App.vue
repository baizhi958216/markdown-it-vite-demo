<template>
  <div v-html="html"></div>
</template>

<script lang="ts" setup>
import MarkdownIt from "markdown-it";

const md = new MarkdownIt();

const html = md.render("# Hello, World");
</script>

<style lang="scss"></style>
