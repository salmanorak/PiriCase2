<template>
          <div class="row">
            <div class="cell">
                {{item.name}}
            </div>
            <div class="cell">
                {{item.surname}}
            </div>
            <div class="cell">
                {{item.phoneNumber}}
            </div>
            <div class="cell transacition">
                <span 
                    class="edit" 
                    @click="editItem"
                    >Edit
                </span>
                <span 
                    class="delete" 
                    @click="removeItem"
                    >Del
                </span>
            </div>
        </div>
</template>

<script>
export default {
    props:{
        item: Object
    },
    methods:{
        removeItem(){
            this.$emit('itemDeleted', this.item)
        },
        editItem(){
            this.$emit('editItem', this.item)
        }
    }
}
</script>

<style>
.edit, .delete {
    display: inline-block;
    min-width: 40px;
    padding: 3px 5px;
    cursor: pointer;
    color:white;
    margin: 5px;
    text-align: center;
    border-radius: 5px;;
}
.edit{
    background-color:salmon;
}
.delete{
    background-color: red;
}

</style>