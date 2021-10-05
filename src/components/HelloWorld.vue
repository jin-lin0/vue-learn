<template>
  <div class="hello">
    <button @click="sumStr">+</button>
    <h1>{{ msg }}</h1>
    <h2>{{ testNum }}</h2>
    <button @click="toggle">toggle</button>
    <div v-if="books.length > 0">
      <ul>
        <li v-for="(book, index) in books" :key="index">{{ book.title }}</li>
      </ul>
    </div>
    <div v-else>no books</div>
    <div>{{ sortBooks }}</div>
  </div>
</template>

<script>
import { sum, parseCookie } from "special-utils";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      testNum: 0,
      show: false,
      books: [
        { title: "vue", id: 0 },
        { title: "react", id: 1 },
      ],
    };
  },
  methods: {
    sumStr() {
      this.testNum = sum(this.testNum, 1);
      console.log(
        parseCookie("_octo=GH1.1.31138406.1630338540; tz=Asia%2FShanghai")
      );
    },
    toggle() {
      this.show = !this.show;
    },
  },
  computed: {
    sortBooks() {
      return JSON.parse(JSON.stringify(this.books)).sort((a, b) => b.id - a.id);
    },
  },
};
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
