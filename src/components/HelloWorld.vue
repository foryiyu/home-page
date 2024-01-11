<template>
  <el-container>
    <el-header >demo</el-header>
    <el-main>
      <el-row type="flex" justify="center">
        <el-col  :span="8">
          <el-card :body-style="{  padding: '20px' }">
            <h1>{{this.data_list[id].name}}</h1>
            <h3 v-if="this.data_list[id].question != undefined">{{this.data_list[id].question}}</h3>
            <h3>Probability =  {{this.data_list[id].P}}</h3>
            <el-row type="flex" justify="center">
              <el-col :span="6"><el-button @click="handleLeft" v-if="this.data_list[id].question != undefined">left</el-button></el-col>
              <el-col :span="6"><el-button @click="reset">reset</el-button></el-col>
              <el-col :span="6"><el-button @click="handleRight" v-if="this.data_list[id].question != undefined">right</el-button></el-col>
            </el-row>
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
      data_list: [
        {
          name:"Cohor",
          question:"Lesions with Spiculation  or Lesions without Spiculation",
          left:1,
          right: 2,
          P : 0.1151
        },
        {
          name:"Lesions with Spiculation",
          question:"Long - Axis Diameters of the Solid Portions(≥ 1 Lesions ≥ 27 mm) or Long - Axis Diameters of the Solid Portions(All Lesions < 27 mm)",
          left:3,
          right: 4,
          P: 0.2642
        },
        {
          name:"Lesions without Spiculation",
          question: undefined,
          P: 0.0014
        },
        {
          name:"Long - Axis Diameters of the Solid Portions(≥ 1 Lesions ≥ 27 mm)",
          question:"Lesions with Spiculation (N = 1) or Lesions with Spiculation (N ≥ 2)",
          left:5,
          right: 6,
          P: 0.3718
        },
        {
          name:"Long - Axis Diameters of the Solid Portions(All Lesions < 27 mm)",
          question:"CTR(≥ 2 Lesions ≥ 0.90)?  or CTR (0 & 1 Lesion ≤ 0.90)",
          left: 7,
          right: 8,
          P: 0.0888
        },
        {
          name:"Lesions with Spiculation (N = 1)",
          question:"Pure Solid Nodules (N ≥ 2)  or Pure Solid Nodules (N = 0 & 1)",
          left:9,
          right: 10,
          P: 0.3905
        },
        {
          name:"Lesions with Spiculation (N>2)",
          question: undefined,
          P: 0.3196
        },
        {
          name:"CTR(≥ 2 Lesions ≥ 0.90)",
          question:undefined,
          P: 0.1608
        },
        {
          name:"CTR (0 & 1 Lesion ≥ 0.90)",
          question: undefined,
          left:7,
          right: 8,
          P: 0.0625
        },
        {
          name:"Pure Solid Nodules (N > 2)",
          question:undefined,
          P: 0.4540
        },
        {
          name:"Pure Solid Nodules (N = 0 & 1)",
          question:"Long - Axis Diameters of the Lesions(≥ 1 Lesions ≥ 30 mm)  or Long - Axis Diameters of the Lesion(All Lesions ≤ 30 mm)",
          left:11,
          right: 12,
          P: 0.3589
        },
        {
          name:"Long - Axis Diameters of the Lesions(≥ 1 Lesions ≥ 30 mm)",
          question:undefined,
          P: 0.4330
        },
        {
          name:"Long - Axis Diameters of the Lesion(All Lesions ≤ 30 mm)",
          question:undefined,
          P: 0.2440
        },
      ],
      id: 0
    }
  },
  methods:{
    reset(){
      this.id = 0
    },
    handleLeft(){
      let id = this.id
      this.id = this.data_list[id].left
    },
    handleRight(){
      let id = this.id
      this.id = this.data_list[id].right
    },
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
