<template>
  <div class="Jss">
    <div class="gezi">
      <p
        class="el-icon-circle-plus"
        style="font-size: 50px; cursor: pointer"
        v-if="fact"
        @click="select"
      ></p>

      <el-select placeholder="选择角色" v-if="tacf" v-model="value">
        <el-option
          v-for="item in options"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        >
        </el-option>
      </el-select>
      <el-button
        type="success"
        v-if="tacf"
        style="margin: 0 0 15px 0"
        @click="final"
        plain
        >确定</el-button
      >

      <div class="xitong" v-if="acc">
        <p>{{ juesem }}</p>
        <!-- 角色名 -->
        <p>力量</p>
        <el-input-number size="mini" v-model="num1"></el-input-number>
        <p>速度</p>
        <el-input-number size="mini" v-model="num2"></el-input-number>
        <p>智力</p>
        <el-input-number size="mini" v-model="num3"></el-input-number>
        <p>神志</p>
        <el-input-number size="mini" v-model="num4"></el-input-number>
        <p>能力考验</p>
        <el-radio v-model="radio" label="1" style="margin: 0 5px; padding: 0"
          >力量</el-radio
        >
        <el-radio v-model="radio" label="2" style="margin: 0 5px; padding: 0"
          >速度</el-radio
        >
        <el-radio v-model="radio" label="3" style="margin: 0 5px; padding: 0"
          >智力</el-radio
        >
        <el-radio v-model="radio" label="4" style="margin: 0 5px; padding: 0"
          >神志</el-radio
        >
        <br />
        <!--投掷骰子-->
        <el-button 
          @click="qthrow"
          type="success"
          icon="el-icon-check"
          style="margin: 10px 0 0 0" 
          circle
        ></el-button>
        <br />
        <el-input
          placeholder=""
          v-model="input"
          :disabled="true"
          style="width: 50px; margin: 10px 0"
        >
        {{input}}
        </el-input>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      juesem: "", //角色名
      input: "", //计算结果
      radio: "1", //单选
      shake:'1',//确认骰子数量
      num1: "", //各项能力
      num2: "",
      num3: "",
      num4: "",
      fact: true, //添加角色
      tacf: false, //选择角色
      acc: false,
      arr: [
        //角色
        {
          id: 1,
          name: "角色1",
          li: 5,
          su: 5,
          zhi: 5,
          shen: 5,
        },
        {
          id: 2,
          name: "角色2",
          li: 6,
          su: 6,
          zhi: 6,
          shen: 6,
        },
        {
          id: 3,
          name: "角色3",
          li: 4,
          su: 4,
          zhi: 4,
          shen: 4,
        },
        {
          id: 4,
          name: "角色4",
          li: 2,
          su: 3,
          zhi: 4,
          shen: 4,
        },
        {
          id: 5,
          name: "角色5",
          li: 1,
          su: 4,
          zhi: 5,
          shen: 6,
        },
      ],
      options: [
        //多选选择
        {
          value: "1",
          label: "角色1",
        },
        {
          value: "2",
          label: "角色2",
        },
        {
          value: "3",
          label: "角色3",
        },
        {
          value: "4",
          label: "角色4",
        },
        {
          value: "5",
          label: "角色5",
        },
      ],
      value: "",
      
    };
  },
  // watch: {//监听data属性
	// 		radio(newVal,old) {
  //           console.log("11",newVal,old)
  //           if(this.radio == 1){
  //             this.shake = this.num1
  //           }
  //    }
  //   },
  methods: {
    dice(times) {                            //骰子
      var a = 0;
      for(var i = 1; i <= times; i++){
        console.log("qwe",1)
        let j = this.random(0,2)
        a = a+j;
      }
      return a
    },
    random(lower, upper) {                //随机数
      return Math.floor(Math.random() * (upper - lower + 1)) + lower;
    },
    qthrow() {                           //投掷骰子
      let siwei = this.radio;
      if(siwei == 1){
        console.log("1",this.num1)
        this.input = this.dice(this.num1)

      }else if(siwei == 2){
        console.log("2",this.num2)
        this.input = this.dice(this.num2)
      }else if(siwei == 3){
        console.log("3",this.num3)
        this.input = this.dice(this.num3)
      }else if(siwei == 4){
        console.log("4",this.num4)
        this.input = this.dice(this.num4)
      }
    },
    select() {
      //点击选择角色
      let z = this.fact;
      let j = this.tacf;
      // console.log("真的", z, j);
      if (z === true) {
        z = this.fact = false;
      }
      if (j === false) {
        j = this.tacf = true;
      }
    },

    final() {
      //点击确认角色
      let zz = this.tacf;
      let jj = this.acc;
      if (this.value === "") {
        this.$message({
          message: "请选择角色",
          type: "warning",
        });
        return;
      }
      if (zz === true) {
        this.tacf = false;
      }
      if (jj === false) {
        this.acc = true;
      }

      let power = this.arr; //渲染角色数据
      // localStorage.getItem('key')
      
      power.forEach((item) => {
      
        // console.log("wa",item.li);
        if (this.value == item.id) {
          // console.log('wdd',item.id,this.value)
          this.num1 = item.li;
          this.num2 = item.su;
          this.num3 = item.zhi;
          this.num4 = item.shen;
          this.juesem = item.name;
          return;
        }
      });
      let cun = [{//存储数据
        lang:this.num1,
      },{
        du:this.num2,
      },{
        dui:this.num3,
      },{
        zh:this.num4,
      }]
      // cun.forEach((chu) => {
        localStorage.setItem('key',JSON.stringify(cun))
        console.log("新",localStorage.getItem('key'));
        // return
      // })
      
    },
  },
}
</script>

<style scoped >
.gezi {
  width: 300px;
  /* height: 350px; */
  
  border: 2px solid #000;
  float: left;
  margin: 10px 20px 20px;
  border-radius: 30px;
}
.Jss >>> .el-select {
  margin: 20px auto;
  border-color: #9f9;
}
</style>