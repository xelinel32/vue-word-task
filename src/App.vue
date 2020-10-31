<template>
  <div id="app">
    <div class="container">
      <TextEditor />
    </div>
  </div>
</template>

<script>
  import TextEditor from '@/components/TextEditor'
  export default {
    name: 'App',
    components: { TextEditor },
  }
</script>

<style lang="scss">
  @import '~materialize-css/sass/materialize.scss';
  @import 'assets/styles.scss';
</style>
