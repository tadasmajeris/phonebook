<template>
  <div class="hello">

    <h1>{{ msg }}</h1>

    <table>
      <thead>
        <tr>
          <td v-for="option in contactOptions" v-text="option.name" :class="isSelectedClass(option)" @click="selectedOption = option"></td>
        </tr>
      </thead>
      <tbody>
        <tr v-for='(contact, i) in contacts'>
          <td v-for='option in contactOptions' v-text="option.name == 'id' ? (i+1) : contact[option.id]"></td>
        </tr>
      </tbody>
    </table>

  </div>
</template>

<script>
export default {
  name: 'Phonebook',
  props: {
    msg: String
  },

  data() {
    return {
      contacts: [],
      contactOptions: [
        { id: 'id', name: 'id' },
        { id: 'name', name: 'Name' },
        { id: 'phone_number', name: 'Phone' },
        { id: 'address', name: 'Address' },
      ],
      selectedOption: {}
    }
  },

  created() {
    this.selectedOption = this.contactOptions[0];

    const axios = require('axios');

    axios.get('http://www.mocky.io/v2/581335f71000004204abaf83')
    .then(response => {
      this.contacts = response.data.contacts;
    })
    .catch(function (error) {
      console.log(error);
    })
  },

  methods: {
    isSelectedClass(option) {
      return option == this.selectedOption ? 'selected-option' : '';
    }
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
table {
  margin: auto;
  border-collapse: collapse;
}
table td {
  text-align: left;
  padding: 5px 0;
  padding-right: 25px;
}
table thead {
  border-bottom: 1px solid #efefef;
}
table thead td {
  cursor: pointer;
}
.selected-option {
  font-weight: bold;
}
.selected-option:after, table thead td:hover:after {
  content: '↓';
  display: inline-block;
  position: absolute;
  padding-left: 3px;
  margin-top: -2px;
  transform: scale(1.2, 0.88);
}
table thead td:hover:after {
  color: #999;
}
.selected-option:hover:after {
  color: inherit;
}
</style>
