<script>

</script>

<template>
  <div id="header" class="container-fluid bg-dark py-4 menu">

    <div class="row justify-content-center ">
      <div class="col-12 col-lg-3 text-center text-center">
        <RouterLink active-class="active" to="/">
          <button class="rounded-2 btn_bg_green mx-1">
            <span>Home</span>
          </button>
        </RouterLink>

        <RouterLink active-class="active" to="/links">
          <button class="rounded-2 btn_bg_green mx-1">
            <span>Links</span>
          </button>
        </RouterLink>

      </div>
    </div>
  </div>
  <RouterView />
</template>

<style></style>