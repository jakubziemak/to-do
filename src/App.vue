<template>
	<div id="container">
		<h1>TO-DO LIST</h1>
		<div id="todos">
			<todos v-for="item in list"
				v-bind:item="item"
				@item-to-delete='deleteItem(item)'
				:key='item.id'/>
		</div>
		<div id="footer">
			<input type="text" placeholder="New task" v-model="task" @keydown.enter="createNewItem()">
			<img class="add-icon"  v-bind:src=addIcon @click="createNewItem()">
		</div>
	</div>
</template>

<script>
import todos from './components/todos.vue'
import addIcon from './assets/add_black_24dp.svg'


export default{
	name: 'App',
	components: {
		todos
	},
	data(){
		return {
			task: '',
			list: [],
			counter: 0,
			addIcon: addIcon
		}
	},
	methods: {
		createNewItem: function(){
			if(this.task.length>0){
				this.list.push({text: this.task, id: this.counter});
				this.counter++;
				this.task = '';
			}
		},
		deleteItem: function(item){
			const index = this.list.indexOf(item)
			if (index > -1) {
				this.list.splice(index, 1);
			}
		},

	}
}
</script>

<style>
#container{
	height: 600px;
	width: 400px;
	background-color: hsl(212, 11%, 26%);
	-webkit-box-shadow: 0px 0px 41px -12px rgba(0, 0, 0, 1);
	-moz-box-shadow: 0px 0px 41px -12px rgba(0, 0, 0, 1);
	box-shadow: 0px 0px 41px -12px rgba(0, 0, 0, 1);

}
#todos{
	height: 70%;
	position: relative;
	top: 60px;
	background-color: hsl(212, 11%, 70%);
	overflow: auto;
	display: flex;
	flex-direction: column;
}
#footer{
	position: relative;
	bottom: -80px;
	display: flex;
	justify-content: space-evenly;
	width: 90%;
	left: 50%;
	transform: translateX(-50%);
}
input{
	width: 260px;
	border: 0;
	border-bottom: 2px solid hsl(195, 80%, 40%);
	color: hsl(195, 80%, 40%);
	background-color:transparent;
	font-size: 1rem;
}
::placeholder{
	color: hsl(195, 80%, 40%, .3);
}
input:focus{
	outline: none;
}
.add-icon{
	width: 2rem;
	cursor: pointer;
	filter: invert(50%) sepia(43%) saturate(7202%) hue-rotate(169deg) brightness(93%) contrast(84%);
	transition: filter .2s;
}
.add-icon:hover{
	filter: invert(44%) sepia(22%) saturate(855%) hue-rotate(149deg) brightness(94%) contrast(97%);
	transition: filter .2s;
}
::-webkit-scrollbar{
	width: 10px;
	background-color: hsl(0, 0%, 80%);
}
::-webkit-scrollbar-thumb{
	background-color: hsl(0, 0%, 50%);
}
::-webkit-scrollbar-thumb:hover{
	background-color: hsl(0, 0%, 60%);
}
</style>
