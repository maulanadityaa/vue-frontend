<template>
  <form @submit.prevent="submitForm">
    <h2>Add a book</h2>
    <label>Judul Buku: </label>
    <input
      type="text"
      name="judul"
      id="judul"
      placeholder="Judul Buku"
      required
      v-model="form.judul"
    />
    <label>Penulis Buku: </label>
    <input
      type="text"
      name="penulis"
      id="penulis"
      placeholder="Penulis Buku"
      required
      v-model="form.penulis"
    />
    <label>Kategori Buku: </label>
    <input
      type="text"
      name="kategori"
      id="kategori"
      placeholder="Kategori Buku"
      required
      v-model="form.kategori"
    />
    <label>Stock Buku: </label>
    <input
      type="number"
      name="stock"
      id="stock"
      placeholder="Stock Buku"
      required
      v-model="form.stock"
    />
    <br />
    <div class="submit">
      <button type="submit" class="btn btn-primary">Submit</button>
    </div>
  </form>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      form: {
        judul: "",
        penulis: "",
        kategori: "",
        stock: "",
      },
    };
  },
  methods: {
    submitForm() {
      axios
        .post(
          "https://tim-empat-api-gateway.herokuapp.com/api/book",
          this.form,
          {
            params: {
              token: window.sessionStorage.getItem("token"),
            },
          }
        )
        .then((response) => {
          this.$router.push({
            name: "Index",
          });
          this.$router.go(0);
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style>
form {
  max-width: 520px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: grey;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}
.submit {
  text-align: center;
}
</style>