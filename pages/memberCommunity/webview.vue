<template>
  <web-view :src="url"></web-view>
</template>

<script>
export default {
  data() {
    return {
      url: ''
    };
  },
  onLoad(options) {
    // 获取传递过来的URL参数
    if (options.url) {
      this.url = decodeURIComponent(options.url);
    }
  }
};
</script>