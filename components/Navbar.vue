<template>
  <div class="flex justify-between items-center py-4">
    <div>
      <nuxt-link to="/">
        <span class="flex text-white items-center">
          <img src="/images/logo-navbar.png" width="80px" height="80px" />NUXT
          APP
        </span>
      </nuxt-link>
    </div>
    <div>
      <nuxt-link to="/saved">
        <IconsIconSaved class="h-12 w-12" :color="'#6563ff'" :stroke="'none'" />
      </nuxt-link>
    </div>
  </div>
</template>

<script setup></script>

<style lang="scss" scoped></style>
