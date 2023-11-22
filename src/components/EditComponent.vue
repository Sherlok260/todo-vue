<template>
    <div id="myModal" class="modal">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="staticBackdropLabel">Modal title</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"
                            v-on:click="closer"></button>
                </div>
                <div class="modal-body">
                    <label>Category</label>
                    <input type="text" class="form-control" placeholder="Category" v-model="category">

                    <label>Book Name</label>
                    <input type="text" class="form-control" placeholder="Book Name" v-model="bookName">

                    <label>Author</label>
                    <input type="text" class="form-control" placeholder="Author" v-model="author">

                    <label>Year</label>
                    <input type="number" class="form-control" placeholder="Writed year" v-model="year">

                    <label>Price($)</label>
                    <input type="number" class="form-control" placeholder="Price" v-model="price">

                </div>

                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal" v-on:click="closer">Close
                    </button>
                    <button type="button" class="btn btn-primary" v-on:click="saveChanges">Save Changes</button>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
export default {
    name: "EditComponent",
    props: {
        book: Object
    },
    data() {
        return {
            showEditComp: false,
            category: this.book.category,
            bookName: this.book.name,
            author: this.book.author,
            year: this.book.year,
            price: this.book.price
        }
    },
    methods: {
        closer() {
            this.$emit("showEditComp", false)
        },
        saveChanges() {
            let edited_book = {id:this.book.id, category: this.category, name: this.bookName, author: this.author, year: this.year, price: this.price}
            this.$emit("edited", edited_book)
        }
    }
}
</script>

<style scoped>
.modal {
    display: block; /* Hidden by default */
    /*position: fixed; !* Stay in place *!*/
    /*z-index: 2; !* Sit on top *!*/
    left: 0;
    top: 0;
    width: 100%; /* Full width */
    height: 100%; /* Full height */
    /*overflow: auto; !* Enable scroll if needed *!*/
    background-color: rgb(0, 0, 0); /* Fallback color */
    background-color: rgba(0, 0, 0, 0.4); /* Black w/ opacity */
}

/* Modal Content/Box */
.modal-content {
    background-color: #fefefe;
    margin: 15% auto; /* 15% from the top and centered */
    padding: 20px;
    border: 1px solid #888;
    width: 80%; /* Could be more or less, depending on screen size */
}

/*.modal-content input {*/
/*    margin-top: 5px;*/
/*    margin-bottom: 5px;*/
/*    border: 1px solid;*/
/*    border-radius: 5px;*/
/*    padding: 5px;*/
/*}*/

/* The Close Button */

.btnn {
    margin-left: 10px;
    padding: 5px;
    color: white;
    border-radius: 5px;
    text-decoration: none;
    cursor: pointer;
    float: right;
    border: none;
    font-size: 20px;
}

.btn-closee {
    background-color: red;
}

.btn-add {
    background-color: blue;
}

.buttons {
    margin-top: 10px;
    margin-bottom: 10px;
    display: flex;
    float: right;
}
</style>