<template>
  <div>
    <button v-on:click="handleClick">クリック</button>
    <!--
    <br>
    <input v-bind:value="message" v-on:change="handleInput">
    <br>
    <div v-on:click.right="handler">example</div>右ボタンを押した時のコンテキストメニューを表示させない
    <div v-on:click.right.prevent="handler">example</div>

    <div v-on:click="handler('div1')">
      div1
      <a href="#top" v-on:click.stop="handler('div2')">div2</a>
    </div>

    <div v-on:click.capture="handler('div1')">div1
      <div v-on:click="handler('div2')">div2
        <div v-on:click="handler('div3')">div3</div>
      </div>
    </div>
    <textarea v-model="message"></textarea>
    <pre>{{message}}</pre>
    <my-commponent v-on:click.native="handler"></my-commponent>
    <br>
    <my-commponent v-on:click="handler"></my-commponent>
    <lable>
      <input type="checkbox" v-model="val" value="A"> A
    </lable>
    <lable>
      <input type="checkbox" v-model="val" value="B"> B
    </lable>
    <lable>
      <input type="checkbox" v-model="val" value="C"> C
    </lable>
    <p>{{ val }}</p>
    <select v-model="val1">
      <option disabled="disabled"></option>
      <option value="a">A</option>
      <option value="b">B</option>
      <option value="c">C</option>
    </select>
    <p>{{ val1 }}</p>
    -->
    <input type="file" v-on:change="handleChange">
    <div v-if="preview">
      <img v-bind:src="preview">
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      scrollY: 0,
      timer: null,
      preview: "",
      val: [],
      val1: "",
      message: "Hello Vue.js"
    };
  },
  created: function() {
    window.addEventListener("scroll", this.handleScroll);
  },
  beforeDestroy: function() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    handleScroll: function() {
      if (this.timer === null) {
        this.timer = setTimeout(
          function() {
            this.scrollY = window.scrollY;
            clearTimeout(this.timer);
            this.timer = null;
          }.bind(this),
          200
        );
      }
    },
    handleChange: function(event) {
      var file = event.target.files[0];
      if (file && file.type.match(/^image\/(png|jpeg)$/)) {
        this.preview = window.URL.createObjectURL(file);
      }
    },
    handleClick: function() {
      alert("クリックしたよ");
    },
    handleInput: function(event) {
      this.message = event.target.value;
    },
    handler: function(comment) {
      //console.log(comment);
    }
  }
};
</script>