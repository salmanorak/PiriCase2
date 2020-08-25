<template>
  <div id="app">
    <phone-book-form
      @itemAdded = 'addItem($event)'
      v-show="!isEdit"
    ></phone-book-form>
    <phone-book-edit
      @editItem = 'editItem($event)'
      v-show="isEdit"
      :item = "editingItem"
    ></phone-book-edit>
    <phone-book-list
      :list = list
      @itemDeleted = "deleteItem($event)"
      @editItem = "startEdit($event)"
      @sortingChanged = "sortItems($event)"
      @filterByName = "filterByName($event)"
      @filterBySurName = "filterBySurName($event)"
    ></phone-book-list>

  </div>
</template>

<script>
import PhoneBookForm from './components/PhoneBookForm.vue'
import PhoneBookEdit from './components/PhoneBookEdit.vue'
import PhoneBookList from './components/PhoneBookList.vue'

export default {
  name: 'App',
  data(){
    return {
      list : [],
      isEdit: false,
      editingItem : {}
    }
  },
  methods:{
    addItem(item){
      this.list.push(item);
    },
    deleteItem(item){
      this.list = this.list.filter((i)=> i.id != item.id)
    },
    startEdit(item){
      this.isEdit = true
      this.editingItem = item
    },
    editItem(item){
      this.isEdit = false
      this.editingItem = {}
      var l = this.list.length;
      for(let i = 0; i<l; i++){
        if(this.list[i].id == item.id){
          this.list.splice(i,1,item)
          break;
        }
      }
    },
    sortItems(type){
      if(type=='nameAsc'){
        this.list.sort((a, b) => a.name.localeCompare(b.name))
      }
      else if(type=='nameDesc'){
        this.list.sort((a, b) => b.name.localeCompare(a.name))

      }
      if(type=='surNameAsc'){
        this.list.sort((a, b) => a.surname.localeCompare(b.surname))
      }
      else if(type=='surNameDesc'){
        this.list.sort((a, b) => b.surname.localeCompare(a.surname))
      }
    },
    filterByName(key){
      this.filterByKey(this.list, 'name',key)
    },
    filterBySurName(key){
      this.filterByKey(this.list,'surname', key)
    },
    filterByKey(arr, property, key){
        var l = key.length
        arr.forEach(item=>{ 
          if(item[property].substring(0,l).toLowerCase() == key){
            item.isShown= true
          }else{
            item.isShown = false
          }
        })
    }
  },
  components: {
    PhoneBookForm,
    PhoneBookList,
    PhoneBookEdit
  },

}
</script>

<style>

</style>
