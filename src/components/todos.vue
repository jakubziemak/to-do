<template>
    <div class="task" v-bind:id='item.id'>
        <p v-bind:class="{active: isActive}" @click="cahangeClass">{{ item.text }}</p>
        <img class="delete-icon" v-bind:src=deleteIcon @click="deleteItem(item)">
    </div>
</template>

<script>
import deleteIcon from '../assets/delete_black_24dp.svg'

export default{
    name: 'todos',
    props: ['item'],
    data(){
        return{
            isActive: true,
            deleteIcon: deleteIcon
        }
    },
    methods: {
        cahangeClass: function(){
            this.isActive = !this.isActive
        },
        deleteItem: function(item){
            this.$emit('item-to-delete', item)
        }
    }
}
</script>

<style scoped>
/* #todos{
    height: 70%;
    width: 90%;
    position: relative;
    top: 60px;
    border-top: 2px solid hsl(0, 0%, 61%);
    border-bottom: 2px solid hsl(0, 0%, 61%);
    left: 50%;
    transform: translateX(-50%);
} */
.task{
    /* min-height: 2rem; */
    width: 100%;
    display: flex;
    align-items: center;
    font-size: 1.25rem;
    margin-top: .4rem;
    transition: background-color .2s;

}
.task:hover{
    background-color: hsla(208, 100%, 97%, .1);
    transition: background-color .2s;
}
.delete-icon{
    right: 10px;
    position: absolute;
    cursor: pointer;
    width: 1.75rem;
    transition: filter .2s;
}
.delete-icon:hover{
    transition: filter .2s;
    filter: invert(39%) sepia(65%) saturate(2887%) hue-rotate(169deg) brightness(93%) contrast(84%);
}
p{
    min-height: 2rem;
    max-width: 80%;
    overflow-wrap: break-word;
    word-wrap: break-word;
    /* -ms-word-break: break-all; */
    position: relative;
    left: 12px;
    cursor: pointer;
    text-decoration: line-through;
    margin: 0;
    color: hsl(0, 0%, 2%);
}
.active{
    text-decoration: none;
}
</style>
