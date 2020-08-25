<template>
  <div class='item-list-container'>
    <div class="search">
    <div class="table">
        <div class="row">
            <div class="cell">
                <input type="text" name="nameText" v-model="nameSearchText" @keyup="checkNameSearch">
            </div>
            <div class="cell">
                <input type="text" name="surNameText" v-model="surNameSearchText" @keyup="checkSurnameSearch">
            </div>
            <div class="cell">
                <select type="text" name="sort" v-model="sortingType" @change="changeSortingType">
                    <option value="nameAsc"> Ad A-Z </option>
                    <option value="nameDesc"> Ad Z-A </option>
                    <option value="surNameAsc"> Soyad A-Z </option>
                    <option value="surNameDesc"> Soyad Z-A </option>
                </select>

            </div>
        </div>
        <div class="row">
            <div class="cell">
                Ad
            </div>
            <div class="cell">
                Soyad
            </div>
            <div class="cell">
                Telefon
            </div>
            <div class="cell transacition">
            </div>
        </div>
        <phone-book-list-item
            v-for="item in activeList"
            :key = "item.id"
            :item = item
            @itemDeleted = "deleteItem($event)"
            @editItem = "editItem($event)"
        >
        </phone-book-list-item>
    </div>
    </div>
  </div>

</template>

<script>
import PhoneBookListItem from './PhoneBookListItem'
export default {
    data(){
        return{
            sortingType: '',
            nameSearchText:'',
            surNameSearchText:''
        }
    },
    props:{
        list : Array
    },
    computed:{
        activeList() {
            return this.list.filter(item => item.isShown)
        }
    },
    methods:{
        deleteItem(item){
            this.$emit('itemDeleted', item)
        },
        editItem(item){
            this.$emit ('editItem', item)
        },
        changeSortingType(){
            this.$emit ('sortingChanged', this.sortingType)
        },
        checkNameSearch(){
            this.$emit('filterByName', this.nameSearchText)
        },
        checkSurnameSearch(){
            this.$emit('filterBySurName', this.surNameSearchText)
        }
    },
    components:{
        PhoneBookListItem
    }
}
</script>

<style>
.item-list-container{
    width : 600px;
}
.table {
   display: table;
   width: 100%;
}
.row {
   display: table-row;
}
.cell{
   display: table-cell;
   padding: 3px 10px;
   border: 1px solid #999999;
}

</style>