<template>
  <div class="hello">

    <h1>{{ msg }}</h1>

    <table>
      <thead>
        <tr>
          <td v-for="option in contactOptions" v-text="option.name" :class="isSelectedClass(option)" @click="onOptionClick(option)" class='noselect'></td>
        </tr>
      </thead>
      <tbody>
        <tr v-for='(contact, i) in sortedContacts'>
          <td v-for='option in contactOptions' v-text="contact[option.id]"></td>
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
      selectedOption: {},
      sortingAsc: true,
    }
  },

  created() {
    this.selectedOption = this.contactOptions[0];

    const axios = require('axios');

    axios.get('http://www.mocky.io/v2/581335f71000004204abaf83')
    .then(response => {
      this.contacts = response.data.contacts;
      for (let i=0; i<this.contacts.length; i++) {
        this.contacts[i].id = String(i+1);
      }
    })
    .catch(function (error) {
      console.log(error);
    })
  },

  computed: {
    sortedContacts() {
      let sortKey = this.selectedOption.id;
      if (this.sortingAsc) {
        return this.contacts.sort((a, b) => a[sortKey].localeCompare(b[sortKey], "en-u-kn-true"));
      } else {
        return this.contacts.sort((b, a) => a[sortKey].localeCompare(b[sortKey], "en-u-kn-true"));
      }
    }
  },

  methods: {
    isSelectedClass(option) {
      if (option == this.selectedOption) {
        return this.sortingAsc ? 'selected-option' : 'selected-option desc';
      } else {
        return '';
      }
    },

    onOptionClick(option) {
      this.sortingAsc = (this.selectedOption == option) ? !this.sortingAsc : true;
      this.selectedOption = option;
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
.selected-option.desc:after {
  content: '↑';
}
table thead td:hover:after {
  color: #999;
}
.selected-option:hover:after {
  color: inherit;
}
.noselect {
  -webkit-touch-callout: none; /* iOS Safari */
    -webkit-user-select: none; /* Safari */
     -khtml-user-select: none; /* Konqueror HTML */
       -moz-user-select: none; /* Firefox */
        -ms-user-select: none; /* Internet Explorer/Edge */
            user-select: none; /* Non-prefixed version, currently
                                  supported by Chrome and Opera */
}
</style>
