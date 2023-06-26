<template>
<<<<<<< HEAD
  <div>
    <h1>Daftar Anggota</h1>
    <div class="search-form">
      <input type="text" v-model="searchQuery" placeholder="Cari nomor anggota">
      <button @click="searchAnggota">Search</button>
    </div>

    <!-- Tampilkan seluruh anggota -->
    <table class="table">
      <thead>
      <tr>
=======
  <h1>Anggota Pustaka</h1>
  <div>
    <input type="number" v-model="selectedNumber" />
    <button @click="selectMember">Pilih Anggota</button>

    <h3>Tambah Anggota Baru</h3>
    <div>
      <input type="text" v-model="newMember.nomor" placeholder="Nomor" />
      <input type="text" v-model="newMember.nama" placeholder="Nama" />
      <input type="text" v-model="newMember.jenis_kelamin" placeholder="Jenis Kelamin" />
      <input type="text" v-model="newMember.alamat" placeholder="Alamat" />
      <input type="text" v-model="newMember.no_hp" placeholder="No. HP" />
      <input type="text" v-model="newMember.tanggal_terdaftar" placeholder="Tanggal Terdaftar" />
      <button @click="addMember">Tambah</button>
    </div>

    <h3>Update Anggota</h3>
    <div>
      <input type="text" v-model="updateMember.nomor" placeholder="Nomor" />
      <input type="text" v-model="updateMember.nama" placeholder="Nama" />
      <input type="text" v-model="updateMember.jenis_kelamin" placeholder="Jenis Kelamin" />
      <input type="text" v-model="updateMember.alamat" placeholder="Alamat" />
      <input type="text" v-model="updateMember.no_hp" placeholder="No. HP" />
      <input type="text" v-model="updateMember.tanggal_terdaftar" placeholder="Tanggal Terdaftar" />
      <button @click="updateMemberData">Update</button>
    </div>

    <h3>Hapus Anggota</h3>
    <div>
      <input type="number" v-model="deleteMemberNumber" placeholder="Nomor" />
      <button @click="deleteMember">Hapus</button>
    </div>

    <h3>Semua Anggota</h3>
    <table class="table">
      <thead>
      <tr>
        <th>Id</th>
>>>>>>> bd062a7 (Initial commit)
        <th>Nomor</th>
        <th>Nama</th>
        <th>Jenis Kelamin</th>
        <th>Alamat</th>
        <th>No. HP</th>
        <th>Tanggal Terdaftar</th>
<<<<<<< HEAD
        <th>Aksi</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="anggota in anggotaList" :key="anggota.id">
        <td>{{ anggota.nomor }}</td>
        <td>{{ anggota.nama }}</td>
        <td>{{ anggota.jenis_kelamin }}</td>
        <td>{{ anggota.alamat }}</td>
        <td>{{ anggota.no_hp }}</td>
        <td>{{ anggota.tanggal_terdaftar }}</td>
        <td>
          <button class="btn btn-primary" @click="editAnggota(anggota)">Edit</button>
          <button class="btn btn-danger" @click="hapusAnggota(anggota.nomor)">Hapus</button>
        </td>
      </tr>
      </tbody>
    </table>

    <!-- Form untuk menambah dan mengedit anggota -->

    <div class="card">
      <div class="card-body">
        <h2>{{ mode === 'tambah' ? 'Tambah Anggota' : 'Edit Anggota' }}</h2>
        <form @submit.prevent="submitForm">
          <div class="form-group">
            <label for="nomor">Nomor:</label>
            <input type="text" class="form-control" v-model="anggota.nomor" required>
          </div>
          <div class="form-group">
            <label for="nama">Nama:</label>
            <input type="text" class="form-control" v-model="anggota.nama" required>
          </div>
          <div class="form-group">
            <label for="jenis_kelamin">Jenis Kelamin:</label>
            <select class="form-control" v-model="anggota.jenis_kelamin" required>
              <option value="Laki-laki">Laki-laki</option>
              <option value="Perempuan">Perempuan</option>
            </select>
          </div>
          <div class="form-group">
            <label for="alamat">Alamat:</label>
            <textarea class="form-control" v-model="anggota.alamat" required></textarea>
          </div>
          <div class="form-group">
            <label for="no_hp">No. HP:</label>
            <input type="text" class="form-control" v-model="anggota.no_hp" required>
          </div>
          <div class="form-group">
            <label for="tanggal_terdaftar">Tanggal Terdaftar:</label>
            <input type="date" class="form-control" v-model="anggota.tanggal_terdaftar" required>
          </div>
          <button type="submit" class="btn btn-primary" @click="submitForm">{{ mode === 'tambah' ? 'Tambah' : 'Simpan' }}</button>
          <button type="button" class="btn btn-secondary" @click="resetForm">Batal</button>
        </form>
      </div>
    </div>
=======
      </tr>
      </thead>
      <tr v-for="member in members" :key="member.id">
        <td>{{ member.id }}</td>
        <td>{{ member.nomor }}</td>
        <td>{{ member.nama }}</td>
        <td>{{ member.jenis_kelamin }}</td>
        <td>{{ member.alamat }}</td>
        <td>{{ member.no_hp }}</td>
        <td>{{ member.tanggal_terdaftar }}</td>
      </tr>
    </table>
>>>>>>> bd062a7 (Initial commit)
  </div>
</template>

<script>
<<<<<<< HEAD
import axios from 'axios';

