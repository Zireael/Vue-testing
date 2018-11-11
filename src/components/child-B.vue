<template lang="html">
  <div>
    <p>{{uAge}}</p>
    <button @click="editAge">send message to sibling component: 35</button>
  </div>
</template>

<script>
import {
  eventBus
} from '../main.js'

export default {
  props: ['uAge'],
  methods: {
    editAge: function() {
      var newAge = 35
      //eventBus.$emit('ageWasEdited', newAge)
      eventBus.emitFn('ageWasEdited', newAge)
    },
  },
}
</script>

<style lang="css" scoped>
  p {
    border: solid green;
  }
</style>
