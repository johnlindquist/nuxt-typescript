<template>
  <section class="container">
    {{count}} {{message}}
    <button @click="onClick"></button>
    <hr>
    <div v-for="item in children">
      <div>{{item.title}}</div>
  
    </div>
  
  </section>
</template>
<script lang="ts">
import Vue from "vue";
import Component from "~plugins/nuxt-class-component";
import axios from "~plugins/axios";
import { mapState } from "vuex"

@Component({
  computed: mapState(['count'])
})
export default class extends Vue {
  message = "awesome"

  async asyncData() {
    const response = await axios.get('https://www.reddit.com/r/javascript.json')
    const children = response.data.data.children.map(c => c.data)
    return { children }
  }

  onClick() {
    this.message = "clicked"
  }
}
</script>