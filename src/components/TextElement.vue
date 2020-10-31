<template>
  <div
    class="text-element"
    :style="{
      backgroundColor: textBackground,
      color: textColor,
      fontSize: textSize + 'px',
    }"
    @click="selectHandler"
  >
    <slot name="content"></slot>
  </div>
</template>

<script>
  export default {
    name: 'TextElement',
    props: {
      id: {
        type: Number,
        required: true,
      },
      textColor: {
        type: String,
        required: true,
        default: '#ffffff',
      },
      textBackground: {
        type: String,
        required: true,
        default: '#ffffff',
      },
      textSize: {
        type: Number,
        required: true,
        default: 32,
      },
    },
    methods: {
      selectHandler() {
        this.$emit('selectElement', this.id)
      },
    },
  }
</script>

<style lang="scss">
  .text-element {
    display: inline-flex;
    cursor: pointer;
  }
</style>
