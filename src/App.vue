
<script>
const API_URL = `/live/list`

export default {
  data: () => ({
    room_list: [],
    refreshing: false,
    data: null,
    total: 0,
    count: 0
  }),

  created() {
    console.log('iii');
    this.fetchData()
  },

  watch: {
  },

  methods: {
    async fetchData() {
      this.refreshing = true;
      console.log('fetch data...');
      var data = await (await fetch(API_URL)).json();
      this.room_list = data.data.liveRoomResults
      this.total = data.data.total
      console.log("fetch success")
      this.refreshing = false;
    }

  }
}
</script>

<template>
  <!-- <button @click="increment">count is: {{ count }}</button> -->
  <h3>以下房间正在直播中</h3>

  <button v-if="!refreshing" @:click="fetchData">刷新</button>
  <p v-if="refreshing">正在查询...</p>

  <ul>
    <li v-for="{ roomStatus, uname, roomTitle, platform, url } in room_list">
      <a :href="url" target="_blank" class="commit">{{ uname }}</a>
      - <span class="message">{{ roomTitle }}</span><br>
    </li>
  </ul>
  <p>总计（{{ room_list.length }}/{{total}}）</p>
</template>

<style>
a {
  text-decoration: none;
  color: #42b883;
}

li {
  line-height: 1.5em;
  margin-bottom: 20px;
}

.author,
.date {
  font-weight: bold;
}
</style>