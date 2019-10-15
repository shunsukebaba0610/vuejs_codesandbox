<template>
  <div>
    <button v-on:click="handleClick">カウントアップ</button>
    <button v-on:click="show=!show">表示/非表示</button>
    <span ref="count" v-if="show">0</span>
    <br>
    <br>
    <ul>
      <li
        v-for="(item, index) in list"
        v-bind:key="item.id"
        v-bind:class="{ tuyoi: item.hp > 300 }"
      >
        <button v-on:click="doRemove(index)">削除</button>
        ID.{{ item.id }}{{ item.name }} HP.{{ item.hp }}
        <span v-if="item.hp > 300">つよい！</span>
        <button v-on:click="doAttack(index)">攻撃</button>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Lesson",
  data() {
    return {
      list: [],
      show: true,
      num: 1,
      url: "https://pohjd.codesandbox.io/json/list.json"
    };
  },
  created: function() {
    this.apiRequest(this.url);
  },
  methods: {
    handleClick: function() {
      var count = this.$refs.count;
      if (count) {
        count.innerText = parseInt(count.innerText, 10) + 1;
      }
    },
    doAdd: function() {
      // リスト内で1番大きいIDを取得
      var max = this.list.reduce(function(a, b) {
        return a > b.id ? a : b.id;
      });
      this.list.push({ id: max + 1, name: this.name, hp: 500 });
    },
    doRemove: function(index) {
      this.list.splice(index, 1);
    },
    doAttack: function(index) {
      this.list[index].hp -= 10;
    },
    apiRequest: function(url) {
      axios
        .get(url)
        .then(
          function(response) {
            this.list = response.data;
          }.bind(this)
        )
        .catch(function(e) {
          console.error(e);
        });
    }
  }
};
</script>
<style lang="scss" scoped>
ul {
  li {
    list-style-type: none;
  }
}
</style>