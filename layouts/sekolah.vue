<template>
  <div class="hold-transition sidebar-mini">
    <div class="wrapper min-vh-100">
      <!-- Header -->
      <Header />
      <!-- /.Hader -->

      <aside
        class="main-sidebar elevation-4 px-3"
        style="background-color: #037cab"
      >
        <a to="/dashboard" class="brand-link text-center">
          <span class="brand-text font-weight-bold text-light">
            Aplikasi E-sekolah
          </span>
        </a>

        <!-- Sidebar -->
        <div class="sidebar mb-5">
          <Sidebar />
        </div>
        <!-- /.sidebar -->
      </aside>

      <!-- content -->
      <Nuxt />
      <!-- / .content -->

      <!-- <footer class="main-footer">
          <div class="float-right d-none d-sm-block"><b>Version</b> 1.0.0</div>
          <strong>Copyright &copy; 2024 Assessment Diskominfo Kota Bogor.</strong>
          All rights reserved.
        </footer> -->
      <aside class="control-sidebar control-sidebar-dark"></aside>
    </div>
  </div>
</template>

<script>
import Header from "@/components/sekolah/header.vue";
import Sidebar from "@/components/sekolah/sidebar.vue";

export default {
  //middleware auth
  //   middleware: "auth",

  components: {
    Header,
    Sidebar,
  },
};
</script>

<style>
.wrapper,
.content-wrapper {
  background-color: #fff !important;
  overflow: hidden;
}
</style>
