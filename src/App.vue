<template>
  <div id="app">
    {{ message }}
    <br>
    <br>
    <div style="text-align:center;">
      <button v-for="tab in tabs" v-on:click="Tab(tab)">
        <div v-if="tab === 1">HelloWorld</div>
        <div v-else>Lesson{{ tab }}</div>
      </button>
    </div>
    <ul>
      <li v-if="current == 3">
        <div class="tabView" v-cloak>
          <Lesson3/>
        </div>
      </li>
      <li v-if="current == 2">
        <div class="tabView" v-cloak>
          <Lesson/>
        </div>
      </li>
      <li v-if="current == 1">
        <div class="tabView" v-cloak>
          <img width="25%" src="./assets/logo.png">
          <HelloWorld msg="Hello Vue in CodeSandbox!"/>
        </div>
      </li>
    </ul>
    <div class="content">...</div>
    <div v-on:click="scrollTop">ページ上部へ移動</div>
  </div>
</template>

<script>
import Scroll from "smooth-scroll";
import Lesson3 from "./components/Lesson3";
import Lesson from "./components/Lesson";
import HelloWorld from "./components/HelloWorld";

export default {
  name: "App",
  components: {
    Lesson3,
    Lesson,
    HelloWorld
  },
  data() {
    return {
      current: "",
      tabs: [3, 2, 1],
      contents: [3, 2, 1],
      message: "Hello Vue.js!"
    };
  },
  created: function() {
    this.Tab(3);
  },
  methods: {
    Tab: function(n) {
      return (this.current = n);
    },
    scrollTop: function() {
      var scroll = new Scroll();
      scroll.animateScroll(0);
    }
  }
};
</script>

<style lang="scss" scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
@keyframes cloak-in {
  0% {
    opacity: 0;
  }
}
.tabView {
  animation: cloak-in 1s;
}
.tabView[v-cloak] {
  opacity: 0;
}
ul {
  li {
    list-style-type: none;
  }
}
</style>
