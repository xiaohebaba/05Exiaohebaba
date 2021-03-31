<template>
  <div id="app">
    <input type="text" name="" id="" @input.13="search" v-model="val" />
    <table style="cellpadding: 0">
      <tr>
        <th style="width: 300px; font-size: 25px">
          编号<img src="./assets/arrow-down.png" v-show="show" alt="" @click="tab" /><img
            src="./assets/arrow-red.png"
            v-show="!show" @click="tab"
            alt=""
          />
        </th>
        <th style="width: 300px; font-size: 25px">名称</th>
        <th style="width: 300px; font-size: 25px">
          价格<img src="./assets/arrow-down.png" v-show="!show" alt="" @click="tab" /><img
            src="./assets/arrow-red.png"
            v-show="show" @click="tab"
            alt=""
          />
        </th>
      </tr>
      <tr v-for="item in list" :key="item.id">
        <td>{{ item.id }}</td>
        <td>{{ item.goods_name }}</td>
        <td>{{ item.price }}</td>
      </tr>
    </table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      show: true,
      list: [],
      val: "",
      searchList: []
    };
  },
  created() {
    this.$axios({
      url: "data.json",
      method: "get",
    }).then((res) => {
      this.list = res.data.data;
    });
  },
  methods: {
    tab() {
      this.show = !this.show
    },
    
    search() {
      this.list = this.list.filters(function(item) {
        return item.goods_name.include(this.val)
      })
      console.log(this.searchList);
    }
  },
};
</script>

<style>
/* table{
  cellpadding: 0;
} */
th{
  background-color: #ccc;
}
td,th {
  border: 1px solid #ccc;
}
</style>
