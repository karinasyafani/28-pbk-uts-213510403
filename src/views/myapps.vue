<template>
    <div class="container">
      <h2 class="title">To-Do List Tugas Kuliah</h2>
      <form @submit.prevent="tambahtugas" class="form-tambah">
        <input type="text" v-model="tugasBaru" placeholder="Tambah tugas baru" class="form-tambah__input">
        <button type="submit" class="form-tambah__button">Tambah</button>
      </form>
      <ul class="list-tugas">
        <li v-for="(tugas, index) in daftartugas" :key="index" class="list-tugas__item">
          <input type="checkbox" :id="'tugas-' + index" :checked="tugas.selesai" @change="tandaiSelesai(index)" class="list-tugas__checkbox">
          <label :for="'tugas-' + index" class="list-tugas__label">{{ tugas.nama_tugas }}</label>
          <button @click.prevent="hapustugas(index)" class="list-tugas__button">Hapus</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        tugasBaru: '',
        daftartugas: []
      }
    },
    methods: {
      tambahtugas() {
        if (this.tugasBaru !== '') {
          this.daftartugas.push({ nama_tugas: this.tugasBaru, selesai: false });
          this.tugasBaru = '';
        }
      },
      tandaiSelesai(index) {
        this.daftartugas[index].selesai = !this.daftartugas[index].selesai;
      },
      hapustugas(index) {
        this.daftartugas.splice(index, 1);
      }
    }
  }
  </script>
  
  <style>
  .container {
    max-width: 800px;
    margin: 0 auto;
  }
  .title {
    font-size: 24px;
    font-weight: bold;
    margin-top: 30px;
    margin-bottom: 20px;
  }
  .form-tambah {
    display: flex;
    margin-bottom: 20px;
  }
  .form-tambah__input {
    flex: 1;
    padding: 10px;
    border-radius: 3px;
    border: 1px solid #ccc;
  }
  .form-tambah__button {
    background-color: #0080ff;
    color: #fff;
    padding: 10px;
    border-radius: 3px;
    border: none;
    margin-left: 10px;
    cursor: pointer;
  }
  .list-tugas {
    list-style: none;
    margin: 0;
    padding: 0;
  }
  .list-tugas__item {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
    border-radius: 3px;
    background-color: #f8f8f8;
    padding: 10px;
  }
  .list-tugas__checkbox {
    margin-right: 10px;
  }
  .list-tugas__label {
    font-size: 18px;
    font-weight: bold;
    color: #333;
  }
  .list-tugas__label:before {
    content: "\2022";
    margin-right: 10px;
    color: #ccc;
  }
  .list-tugas__label.selesai {
    color: #C0C0C0;
  }
  </style>