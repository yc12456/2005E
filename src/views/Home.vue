<template>
  <div class="Home">
    <div class="Home-box">
      <p>
        <input type="text" v-model="Home_model" placeholder="商品名称" @input="Home_key" />
      </p>

      <table class="Home-table">
        <thead>
          <th>
            编号
            <span>
              <span @click="Home_aaa" v-if="!flgh">▼</span>
              <span @click="Home_a" v-show="flgh">▲</span>
            </span>
          </th>
          <th>名称</th>
          <th>
            价格
            <span >
              <span @click="Home_bbb" v-if="!flay">▼</span>
              <span @click="Home_b" v-show="flay">▲</span>
            </span>
          </th>
        </thead>
        <tbody>
          <tr v-for="(ele,index) in num" :key="index">
            <td>{{ele.id}}</td>
            <td>{{ele.goods_name}}</td>
            <td>{{ele.price}}</td>
          </tr>
        </tbody>
      </table>
      <template>
        <div class="block">
          <el-pagination
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
            :current-page="currentPage4"
            :page-sizes="[2, 3, 4, 10]"
            :page-size="pagesize"
            layout="total, sizes, prev, pager, next, jumper"
            :total="list.length"
          ></el-pagination>
        </div>
      </template>
    </div>
  </div>
</template>
            </div>
           
</div>
</template>

<script>
import Fan from "../components/fan";
import Tuo from "../components/tuo";
export default {
  data() {
    return {
      Home_model: "",
      list: [],
      currentPage4: 1,
      pagesize: 6,
      flgh: false,
      flay: false,
      hhhh:false
    };
  },
  mounted() {
    this.getlist();
  },
  methods: {
    getlist() {
      this.$http("/data.json", "get").then((date) => {
        console.log(date.data.data);
        this.list = date.data.data;
      });
    },
    Home_key() {
      this.list = this.list.filter((i) => {
        return i.goods_name.includes(this.Home_model);
      });
    },
    handleSizeChange(e) {
      this.pagesize = e;
    },
    handleCurrentChange(e) {
      this.currentPage4 = e;
    },
    Home_aaa() {
      this.flgh = !this.flgh;
      return this.list.sort(function (a, b) {
        return b.id - a.id;
      });
    },
    Home_bbb() {
      this.flay = !this.flay;
      return this.list.sort(function (a, b) {
        return b.price - a.price;
      });
    },
    Home_a() {
      this.flgh = !this.flgh;
      this.$http("/data.json", "get").then((date) => {
        this.list = date.data.data;
      });
    },
    Home_b() {
      this.flay = !this.flay;
      this.$http("/data.json", "get").then((date) => {
        this.list = date.data.data;
      });
    },
    
  },
  components: {
    Fan,
    Tuo
  },
  computed: {
    num() {
      return this.list.slice(
        this.pagesize * (this.currentPage4 - 1),
        this.pagesize * this.currentPage4
      );
    },
  },
};
</script>

<style lang='scss'>
.Home {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.Home-box {
  width: 80vw;
  height: 60vh;
  background-color: aquamarine;
  padding: 1vw 2vw;
}
.Home-table {
  width: 100%;
}
th {
  width: 33%;
}
</style>
