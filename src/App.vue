
<template>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.4/css/bulma.min.css">
  <p>Электропочта <input v-model="mail"></p>
  <p>Пароль <input v-model="password" type="password"></p>
  <p>
    <input type="date" id="input-date">
  </p>
  <button v-on:click="validate()">Забронировать мероприятие</button>
  <ul>
    <li v-for="value in meetings">
     <p>{{ value }}</p>
  </li>
</ul>
</template>

<script setup lang="ts">
let mail: string = '';
let password: string = '';
let meetings: Array<any> = [];

let flag_mail: boolean = false;
let flag_password: boolean = false;
let flag_date: boolean = false;

function add(user: string, date: Date): void {
   meetings.push({
    obj_user: user,
    obj_date: date
   });
  };

function validate(): void {
  console.log('It works');

  if (mail.indexOf('@') == -1) {
    console.log('Почта некорректна');
    alert('Почта некорректна');
  } else {
    flag_mail = true;
  }

  if (password.length < 6) {
    console.log('Пароль некорректен');
    alert('Пароль должен содержать от 6 символов');
  } else {
    flag_password = true;
  }
  let currentDate :Date = new Date();
  let inputDate :Date = new Date(document.getElementById("input-date").value);

  if (inputDate > currentDate) {
    flag_date = true;
    console.log("Дата в будущем!");
    add(mail, inputDate);
  } else if (inputDate < currentDate) {
    console.log("Дата в прошлом!");
    flag_date = false;
  } else {
    flag_date = true;
    console.log("Дата совпадает с текущей датой!");
  }
  if (flag_mail == true && flag_date == true && flag_password == true) {
    add(mail, inputDate);
    console.log(meetings)
  }
};
</script>

<style>
</style>