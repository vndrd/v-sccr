<template>
  <div id="todolist">
    <h1>{{title}}
        <span>Club Bolivar</span>
    </h1>
  <template v-if="todo.length">
    <transition-group name="todolist" tag="ul">
      <tr v-for="item in todoByStatus" :class="clasePos(item.posnum)" v-bind:key="item.id" >
        <td class="label " style="width: 50px"> {{item.pos}} </td>
        <td class="label" style="width: 150px"> {{item.label}} </td>
        <td class="label" style="width: 150px">
            <img :src="require(`@/assets/images/${item.nat}.png`)" width="40px" /> 
        </td>
        <td class="actions">    
            <button class="btn btn-success" @click="exchangeItem(item)"> 
                <b-icon :icon="iconAll"></b-icon>
            </button>
        </td>
      </tr>
    </transition-group>
        <togglebutton 
            label="Move done items at the end?"
            name="todosort"
            v-on:clicked="clickontoogle" />
        <button class="btn btn-lg btn-warning" @click="btnOrderByPos">por Posición</button>
        <button class="btn btn-lg btn-info"     @click="btnOrderByAge">por Edad</button>
  </template>
    <p v-else class="emptylist">Your todo list is empty.</p>
    <form name="newform" v-on:submit.prevent="addItem">
        <label for="newitem">Add to the todo list</label>
        <input type="text" name="newitem" id="newitem" v-model="newitem">
        <button type="submit">Add item</button>
        
    </form>
  </div>
</template>

<script>
import togglebutton from '@/components/Togle.vue'
//https://www.bennadel.com/blog/3559-animating-elements-in-from-a-mouse-event-location-in-vue-js-2-5-21.htm

/*
<button class="btn-picto" type="button" 
                v-on:click="markAsDoneOrUndone(item)" 
                v-bind:aria-label="item.done ? 'Undone' : 'Done'" 
                v-bind:title="item.done ? 'Undone' : 'Done'">
            <i aria-hidden="true" class="material-icons">
                {{ item.done ? 'cb' : 'cbob' }}</i>
          </button>
          <button class="btn-picto" type="button" 
                v-on:click="deleteItemFromList(item)" 
                aria-label="Delete" 
                title="Delete">
            <i aria-hidden="true" class="material-icons">delete</i>
          </button>
 */

