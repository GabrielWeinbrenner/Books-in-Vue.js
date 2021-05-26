<template>
  <div class="hello">
    <!-- <h1>{{ msg }}</h1>
    <h2>{{ count }}</h2>
    <button v-on:click="count++">Add + 1</button> -->
    <div>
      <p>What type of books to look for?</p>
      <input v-model="category" v-on:keyup.enter="getName">
      <div v-for="book in data.items" :key="book.id">
        <h3>{{book.volumeInfo.title}}</h3>
        <img :src="book.volumeInfo.imageLinks.thumbnail" >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  beforeMount(){
    this.getName()
  },
  methods: {
    async getName(){
      const res = await fetch("https://www.googleapis.com/books/v1/volumes?q=" + this.category)
      const data = await res.json()
      this.data = data
      console.log(this.data)
    }
  },
  data(){
    return {
      count: 0,
      category: "cooking",
      data: "",
    }
  },
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
