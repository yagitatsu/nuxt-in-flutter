<template>
  <div style="text-align:center;">
    <p>Vue Counter: {{ counter }}</p>
    <button v-on:click="clicked()">Increment</button>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
    data() {
        return {
            counter: 0
        }
    },
    methods: {
        clicked() {
            window.parent.postMessage({
                method: 'increment',
                params: {}
            }, '*');
        }
    }
})

</script>
