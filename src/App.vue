<template>
  <div class="app">
    <div class="navbar">
      <div class="dropdown">
        <img src="./assets/menuPic.png" alt="menu picture" class="dropbtn" />
        <div class="dropdown-content">
          <ul>
            <li
              v-for="option in dropdownOptions"
              :key="option"
              @click="dropdownSelect(option.title)"
            >
              {{ option.title }}
            </li>
          </ul>
        </div>
      </div>
      <span class="activeUser">{{ activeUser }}</span>

      <Button title="log out" @click="logout()" />
    </div>

    <div v-if="loading">
      <div class="loader"></div>
    </div>
    <div v-else>
      <table class="userTable">
        <tr>
          <th>User:</th>
          <th>Name:</th>
          <th>E-mail:</th>
        </tr>
        <tr
          id="user"
          v-for="user in fetchedData"
          :key="user"
          @click="selectUser(user)"
        >
          <td>{{ user.username }}</td>
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
        </tr>
      </table>
    </div>
  </div>
  <div></div>
  <br />
</template>

<script>
import Button from "./components/Button.vue";

export default {
  name: "App",

  components: {
    Button,
  },

  data() {
    return {
      activeUser: "Unknown user",
      fetchedData: [],
      loading: true,
      dropdownOptions: [
        { title: "Users" },
        { title: "About me" },
        { title: "Admin only" },
      ],
      selectedDropdown: "",
    };
  },

  created() {
    fetch("/v3/efcaa20a-6049-4dc0-9d28-6ece8529dac0?mocky-delay=10000ms")
      .then((res) => res.json())
      .then((data) => {
        this.fetchedData = data;
        this.loading = false;
        console.log(this.fetchedData);
      })
      .catch((err) => console.log(err.message));
  },

  methods: {
    dropdownSelect(selected) {
      this.selectedDropdown = selected;
    },

    selectUser(userData) {
      console.log(userData);
      this.user = userData;
      this.activeUser = userData.username;
    },

    logout() {},
  },
};
</script>

<style>
#title {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: black;
  font-size: 10px;
  margin-top: 30px;
  margin-left: 30px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text: black;
}

.navbar {
  background-color: #4f92dd;
  height: 62px;
}

.dropbtn {
  background-color: #4f92dd;
  color: white;
  padding: 16px;
  font-size: 16px;
  border: none;
}

.dropdown {
  position: relative;
  display: inline-block;
}

.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f1f1f1;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  z-index: 1;
}

.dropdown-content ul li {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}

.dropdown-content ul li:hover {
  background-color: #ddd;
  cursor: pointer;
}

.dropdown:hover .dropdown-content {
  display: block;
}

.dropdown:hover .dropbtn {
  background-color: #ddd;
}

.img {
  height: 100%;
}

.activeUser {
  position: absolute;
  display: inline-block;
  width: 150px;
  margin-top: 23px;
  margin-left: 5px;
}

.userTable {
  width: 100%;
  background-color: #f5f3f3;
  border-collapse: collapse;
  border-style: hidden;
  text-align: justify;
}

.userTable tr {
  border: 1px solid black;
}
#user:hover {
  background-color: #ddd;
  cursor: pointer;
}

.loader {
  border: 16px solid #f3f3f3;
  border-top: 16px solid #4f92dd;
  border-radius: 50%;
  width: 120px;
  height: 120px;
  animation: spin 2s linear infinite;
  margin: auto;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  position: fixed;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
