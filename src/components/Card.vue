<template>
  <div class="wrapper">
  <wired-card class="card" elevation="5">
    <div class="grid-box">
    <h2 class="title">{{ content.title }}</h2>
    <div style="display: flex; justify-content: flex-end;"><wired-fab class="fab icon" v-bind:style="{color: activeColor}">{{ this.icon }}</wired-fab></div>
    <div class="text">{{ text }}</div>
    </div>
  </wired-card>
  </div>
</template>

<script>
import 'wired-elements'

export default {
  props: ['content'],
  data () {
    return {
      key: this.content.key,
      icon: 'cached',
      text: 'Koopa hat noch nicht gefrühstückt!',
      activeColor: 'transparent'
    }
  },
  methods: {
    fed () {
      this.icon = 'thumb_up'
      this.activeColor = 'green'
      this.text = this.content.text_yes
      this.gotFood = true
    },
    hungry () {
      this.icon = 'thumb_down'
      this.activeColor = 'red'
      this.text = this.content.text_no
    }
  }
}
</script>

<style scoped>

* {
  padding: 0px;
  margin: 0px;
  border: 0px;
}

.wrapper {
  display: flex;
  flex-direction: row;
}

.card {
  align-self: flex-end;
  display: grid;
  width: 95%;
  height: 95%;
}

.icon-wrap {
  display: flex;
  align-self: flex-end;
  /* margin-top: -20px;
  margin-right: -50px; */
  z-index: 1337;
}

.grid-box {
  width: 100%;
  height: 100%;
  display: grid;
  grid-template-areas: 
  "title icon"
  "text text";
  grid-template-rows: 50% 50%;
}

.title {
  grid-area: title;
  justify-self: center;
  align-self: center;
}

.icon {
  grid-area: icon;
  --wired-fab-bg-color: lightgrey;
  --wired-icon-size: 80px;
  margin-top: -15%;
  margin-right: -10%;
  z-index: 1337;
  align-self: end;
}

.text{
  grid-area: text;
  justify-self: center;
  align-self: center;
  margin: 5% 5%;
}
</style>
