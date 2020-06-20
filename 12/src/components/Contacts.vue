<template>
  <div>
    <div class="form-group w-100">
      <label for="name_id">Введите имя</label>
      <input type="text" id="name_id" v-on:input="getStrName" class="form-control">
    </div>
    <div class="form-group w-100">
      <label for="surname_id">Введите фамилия</label>
      <input type="text" id="surname_id" v-on:input="getStrSurname" class="form-control">
    </div>
    <div class="form-group w-100">
      <label for="phone_id">Введите телефон</label>
      <input type="number" id="phone_id" v-on:input="getStrPhone" class="form-control">
    </div>
    <hr>
    <div class="row">
      <div class="col-3">
        <button class="btn btn-success" @click="getSave()">Сохранить</button>
      </div>
      <div class="col-3">
        <button class="btn btn-outline-secondary" id="edit" @click="getRet()">Изменить</button>
      </div>
      <div class="col-3">
        <button class="btn btn-outline-secondary" id="del" @click="getDel()">Удалить</button>
      </div>
      <div class="col-3">
        <button class="btn btn-outline-info" id="sorting" @click="getSort()">Сортировка</button>
      </div>
    </div>
    <hr>
    <div class="row" style="border: 1px solid gray; margin-top: 10px; border-radius: 10px;">
      <div class="col-4">
        <p id="name_value">Ввод имя</p>
        <p>Имя</p>
      </div>
      <div class="col-4">
        <p id="surname_value">Ввод фамилия</p>
        <p>Фамилия</p>
      </div>
      <div class="col-4">
        <p id="phone_value">Ввод номера</p>
        <p>Номер</p>
      </div>
    </div>

    <div class="row border-row" v-for="note in notes" :key="note.id" @click="getIdElement(note.id)">
      <div class="col-4">{{ note.name }}</div>
      <div class="col-4">{{ note.surname }}</div>
      <div class="col-4">{{ note.phone }}</div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        name: "",
        surname: "",
        phone: "",
        notes: [],
        i: 0,
        ret: false,
        del: false,
        sorting: false,
      }
    },

    methods: {
      getStrName() {
        this.name = document.getElementById('name_id').value;
        document.getElementById('name_value').innerHTML = this.name;
      },
      getStrSurname() {
        this.surname = document.getElementById('surname_id').value;
        document.getElementById('surname_value').innerHTML = this.surname;
      },
      getStrPhone() {
        this.phone = document.getElementById('phone_id').value;
        document.getElementById('phone_value').innerHTML = this.phone;
      },

      getSave() {
        let note = {
          id: this.i,
          name: this.name,
          surname: this.surname,
          phone: this.phone,
        };
        this.notes.push(note);
        this.i++;
      },

      getRet() {
        this.ret = !this.ret;
        document.getElementById('edit').innerHTML = this.ret ? "Активное изменение" : "Изменить";
        document.getElementById('del').disabled = this.ret ? this.ret : this.ret;
      },
      getDel() {
        this.del = !this.del;
        document.getElementById('del').innerHTML = this.del ? "Активное улаление" : "Удалить";
        document.getElementById('edit').disabled = this.del ? this.del : this.del;
      },
      getIdElement(note_id) {
        let note = {
          name: this.ret ? this.name : "",
          surname: this.ret ? this.surname : "",
          phone: this.ret ? this.phone : "",
        };
        if (this.ret == true || this.del == true) {
          this.notes.splice(note_id, 1, note)
        }
      },

      getSort() {
        this.sorting = !this.sorting;
        if (this.sorting == 1) {
          this.notes.sort((a, b) => a.name > b.name ? 1 : -1);
          document.getElementById('sorting').innerHTML = "Сортировка по имени"
        } else {
          this.notes.sort((a, b) => a.surname > b.surname ? 1 : -1);
          document.getElementById('sorting').innerHTML = "Сортировка по фамилии"
        }
      },

    },
  }

</script>
