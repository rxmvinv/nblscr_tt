<template>
  <nav class=" sidebar ">
    <div 
      class="sidebar-sticky"
    >
    <div class="menu-items-list">

      <div class="menu-item"
        v-for="(item, index) in menuItems" 
        v-bind="item"
        v-bind:key="item"
        v-bind:class="{active: item.active}"
        v-on:click="setActiveSection(index)"
      >
        <a :href="item.url" v-if="item.label">
          {{item.label}}
          <span v-if="item.isCounted" class="updates-counter">{{counter}}</span>
        </a>
        <div class="divider-line" v-else></div>
      </div>

    </div>
    <button class="menu-item"><span class="open-icon"></span>Open in browser</button>

    </div>
  </nav>
</template>

<script>
export default {
  name: 'SideBar',
  props: {
    counter: Number
  },
  data() {
    return {
      menuItems: [
        {
          label: 'Home',
          url: '/',
          active: false
        },
        {
          label: 'Updates',
          url: '/updates',
          active: true,
          isCounted: true
        },
        {
          label: 'Learning Center',
          url: '/learning-center',
          active: false
        },
        {
          label: '',
          url: '',
          active: false
        },
        {
          label: 'Community',
          url: '/community',
          active: false
        },
        {
          label: 'Support',
          url: '/support',
          active: false
        },
        {
          label: 'Documentation',
          url: '/documentation',
          active: false
        }
      ]
    }
  },
  methods: {
    setActiveSection (itm) {
      this.menuItems = this.menuItems.map(
          (item, index) => {item.active = index === itm; return item});
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.sidebar {
  border-right: 1px solid #181818;
  position: relative;
  height: 100vh;
  max-width: 236px;
  width: 100%;
  padding-left: 20px;
}
.sidebar-sticky {
  left: 0%;
  right: 7.41%;
  top: 3.96%;
  bottom: 3.84%;
  position: absolute;

  position: -webkit-sticky;
  position: sticky;

  text-align: left;
  top: 0;
  height: 100vh;
  padding-top: .5rem;
  overflow-x: hidden;
  overflow-y: auto;
  max-height: 831px;
}
.menu-item {
  width: 200px;
  height: 48px;
  border-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  font-weight: 500;
  font-size: 12px;
}
.menu-item a {
  color: #DDDDDD;
  padding: 16px;
  width: 100%;
}
.updates-counter {
  display: inline-flex;
  background-color: #FF375F;
  border-radius: 50%;
  width: 15px;
  height: 16px;
  align-items: center;
  justify-content: center;
  text-decoration: none;
  font-size: 11px;
  float: right;
  margin-right: 19.5px;
}
.updates-counter:hover {
  text-decoration: none;
}
button.menu-item {
  height: 32px;
  border: none;
  color: #DDDDDD;
  justify-content: center;
  cursor: pointer;
  position: absolute;
  bottom: 32px;
}
.divider-line {
  border-top: 1px solid #181818;
  width: 100%;
}
.menu-item.active, button.menu-item {
  background: #282828;
}
.open-icon {
  background-image: url('../assets/icon-open.png');
  background-size: contain;
  width: 12px;
  height: 12px;
  display: block;
  margin-right: 9px;
}
</style>
