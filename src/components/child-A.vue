<template lang="html">
  <div>
    <p>{{uname}}</p>
    <p>{{userAge}}</p>
    <p>{{comms}}</p>
    <button type="button" @click="ChangeColor()">Change color (event)</button>
    <button type="button" @click="ufunction('dark')">Darken green (callback fn)</button>
    <div><slot name="one"></slot></div>
    <div><slot name="two"></slot></div>
    <div><slot name="three">[Slot placeholder]</slot></div>
    <div><slot></slot></div>
  </div>
</template>

<script>
  import {eventBus} from '../main.js'

  export default {
    data: function() {
      return {
        comms: ''
      }
    },
    props: {
      uname: {
        type: [String, Array],
        required: true,
        default: '???'
      },
      ufunction: Function,
      userAge: Number
    },
    methods: {
      ChangeColor: function() {
        var newcolor = 'light' + this.uname;
        this.$emit('customEvent', newcolor)
      }
    },
    created: function() {
      eventBus.$on('ageWasEdited', (data) => {
          this.comms = data
      })
    }
}
</script>

<style lang="css" scoped>
  p {
    border: solid thin blue;
  }
</style>
