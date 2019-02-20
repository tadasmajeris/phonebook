<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <table>
      <thead>
        <tr>
          <td v-for="option in contactOptions" v-text="option"></td>
        </tr>
      </thead>
      <tbody>
        <tr v-for='(contact, i) in contacts'>
          <td>{{i+1}}</td>
          <td v-text="contact.name"></td>
          <td v-text="contact.phone_number"></td>
          <td v-text="contact.address"></td>
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
        'id', 'Name', 'Phone', 'Address'
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
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
