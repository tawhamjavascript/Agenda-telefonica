<template>
<h1> Lista telefonica </h1>
<FormSub @add-phone = "addPhone"></FormSub>
<ul>
  <AgenCont @deletePhone = 'deletarPhone' :contact-list="sortedPhone"/>
</ul>
</template>

<script>
import FormSub from "./components/FormSub.vue"
import AgenCont from "./components/AgenCont.vue";
import axios from "axios";
import {Contact} from "./model/Contacts.js"


export default {
  name: 'App',
  components: {
    FormSub,
    AgenCont
},
  data () {
    return {
      contacts: []
    }
  },
  methods: {
    addPhone (phone) {
      console.log(phone);
      this.contacts.push(phone);
    },
    async deletarPhone (id) {
      console.log("entrando aqui")
      await axios.delete(`http://localhost:9000/{id}`);
      const elem = this.contacts.find(contact => contact.id == id);
      elem.delete = true;
      this.contacts.splice(this.contacts.findIndex(contact => contact.id === id), 1, elem);
    },
  },
  async mounted () {
    try {
      const result =  await axios.get("http://localhost:9000");
      for(let i = 0; i < result.length; i++) {
        const contact = new Contact();
        contact.name = result[i].Nome;
        contact.phone = result[i].Telefone;
        contact.id = result[i].ID;
        this.contacts.push(contact);
      }

    }
    catch(err) {
      console.log(err);
    }
  },

  computed: {
    sortedPhone: {
      get: function () {
        let sorted = this.contacts;
        return sorted.sort( function (a,b) {
          if (a.name[0] > b.name[0]) return -1;
          if (a.name[0] < b.name[0]) return 1;
          return 0;
        })
      },
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
