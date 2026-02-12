<template>
  <div class="coffee-navbar">
    <ul class="nav">

      <!-- เมนูกาแฟ (ทุกคนเห็น) -->
      <li>
        <router-link to="/coffees">
          Menu
        </router-link>
      </li>

      <!-- Order -->
      <li>
        <router-link to="/orders">
          Order
        </router-link>
      </li>

      <!-- แสดงเมื่อ Login แล้ว -->
      <li v-if="isLoggedIn">
        <router-link to="/blogs">
          Blog
        </router-link>
      </li>

      <li v-if="isLoggedIn">
        <router-link to="/users">
          User
        </router-link>
      </li>

      <!-- ยังไม่ Login -->
      <li v-if="!isLoggedIn">
        <router-link :to="{ name: 'login' }">
          Login
        </router-link>
      </li>

      <!-- Login แล้ว -->
      <li v-if="isLoggedIn">
        <a href="#" @click.prevent="logout">
          Logout
        </a>
      </li>

    </ul>

    <div class="clearfix"></div>
  </div>
</template>

<script>
import { useAuthenStore } from '@/stores/authen'

export default {
  name: 'CoffeeHeader',
  computed: {
    isLoggedIn () {
      const authenStore = useAuthenStore()
      return authenStore.isUserLoggedIn
    }
  },
  methods: {
    logout () {
      const authenStore = useAuthenStore()
      authenStore.logout()
      this.$router.push({ name: 'login' })
    }
  }
}
</script>

<style scoped>
.coffee-navbar {
  background-color: #1e90ff; /* ฟ้า */
  width: 100%;
  padding: 10px 15px;
  border-radius: 12px;        /* ขอบมนทั้งแถบ */
}

.coffee-navbar .nav {
  list-style: none;
  margin: 0;
  padding: 0;
  float: left;
}

.coffee-navbar .nav li {
  float: left;
  margin-right: 6px;
}

.coffee-navbar .nav li a {
  display: block;
  padding: 10px 16px;
  text-decoration: none;
  color: white;
  font-weight: bold;
  border-radius: 10px;        /* ขอบมนปุ่ม */
  transition: background-color 0.3s;
}

.coffee-navbar .nav li a:hover {
  background-color: #63b3ff; /* ฟ้าอ่อน */
}

.coffee-navbar .nav li a.router-link-active {
  background-color: #0b5ed7; /* ฟ้าเข้ม */
}

.clearfix {
  clear: left;
}
</style>