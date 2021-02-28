<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <h1>Menu</h1>
    <Navbar />
    <Blogs />
    <AllFriends :friends="friends" @delete="deleteFriend"/>
    <OnlineFriends :friends="friends" />
    <h3>{{textSearch}} (длина): {{textSearch.length}}</h3>
    <input type='text' size='50' v-model="textSearch"> 
    <button @click='getHastags'>Hashtags</button>
    <button @click='getCities'>Cities</button>
    <ul>
      <li v-for='hashtag in hashtags' :key='hashtag.id'>
        {{ hashtag }}
      </li>
    </ul>
    <ul>
      <li v-for='city in cities' :key='city.id'>
        {{ city.region }}: {{city.city}}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'
import Navbar from "./components/Navbar";
import AllFriends from "./components/AllFriends";
import OnlineFriends from "./components/OnlineFriends";
import Blogs from "./components/Blogs";

export default {
  name: 'App',
  components: {
    Navbar,
    AllFriends,
    OnlineFriends,
    Blogs,
  },
  data () {
    return {
      title: 'Vue-Firebase App',
      friends: [
                {name: 'Tamir', online: false},
                {name: 'Edo', online: true},
                {name: 'Aldik', online: false},
                {name: 'Era', online: true},
                {name: 'Giba', online: false},
            ],
      hashtags: [],
      cities: [],
      textSearch: '',
      url: {
        hashtags: 'https://dka-develop.ru/api?type=hashtag', 
        cities: 'https://dka-develop.ru/api?type=city'
      }
    }
  },
  watch: {
    textSearch() {
      if (this.textSearch.length > 3) {
        this.textSearch = 'Меняем содержимое поля из кода'
      }
    }
  },
  created() {
    
  },
  methods: {
    deleteFriend(payload) {
      console.log(payload)
      this.friends = this.friends.filter(friend => {
        return friend.name !== payload.name
      })
    },
    
    getHastags() {
      axios.get(this.url.hashtags).then(response => {
        console.log(response.data)
        this.hashtags = response.data
      })
    },
    getCities() {
      axios.get(this.url.cities).then(response => {
        console.log(response.data)
        this.cities = response.data
      })
    },
  }
}
</script>

<style>
h1 {
  color: #444;
  text-align: center;
  font-weight: normal;
}
</style>
