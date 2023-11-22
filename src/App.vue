<template>
    <div class="container">
        <h1>TODO List</h1>
        <SearchComponent @search_text="search"/>
        <AddComponent :books_count="Math.max(...this.books.map(o=>{return o.id}))" @new_book="addBook"/>
        <BookComponent :books="search_result()" @delete_id="deleteBook" @edit_book="get_edit_book_id"/>
        <EditComponent v-if="showEditComp" :book="book" @showEditComp="showEditCompFunc" @edited="editBook"/>
    </div>
</template>

<script>
import SearchComponent from "@/components/SearchComponent.vue";
import AddComponent from "@/components/AddComponent.vue"
import BookComponent from "@/components/BookComponent.vue";
import EditComponent from "@/components/EditComponent.vue";
import {defineComponent} from "vue";

import * as req from "@/connect_db/request"

import axios from "axios";

export default defineComponent({
    components: {EditComponent, BookComponent, AddComponent, SearchComponent},
    data() {
        return {
            books: [
                {id: 1, author: 'Arthur', name: 'Secret door', category: 'Fantastic', year: 1900, price: 120},
                // {id: 2, author: 'Arthur', name: 'Sherlock', category: 'Fantastic', year: 1900, price: 120},
                // {id: 3, author: 'Arthur', name: 'Secret door', category: 'Fantastic', year: 1900, price: 120},
                // {id: 4, author: 'Arthur', name: 'Secret door', category: 'Fantastic', year: 1900, price: 120},
            ],
            text: '',
            showEditComp: false,
            book: {id: null, author: '', name: '', category: '', year: null, price: null}
        }
    },
    mounted() {
        axios.get(req.url + "books/getAll")
            .then(response=> this.books = response.data)
            .catch(e => {console.log(e.error)});
    },
    methods: {
        addBook(new_book) {
            axios.post(req.url + "books/addBook", new_book)
                .then(response=> this.books.push(response.data['obj']))
                .catch(e => {console.log(e.error)});
        },
        deleteBook(i) {
            axios.delete(req.url + "books/delete/"+i)
                .then(response=> {
                    console.log(response.data['message'])})
                .catch(e => {console.log(e.error)});
            this.books = this.books.filter((b) => b.id != i);
        },
        search(k) {
            this.text = k
        },
        search_result() {
            if(this.text.length != 0) {
                return this.books.filter(b => b.name.toLowerCase().indexOf(this.text.toLowerCase()) > -1)
            } else {
                return this.books
            }
        },
        get_edit_book_id(id) {
            for (let i=0; i<this.books.length; i++) {
                if(this.books[i].id == id) {
                    this.book = this.books[i];
                    break;
                }
            }
            this.showEditComp = true
        },
        editBook(book) {
            axios.put(req.url + "books/editBook", book)
                .then(response=> {
                    console.log(response.data)})
                .catch(e => {console.log(e.error)});

            for (let i=0; i<this.books.length; i++) {
                if(this.books[i].id == book.id) {
                    this.books[i] = book;
                    break;
                }
            }
            this.showEditComp = false
        },
        showEditCompFunc() {
            this.showEditComp = false
        }
    }
})

</script>

<style scoped>
.container {
    width: 80%;
    margin: 0 auto;
}
h1 {
    margin-top: 10px;
}
</style>