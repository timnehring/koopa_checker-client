<template>
  <v-app>
    <v-toolbar>
      <v-toolbar-title>
        <v-icon id="title_icon">pets</v-icon> {{title}}
      </v-toolbar-title>
    </v-toolbar>
    <v-content>
      <v-container>
        <v-layout column>
          <v-flex xs12>
            <card ref="breakfast" :content="breakfast"></card>
          </v-flex>
          <v-flex xs12>
            <card ref ="dinner" :content="dinner"></card>
          </v-flex>
        </v-layout>
        <v-layout>
          <v-spacer></v-spacer>
          <v-flex xs3>
            <v-btn
            class="my-3"
            @click="reset"
            color="error"
            large
            bottom
            right
            fab
            >
              <v-icon>cached</v-icon>
            </v-btn>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
    <v-footer fixed>
      <span>&copy; 2018</span>
    </v-footer>
  </v-app>
</template>

<script>
import Card from './components/Card'

export default {
  name: 'App',
  data () {
    return {
      title: 'Koopa Futter Checker',
      icon: 'pets',
      gotFood: null,
      breakfast: {
        key: 'breakfast',
        title: 'Frühstück',
        text_no: 'Koopa hat noch nicht gefrühstückt!',
        text_yes: 'Koopa hat schon gefrühstückt!'
      },
      dinner: {
        key: 'dinner',
        title: 'Abendessen',
        text_no: 'Koopa hat noch nicht zu Abend gegessen!',
        text_yes: 'Koopa hat schon zu Abend gegessen!'
      }
    }
  },
  sockets: {
    connect: function () {
      console.log('socket connected')
    },
    status: function (data) {
      this.gotFood = data
      console.log(this.gotFood)
    }
  },
  methods: {
    reset () {
      this.$refs.breakfast.hungry()
      this.$refs.dinner.hungry()
      this.$socket.emit('reset')
    }
  },
  components: {
    Card
  },
  watch: {
    gotFood: function () {
      if (this.gotFood.breakfast === true) {
        console.log('breakfast is true')
        this.$refs.breakfast.fed()
      } else {
        console.log('breakfast is false')
        this.$refs.breakfast.hungry()
      }
      if (this.gotFood.dinner === true) {
        console.log('dinner is true')
        this.$refs.dinner.fed()
      } else {
        console.log('dinner is false')
        this.$refs.dinner.hungry()
      }
    }
  }
}
</script>

<style scoped>
#title_icon{
  vertical-align: text-top;
}
</style>
