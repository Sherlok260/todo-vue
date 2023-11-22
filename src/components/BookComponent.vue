<template>
    <div class="containerr">
        <div class="book">
            <div class="b_id">Id</div>
            <div class="b_author">Author</div>
            <div class="b_name">Name</div>
            <div class="b_category">Category</div>
            <div class="b_year">Year</div>
            <div class="b_price">Price($)</div>
            <div class="b_edit_delete">Edit/Delete</div>
        </div>
        <div v-if="books.length == 0">
            <h1>Data Not Found</h1>
        </div>
        <div class="book" v-for="i in books" :key="i.id">
            <div class="b_id">{{ i.id }}</div>
            <div class="b_author">{{ i.author }}</div>
            <div class="b_name">{{ i.name }}</div>
            <div class="b_category">{{ i.category }}</div>
            <div class="b_year">{{ i.year }}</div>
            <div class="b_price">{{ i.price }}</div>
            <div class="b_edit_delete">
                <i class="bi bi-pen" v-on:click="edit(i.id)"></i>
                <i class="bi bi-trash" v-on:click="del(i.id)"></i>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "BookComponent",
    props: {
        books: Array
    },
    data() {
        return {
            showEditComp: true
        }
    },
    methods: {
        edit(i) {
            this.$emit("edit_book", i)
        },
        del(i) {
            this.$emit('delete_id', i)
        }
    }
}
</script>

<style scoped>
.containerr {
    width: 100%;
    /*border: 1px solid red;*/
    margin-top: 10px;
    background-color: #fefefe;
}

.book {
    border: 1px solid black;
    margin: 2px;
    width: 100%;
    padding: 10px;
    display: flex;
}

.b_id {
    /*border: 1px solid red;*/
    width: 5%;
}

.b_author {
    width: 23%;
}

.b_name {
    width: 22%;
}

.b_category {
    width: 15%;
}

.b_year {
    width: 10%;
}

.b_price {
    width: 10%;
}

.b_edit_delete {
    text-align: center;
    width: 15%;
}

.b_edit_delete i {
    padding: 7px;
    cursor: pointer;
}

.b_edit_delete i:hover {
    background-color: aquamarine;
}
</style>