<template>
  <div v-if="isUserLoggedIn && user.type == 'admin'">
    <main-header navsel="back"></main-header>
    <h1>สร้างผู้ใช้งาน</h1>
    <form v-on:submit.prevent="createUser">
      <p>ชื่อ: <input type="text" v-model="user.name" /></p>
      <p>นามสกุล: <input type="text" v-model="user.lastname" /></p>
      <p>E-mail: <input type="text" v-model="user.email" /></p>
      <p>รหัสผ่าน: <input type="text" v-model="user.password" /></p>
      <p><button type="submit">สร้างผู้ใช้งาน</button></p>
    </form>
    <hr />
    <div>
      <p>ชื่อ: {{ user.name }}</p>
      <p>นามสกุล: {{ user.lastname }}</p>
      <p>E-mail: {{ user.email }}</p>
      <p>รหัสผ่าน: {{ user.password }}</p>
    </div>
  </div>
</template>
<script>
import UsersService from "@/services/UsersService";

export default {
  data() {
    return {
      user: {
        name: "",
        lastname: "",
        email: "",
        password: "",
        status: "active",
      },
    };
  },
  methods: {
    async createUser() {
      try {
        await UsersService.post(this.user);
        this.$router.push({
          name: "users",
        });
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
<style scoped>
</style>