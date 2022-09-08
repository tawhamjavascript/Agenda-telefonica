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
    deletarPhone (id) {
      console.log("entrando aqui")
      const elem = this.contacts.find(contact => contact.id == id);
      elem.delete = true;
      //this.contacts.splice(this.contacts.findIndex(contact => contact.id === id), 1, elem);
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
