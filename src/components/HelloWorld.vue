<template>
  <el-container>
    <el-header >Prediction model</el-header>
    <el-main>
      <el-row type="flex" justify="center">
        <el-col  :span="8">
          <el-card :body-style="{  padding: '20px' }" v-loading="loading">
            <div v-if="visit[0]">
              <h2>{{data_list[options[0]].question}}</h2>
              <el-radio-group v-model="radio[0]"  @change="change($event,options[0])">
                <el-radio :label="select_value[0][0]">{{data_list[options[0]].leop}}</el-radio>
                <el-radio :label="select_value[0][1]">{{data_list[options[0]].riop}}</el-radio>
              </el-radio-group>
            </div>
            <el-row></el-row>
            <div v-if="visit[1]">
              <h2>{{data_list[options[1]].question}}</h2>
              <el-radio-group v-model="radio[1]"  @change="change($event,options[1])">
                <el-radio :label="select_value[1][0]">{{data_list[options[1]].leop}}</el-radio>
                <el-radio :label="select_value[1][1]">{{data_list[options[1]].riop}}</el-radio>
              </el-radio-group> 
            </div>
            <div v-if="visit[2]">
              <h2>{{data_list[options[2]].question}}</h2>
              <el-radio-group v-model="radio[2]"  @change="change($event,options[2])">
                <el-radio :label="select_value[2][0]">{{data_list[options[2]].leop}}</el-radio>
                <el-radio :label="select_value[2][1]">{{data_list[options[2]].riop}}</el-radio>
            </el-radio-group>
            </div>
            <div v-if="visit[3]">
              <h2>{{data_list[options[3]].question}}</h2>
              <el-radio-group v-model="radio[3]"  @change="change($event,options[3])">
                <el-radio :label="select_value[3][0]">{{data_list[options[3]].leop}}</el-radio>
                <el-radio :label="select_value[3][1]">{{data_list[options[3]].riop}}</el-radio>
              </el-radio-group>
            </div>
            <div v-if="visit[4]">
              <h2>{{data_list[options[4]].question}}</h2>
              <el-radio-group v-model="radio[4]"  @change="change($event,options[4])">
                <el-radio :label="select_value[4][0]">{{data_list[options[4]].leop}}</el-radio>
                <el-radio :label="select_value[4][1]">{{data_list[options[4]].riop}}</el-radio>
            </el-radio-group>
            </div>
            <div>
              <el-button @click="handle_perdict">
                Predict
              </el-button>
              <el-button @click="reset">
                Reset
              </el-button>
            </div>
            <div v-if="p_visit">
              <h3>The probability is {{ prob }}</h3>
            </div>
          </el-card>
          
        </el-col>
      </el-row>
    </el-main>
  </el-container>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  created() {
    this.reset();
    
  },
  data() {
    return {
      loading: false,
      data_list: [
        {
          name:"Cohor",
          question:"Lesions with Spiculation  or Lesions without Spiculation",
          leop:"Lesions with Spiculation",
          riop:"Lesions without Spiculation",
          left:1,
          right: 2,
          height:0,
          P : 0.1151
        },
        {
          name:"Lesions with Spiculation",
          question:"Long - Axis Diameters of the Solid Portions",
          leop:"Long - Axis Diameters of the Solid Portions(≥ 1 Lesions ≥ 27 mm)",
          riop:"Long - Axis Diameters of the Solid Portions(All Lesions < 27 mm)",
          left:3,
          right: 4,
          height:1,
          P: 0.2642
        },
        {
          name:"Lesions without Spiculation",
          question: undefined,
          height:1,
          P: 0.0014
        },
        {
          name:"Long - Axis Diameters of the Solid Portions(≥ 1 Lesions ≥ 27 mm)",
          question:"Lesions with Spiculation",
          leop:"Lesions with Spiculation (N = 1)",
          riop:"Lesions with Spiculation (N ≥ 2)",
          left:5,
          right: 6,
          height:2,
          P: 0.3718
        },
        {
          name:"Long - Axis Diameters of the Solid Portions(All Lesions < 27 mm)",
          question:"CTR",
          leop:"CTR(≥ 2 Lesions ≥ 0.90)",
          riop:"CTR (0 & 1 Lesion ≤ 0.90)",
          left: 7,
          right: 8,
          height:2,
          P: 0.0888
        },
        {
          name:"Lesions with Spiculation (N = 1)",
          question:"Pure Solid Nodules",
          leop:"Pure Solid Nodules (N ≥ 2)",
          riop:"Pure Solid Nodules (N = 0 & 1)",
          left:9,
          right: 10,
          height:3,
          P: 0.3905
        },
        {
          name:"Lesions with Spiculation (N>2)",
          question: undefined,
          height:3,
          P: 0.3196
        },
        {
          name:"CTR(≥ 2 Lesions ≥ 0.90)",
          question:undefined,
          height:3,
          P: 0.1608
        },
        {
          name:"CTR (0 & 1 Lesion ≥ 0.90)",
          question: undefined,
          height:3,
          P: 0.0625
        },
        {
          name:"Pure Solid Nodules (N > 2)",
          question:undefined,
          height:4,
          P: 0.4540
        },
        {
          name:"Pure Solid Nodules (N = 0 & 1)",
          question:"Long - Axis Diameters of the Lesions",
          leop:"Long - Axis Diameters of the Lesions(≥ 1 Lesions ≥ 30 mm)",
          riop:"Long - Axis Diameters of the Lesion(All Lesions ≤ 30 mm)",
          left:11,
          right: 12,
          height:4,
          P: 0.3589
        },
        {
          name:"Long - Axis Diameters of the Lesions(≥ 1 Lesions ≥ 30 mm)",
          question:undefined,
          height:5,
          P: 0.4330
        },
        {
          name:"Long - Axis Diameters of the Lesion(All Lesions ≤ 30 mm)",
          question:undefined,
          height:5,
          P: 0.2440
        },
      ],
      id: 0,
      options:[
        0,1,3,5,10,11
      ],
      visit:[
        true,false,false,false,false
      ],
      radio:[0,0,0,0,0],
      select_value:[
        [1,2],[0,0],[0,0],[0,0],[0,0]
      ],
      prob:0,
      p_visit:false
    }
  },
  methods:{
    reset(){
      this.id = 0
      this.p_visit = false;
      this.visit = [
        true,false,false,false,false
      ];
      this.radio = [0,0,0,0,0];
    },
    handleLeft(){
      let id = this.id
      this.id = this.data_list[id].left
    },
    handleRight(){
      let id = this.id
      this.id = this.data_list[id].right
    },
    change(val, idx){
      this.loading = true
      this.$nextTick(() => {
        let now = this.data_list[idx]
        let height = now.height
        for (let i = height+1 ;i < this.visit.length;i++){
          this.visit[i] = false;
        }
        this.$set(
            this.visit,
          )
        this.options[height+1] = val
        let iss = this.radio[height]
        if (this.data_list[iss].left != undefined){
          this.visit[height+1] = true;
          this.select_value[height + 1][0] = this.data_list[iss].left
          this.select_value[height + 1][1] = this.data_list[iss].right
        }
        this.$set(
            this.visit,
            this.select_value
          )
        this.loading = false
      });
    },
    handle_perdict(){
      let idx = 0
      for(let i in this.visit){
        if(this.visit[i]){
          idx = this.radio[i]
        }
      }
      this.prob = this.data_list[idx].P
      this.p_visit = true
    }
  }
}
</script>


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

 .el-header {
   background-color: #409EFF;
   color: #333;
   line-height: 60px;

 }


</style>
