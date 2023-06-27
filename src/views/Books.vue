<template>
    <div>
      <h1>Book List</h1>
      <router-link to="/books/add" class="btn btn-primary">Add Book</router-link>
  
      <table class="table">
        <thead>
        <tr>
          <th>Code</th>
          <th>Title</th>
          <th>Author</th>
          <th>Publisher</th>
          <th>Year</th>
          <th>Price</th>
          <th>Action</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="book in books" :key="book.id">
          <td>{{ book.kode }}</td>
          <td>{{ book.judul }}</td>
          <td>{{ book.pengarang }}</td>
          <td>{{ book.penerbit }}</td>
          <td>{{ book.tahun }}</td>
          <td>{{ book.harga }}</td>
          <td>
            <router-link :to="`/books/edit/${book.kode}`" class="btn btn-primary">Edit</router-link>
            <button @click="deleteBook(book.kode)" class="btn btn-danger">Delete</button>
          </td>
        </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: 'App',
    data() {
      return {
        books: [],
      };
    },
    methods: {
      fetchBooks() {
        axios.get('http://localhost/bukuweb/selectbuku.php')
            .then(response => {
              this.books = response.data;
            })
            .catch(error => {
              console.error(error);
            });
      },
      deleteBook(kode) {
        if (confirm('Are you sure you want to delete this book?')) {
          axios.delete(`http://localhost/bukuweb/deletebukukode.php?kode=${kode}`)
              // eslint-disable-next-line no-unused-vars
              .then(response => {
                this.fetchBooks();
              })
              .catch(error => {
                console.error(error);
              });
        }
      },
    },
    mounted() {
      this.fetchBooks();
    },
  };
  </script>
  