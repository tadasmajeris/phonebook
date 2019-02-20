<template>
  <div class="hello">

    <h1>{{ msg }}</h1>

    <table>
      <thead>
        <tr>
          <td v-for="option in contactOptions" v-text="option.name"></td>
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
      ]
    }
  },

  created() {
    const axios = require('axios');

    axios.get('http://www.mocky.io/v2/581335f71000004204abaf83')
    .then(response => {
      this.contacts = response.data.contacts;
    })
    .catch(function (error) {
      console.log(error);
    })
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
  padding-right: 20px;
}
table thead {
  border-bottom: 1px solid #efefef;
}
</style>
