<template>
  <div class="row col-12 q-ma-lg">
    <h2>welcome to Login pagw</h2>
    <div class="row col-12">
      <q-input square standout v-model="userName" label="user name" />
    </div>
    <div class="row col-12 q-mt-lg">
      <q-input square standout v-model="password" label="password" />
    </div>
    <q-btn label="submit" class="primary q-mt-lg" @click="submit" />
  </div>
</template>
<script setup>
import { api } from "src/boot/axios";
import { useRouter } from "vue-router";
import { ref } from "vue";

const userName = ref();
const password = ref();

const router = useRouter();
const submit = () => {
  api
    .post("/accounts/api/v1/user/login/", {
      email: userName.value,
      password: password.value,
    })
    .then((result) => {
      console.log(result);
      api.defaults.headers.common["Authorization"] =
        "Bearer " + result.data.access_token;
      router.push("/");
    })
    .catch((err) => {
      alert(err.response.data.detail);
    });
};
</script>
