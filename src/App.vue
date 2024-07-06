<template>
  <div class="markdown-body" v-html="html"></div>
  <div class="hover-underline-animation" ref="hoverRef">
    hover-underline-animationhover-underline-animationh
  </div>
</template>

<script lang="ts" setup>
import MarkdownIt from "markdown-it";
import Hello from "./md/Hello.md?raw";
import { onMounted, onUnmounted, ref } from "vue";

const md = new MarkdownIt({});

const html = md.render(Hello);

const hoverRef = ref<HTMLElement | null>(null);

const changeWidth = (newWidth: string) => {
  if (hoverRef.value) {
    hoverRef.value.style.setProperty("--underline-width", newWidth);
  }
};

onMounted(() => {
  hoverRef.value?.addEventListener("mousemove", (e) => {
    const { left } = hoverRef.value!.getBoundingClientRect();
    const mouseX = e.clientX - left;
    changeWidth(mouseX + "px");
  });
});

onUnmounted(() => {
  hoverRef.value?.removeEventListener("mousemove", () => {});
});
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

@keyframes slide {
  from {
    background-position: 0% 0;
  }
  to {
    background-position: 100% 0;
  }
}

.hover-underline-animation {
  display: inline-block;
  position: relative;
  cursor: default; /* 鼠标遇到字体会变成I, 给默认好看点 */
}

.hover-underline-animation::after {
  content: "";
  position: absolute;
  width: var(--underline-width, 12px);
  height: 2px; /* 线条高度 */
  bottom: 0;
  left: 0;
  background-image: linear-gradient(
    90deg,
    #778beb,
    #e15f41,
    #3dc1d3
  ); /* 呼啸呼啸渐变 */
  background-size: 200% 100%; /* 背景大小 */
  background-position: -100% 0; /* 初始背景位置 */
  opacity: 0;
  transition: opacity 0.3s, background-position 0.3s;
}

.hover-underline-animation:hover::after {
  background-position: 0 0;
  opacity: 1;
  animation: slide 3s linear infinite;
}
</style>
