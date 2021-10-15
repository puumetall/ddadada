<template>
<div>
  <div class="tabs is-centered is-large">
    <ul>
      <li v-for="(item,index) in items"
      :key="index"
      :class="{'is-active': index === active}"
      @click="active = index">
        <a>{{item.title}}</a>
      </li>
    </ul>
  </div>
  <section class="section">
    <component :is="items[active].componentName"></component>
  
  </section>
</div>
</template>

<script>
import ClickerExample from './ClickerExample.vue'

export default {
  components: {ClickerExample},
    data(){
      return {
        active: 0,
        items: [
          {title:'Shrek Clicker', componentName:'ClickerExample'}
        ]
      }
    } 
}
</script>

<style>

</style>