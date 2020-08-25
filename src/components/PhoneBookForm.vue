<template>
    <form>
        <div class="name">
            <label for="name">Ad:</label>
            <input 
                id="name"
                type="text" 
                name="name"
                v-model="name">
        </div>
        <div class="surname">
            <label for="surname">Soyad:</label>
            <input 
                id="surname"
                type="text" 
                name="surname"
                v-model="surname">
        </div>
        <div class="phone-number">
            <label for="phone-number">Telefon:</label>
            <input 
                id="phone-number"
                type="text" 
                name="phone-number"
                v-model="phoneNumber">
        </div> 
        <button 
            class="submit-button" 
            @click.prevent="addItem"
            >Ekle
        </button>
        <div id="error" v-show="hasError">
            Lütfen bütün Alanları Doldurunuz
        </div>
        <div id="success" v-show="hasSuccess">
            Kayıt Eklendi.
        </div> 
    </form>
</template>

<script>
export default {
    data(){
        return {
            name:'',
            surname:'',
            phoneNumber: '',
            hasError: false,
            hasSuccess: false
        }
    },
    methods:{
        addItem (){
            if(this.name && this.surname && this.phoneNumber){                    
                this.hasError = false;
                this.$emit('itemAdded', {
                    id: new Date().getTime(),
                    name:this.name, 
                    surname: this.surname, 
                    phoneNumber:this.phoneNumber,
                    isShown: true
                })
                this.clearForm();
            }else{
                this.hasError = true;
            }

        },
        clearForm(){
                this.name = '';
                this.surname= '';
                this.phoneNumber= '';
                this.hasSuccess = true
                setTimeout (()=>{ this.hasSuccess = false}, 5000)
        }
    }

}
</script>

<style>
form{
    display: inline-block;
    border: 1px solid mediumseagreen;
    border-radius: 5px;
    padding: 10px;
    margin : 20px;
    width: 200px;
    height: 210px;;
}
form input{
    width: 195px;
}
label {
    display: block;
    margin-top: 10px;
}
.submit-button{
    display: inline-block;
    background-color: mediumseagreen;
    color: white;
    margin-top: 10px;
    font-weight: 100;
    border: none;
    padding: 5px 10px;
    border-radius: 5px;
    border: 1px solid mediumseagreen;
    cursor: pointer;
}
.submit-button:hover{
    background-color: white;
    color: mediumseagreen;
}
#error{
    color: red;
    font-size: 12px;
    margin-top: 10px;
}
#success{
    color: green;
    font-size: 12px;
    margin-top: 10px; 
}

</style>