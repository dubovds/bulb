<template>
  <section class="container">
    <div>
      <app-logo/>
      <h1 class="title">
        bulb
      </h1>
      <to-do/>
    </div>
  </section>
</template>

<script>
import Vue from 'vue'
import ToDo from '~/components/ToDo.vue'
import AppLogo from '~/components/AppLogo.vue'

export default {
  components: {
    ToDo,
    AppLogo
  }
}

</script>

<style>
.container {
  width: 1140px;
  margin: auto;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
.add_room{
  display: inline-block;
  margin-top: 15px;
  padding: 5px 15px;
  border: 1px solid green;
  border-radius: 5px;
  cursor: pointer;
}
</style>
