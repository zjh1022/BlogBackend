<template>
  <div>
    <svg-icon icon-class="skill" @click="goto"/>
  </div>
</template>

<script>
  export default {
    name: 'DimpleBlogDoc',
    data() {
      return {
        url: 'http://jianghai.yixingyuntech.com/'
      }
    },
    methods: {
      goto() {
        window.open(this.url)
      }
    }
  }
</script>
