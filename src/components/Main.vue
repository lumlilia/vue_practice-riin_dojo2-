<script>
import HelloWorld from './HelloWorld.vue'
import MyComponent from './MyComponent.vue'
import C230912 from './Component230912.vue'
import SharedCounter from './SharedCounter.vue'

export default{
  components:{
    HelloWorld,
    MyComponent,
    C230912,
    SharedCounter,
  },

  data(){
    return{
      hoge: "nekoneko",
      isShow: true,
      arr: [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610],
      car: {
        name: "kuruma",
        speed: "hayai",
        price: "takai",
      },
      counter: 0,
      dog: undefined,

      sc_count: 0,
    }
  },

  mounted(){
    this.getDog()
  },

  methods:{
    toggleShow(){
      this.isShow = !this.isShow
      console.log(this.isShow)
    },

    increment(){
      this.counter++
    },
    increment3(){
      this.counter += 3
    },
    incrementX(add){
      this.counter += add
    },
    decrementX(rm){
      this.counter -= rm
    }, reset(){
      this.counter = 0
    },

    async getDog(){
      this.dog = await(await fetch("https://dog.ceo/api/breeds/image/random ")).json()
    },

    ScIncrement(){
      this.sc_count++
    },
  },
}
</script>

<template>
  <C230912 />
  <C230912 />
  <C230912 />

  <div v-for="i in [0,0,0]">
    <SharedCounter :num="sc_count" :p_num="sc_count" @myEvent="(e) => sc_count = e" />
    <button @click="ScIncrement">SharedCounter++</button>
  </div>

  <header>
    <button @click="getDog">inu</button>
    <div><img v-if="dog" :src="dog.message" /></div>
    <router-view />
    <p><router-link to="/main">Home</router-link></p>
    <p><router-link to="/main/about">About</router-link></p>
    <p><router-link to="/main/neko">nekokoneko</router-link></p>
    <div id="counterbox">
      <p>{{counter}}</p>
      <div class="btnbox">
        <button v-for="item in arr" @click="incrementX(item)">
          {{item}}
        </button>
      </div>
      <div class="btnbox">
        <button @click="increment">+1</button>
        <button @click="increment3">+3</button>
        <button @click="incrementX(10)">+10</button>
        <button @click="incrementX(255)">+255</button>
      </div>
      <div class="btnbox">
        <button @click="decrementX(1)">-1</button>
        <button @click="decrementX(3)">-3</button>
        <button @click="decrementX(10)">-10</button>
        <button @click="decrementX(255)">-255</button>
      </div>
      <div class="btnbox">
        <button @click="reset">reset</button>
      </div>
    </div>

    <img v-if="isShow" alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <button @click="toggleShow()">toggle</button>
    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <MyComponent msg="nya" title="ふつうねこ" />
    <MyComponent msg="gorogoro" title="あまえねこ" />
    <MyComponent msg="shaaaa!!" title="おこねこ" />
    {{hoge}}
    <button @click="toggleShow">toggle</button>
    <ul>
      <li v-for="item in arr">
        <MyComponent :msg="hoge" title="ねこれんだ！！" />
        {{item}}
      </li>
      <li>{{car.name}}</li>
      <li>{{car.speed}}</li>
      <li>{{car.price}}</li>
    </ul>
    <p>{{car}}</p>
    <HelloWorld v-for="item in arr" msg="You did it!" />
    <HelloWorld v-for="item in arr" :msg="item" />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

button{
  border: 2px black solid;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}

#counterbox{
  position: relative;
  display: flex;
  flex-direction: column;
  width: 600px;
}
#counterbox p{
  text-align: center;
  font-size: 2em;
  font-weight: bold;
}
.btnbox{
  display: flex;
  width: 100%;
  height: 36px;
}
.btnbox button{
  width: 100%;
}
</style>
