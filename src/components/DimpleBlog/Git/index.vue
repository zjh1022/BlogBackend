<template>
  <div>
    <svg-icon icon-class="github" @click="goto"/>
  </div>
</template>

<script>
  export default {
    name: 'DimpleBlogGit',
    data() {
      return {
        url: 'https://github.com/zjh1022'
      }
    },
    methods: {
      goto() {
        window.open(this.url)
      }
    }
  }
</script>
