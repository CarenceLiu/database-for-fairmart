<!-- upload a good with title,description,num and otc -->
<head>
  <meta charset="utf-8" />
</head>
<template>
  <div class="createInput">
    <div class="title">
      <span id="title">商品标题</span>
      <span id="inputTitle">
        <div id="titleTextbox">
          <el-input
            v-model="inputTitle"
            placeholder="请输入内容"
            @input="change($event)"
          ></el-input>
        </div>
      </span>
    </div>

    <div class="description">
      <span id="description">商品描述</span>
      <span id="inputDescription">
        <div id="descriptionTextbox">
          <el-input
            v-model="inputDescription"
            type="textarea"
            placeholder="请输入内容"
            :autosize="{ minRows: 2, maxRows: 5 }"
            @input="change($event)"
          ></el-input>
        </div>
      </span>
    </div>
    <div class="goodsNum">
      <span id="goodsNum">选择数量</span>
      <span id="selectNum">
        <el-input-number
          v-model="num"
          @change="handleChange"
          :min="1"
          :max="10"
          label="描述文字"
          @input="change($event)"
        ></el-input-number>
      </span>
    </div>
    <div class="price1">
      <span id="price">选择价格</span>
      <span id="inputPrice">
        <div id="priceTextbox">
          <el-input
            v-model="inputPrice"
            placeholder="请输入价格"
            prefix-icon=""
            @input="change($event)"
          ></el-input>
        </div>
      </span>
    </div>
    <div class="catagory">
      <span id="catagory">选择分类</span>
      <span id="selectCatagory">
        <div id="catagorySelector">
          <el-select
            v-model="value"
            placeholder="请选择"
            @input="change($event)"
          >
            <!--
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
              @input="change($event)"
            </el-option>-->
            <el-option label="二手书本" value="1"></el-option>
            <el-option label="数码产品" value="2"></el-option>
            <el-option label="票务转让" value="3"></el-option>
            <el-option label="二手衣物" value="4"></el-option>
            <el-option label="生活用品" value="5"></el-option>
            <el-option label="运动装备" value="6"></el-option>
            <el-option label="其他二手" value="7"></el-option>
          </el-select>
        </div>
      </span>
    </div>
    <div class="confirmButton">
      <div id="button">
        <el-button type="success" @click="sendMsg">确认发布</el-button>
        <el-button type="success" @click="gotoHome">返回</el-button>
      </div>
    </div>

  </div>
</template>

<script>
import GLOBAL from "@/global/global";
import axios from "axios";
export default {
  data() {
    return {
      inputTitle,
      inputDescription: "",
      inputPrice: "",
      num: 1,
      options: [
        { value: "选项1", label: "二手书本" },
        { value: "选项2", label: "数码产品" },
        { value: "选项3", label: "票务转让" },
        { value: "选项4", label: "二手衣物" },
        { value: "选项5", label: "生活用品" },
        { value: "选项6", label: "运动装备" },
        { value: "选项7", label: "其他二手" },
      ],
    };
  },

  components: {},

  computed: {},

  mounted: {},

  methods: {
    handleChange(value) {
      console.log(value);
    },	
    sendMsg() {
      const that = this;

      GLOBAL.picture = "static/logo.jpg";
      //在这里传给后端
      const path = "http://localhost:8081/userpostwanted";
      var goodsInformation = {
        wanted_name: that.inputTitle,
        description: that.inputDescription, 
        price: that.inputPrice,
        category_value: that.value,
        source_id: GLOBAL.currentUser_ID,
      };
      console.log(goodsInformation);
      axios
        .post(path, JSON.stringify(goodsInformation))
        .then(function (response) {
          // response.setContentType("text/javascript;charset=UTF-8");
          var goods = response.data;    
        });
        alert("发布成功");
        this.$router.replace("/");
    },
    gotoHome() {
      this.$router.replace("/");
      //this.$router.go(0)
    },
    change(e) {
      this.$forceUpdate();
    },
  },
};
</script>

<style>
.createInput {
  float: right;
  position: relative;
  width: 1300px;
  height: 670px;
  background: #deb887;

  margin-top: 15px;

  border-top-style: solid;
  border-top-color: darkgray;
  border-top-width: 2px;
}
#titleTextbox,
#descriptionTextbox {
  margin-left: 50px;
  width: 400px;
}
#selectNum,
#priceTextbox,
#catagorySelector {
  margin-left: 50px;
}

.title {
  height: 100px;
  width: 670px;
  position: absolute;
  top: 50px;
  left: 50px;
}
.description {
  height: 100px;
  width: 670px;
  position: absolute;
  top: 150px;
  left: 50px;
}
.goodsNum {
  height: 100px;
  width: 670px;
  position: absolute;
  top: 250px;
  left: 50px;
}
.price1 {
  height: 100px;
  width: 670px;
  position: absolute;
  top: 350px;
  left: 50px;
}
.catagory {
  height: 100px;
  width: 670px;
  position: absolute;
  top: 450px;
  left: 50px;
}
.confirmButton {
  height: 100px;
  width: 670px;
  position: absolute;
  top: 550px;
  left: 50px;
}
.picture {
  height: 300px;
  width: 300px;

  position: absolute;
  left: 700px;
  top: 160px;
}
#title,
#inputTitle {
  float: left;
  margin: auto;
}
#description,
#inputDescription {
  float: left;
}
#goodsNum,
#selectNum {
  float: left;
}
#price,
#inputPrice {
  float: left;
}
#catagory,
#selectCatagory {
  float: left;
}
#button {
  float: center;
}
</style>