<template>
    <div>
        <div class="row">
            <div class="col-4 ">
                <button type="button" class="mx-auto btn btn-primary" @click="addInput()">Add</button>
            </div>
            <div class="col-4">
                <button type="button" class="btn btn-secondary" @click="postApi()">Save</button>
            </div>
            <div class="col-4">
                <button type="button" class="btn btn-success" @click="getApi()">Update</button>
            </div>
        </div>
        <table class="table" >
            <thead>
                <tr class="row">
                    <th class="col-3">Name</th>
                    <th class="col-3">Birthday</th>
                    <th class="col-3">Salary</th>
                    <th class="col-3">Address</th>
                </tr>
            </thead>
            <tbody id="app">

                <tr class="row emp_data" id="emp" v-for="(emp, index) in newemp" :key="index">
                    <th class="col-3"><input name="name" type="text" v-model="emp.name"/></th>
                    <th class="col-3"><input name="dateOfBirth" type="date" v-model="emp.dateOfBirth"/></th>
                    <th class="col-3"><input name="salary" type="range" min="0" max="100000" v-model="emp.salary"/></th>
                    <th class="col-3"><input name="address" type="text" v-model="emp.address"/></th>
                </tr>
                <tr class="row" id="employee" v-for="emp in employee" :key="emp.name">
                    <th class="col-3"><input type="text" v-model="emp.name"/></th>
                    <th class="col-3"><input type="date" v-model="emp.dateOfBirth"/></th>
                    <th class="col-3"><input type="range" min="0" max="100000" v-model="emp.salary"/></th>
                    <th class="col-3"><input type="text" v-model="emp.address"/></th>
                </tr>

            </tbody>
        </table>
    </div>
</template>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.min.js"></script>

<script>
export default {
  data () {
    return {
      employee: null,
      newemp:[]
    }
  },
  mounted () {
  },
  methods: {
    getApi(){
        axios
      .get('http://localhost:8080/emp/getEmp')
      .then(response => (this.employee = response.data))
      .catch(function (error) {
        console.log(error);
      });
    },
    postApi(){
        const jsonData = this.newemp.concat(this.employee);
        console.log(jsonData);
        axios.post('http://localhost:8080/emp/create',jsonData)
        .then( res=>{
            this.newemp = [];
            this.getApi();
            }
        );
    },
    addInput(){
       this.newemp.push(
            {
                name: '',
                dateOfBirth: '',
                salary: '',
                address: ''
            }
        )
    }
  }
}
</script>