export default {
    name: 'Todo',
    props: ['todo', 'title','direction'],
    data() {
        return {
            iconcon: 'chevron-left',
            newitem:'',
            sortByStatus:false,
        }
    },    
    created: function(){

    },
    methods: {
        addItem: function() {
            this.todo.push({id: Math.floor(Math.random() * 9999) + 10, label: this.newitem, done: false});
            this.newitem = '';
        },
        markAsDoneOrUndone: function(item) {
            item.done = !item.done;
        },
        deleteItemFromList: function(item) {
            let index = this.todo.indexOf(item)
            this.todo.splice(index, 1);
        },
        clickontoogle: function(active) {
            this.sortByStatus = active;
        },
        btnOrderByPos: function(e){
            e.preventDefault();
            this.todo.sort((a,b) => {
                if(a.posnum > b.posnum)
                return 1;
                return -1;
            })
            console.log('todo',this.todo)
        },
        btnOrderByAge: function(e){
            e.preventDefault();
            this.todo.sort((a,b) => {
                if(a.age > b.age)
                return 1;
                return -1;
            })
            console.log('todo',this.todo)
        },
        exchangeItem: function(item){
            if(this.direction === 'right'){
                this.$parent.toPlantillaList(item)
            }else{
                this.$parent.toPlantelList(item)
            }
        },
        clasePos: function(pos){
            console.log("asdas");
            return 'pos'+pos
        },
    },
    computed: {
        iconAll: function(){
            return "chevron-"+this.direction;
        },
        todoByStatus: function() {

        if(!this.sortByStatus) {
            return this.todo;
        }

        var sortedArray = []
        var doneArray = this.todo.filter(function(item) { return item.done; });
        var notDoneArray = this.todo.filter(function(item) { return !item.done; });
        
        sortedArray = [...notDoneArray, ...doneArray];
            return sortedArray;
        }
    },
    components: {
        togglebutton
    }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
* {
	margin:0;
	padding:0;
	box-sizing:border-box;
}
.pos1 {
    border-left: rgba(219, 164, 26, 1.0) 10px solid;
}
.pos2 {
    border-left: rgba(100, 219, 26, 1.0) 10px solid;
}
.pos3 {
    border-left: rgba(26, 158, 219, 1.0) 10px solid;
}
.pos4 {
    border-left: rgba(219, 61, 26, 1.0) 10px solid;
}
html, body {
	background:#17f1f1;
	font-size:1.1rem;
	font-family:'Quicksand', sans-serif;
	height:100%;
}
@keyframes strikeitem {
	to { width:calc(100% + 1rem); }
}
/*          enter-leave transition */
.todolist-enter{
    opacity: 0;
}
.todolist-enter-to{
    opacity: 1;
    transition: all 1s;
}
.todolist-enter-active{}
.todolist-leave{
    height: 50px;
}
.todolist-leave-to{
    height: 0px !important;
    transition: all 4s;
}
.todolist-leave-active{
    display:none !important;
    margin: 0px;
    padding:0px;
}
/*          enter leave transition END */
#todolist {
    overflow: hidden;
	margin:4rem ;
    float: left;
	padding:2rem 3rem 3rem;
	max-width:500px;
	background:#45a;
	color:#FFF;
	box-shadow:-20px -20px 0px 0px rgba(100,100,100,.1);
    h1 {
        /*text-align:center;*/
        font-weight: normal;
        font-size: 2.6rem;
        letter-spacing: 0.05em;
        border-bottom: 1px solid rgba(255,255,255,.3); 
    }
    h1 span {
        display:block;
        font-size:0.8rem;
        margin-bottom:0.7rem;
        margin-left:3px;
        margin-top:0.2rem;   
    }
    img{
        opacity: 0.7;
        box-shadow: 10px 10px #444 ;
    }
    .emptylist {
        margin-top:2.6rem;
        text-align:center;
        letter-spacing:.05em;
        font-style:italic;
        opacity:0.8;
    }
    ul {
        margin-top:2.6rem;
        list-style:none;
    }
    .todolist-move {
        transition: transform 1s;
    }
    tr {
        display:flex;
        margin:0 -3rem 4px;
        padding:1.1rem 3rem;
        
        align-items:center;
        background:rgba(255,255,255,0.1);
    }
    td {
        
    }
    .actions {
        flex-shrink:0;
        padding-left:0.7em;
    }
    .label {
        position:relative;
        transition:opacity .2s linear;
    }
    .done .label {
        opacity:.6;
    }
    .done .label:before {
        content:'';
        position:absolute;
        top:50%;
        left:-.5rem;
        display:block;
        width:0%;
        height:1px;
        background:#FFF;
        animation:strikeitem .3s ease-out 0s forwards;
    }
    .btn-picto {
        border:none;
        background:none;
        -webkit-appearance:none;
        cursor:pointer;
        color:#FFF;
    }
}

/* FORM */
form {
	margin-top:3rem;
	display:flex;
	flex-wrap:wrap;
}
form label {
	min-width:100%;
	margin-bottom:.5rem;
	font-size:1.3rem;
}
form input {
	flex-grow:1;
	border:none;
	background:#f7f1f1;
	padding:0 1.5em;
	font-size:initial;
}
form button {
	padding:0 1.3rem;
	border:none;
	background:#FF6666;
	color:white;
	text-transform:uppercase;
	font-weight:bold;
	border:1px solid rgba(255,255,255,.3);
	margin-left:5px;
	cursor:pointer;
	transition:background .2s ease-out;
}
form button:hover {
	background:#FF5E5E;
}
form input, 
form button {
	font-family:'Quicksand', sans-serif;
	height:3rem;
}


</style>
