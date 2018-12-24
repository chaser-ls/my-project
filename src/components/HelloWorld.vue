<template>
  <div class="hello">
    <div class="container">
      <div class="row">
        <div class="col-md-3"></div>
        <div class="col-md-6 col-md-offset-3">
          <div class="input-group">
            <label style="margin-top: 2%">Name:</label>
            <input v-model="newPerson.name" type="text" class="form-control" placeholder="请输入您的姓名...">
            <span class="warn">{{warnName}}</span>
          </div>
          <br>
          <div class="input-group">
            <label style="margin-right: 3%;margin-top: 2%">Age:</label>
            <input  v-model="newPerson.age" type="text" class="form-control" placeholder="请输入您的年龄...">
            <span class="warn">{{warnAge}}</span>
          </div>
          <br>
          <div class="input-group">
            <label style="margin-right: 3%;margin-top: 2%">Sex:</label>
            <select  v-model="newPerson.sex" >
              <option value="Male">Male</option>
              <option value="Female">Female</option>
            </select>
          </div>
          <br>
          <button v-on:click="create" type="button" class="btn btn-info ">create</button>
          <button v-on:click="changeTableStyle" class="btn btn-danger">changeTableStyle</button>
        </div>
      </div>
       <br>
      <div class="row">
        <div class="col-md-3"></div>
        <div class="col-md-6 col-md-offset-">
          <form>
            <table v-bind:class="[isActive? beforeTableStyle:'',afterTableStyle]">
              <thead>
                <td>Name</td>
                <td>Age</td>
                <td>Sex</td>
                <td>Delete</td>
				      </thead>
              <tbody>
                <tr v-for="(person, index) in people" :key="index">
                  <td>{{ person.name }}</td>
                  <td>{{ person.age }}</td>
                  <td>{{ person.sex }}</td>
                  <td><button @click="Delete(person,index)">Delete</button></td>
                </tr>
              </tbody>
            </table>
          </form>
        </div>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      warnName:'',
      warnAge:'',
      newPerson: {
					name: '',
					age: '',
					sex: 'Male',
        },
        people: [],
        isActive:false,
        beforeTableStyle:{
          'table':true,
          'table-bordered':true,
          'table-hover':true,
        },
        afterTableStyle:{
          'table':true,
          'table-bordered':true,
          'table-background':true
        }
    }
  },
  methods:{
    create: function (){
      if(this.newPerson.name==''&&this.newPerson.age==''){
        this.warnName='*选项不允许为空！'
        this.warnAge='*选项不允许为空！'
      }else if (this.newPerson.name=='') {
        this.warnAge=''
        this.warnName='*选项不允许为空！'
      }else if (this.newPerson.age=='') {
        this.warnName=''
        this.warnAge='*选项不允许为空！'
      }else{
        this.people.unshift(this.newPerson)
      //添加完newPerson对象后，重置它
        this.newPerson = {
          name: '',
          age: '',
          sex: 'Male',
        },
        this.warnName='',
        this.warnAge=''
      }
    },
    Delete: function(index){
      this.people.splice(index, 1)
    },
    changeTableStyle(){
      this.isActive=!this.isActive
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .warn{color:red}
  .table-background{background: rgb(233, 206, 156)}
</style>
