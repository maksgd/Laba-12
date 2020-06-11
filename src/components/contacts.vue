<template>
  <div id="app">
    <div>
      <div>
        <label>Фамилия 
          <input type="text" v-model="contNow.surname">
        </label>
      </div>
      <div>
        <label>Имя 
          <input type="text" v-model="contNow.name">
        </label>
      </div>
      <div>
        <label>Отчество 
          <input type="text" v-model="contNow.otchestvo">
        </label>
      </div>
      <div>
        <label>Телефон 
          <input type="text" v-model="contNow.phone">
        </label>
      </div>
      <div>
        <label>Избранное 
          <input type="checkbox" v-model="contNow.fav">
        </label>
      </div>
    </div>
    <div>
      <button v-on:click="addContact()">Записать</button>
    </div>
    <div>
      <p>Сортировать</p>
      <input type="radio" name="sort" value="surname" v-on:click="contactsSort('surname')"> По фамилии
      <input type="radio" name="sort" value="name" v-on:click="contactsSort('name')"> По имени
    </div>
    <div>
      <ul>Список контактов
        <li v-for="(item, index) in contacts" v-bind:key=index>{{item.surname}} {{item.name}} {{item.otchestvo}} {{item.phone}}
          <span v-if="item.fav">❤</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    name: "contacts",
    data() {
      return {
        contNow: {
          surname: "",
          name: "",
          otchestvo: "",
          phone: "",
          fav: false,
        },
        contacts: [],
      }
    },
    methods: {
      addContact: function () {
        if (this.contNow.surname != "" && this.contNow.name != "" && this.contNow.phone != "") {
          this.contacts.push({
            surname: this.contNow.surname,
            name: this.contNow.name,
            otchestvo: this.contNow.otchestvo,
            phone: this.contNow.phone,
            fav: this.contNow.fav
          });
          this.contNow.surname = "";
          this.contNow.name = "";
          this.contNow.otchestvo = "";
          this.contNow.phone = "";
          this.contNow.fav = false;
        }
        else {
          alert("Заполните поля Фамилия, Имя и Телефон!");
        }
      },
      contactsSort : function (typeSort) {
        if (typeSort === "surname") {
          this.contacts.sort((c1, c2) => c1.surname < c2.surname ? 1 : -1);
        }
        else {
          if (typeSort === "name") {
            this.contacts.sort((c1, c2) => c1.name < c2.name ? 1 : -1);
          }
        }
        this.contacts.sort((c1, c2) => c1.fav < c2.fav ? 1 : -1);
      },
      deleteContact: function (id) {
        this.contacts.splice(id, 1);
      }
    }
  }
</script>