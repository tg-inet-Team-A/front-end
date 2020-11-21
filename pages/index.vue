<template>
  <div>
    <v-row>
      <v-col cols="3"></v-col>
      <v-col cols="6">
        エリアを選択してください
        <v-select 
          v-model="erea"
          :items="ereas"
          item-text="name"
          item-value="id"
          return-object
        ></v-select>
      </v-col>
      <v-col cols="3"></v-col>
    </v-row>
    <template v-if="erea != null">
      <v-card class="mx-auto my-10"
        max-width="400" outlined>
        <v-card-title>
          おはようございます
        </v-card-title>
        <v-card-text>
          現在、{{erea.name}}では {{res.wakeup_people}} 人の方が起きています。
        </v-card-text>
      </v-card>
    </template>
  </div>
</template>

<script>
export default {
  components: {
  },
  data: () => ({
    erea : null,
    ereas : [],
    res : "",
  }),
  methods: {
    async get_erea_all() {
      return [
        {name:"東京", id:0},
        {name:"大阪", id:1},
      ]
    },
    async get_count_people() {
      console.log("get_count_people");
      const that = this;
      var res = 1;
      this.$axios.$get("http://localhost:5000/erea/0/wakeup_people")
        .then(function (response) {
          console.log(response);
          that.res = response;
        });
    },
  },
  async mounted() {
    this.ereas = await this.get_erea_all();
    await this.get_count_people();
  }
}
</script>
