<template>
  <v-app>
    <header>
      <v-app-bar flat color="primary">
        <v-toolbar-title
        class="white--text">
          <strong>ひとりじゃないよ</strong>
        </v-toolbar-title>
        <v-col class="text-right">
          <img src="@/assets/image/icon.png" class="icon">
        </v-col>
      </v-app-bar>
    </header>
    <nuxt />
  </v-app>
</template>

<script>
export default {
  data () {
    return {
    }
  }
}
</script>

<style>
.bg {
  text-align: right;
}

.pattyo-icon {
  width: 40px;
  height: 40px;
  margin-right: 5px;
}

.icon {
  width: 100px;
  height: 20px;
}
</style>
