
<script>
const API_URL = `http://127.0.0.1:8088/live/list`

export default {
  data: () => ({
    room_list: null,
    count: 0
  }),

  created() {
    console.log('iii');
    this.fetchData()
  },

  watch: {
  },

  methods: {
    fetchData() {
      let headers = new Headers();

      console.log('fetchData() invoke');
      const url = `${API_URL}`
      this.room_list = ''
      fetch(url, {
        headers: headers
      })
        .then((response) => response.json())
        .then((data) => this.room_list = data);
    },
    increment() {
      this.count++
      this.fetchData()
    }

  }
}
</script>

<template>
  <!-- <button @click="increment">count is: {{ count }}</button> -->
  <h3>以下房间正在直播中</h3>
  <ul>
    <li v-for="{ roomStatus, uname, roomTitle, platform, url } in room_list">
      <a :href="url" target="_blank" class="commit">{{ uname }}</a>
      - <span class="message">{{ roomTitle }}</span><br>
    </li>
  </ul>
  <p>总计（{{ room_list.length }}）</p>
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