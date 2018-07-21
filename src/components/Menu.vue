<template>
  <div id="menu">
    <h1>Accessible Drop Down Menu</h1>
    <nav role="navigation">
        <ul class="access-menu">
            <li v-for="(value, key) in menu" :key="key">
                <a v-shortkey.focus="[value.key]" href="#" >{{ key }}</a>
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
          ],
          key: 1
        },
        Mens: {
          childs: [
            'Featured',
            'Shoes',
            'Clothing',
            'Accessories',
            'Sports',
            'Sale'
          ],
          key: 2
        },
        Kids: {
          childs: [
           'Featured',
           'Boys',
           'Girls',
           'Infant',
           'Sale'],
           key: 3
        },
        Sale: {
          childs: [
              'Men\'s Sale',
              'Women\'s Sale',
              'Plus Sale',
              'Kids\' Sale'
              ],
              key: 4
        }
      }
    }
  }
}
</script>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style scoped>
</style>
