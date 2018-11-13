<template>
  <div class="vue-simple-markdown markdown-body" v-html="parsed"></div>
</template>

<script>
import { VueSimpleMarkdownParser } from './vue-simple-markdown-parser.js'

export default {
  name: 'vue-simple-markdown',
  props: {
    source: {
      type: [String, Number],
      default: ''
    },
    prerender: {
      type: Function,
      default: (source) => { return source }
    },
    postrender: {
      type: Function,
      default: (html) => { return html }
    },
    strong: {
      type: Boolean,
      default: true
    },
  },
  computed: {
    parsed () {
      let source = this.prerender(this.source.toString())

      source = VueSimpleMarkdownParser.parse(source, {
        strong: this.strong,
      })

      return this.postrender(source)
    }
  }
}
</script>