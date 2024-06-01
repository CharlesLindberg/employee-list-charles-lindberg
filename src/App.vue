<template>
  <div id="app">
    <header>
      <img
        src="@/assets/vendre-optimizers_logo-black.webp"
        alt="Logo"
        class="logo"
      />
      <h1></h1>
    </header>
    <main>
      <EmployeeList />
    </main>
    <footer>
      <p>&copy; 2024 Vendre. All rights reserved.</p>
    </footer>
  </div>
</template>

<script>
import EmployeeList from "./components/EmployeeList.vue";

export default {
  name: "App",
  components: {
    EmployeeList,
  },
};
</script>

<style>
body {
  font-family: "Arial", sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background-color: #f0f2f5;
  color: #333;
}

.logo {
  height: 100px;
  margin-right: 20px;
}

#app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

header {
  background-color: #fff;
  color: #333;
  padding: 20px;
  text-align: center;
  border-bottom: 1px solid #e0e0e0;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

main {
  flex: 1;
  padding: 20px;
}

footer {
  background-color: #fff;
  color: #333;
  padding: 10px;
  text-align: center;
  border-top: 1px solid #e0e0e0;
  box-shadow: 0 -2px 4px rgba(0, 0, 0, 0.1);
}

@media (max-width: 600px) {
  header {
    padding: 15px;
  }

  main {
    padding: 10px;
  }

  footer {
    padding: 5px;
  }
}
</style>
