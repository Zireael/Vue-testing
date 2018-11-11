<template lang="html">
  <div>
      <input type="text" v-model.lazy.trim.number="exinput">
      <input type="text" v-model="name" :style="{'color': name}">
      <select v-model="selected_nOption">
        <option v-for="option in nOptions" :value="option.value">{{option.text}}</option>
      </select>
      <p>{{age}}</p>
    <hr>
      <app-user-detail v-bind:uname="name" v-bind:userAge="age" v-bind:ufunction="nameGreen" @customEvent="name = $event">
        <hr>
          <span slot="two">1) Some slotted text</span>
          <span slot="one">2) ABC-123</span>
          <span>3) everything else</span>
        <hr>
      </app-user-detail>
    <hr>
      <app-user-age v-bind:uAge="age"></app-user-age>
    <hr>
      <button @click="dynamicComponent = 'app-dynamic-a'">dynamic A</button>
      <button @click="dynamicComponent = 'app-dynamic-b'">dynamic B</button>
    <br>
      <keep-alive> <!-- keeps dynamic component from getting destroyed and recreated. Use activated() and deactivated() methods to react to loading/unloading -->
        <component v-bind:is="dynamicComponent">
        </component>
      </keep-alive>

      <app-defaultcomponent></app-defaultcomponent>
  </div>

</template>

<script>
  import UserDetail from './child-A.vue'
  import UserAge from './child-B.vue'
  import dynamicA from './dynamic-A.vue'
  import dynamicB from './dynamic-B.vue'
  import defaultcomponent from './default-component.vue'

  export default {
    data: function() {
      return {
        name: 'blue',
        age: 17,
        dynamicComponent: '',
        exinput: 'input field with extra modifiers',
        nOptions: [
          { text: 'One', value: 'A' },
          { text: 'Two', value: 'B' },
          { text: 'Three', value: 'C' }
        ],
        selected_nOption: 'B'
      }},
    components: {
      'app-user-detail': UserDetail,
      'app-user-age': UserAge,
      'app-dynamic-a': dynamicA,
      'app-dynamic-b': dynamicB,
      'app-defaultcomponent': defaultcomponent,
    },
    methods: {
      nameGreen: function(d) {
        this.name = d + this.name
      }
    }
  }
</script>

<style lang="css" scoped>
  input {
    border: solid thin red;
  }
</style>
