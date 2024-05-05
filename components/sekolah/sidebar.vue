<template>
  <!-- Sidebar Menu -->
  <nav class="mt-2 text-white overflow-hidden">
    <ul
      class="nav nav-pills nav-sidebar flex-column"
      data-widget="treeview"
      role="menu"
      data-accordion="false"
    >
      <li class="nav-item">
        <nuxt-link :to="{ name: 'dashboard' }" class="nav-link">
          <i class="nav-icon fas fa-tachometer-alt text-white"></i>
          <p>Dashboard</p>
        </nuxt-link>
      </li>

      <!-- <li class="nav-header">
        <h5>CONTENT</h5>
      </li> -->

      <li class="nav-item">
        <nuxt-link :to="{ name: 'absen' }" class="nav-link">
          <!-- <i class="nav-icon fas fa-tags"></i> -->
          <p>Absen</p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'bacaan' }" class="nav-link">
          <!-- <i class="nav-icon fas fa-folder"></i> -->
          <p>Bacaan</p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'catatan' }" class="nav-link">
          <!-- <i class="nav-icon fas fa-book-open"></i> -->
          <p>Catatan</p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'guru' }" class="nav-link">
          <p>Guru</p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'Jadwal_Pelajaran' }" class="nav-link">
          <p>Jadwal Pelajaran</p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'jurusan' }" class="nav-link">
          <p>Jurusan</p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'kalender_event' }" class="nav-link">
          <p>Kalender Event</p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'kelasjurusan_ta' }" class="nav-link">
          <p>Kelas Jurusan</p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'konsultasi_bk' }" class="nav-link">
          <p>Bimbingan Konseling</p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'penerbit' }" class="nav-link">
          <p>Penerbit</p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'penulis' }" class="nav-link">
          <p>Penulis</p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'siswa_kelas' }" class="nav-link">
          <p>Siswa Kelas</p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'Tabungan' }" class="nav-link">
          <p>Tabungan</p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'tugassekolah' }" class="nav-link">
          <p>Tugas</p>
        </nuxt-link>
      </li>

      <!-- <li class="nav-header">
        <h6>SETTINGS</h6>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'admin-menu' }" class="nav-link">
          <i class="nav-icon fas fa-clone"></i>
          <p>Menus</p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'admin-slider' }" class="nav-link">
          <i class="nav-icon fas fa-image"></i>
          <p>Sliders</p>
        </nuxt-link>
      </li>

      <li class="nav-item">
        <nuxt-link :to="{ name: 'admin-user' }" class="nav-link">
          <i class="nav-icon fas fa-users"></i>
          <p>Users</p>
        </nuxt-link>
      </li> -->
    </ul>
  </nav>
  <!-- /.sidebar-menu -->
</template>

<script>
export default {};
</script>

<style scoped>
a.nuxt-link-active {
  background-color: rgba(255, 255, 255, 0.1);
}

p {
  color: white;
}
</style>
