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
                v-model="surname"
                >
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
            @click.prevent="editItem"
            >Düzenle
        </button>
        <div id="error" v-show="hasError">
            Lütfen bütün Alanları Doldurunuz
        </div>
    </form>
</template>

<script>
export default {
    data(){
        return {
            id: this.item.id,
            name: this.item.name,
            surname: this.item.surname,
            phoneNumber: this.item.phoneNumber,
            hasError: false,
            hasSuccess: false
        }
    },
    props:{
        item : Object
    },
    watch:{
        item(){
            this.id= this.item.id
            this.name= this.item.name
            this.surname= this.item.surname
            this.phoneNumber= this.item.phoneNumber
            this.isShown = this.item.isShown
        }
    },
    methods:{
        editItem (){

            if(this.name && this.surname && this.phoneNumber){                    
                this.hasError = false;
                this.$emit('editItem', {
                    id: this.id,
                    name:this.name, 
                    surname: this.surname, 
                    phoneNumber:this.phoneNumber,
                    isShown: this.isShown
                    }
                )
            }else{
                this.hasError = true;
            }

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