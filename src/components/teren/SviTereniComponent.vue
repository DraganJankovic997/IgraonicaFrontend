<template>
  <div class="container">
    <p></p>
    <button class="btn btn-secondary" @click="dodajTeren">Dodaj teren</button>
    <p></p>
    <table class="table text-center table-hover">
      <thead class="thead-dark">
        <tr>
          <th scope="col">#</th>
          <th scope="col">Naziv</th>
          <th scope="col">Sport</th>
          <th scope="col">Lokacija</th>
          <th scope="col">Opcije</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for=" (l, i) in computedTereni" :key="l.id" @click="redirekcija(l.id)">
          <th scope="row">{{ i + 1 }}</th>
          <td>{{l.naziv}}</td>
          <td>{{l.sport.naziv}}</td>
          <td>{{l.lokacija.naziv}}</td>
          <td>
            <button class="btn btn-success btn-sm" @click="izmeniTeren(l.id)">Izmeni</button>
            <button class="btn btn-danger btn-sm ml-1" @click="obrisiTeren(l.id)">Obrisi</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
import terenService from "../../services/teren.service";

export default {
  data: function () {
    return {
      tereni: [],
    };
  },
  methods: {
    dodajTeren() {
      this.$router.push("/dodajTeren");
    },
    izmeniTeren(id) {
      this.$router.push("/tereni/edit/" + id);
    },
    obrisiTeren(id) {
      terenService
        .deleteTeren(id)
        .then((res) => {
          this.$toastr.s("Teren obrisan", "Brisanje uspesno");
          this.$router.go("/");
        })
        .catch((err) => {
          this.$toastr.e("Teren nije obrisan", "Brisanje neuspesno");
        });
    },
    redirekcija(id) {
      this.$router.push("/tereni/" + id);
    },
  },
  created() {
    terenService
      .getAllTeren()
      .then((res) => {
        this.tereni = res["data"];
        console.log("hi");
        console.log(res["data"]);
      })
      .catch((err) => {
        console.log(err);
      });
  },
  computed: {
    computedTereni() {
      return this.tereni;
    },
  },
};
</script>
<style>
</style>