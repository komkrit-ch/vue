<template>
  <div id="app" class="small-container">
    <h1>Employees</h1>
    <employee-form @add:employee="addEmployee" />
    <employee-table 
      :employees="Employees" 
      @delete:employee="deleteEmployee"
      @edit:employee="editEmployee" />
  </div>
</template>

<script>
import EmployeeTable from '@/components/EmployeeTable'
import EmployeeForm from '@/components/EmployeeForm'

export default {
  name: 'App',
  components:{
    EmployeeTable,
    EmployeeForm
  },
  data() {
    return {
      Employees:[
        {
          id: 1,
          name: 'Komkrit Chaiarerk',
          email: 'komkrit.ch@gmail.com'
        },
        {
          id: 2,
          name: 'Mayura Chaiyarerk',
          email: 'mayura.ch@gmail.com'
        },
        {
          id: 3,
          name: 'May Chaiyarerk',
          email: 'may.ch@gmail.com'        
      }
    ]
    }
  },
  methods: {
    addEmployee(employee){
      const lastid =
        this.Employees.length > 0 ? this.Employees[this.Employees.length - 1].id : 0;
      const id = lastid + 1;
      const newEmployee = {...employee, id};
      this.Employees = [...this.Employees, newEmployee];
      console.log(this.Employees);
    },
    deleteEmployee(id){
      this.Employees = this.Employees.filter(emp=>emp.id !== id)
    },
    editEmployee(id, updatedEmployee) {      
      this.Employees = this.Employees.map(emp=>emp.id === id ? updatedEmployee : employee) 
    }
  },
}
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
    padding: .8em;
    color: #fff;
  }

  button:hover,
  button:active,
  button:focus {    
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
      max-width: 680px;
    }
</style>
