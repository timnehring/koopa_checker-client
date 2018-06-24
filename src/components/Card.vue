<template>
  <v-card class="my-2">
    <v-card-title class="title" primary-title>{{content.title}}</v-card-title>
    <v-layout wrap>
      <v-flex xs8>
        <v-card-text>
          {{text}}
        </v-card-text>
      </v-flex>
      <v-spacer></v-spacer>
      <v-flex xs4>
        <v-card-text>
          <v-icon x-large :color="color">{{icon}}</v-icon>
        </v-card-text>
      </v-flex>
    </v-layout>
  </v-card>
</template>

<script>

export default {
  props: ['content'],
  data () {
    return {
      key: this.content.key,
      icon: '',
      text: 'aktuelle Daten werden geladen',
      color: 'red'
    }
  },
  methods: {
    fed () {
      this.icon = 'thumb_up'
      this.color = 'green'
      this.text = this.content.text_yes
      this.gotFood = true
    },
    hungry () {
      this.icon = 'thumb_down'
      this.color = 'red'
      this.text = this.content.text_no
    }
  }
}
</script>

<style scoped>

</style>
