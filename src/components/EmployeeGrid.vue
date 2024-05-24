

<template>
  <div>
    <button @click="openForm">Add Employee</button>
    <table>
      <thead>
        <tr>
          <th>EmployeeId</th>
          <th>FirstName</th>
          <th>LastName</th>
          <th>DOB</th>
          <th>Salary</th>
          <th>Address</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="employee in employees" :key="employee.EmployeeId">
          <td>{{ employee.EmployeeId }}</td>
          <td>{{ employee.FirstName }}</td>
          <td>{{ employee.LastName }}</td>
          <td>{{ employee.DOB }}</td>
          <td>{{ employee.Salary }}</td>
          <td>{{ employee.Address }}</td>
          <td>
            <button @click="openForm(employee)">Edit</button>
            <button @click="deleteEmployee(employee.EmployeeId)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
    <EmployeeForm
      v-if="isFormVisible"
      :employee="currentEmployee"
      @save="saveEmployee"
      @close="closeForm"
    />
  </div>
</template>

<script>
import employees from '../data/employees';
import EmployeeForm from './EmployeeForm.vue';

export default {
  components: { EmployeeForm },
  data() {
    return {
      employees,
      isFormVisible: false,
      currentEmployee: null,
    };
  },
  methods: {
    openForm(employee = null) {
      this.currentEmployee = employee;
      this.isFormVisible = true;
    },
    closeForm() {
      this.currentEmployee = null;
      this.isFormVisible = false;
    },
    saveEmployee(employee) {
      if (employee.EmployeeId) {
        const index = this.employees.findIndex(e => e.EmployeeId === employee.EmployeeId);
        if (index !== -1) {
          this.$set(this.employees, index, employee);
        }
      } else {
        employee.EmployeeId = this.employees.length + 1;
        this.employees.push(employee);
      }
      this.closeForm();
    },
    deleteEmployee(id) {
      this.employees = this.employees.filter(employee => employee.EmployeeId !== id);
    },
  },
};
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

table, th, td {
  border: 1px solid black;
}

th, td {
  padding: 10px;
  text-align: left;
}

button {
  margin-right: 5px;
}
</style>
