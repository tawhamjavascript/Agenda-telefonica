<template>
<ul> 
  <li v-for = 'contato in contactList' :key = 'contato.id'> 
    <div class = "content" v-if = '!contato.delete'> 
      <p> nome : {{ contato.name }} </p>
      <p> telefone: {{ contato.phone }} </p>
      <button class = "enviar" @click = "deletar(contato.id)"> deletar </button>
    </div>
  </li>
</ul>
</template>
<script>
export default {
    props: ['contactList'],
    methods: {
      deletar (id) {
        this.$emit('deletePhone', id);
      }
    },
}
</script>

<style>
li {
  list-style-type: none;
  margin-bottom: 2%;

}
.content {
  border: 1px solid black;
  padding: -20px;
  width: 30%;
  height: 140px;
  margin-left: auto;
  margin-right: auto;
}
.enviar {
  padding: 2%;
  width: 40%;
  background-color: crimson;
  border-radius: 5%;

}
</style>