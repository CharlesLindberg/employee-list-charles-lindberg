<!-- EmployeeList.vue -->
<template>
  <div class="employee-list">
    <h1>Our team</h1>
    <div v-for="employee in employees" :key="employee.id" class="employee">
      <img :src="employee.avatar" alt="Profile" class="profile-pic" />
      <div class="employee-details">
        <h2>{{ employee.first_name }} {{ employee.last_name }}</h2>
        <a :href="'mailto:' + employee.email">Contact</a>
      </div>
    </div>
    <div class="pagination">
      <button
        @click="fetchEmployees(currentPage - 1)"
        :disabled="currentPage <= 1"
      >
        Previous Page
      </button>
      <button
        @click="fetchEmployees(currentPage + 1)"
        :disabled="currentPage >= totalPages"
      >
        Next Page
      </button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      employees: [],
      currentPage: 1,
      totalPages: 1,
    };
  },
  methods: {
    fetchEmployees(page) {
      if (page < 1 || page > this.totalPages) return;

      axios
        .get(`https://reqres.in/api/users?page=${page}`)
        .then((response) => {
          this.employees = response.data.data;
          this.currentPage = page;
          this.totalPages = response.data.total_pages;
        })
        .catch((error) => {
          console.error("There was an error fetching the employees!", error);
        });
    },
  },
  created() {
    this.fetchEmployees(this.currentPage);
  },
};
</script>

<style scoped>
.employee-list {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  border: 1px solid #e0e0e0;
  text-align: center;
}

.employee-list h1 {
  font-size: 50px;

  background: linear-gradient(
    66deg,
    rgba(21, 61, 255, 0.8548012955182073) 12%,
    rgba(255, 8, 58, 0.8632046568627451) 81%
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-fill-color: transparent;
}

.employee {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 10px;
  transition: background-color 0.3s, transform 0.3s;
}

.employee:hover {
  background-color: #f9f9f9;
  transform: translateY(-5px);
}

.profile-pic {
  border-radius: 50%;
  width: 100px;
  height: 100px;
  margin-right: 20px;
}

.employee-details {
  flex: 1;
  text-align: left;
}

.employee-details h2 {
  margin: 0 0 10px;
  font-size: 1.5em;
  color: #333;
}

.employee-details a {
  color: #007bff;

  text-decoration: none;
  font-weight: bold;
  transition: color 0.3s;
}

.employee-details a:hover {
  color: #0056b3;
}

.pagination {
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
}

.pagination button {
  padding: 10px 20px;

  background: rgb(149, 149, 149);
  background: linear-gradient(
    357deg,
    rgba(149, 149, 149, 1) 2%,
    rgba(58, 58, 58, 1) 66%
  );
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background 0.3s;
}

.pagination button:disabled {
  background: #ddd;
  cursor: not-allowed;
}

.pagination button:hover:not(:disabled) {
  background-color: grey;

  transform: scale(1.02);
}

@media (max-width: 600px) {
  .employee {
    flex-direction: column;
    align-items: center;
  }

  .profile-pic {
    width: 75px;
    height: 75px;
    margin-right: 0;
    margin-bottom: 10px;
  }

  .employee-details {
    text-align: center;
  }

  .employee-details h2 {
    font-size: 1.2em;
  }
}
</style>
