<template>
    <div>
        <h1>Example transicionsss</h1>
        <button class="btn btn-info btn-lg" @click="agregar">Add</button>
        <button class="btn btn-secondary btn-lg" @click="changes">Shuffle</button>
        <transition-group name="list" tag="ul">
            <li v-for="item in items" :key="item.id" class="itemclass">
                item: {{item.id}}
            </li>
        </transition-group>
    </div>
</template>
<script>
export default({
    name: 'transitionExample',
    data(){
        return {
            nextItem: 4,
            items: [
                {id: 1 },
                {id: 2 },
                {id: 3 }
            ],
            numeros: [1,2,3]
        }
    },
    methods: {
        agregar: function(){
            this.items.push({id: this.nextItem});
            this.nextItem = this.nextItem + 1 ;
            
        },
        changes: function(){
            const shuffled = []
            while (this.items.length > 0) {
                const index = this.random(this.items.length - 1)
                shuffled.push(this.items[index])
                this.items.splice(index, 1)
            }
            this.items = shuffled
        },  
        random(max) {
            return Math.floor(Math.random() * (max + 1))
         }
    }
})
</script>
<style lang="scss">
    input {
        padding: 8px;
        margin: 5px;
    }
    .itemclass {
        width: 100px;
        background: #ccc;
        padding: 5px;
        margin: 5px;
    }
    ul {
        list-style-type: none;
    }
    .list-move {
        transition: transform 1s;
    }
    .list-enter{
        opacity: 1;
        transition: all 2s;
        transform: translateX(-50px);
        border-left: 10px solid ;
    }
    .list-enter-to{
        opacity: 1;
        transition: all 2s;
        border-left: 0px solid ;
    }
    .list-enter-active{
        
    }
    
</style>