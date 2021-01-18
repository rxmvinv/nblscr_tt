<template>
  <div class="tabs">
      <div class="tabs-header" v-bind:class="{'tabs-header-fixed': isFixed}">{{tabsHeader}}</div>
      <div class="tabs-list" v-bind:class="{'tabs-list-fixed': isFixed}">
        <div 
          class="tab-container"
          v-for="(tab, index) in tabsList" 
          v-bind="tab"
          v-bind:key="tab.label + index" 
          v-on:click="onSwitchAction(index)"
        >
          <div 
            class="tab tab-button" 
            v-bind:class="{active: tab.active, all: index === 0}"
          >
            {{tab.label}}
          </div> 
          <span 
            class="tabs-pipe" 
            v-if="index===0"
          ></span>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'Tabs',
  props: {
    header: String,
    tabsContent: Array,
    isFixed: Boolean
  },
  data () {
    return {
      tabsHeader: this.header,
      tabsList: [
        {
          label: 'All',
          active: true
        },
        {
          label: 'Test 1',
          active: false
        },
        {
          label: 'Test 2',
          active: false
        },
        {
          label: 'Test 3',
          active: false
        },
        {
          label: 'Test 4',
          active: false
        }
      ]
    }
  },
  methods: {
    onSwitchAction (t) {
        // TODO: make it shorter
        let tL = this.tabsList;
        this.tabsList = this.tabsList.map(
          (tab, index) => {
            let allTabs = t === 0,
              allVal = !this.tabsList[0].active;
            if (allTabs) {
              tL = tL.map(t => t.active = allVal);
            } else {
              tab.active = index === t;
            } 
            return tab;
          });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.tabs {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
.tabs-header {
  color: #fff;
  font-size: 32px;
  margin-top: 32px;
  margin-bottom: 16px;
}
.tabs-header-fixed {
  margin-top: 74px;
  margin-bottom: 58px;
}
.tabs-list {
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  margin-bottom: 24px;
}
.tab-container {
  display: flex;
}
.tab-button {
  margin: 0 8px;
  padding: 8px 16px;
  font-size: 12px;
  color: #fff;
  border-radius: 104px;
  cursor: pointer;
  background: none;
  border: 1px solid #484848;
  user-select: none;
}
.tab-button:hover {
  background: none;
  border: 1px solid #9E9E9E;
}
.tab-button.active {
  background-color: #484848;
  border: 1px solid transparent;
}
.tab-button.active:hover {
  border: 1px solid #9E9E9E;
}
.all {
  text-transform: uppercase;
  margin-left: 0;
}
.tabs-pipe {
  display: flex;
  width: 1px;
  height: 16px;
  padding: 18px 0;
  background-color: #181818;
  margin-left: 8px;
  margin-right: 8px;
}
.tabs-list-fixed {
  width: 100%;
  position: fixed;
  background: #232323;
  margin: 0;
  padding: 24px 0;
}
</style>