export default {
  data() {
    return {
      anggotaList: [], // Daftar anggota
      anggota: {
        searchNumber: '',
        searchedMember: null,
        nomor: '',
        nama: '',
        jenis_kelamin: '',
        alamat: '',
        no_hp: '',
        tanggal_terdaftar: ''
      },
      mode: 'tambah', // Mode form: tambah atau edit
      searchNumber: '',
      searchedMember: null,
    };
  },
  mounted() {
    // Ambil seluruh anggota saat komponen di-load
    this.getAnggotaList();
    this.search();
  },
  methods: {
      search() {
        const number = this.searchNumber;
        axios.get(`http://localhost/buku/select-nomor-anggota.php?nomor=${number}`)
            .then(response => {
              this.searchedMember = response.data;
            })
            .catch(error => {
              console.error(error);
              this.searchedMember = null;
            });
      },
    // Ambil seluruh anggota dari backend API
    getAnggotaList() {
      axios.get('http://localhost/buku/select-anggota.php')
          .then(response => {
            this.anggotaList = response.data;
          })
          .catch(error => {
            console.log(error);
          });
    },
    // Reset form
    resetForm() {
      this.anggota = {
        nomor: '',
        nama: '',
        jenis_kelamin: '',
        alamat: '',
        no_hp: '',
        tanggal_terdaftar: ''
      };
      this.mode = 'tambah';
    },
    // Menambah atau mengedit anggota
    submitForm() {
      if (this.mode === 'tambah') {
        axios.post('http://localhost/buku/insert-anggota.php', this.anggota)
            .then(response => {
              console.log(response.data);
              // Reset form dan ambil seluruh anggota setelah sukses menambahkan anggota
              this.resetForm();
              this.getAnggotaList();
            })
            .catch(error => {
              console.log(error);
            });
      } else {
        axios.put('http://localhost/buku/update-nomor-anggota.php' + this.anggota.nomor, this.anggota)
            .then(response => {
              console.log(response.data);
              // Reset form dan ambil seluruh anggota setelah sukses mengedit anggota
              this.resetForm();
              this.getAnggotaList();
            })
            .catch(error => {
              console.log(error);
            });
      }
    },
    // Menghapus anggota berdasarkan nomor
    hapusAnggota(nomor) {
      axios.delete('http://localhost/buku/delete-nomor-anggota.php' + nomor)
          .then(response => {
            console.log(response.data);
            // Ambil seluruh anggota setelah sukses menghapus anggota
            this.getAnggotaList();
          })
          .catch(error => {
            console.log(error);
          });
    },
    // Mengisi form dengan data anggota yang akan di-edit
    editAnggota(anggota) {
      this.anggota = { ...anggota };
      this.mode = 'edit';
=======
export default {
  data() {
    return {
      selectedNumber: null,
      deleteMemberNumber: null,
      members: [],
      newMember: {
        nomor: "",
        nama: "",
        jenis_kelamin: "",
        alamat: "",
        no_hp: "",
        tanggal_terdaftar: ""
      },
      updateMember: {
        nomor: "",
        nama: "",
        jenis_kelamin: "",
        alamat: "",
        no_hp: "",
        tanggal_terdaftar: ""
      }
    };
  },
  mounted() {
    this.fetchMembers();
  },
  methods: {
    async fetchMembers() {
      try {
        const response = await fetch("http://localhost/buku/select-anggota.php");
        if (response.ok) {
          const data = await response.json();
          this.members = data;
        } else {
          console.error("Gagal memuat data anggota");
        }
      } catch (error) {
        console.error(error);
      }
    },
    async selectMember() {
      try {
        const response = await fetch(`http://localhost/buku/select-nomor-anggota.php?nomor=${this.selectedNumber}`);
        if (response.ok) {
          const data = await response.json();
          console.log(data);
        } else {
          console.error("Gagal memuat data anggota");
        }
      } catch (error) {
        console.error(error);
      }
    },
    async addMember() {
      try {
        const response = await fetch("http://localhost/buku/insert-anggota.php", {
          method: "POST",
          headers: {
            "Content-Type": "application/json"
          },
          body: JSON.stringify(this.newMember)
        });
        if (response.ok) {
          console.log("Anggota baru ditambahkan");
          this.fetchMembers();
        } else {
          console.error("Gagal menambahkan anggota baru");
        }
      } catch (error) {
        console.error(error);
      }
    },
    async updateMemberData() {
      try {
        const response = await fetch(`http://localhost/buku/update-nomor-anggota.php?nomor=${this.updateMember.nomor}`, {
          method: "PUT",
          headers: {
            "Content-Type": "application/json"
          },
          body: JSON.stringify(this.updateMember)
        });
        if (response.ok) {
          console.log("Data anggota diperbarui");
          this.fetchMembers();
        } else {
          console.error("Gagal memperbarui data anggota");
        }
      } catch (error) {
        console.error(error);
      }
    },
    async deleteMember() {
      try {
        const response = await fetch(`http://localhost/buku/delete-nomor-anggota.php?nomor=${this.deleteMemberNumber}`, {
          method: "DELETE"
        });
        if (response.ok) {
          console.log("Anggota dihapus");
          this.fetchMembers();
        } else {
          console.error("Gagal menghapus anggota");
        }
      } catch (error) {
        console.error(error);
      }
>>>>>>> bd062a7 (Initial commit)
    }
  }
};
</script>
<<<<<<< HEAD

<style scoped>
/* Styling sesuai kebutuhan Anda */
</style>
=======
>>>>>>> bd062a7 (Initial commit)
