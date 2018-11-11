<template lang="html">
  <div class="vue-template-wrapper" v-cloak>

    <keep-alive> <!-- keeps dynamic component from getting destroyed and recreated. Use activated() and deactivated() methods to react to loading/unloading -->
      <component v-bind:is="dynamicComponent">
      </component>
    </keep-alive>

    <div><slot name="one"></slot></div>
    <div><slot name="two">[Slot placeholder]</slot></div>
    <div><slot></slot></div>  <!-- default slot -->

    <transition name="transition1" type="transition" mode="out-in" appear> <!-- type="transition | animation" --> <!-- mode="out-in | in-out" animation replacing element key1->key2 --> <!-- enter-class="" enter-active-class="" leave-class="" leave-active-class="" -->
      <!-- <div v-if="true" key="xxx"></div> -->
      <!-- <div v-else key="yyy"></div> -->
      <!-- <div v-show="true"></div> -->
    </transition>
    <transition
        @before-enter="fnA"
        @enter="fnB" <!-- enter(el, done) -->
        @after-enter="fnC"
        @enter-cancelled="fnD"
        @before-leave="fnE"
        @leave="fnF"
        @after-leave="fnG"
        @leave-cancelled="fnH"
        :css="false"> <!-- transition event flow emitters -->
    </transition>

    <transition-group tag="v-transition-group">
      <div key="unique-for-each-element" class="slide-move"></div>
    </transition-group>


  </div> <!-- end: vue-template-wrapper -->
</template>

<script>
  //import {eventBus} from '../main.js'
  //import ComponentImport from './someComponent.vue'
  //import {Mixin1} from './someMixin.js'

  // export const eventBus = new Vue({
  //   methods: {
  //     emitFn: function (eventNm, dataNm) {
  //       this.$emit(eventNm, dataNm)
  //     }
  //   }
  // })

  export default {
    data: function() {
      return {
        // data1: 'green'
      }
    },
    props: {
      // ['prop1','prop2']
      // prop3: {
      //   type: [String, Array],
      //   required: false,
      //   default: '???'
      // },
      // prop4: Function,
    },
    computed: {
      // filter1: function() {
      //   return this.array1.filter((element) => {
      //     return element.match(this.somefilter1)
      //   })
      // },
      // fullName: {
      //   // getter
      //   get: function () {
      //     return this.firstName + ' ' + this.lastName
      //   },
      //   // setter
      //   set: function (newValue) {  // newValue = 'John Doe'
      //     var names = newValue.split(' ') // ['John','Doe']
      //     this.firstName = names[0] // John
      //     this.lastName = names[names.length - 1] // Doe
      //   }
      // }
    },
    methods: {
      // emitEvent: function() {
      //   eventBus.$emit('customEvent', this.dataOut)
      //   eventBus.emitFn('customEvent', this.dataOut)
      // },
    },
    components: {
      //'app-some-component': ComponentImport,
      //'appSomeComponent': ComponentImport,
    },
    mixins: [], // [Mixin1],
    watch: {  // not recommended to synchronous use -> computed{}, useful for async/expensive with underscore repeat limiter: _.debounce(this.getAnswer, 500)
      // question: function (newValue, oldValue) {  // https://vuejs.org/v2/guide/computed.html#Watchers
      //   this.answer = 'xyz'
      //   this.debouncedGetAnswer()
      // }
    },
    filters: {  // not recommended to use -> computed{}
      // filter1: function(value) {
      //   return value + 'x'
      // }
    },
    created: function() {
      //  eventBus.$on('customEvent', (dataIn) => {
      //      this.data99 = dataIn
      //  })
    }
  }
</script>

<style lang="css" scoped>
  .transition1-enter {        /* active for 1 frame */
    opacity:0;
    }
  .transition1-enter-active {
    transition: opacity 1s;
  }
  .transition1-leave {        /* active for 1 frame */
    }
  .transition1-leave-active {
    position: absolute !important;
    transition: opacity 1s;
    opacity: 1;
  }

  .transition2-enter {        /* active for 1 frame */
    opacity: 0;
    }
  .transition2-enter-active {
    animation: slide-in 1s ease-out forwards;
    transition: opacity 1s;
  }
  .transition2-leave {        /* active for 1 frame */
    }
  .transition2-leave-active {
    position: absolute !important;
    animation: slide-out 1s ease-out forwards;
    transition: opacity 1s;
    opacity: 0;
  }

  .slide-move {        /* transition-group, added to every element that needs to move */
    transition: transform 1s;
  }

  @keyframes slide-in {
    from {
      transform: translateY(0.5em)
    }
    to {
      transform: translateY(0)
    }
  }

  @keyframes slide-out {
    from {
      transform: translateY(0)
    }
    to {
      transform: translateY(0.5em)
    }
  }

  [v-cloak] > * { display:none; }
  [v-cloak]::before {
    content: " ";
    display: block;
    width: 16px;
    height: 16px;
    background-image: url('data:image/gif;base64,R0lGODlhEAAQAPIAAP///wAAAMLCwkJCQgAAAGJiYoKCgpKSkiH/C05FVFNDQVBFMi4wAwEAAAAh/hpDcmVhdGVkIHdpdGggYWpheGxvYWQuaW5mbwAh+QQJCgAAACwAAAAAEAAQAAADMwi63P4wyklrE2MIOggZnAdOmGYJRbExwroUmcG2LmDEwnHQLVsYOd2mBzkYDAdKa+dIAAAh+QQJCgAAACwAAAAAEAAQAAADNAi63P5OjCEgG4QMu7DmikRxQlFUYDEZIGBMRVsaqHwctXXf7WEYB4Ag1xjihkMZsiUkKhIAIfkECQoAAAAsAAAAABAAEAAAAzYIujIjK8pByJDMlFYvBoVjHA70GU7xSUJhmKtwHPAKzLO9HMaoKwJZ7Rf8AYPDDzKpZBqfvwQAIfkECQoAAAAsAAAAABAAEAAAAzMIumIlK8oyhpHsnFZfhYumCYUhDAQxRIdhHBGqRoKw0R8DYlJd8z0fMDgsGo/IpHI5TAAAIfkECQoAAAAsAAAAABAAEAAAAzIIunInK0rnZBTwGPNMgQwmdsNgXGJUlIWEuR5oWUIpz8pAEAMe6TwfwyYsGo/IpFKSAAAh+QQJCgAAACwAAAAAEAAQAAADMwi6IMKQORfjdOe82p4wGccc4CEuQradylesojEMBgsUc2G7sDX3lQGBMLAJibufbSlKAAAh+QQJCgAAACwAAAAAEAAQAAADMgi63P7wCRHZnFVdmgHu2nFwlWCI3WGc3TSWhUFGxTAUkGCbtgENBMJAEJsxgMLWzpEAACH5BAkKAAAALAAAAAAQABAAAAMyCLrc/jDKSatlQtScKdceCAjDII7HcQ4EMTCpyrCuUBjCYRgHVtqlAiB1YhiCnlsRkAAAOwAAAAAAAAAAAA==');
  }



</style>
