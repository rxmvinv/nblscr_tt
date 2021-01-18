<template>
  <div class="header">
    <div class="custom-centered">
    <div class="left-column">
      <div class="title">INSTALLED VERSION</div>
      <ul class="version-details">
        <li class="version-date">
          <span class="installed-version-icon"></span> <!--:style="{backgroundImage: `url(${installedVersion.mediaUrl})`}"-->
          {{installedVersion.version}} ({{installedVersion.date}})
        </li>
        <li class="version-status">{{installedVersion.status}}</li>
        <li class="version-missing">{{installedVersion.missingFeatures}} features missing</li>
      </ul>
    </div>
    <div class="right-column">
      <div class="latest-version-details">
        <div class="title">LATEST VERSION</div>
        <div class="version-date">
          <span class="latest-version-icon"></span> <!--:style="{backgroundImage: `url(${latestVersion.mediaUrl})`}" -->
          {{latestVersion.version}} ({{latestVersion.date}})
        </div>
      </div>
      <div class="version-download">
        <button class="download-button" v-on:click="downloadLatest()">Install</button>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
export default {
  name: 'Header',
  props: {

  },
  data () {
    return {
      installedVersion: {
        version: 20.1,
        date: "Aug 2020",
        status: "Outdated",
        missingFeatures: 186,
        // mediaUrl: 'assets/current-version-icon.png'
      },
      latestVersion: {
        version: 20.4,
        date: "Oct 2020",
        sourceUrl: '',
        // mediaUrl: '../assets/latest-version-icon.png'
      }
    }
  },
  methods: {
    downloadLatest () {
      window.open(this.latestVersion.sourceUrl, "_blank");
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
  min-height: 76px;
  flex-basis: 100%;
  flex-direction: row;
  display: flex;
  height: max-content;
  background: #1C1C1C;
  border: 1px solid #181818;
  justify-content: space-between;
  padding-top: 14px;
  padding-bottom: 14px;

  position: absolute;
  width: 100%;
  top: 0;
}
.left-column {
  display: flex;
  justify-content: space-evenly;
  flex-direction: column;
}
.title {
  display: flex;
  font-size: 10px;
  color: #9E9E9E;
  text-transform: uppercase;
}
.version-details {
  display: flex;
  margin: 0;
  padding: 0;
  list-style: none;
  font-size: 12px;
}
.installed-version-icon {
  background-image: url('../assets/current-version-icon.png');
  background-size: contain;
  width: 10px;
  height: 14px;
  display: inline-block;
  margin-right: 8px;
}
.version-date {
  color: #ffffff;
  font-size: 12px;
  display: flex;
  align-items: center;
}
.version-status {
  color: #FF9F0A;
}
.version-missing {
  color: #FF9F0A;
}
.version-status::before, .version-missing::before {
  content: "\2022";
  color: #484848;
  padding: 0 8px;
}
.right-column {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
}
.latest-version-details {
  display: flex;
  justify-content: space-evenly;
  flex-direction: column;
  height: 100%;
}
.latest-version-icon {
  background-image: url('../assets/latest-version-icon.png');
  background-size: contain;
  width: 9px;
  height: 16px;
  display: inline-block;
  margin-right: 8px;
}
.version-download {
  margin-left: 16px;
}
.download-button {
  color: #fff;
  background-color: #3A75AD;
  border: none;
  border-radius: 4px;
  padding: 8px 16px;
}
</style>
