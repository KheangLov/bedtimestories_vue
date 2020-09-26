<template>
  <b-container class="h-100 d-flex justify-content-center">
    <b-card
      class="my-auto border-0 shadow-sm rounded auth-form"
    >
      <b-img src="http://mybedtimestories.epizy.com/assets/images/icon-logo.png" fluid center></b-img>
      <Nuxt />
    </b-card>
  </b-container>
</template>

<style lang="scss">
  html, body {
    height: 100%;

    #__nuxt {
      height: 100%;

      #__layout {
        height: 100%;

        .auth-form {
          width: 360px;
        }
      }
    }
  }
</style>
