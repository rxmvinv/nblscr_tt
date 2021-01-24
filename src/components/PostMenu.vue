<template>
  <div class="post-menu">
    <div class="column first">
      <ul>
       <li class="section">PCB</li>
       <li>Project and Design File Renaming</li>
       <li>Managed Project Renaming</li>
       <li>Managed Project History</li>
       <li>Project Sharing</li>
       <li>Soft Delete</li>
      </ul>
    </div>
    <div class="column second">
      <ul>
       <li class="section">Schematic </li>
       <li>Third-party Sign-in</li>
       <li>Single Sign On</li>
       <li>Library Migrator Updates</li>
       <li>Altium Designer Security Upgrades</li>
      </ul>
    </div>
    <div class="column third">
      <ul>
       <li class="section">Altium 365</li>
       <li>Third-party Sign-in</li>
       <li>Single Sign On</li>
       <li>Library Migrator Updates</li>
       <li>Altium Designer Security Upgrades</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PostMenu',
  props: {
    menuItems: Function,
  },
  data () {
    return {
    }
  },
  methods: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .post-menu {
    background: #282828;
    display: flex;
    justify-content: space-evenly;
    width: 820px;
    border-radius: 4px;
    margin: auto;
  }
  .post-menu .column {
    text-align: left;
    margin-top: 8px;
  }
  .post-menu .column .section {
    font-size: 10px;
    color: #9E9E9E;
    text-transform: uppercase;
  }
  .post-menu .column ul {
    padding: 0;
  }
  .post-menu .column li {
    list-style: none;
    font-size: 11px;
    color: #fff;
    padding: 8px 0;
  }
  .post-menu .column.first {
    margin-left: -42px;
  }
</style>
