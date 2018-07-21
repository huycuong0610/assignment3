<template>
  <div id="menu">
    <h1>Accessible Drop Down Menu</h1>
    <nav role="navigation">
        <ul class="access-menu">
            <li v-for="(value, key) in menu" :key="key">
                <a href="#" >{{ key }}</a>
                <ul class="access-submenu">
                  <a v-for="children in value.childs" :key="children" href="#"><li> {{children}} </li></a>
                </ul>
            </li>
        </ul>
    </nav>
  </div>
</template>

<script>
export default {
  name: 'Menu',
  data () {
    return {
      menu: {
        Womens: {
          childs: [
            'Featured',
            'Shoes',
            'Clothing',
            'Accessories',
            'Sports',
            'Sale'
          ]
        },
        Mens: {
          childs: [
            'Featured',
            'Shoes',
            'Clothing',
            'Accessories',
            'Sports',
            'Sale'
          ]
        },
        Kids: {
          childs: [
           'Featured',
           'Boys',
           'Girls',
           'Infant',
           'Sale']
        },
        Sale: {
          childs: [
              'Men\'s Sale',
              'Women\'s Sale',
              'Plus Sale',
              'Kids\' Sale'
              ]
        }
      }
    }
  }
}
</script>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style scoped>
</style>
