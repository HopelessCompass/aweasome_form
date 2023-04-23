
<template>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.4/css/bulma.min.css">
  <p>Электропочта <input v-model="mail"></p>
  <p>Пароль <input v-model="password" type="password"></p>
  <p>
    <input type="date" id="input-date">
  </p>
  <button v-on:click="validate()">Забронировать мероприятие</button>
  <ul id="example-1">
    <ul id="v-for-object" class="demo">
  <li v-for="value in meetings">
    {{ value.mail, value.date }}
  </li>
</ul>
</ul>
  <div>

  </div>
</template>

<script setup lang="ts">
let mail: string = '';
let password: string = '';
let meetings: Array<object> = [{}];

let flag_mail: boolean = false;
let flag_password: boolean = false;
let flag_date: boolean = false;

function validate(): void {
  console.log('It works');

  if (mail.indexOf('@') == -1) {
    console.log('Почта некорректна');
    alert('Почта некорректна');
  } else {
    flag_mail = true;
  }

  if (password.length < 6) {
    console.log('Пароль некорректен')
    alert('Пароль должен содержать от 6 символов')
  } else {
    flag_password = true;
  }
  // Получаем текущую дату
  const currentDate :Date = new Date();
  // Получаем значение даты из input
  const inputDate :Date = new Date(document.getElementById("input-date").value);
  
  // Сравниваем даты
  if (inputDate > currentDate) {
    console.log("Дата в будущем!");
  } else if (inputDate < currentDate) {
    console.log("Дата в прошлом!");
  } else {
    flag_date = true;
    console.log("Дата совпадает с текущей датой!")
  }
  add(mail, inputDate);
};

function add(user: string, date: Date) {
  meetings.push({
    obj_user: user,
    obj_date: date
  });
</script>

<style>
</style>