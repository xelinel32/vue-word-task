<template>
  <div class="row text-editor">
    <h4 class="text-editor__title">Vue word</h4>
    <div class="col s12 text-editor__block">
      <TextElement
        :id="firstElement.id"
        :style="firstElement.textStyles"
        :text-size="firstElement.textSize"
        :text-color="firstElement.color"
        :text-background="firstElement.textBackground"
        class="center-align"
        @selectElement="seteSelectElem"
      >
        <template #content>
          {{ firstElement.text }}
        </template>
      </TextElement>
    </div>
    <br />
    <div class="col s12 text-editor__block">
      <TextElement
        v-for="elem in withoutFirst"
        :id="elem.id"
        :key="elem.id"
        :style="elem.textStyles"
        :text-size="elem.textSize"
        :text-color="elem.color"
        :text-background="elem.textBackground"
        @selectElement="seteSelectElem"
      >
        <template #content>
          {{ elem.text }}
        </template>
      </TextElement>
    </div>
    <div class="col s12">
      <div class="row">
        <div class="input-field col s12"></div>
      </div>
    </div>
  </div>
</template>

<script>
  import TextElement from '@/components/TextElement'
  export default {
    name: 'TextEditor',
    components: { TextElement },
    data: () => ({
      textElements: [
        {
          id: 0,
          textStyles:
            'padding-left:3px; padding-right: 3px; border-radius: 4px;',
          text: 'Hi',
          color: '#ffffff',
          textBackground: '#f8bbd0',
          textSize: 32,
        },
        {
          id: 1,
          textStyles:
            'padding-left:3px; padding-right: 3px; border-radius: 4px',
          text: 'My lovely',
          color: '#ffffff',
          textBackground: '#f8bbd0',
          textSize: 32,
        },
        {
          id: 2,
          textStyles:
            'padding-left:3px; padding-right: 3px; border-radius: 4px',
          text: 'little',
          color: '#880e4f',
          textBackground: '#fff',
          textSize: 54,
        },
        {
          id: 3,
          textStyles:
            'padding-left:3px; padding-right: 3px; border-radius: 4px',
          text: 'Ponny',
          color: '#ba68c8',
          textBackground: '#f8bb00',
          textSize: 54,
        },
      ],
      currentElementId: 0,
      isShowJson: false,
    }),
    computed: {
      withoutFirst() {
        return this.textElements.slice(1)
      },
      firstElement() {
        return this.textElements[0]
      },
      currentTextElement() {
        return this.textElements.find(el => el.id === this.currentElementId)
      },
    },
    methods: {
      seteSelectElem(id) {
        this.currentElementId = id
      },
    },
  }
</script>

<style lang="scss">
  .text-editor {
    &__block {
      display: flex;
      align-items: center;
      justify-content: center;
    }
  }
</style>
