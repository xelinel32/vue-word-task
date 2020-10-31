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
      <div class="divider"></div>
      <div class="row">
        <div class="input-field col s6">
          <textarea
            v-model="currentTextElement.text"
            class="materialize-textarea text-editor__place"
          ></textarea>
        </div>
        <div class="col s6">
          <div class="text-editor__showed">
            <button
              class="waves-effect waves-light btn"
              type="button"
              aria-label="logJsonBlock"
              title="JSON log"
              @click="isShowJson = !isShowJson"
            >
              JSON log
            </button>
            <button
              class="waves-effect waves-light btn"
              type="button"
              aria-label="logJson"
              title="Console Log"
              @click="consoleLogJson"
            >
              Console Log
            </button>
          </div>
          <div class="text-editor__control">
            <div class="input-field">
              <span class="flow-text">Balckgroun color - </span>
              <input
                v-model="currentTextElement.textBackground"
                type="color"
                name="color"
              />
            </div>
            <div class="input-field">
              <span class="flow-text">Text color - </span>
              <input
                v-model="currentTextElement.color"
                type="color"
                name="color"
              />
            </div>
            <div class="input-field">
              <select ref="select" v-model="currentTextElement.textSize">
                <option value="" disabled selected>Choose size</option>
                <option v-for="s in sizes" :key="s" :value="s">{{ s }}</option>
              </select>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="col s12">
      <transition name="slide">
        <pre v-if="isShowJson">
        {{ currentTextElement }}
      </pre
        >
      </transition>
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
      select: null,
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
      sizes() {
        const sizes = []
        for (let i = 8; i <= 72; i += 1) sizes.push(i)
        return sizes
      },
    },
    mounted() {
      // eslint-disable-next-line no-undef
      this.select = M.FormSelect.init(this.$refs.select)
    },
    destroyed() {
      if (this.select && this.select.destroy) {
        this.select.destroy()
      }
    },
    methods: {
      seteSelectElem(id) {
        this.currentElementId = id
        // eslint-disable-next-line no-undef
        this.select = M.FormSelect.init(this.$refs.select)
      },
      consoleLogJson() {
        console.log(JSON.stringify(this.currentTextElement, null, 1))
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
    &__place {
      height: 200px !important;
    }
    &__showed {
      button:not(:last-child) {
        margin-right: 1rem;
      }
    }
    .divider {
      margin: 2rem 0;
    }
    pre {
      white-space: pre-line;
      border: 1px solid #000;
      padding: 5px;
      border-radius: 3px;
      pointer-events: none;
      user-select: none;
    }
    .slide-enter-active {
      transition: all 0.3s ease;
    }
    .slide-leave-active {
      transition: all 0.8s ease;
    }
    .slide-enter,
    .slide-leave-to {
      transform: translateY(-30%);
      opacity: 0;
    }
  }
</style>
