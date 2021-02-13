<template>
    <div class="item">
        <input type="checkbox" @change="updateCheck()" v-model="item.completed"/>
        <span :class="[item.completed ? 'completed' : '','itemText']">{{item.name}}</span>
        <button class="trashCan" @click="removeItem()">Delete</button>
    </div>
</template>

<script>
export default{
    props:['item'],
    methods:{
        updateCheck(){
            axios.put('api/item/' + this.item.id,{
                item:this.item
            }).then(response =>{
                if (reponse.status == 200){
                    this.$emit('itemchanged');
                }
            }).catch(error =>{
                console.log(error);
            })
        },removeItem(){
            axios.delete('api/item/' + this.item.id).then(response=>{
                if (this.response.status == 200){
                    this.$emit('itemchanged');
                }
            }).catch(error =>{
                console.log('error');
            })
        }
    }

}
</script>
<style scoped>
.completed{
    text-decoration: line-through;
    color:#999999;
}
.itemText{
    width: 100%;
    margin-left:20px;
}
.item{
    display: flex;
    justify-content: center;
    align-items: center;
}
.trashCan{
    background: #red;
    color:#fff;
    border: none;
    padding: 2px;
    outline: none;
}
</style>
