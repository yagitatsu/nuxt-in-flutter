<template>
  <div style="text-align:center;">
    <p>Vue Counter: {{ counter }}</p>
    <button @click="clicked()">
      Increment
    </button>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

interface Message {
  method: string
  // eslint-disable-next-line no-use-before-define
  params: Params
}

interface Params {
}

export default Vue.extend({
  data () {
    return {
      counter: 0
    }
  },

  mounted () {
    window.addEventListener('message', this.listen, true)
  },

  destroyed () {
    window.removeEventListener('message', this.listen, true)
  },

  methods: {
    clicked () {
      window.parent.postMessage({
        method: 'increment',
        params: {}
      }, '*')
    },
    listen (event: MessageEvent): void {
      if (event.data.method === 'increment') {
        this.counter++
      }
    }
  }

})

</script>
