<template>
<form @submit="addPhone">
    <div> 
        <label for = "name" > Nome:  </label>
        <input v-model = "name" id = "name" required/>
    </div>
    <div> 
        <label for = "number"> Número: </label>
        <input  v-model = "phone" id = "number" type = "number" required/>
    </div>
    <div>
        <input class = "submit" type = "submit" value = "adicionar" />
    </div>
</form>
</template>

<style>
#name, #number {
    width: 30%;
    padding: 0.5%;
    margin: 1%;
    height: 20px;
    border-radius: 2%;
}
.submit {
  background-color:darkgreen;
  width: 20%;
  height: 50px;
  font-size: medium;


}
</style>
<script>
import {Contact} from "../model/Contacts.js"
export default {
    data() {
        return {
            name: "",
            phone: "",
        }
    },
    methods: {
        addPhone(e) {
            e.preventDefault();
            const contact = new Contact();
            contact.id = Math.floor(Math.random() * 100);
            contact.name = this.name;
            contact.phone = this.phone;
            contact.delete = false;
            this.name = '';
            this.phone = '';
            this.$emit('add-phone', contact);
            
        }
    }
}
</script>
