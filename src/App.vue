<template>
  <div id="app" class="grid-content">
    <wired-card id="header">
      <wired-fab class="title-icon">pets</wired-fab>
      {{title}}
    </wired-card>
    <card class="card1" ref="breakfast" :content="breakfast"></card>
    <card class="card2" ref ="dinner" :content="dinner"></card>
    <div class="fab">
      <wired-fab
      class="fab-icon"
      @click="fedHim"
    >
      restaurant
    </wired-fab>
    </div>
    <wired-card id="footer">
      <div class="text">&copy; Tim Nehring</div>
    </wired-card>
  </div>
</template>

<script>
import 'wired-elements'
import Card from './components/Card'

export default {
  name: 'App',
  data () {
    return {
      title: 'KOOPA FUTTER CHECKER',
      icon: 'pets',
      gotFood: null,
      breakfast: {
        key: 'breakfast',
        title: 'FRÜHSTÜCK',
        text_no: 'Koopa hat noch nicht gefrühstückt!',
        text_yes: 'Koopa hat schon gefrühstückt!'
      },
      dinner: {
        key: 'dinner',
        title: 'ABENDESSEN',
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
    },
    fedHim () {
      this.$socket.emit('pushed')
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

* {
  padding: 0px;
  margin: 0px;
  border: 0px;
}

#app {
  font-family: 'Gloria Hallelujah', cursive;
  font-size: 20px;
  overflow-y: hidden;
}

#header { 
  grid-area: header;
  z-index: 9998;
  width: 100%;
  display: flex;
  align-items: center;
} 

.title-icon {
  --wired-fab-bg-color: #009688;
  z-index: 9999;
  --wired-icon-size: 40px;
}

.grid-content {
  width: 100%;
  height: 98vh;
  display: grid;
  grid-template-areas: 
  "header"
  "."
  "card1"
  "."
  "card2"
  "."
  "fab"
  "."
  "footer";
  grid-template-rows: 5% 3% 34% 3% 34% 3% 10% 3% 5%;
  grid-template-columns: 100%;
  justify-content: center;
}

.card1 {
  grid-area: card1;
}

.card2 {
  grid-area: card2;
}

#footer {
  grid-area: footer;
  z-index: 9998;
  width: 100%;
  display: flex;
  flex-direction: row;
  align-items: center;
}

.fab {
  grid-area: fab;
  align-self: center;
  justify-self: end;
}

.fab-icon {
  color: #FFFDF6;
  --wired-fab-bg-color: #FF7400;
  --wired-icon-size: 90px;
}

.text {
  width: 100%;
  margin: 5%;
}

</style>
