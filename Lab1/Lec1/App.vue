<template>
  <div>
    <h1>Hello World</h1>
    <p>This is a simple example of a Vue.js component.</p>
    <!-- mustache syntax -->
    <h1>{{ name }}</h1>
    <h1 v-pre>{{ name }}</h1>
    <h1 v-once>{{ name }}</h1>
    <button @click="name = 'smart iti'">change name</button>
    <h1 v-text="name"></h1>
    <p v-html="tagp"></p>
    <!-- v-bind ==> id, class, style -->
    <!-- <p v-bind:id="showRed ? pid1 : pid2">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Eligendi sapiente
      perspiciatis natus nesciunt architecto eius delectus dolores soluta pariatur, at provident quas reiciendis
      excepturi accusantium totam itaque fugiat eveniet libero?</p> -->
    <p :id="showRed ? pid1 : pid2">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Eligendi sapiente
      perspiciatis natus nesciunt architecto eius delectus dolores soluta pariatur, at provident quas reiciendis
      excepturi accusantium totam itaque fugiat eveniet libero?</p>
    <p v-bind:class="pclass">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Eligendi sapiente perspiciatis
      natus nesciunt architecto eius delectus dolores soluta pariatur, at provident quas reiciendis excepturi
      accusantium totam itaque fugiat eveniet libero?</p>
    <button @click="showRed = !showRed">toggle</button>
    <p v-bind:style="mystyle">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Eligendi sapiente perspiciatis
      natus nesciunt architecto eius delectus dolores soluta pariatur, at provident quas reiciendis excepturi
      accusantium totam itaque fugiat eveniet libero?</p>
    <p v-bind:style="{ backgroundColor: 'orange' }">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Eligendi
      sapiente perspiciatis
      natus nesciunt architecto eius delectus dolores soluta pariatur, at provident quas reiciendis excepturi
      accusantium totam itaque fugiat eveniet libero?</p>
    <div v-show="num === 0">the num is zero</div>
    <div v-if="num === 0">the num is zero</div>
    <div v-else-if="num > 0">the num is postive</div>
    <div v-else-if="num < 0">the num is negative</div>
    <div v-else>it's not a number</div>
    <h2>{{ num }}</h2>
    <!-- <button @click="num++">inc</button>
    <button @click="num--">dec</button> -->
    <button @click="increase">inc</button>
    <button @click="decrease">dec</button>
    <!-- list rendering ==> v-for -->
    <!-- array of string -->
    <ul>
      <li v-for="name, index in names" :key="name">{{ index }}. {{ name }}</li>
    </ul>
    <!-- array of objects -->
    <div v-for="name in fullnames" :key="name.fname">
      <h3>{{ name.fname }} {{ name.lname }}</h3>
    </div>
    <!-- array of arrays -->
    <div v-for="actor in actors" :key="actor.name">
      <h1>{{ actor.name }}</h1>
      <div v-for="movie in actor.movies" :key="movie">
        <h6>{{ movie }}</h6>
      </div>
    </div>
    <!-- key-value pair -->
    <div v-for="(value, key) in myInfo" :key="value">
      <h1>{{ key }}: {{ value }}</h1>
    </div>
    <template v-for="name in names" :key="name">
      <div v-if="name === 'sarah'">
        <h1>{{ name }}</h1>
      </div>
    </template>
    {{ JSON.stringify(formValues) }}
    <form @submit.prevent="formHandle">
      <div>
        <input type="text" v-model.trim.lazy="formValues.name">
      </div>
      <br>
      <div>
        <input type="text" v-model.trim.number="formValues.age">
      </div>
      <br>
      <div>
        <button type="submit">submit</button>
      </div>
    </form>
    <div>
      {{ method() }}
      {{ comput }}
    </div>
    <!-- send data from parent to child ==> static data, dynamic data -->
    <childApp name="open source" :fname="fname" :lname="lname" />
    <button @click="show = true">show</button>
    <popupApp @close="closepopup" v-if="show"/>
  </div>
</template>

<script>
import childApp from './components/child.vue'
import popupApp from './components/popup.vue'
export default {
  name: 'App',
  components: {
    childApp,
    popupApp
  },
  // provide: {
  //   username: 'hossam'
  // },
  provide() {
    return {
      username: this.username2
    }
  },
  data() {
    return {
      show: false,
      username2: 'omar',
      name: 'os alex',
      tagp: '<b>hello</b>',
      pid1: 'red',
      pid2: 'yellow',
      pclass: 'green',
      showRed: true,
      mystyle: {
        backgroundColor: "black",
        color: 'white',
        fontSize: '30px',
        padding: '20px'
      },
      num: 0,
      names: ['sarah', 'ryhab', 'omar', 'ali'],
      fullnames: [
        { fname: 'ryhab', lname: 'farouq' },
        { fname: 'omar', lname: 'ali' },
        { fname: 'mhmd', lname: 'ahmd' }
      ],
      actors: [
        { name: 'soad hosny', movies: ['s8ira 3la el7ob', 'amira 7oby ana'] },
        { name: 'di caprio', movies: ['inception', 'titanic'] }
      ],
      myInfo: {
        name: 'ali',
        city: 'alex',
        age: 23
      },
      formValues: {
        name: '',
        age: ''
      }, 
      fname: 'ryhab', 
      lname: 'farouq',
    }
  },
  methods: {
    increase() {
      return this.num++;
    },
    decrease() {
      return this.num--;
    },
    formHandle() {
      // e.preventDefault();
      console.log(this.formValues);
    },
    method() {
      console.log('method');
    },
    closepopup(name){
      this.show = false;
      console.log("name is ", name);
    }
  },
  computed: {
    comput() {
      return console.log("computed");
    }
  },
  watch: {
    num(newValue, oldValue) {
      if (newValue > oldValue && newValue === 5) {
        alert('errorrrrrrrrrrrrrrr')
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#red {
  background-color: red;
  padding: 20px;
  color: white
}

#yellow {
  background-color: yellow;
  padding: 20px;
  color: white
}

.green {
  background-color: green;
  padding: 20px;
  color: white
}
</style>
