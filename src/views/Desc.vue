<template>
    <div class="search-form">
        <input type="text" v-model="searchQuery" placeholder="Search loan id">
        <button @click="searchAnggota">Search</button>
    </div>
    <div>
        <div class="text-center">
            <h1>Data Peminjaman Buku</h1>
            <form @submit.prevent="submitPeminjaman">
                <div class="form-group">
                    <label for="idPeminjaman">ID Peminjaman</label>
                    <input type="text" class="form-control" v-model="pengembalian.idPeminjaman" id="idPeminjaman" required>
                </div>
                <div class="form-group">
                    <label for="tanggal">Tanggal Peminjaman</label>
                    <input type="date" class="form-control" v-model="peminjaman.tanggal" id="tanggal" required>
                </div>
                <div class="form-group">
                    <label for="tanggal">Tanggal Pengembalian</label>
                    <input type="date" class="form-control" v-model="pengembalian.tanggal" id="tanggal" required>
                </div>

                <div class="form-group">
                    <label for="nomorAnggota">Nomor Anggota</label>
                    <input type="text" class="form-control" v-model="peminjaman.nomorAnggota" id="nomorAnggota" required>
                </div>
                <div class="form-group">
                    <label for="kodeBuku">Kode Buku</label>
                    <input type="text" class="form-control" v-model="peminjaman.kodeBuku" id="kodeBuku" required>
                </div>
                <button type="submit" class="btn btn-success">Add</button>
            </form>
            <h1>Data Pengembalian Buku</h1>
            <form @submit.prevent="submitPengembalian">
                <div class="form-group">
                    <label for="idPeminjaman">ID Peminjaman</label>
                    <input type="text" class="form-control" v-model="pengembalian.idPeminjaman" id="idPeminjaman" required>
                </div>
                <div class="form-group">
                    <label for="tanggal">Tanggal Pengembalian</label>
                    <input type="date" class="form-control" v-model="pengembalian.tanggal" id="tanggal" required>
                </div>
                <button type="submit" class="btn btn-success">Add</button>
            </form>
        </div>
        <h2>Riwayat peminjaman buku yang masih dipinjam </h2>
        <table class="table">
            <thead>
            <tr class="table-secondary">
                <th>ID</th>
                <th>Tanggal Peminjaman</th>
                <th>Nomor Anggota</th>
                <th>Status Peminjaman</th>
                <th>Tanggal Pengembalian</th>
                <th>Durasi Keterlambatan</th>
            </tr>
            </thead>
            <tbody class="table-light">
            <tr v-for="peminjaman in peminjamanDipinjam" :key="peminjaman.id">
                <td>{{ peminjaman.id }}</td>
                <td>{{ peminjaman.tanggal_peminjaman }}</td>
                <td>{{ peminjaman.nomor_anggota }}</td>
                <td>{{ peminjaman.status_peminjaman }}</td>
                <td>{{ peminjaman.tanggal_pengembalian }}</td>
                <td>{{ peminjaman.durasi_keterlambatan }}</td>
            </tr>
            </tbody>
        </table>

        <h2>Riwayat peminjaman buku yang sudah dikembalikan</h2>
        <table class="table">
            <thead>
            <tr class="table-secondary">
                <th>ID</th>
                <th>Tanggal Peminjaman</th>
                <th>Nomor Anggota</th>
                <th>Status Peminjaman</th>
                <th>Tanggal Pengembalian</th>
                <th>Durasi Keterlambatan</th>
            </tr>
            </thead>
            <tbody class="table-light">
            <tr v-for="peminjaman in peminjamanDikembalikan" :key="peminjaman.id">
                <td>{{ peminjaman.id }}</td>
                <td>{{ peminjaman.tanggal_peminjaman }}</td>
                <td>{{ peminjaman.nomor_anggota }}</td>
                <td>{{ peminjaman.status_peminjaman }}</td>
                <td>{{ peminjaman.tanggal_pengembalian }}</td>
                <td>{{ peminjaman.durasi_keterlambatan }}</td>
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
            peminjaman: {
                tanggal: '',
                nomorAnggota: '',
                kodeBuku: '',
            },
            pengembalian: {
                idPeminjaman: '',
                tanggalPengembalian: '',
            },
            peminjamanDipinjam: [],
            peminjamanDikembalikan: [],
        };
    },
    mounted() {
        // Mengambil data peminjaman dengan status DIPINJAM dari API backend PHP
        this.fetchPeminjamanDipinjam();
        // Mengambil data peminjaman dengan status DIKEMBALIKAN dari API backend PHP
        this.fetchPeminjamanDikembalikan();
    },
    methods: {
        submitPeminjaman() {
            fetch('hhttp://localhost/buku-backend/peminjamanBuku.php', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(this.peminjaman),
            })
                .then(response => response.json())
                .then(data => {
                    console.log(data);
                    // Lakukan tindakan setelah peminjaman berhasil disimpan
                })
                .catch(error => {
                    console.error(error);
                    // Lakukan tindakan jika terjadi kesalahan saat melakukan peminjaman
                });
        },
        submitPengembalian() {
            fetch('http://localhost/buku-backend/pengembalianBuku.php', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(this.pengembalian),
            })
                .then(response => response.json())
                .then(data => {
                    console.log(data);
                    // Lakukan tindakan setelah pengembalian berhasil disimpan
                })
                .catch(error => {
                    console.error(error);
                    // Lakukan tindakan jika terjadi kesalahan saat melakukan pengembalian
                });
        },
        fetchPeminjamanDipinjam() {
            // Panggil API backend PHP untuk mendapatkan data peminjaman dengan status DIPINJAM
            axios.get('http://localhost/buku-backend/listStatusDipinjam.php')
                .then((response) => {
                    this.peminjamanDipinjam = response.data;
                })
                .catch((error) => {
                    console.error(error);
                });
        },
        fetchPeminjamanDikembalikan() {
            // Panggil API backend PHP untuk mendapatkan data peminjaman dengan status DIKEMBALIKAN
            axios.get( 'http://localhost/buku-backend/listStatusDikembalikan.php')
                .then((response) => {
                    this.peminjamanDikembalikan = response.data;
                })
                .catch((error) => {
                    console.error(error);
                });
        },
    },
};
</script>

<style>
.form-group {
    text-align: left;
}

h1 {
    text-align: left;
    font-family: "Lucida Bright";
}

h2 {
    font-style: italic;
    font-family: "Lucida Bright";
}

.text-center {
    padding-top: 10px;
}

</style>