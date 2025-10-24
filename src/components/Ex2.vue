<script>
    export default { 
        // Add code in appropriate places
        data() {
            return {
                items: ['keyboard', 'mouse', 'iPhone', 'macbook', 'adapter'], 
                newItem:""
            }
            
        },

        methods: {
            addItem(){
                // add the new item
                this.items.push(this.newItem);
            },

        }
    }
</script>

<template>

    <h2>Shopping Cart</h2>
    <!-- TODO: Add Code Here -->

    <!-- u need to know the index to delete an item. then just splice that refer to that index -->
    <ul v-for="(item, idx) in items">
        <li>{{item}} <button @click="items.splice(idx, 1)">Delete!</button></li>
    </ul>

    <input type="text" v-model="newItem"></input>
    <button @click="addItem">Add!</button>
   
</template>

