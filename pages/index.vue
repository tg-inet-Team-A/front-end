<template>
  <div>
    <v-row>
      <v-col cols="3"></v-col>
      <v-col cols="6">
        エリアを選択してください
        <v-autocomplete
          v-model="erea"
          :items="ereas"
          item-text="erea_name"
          item-value="erea_id"
          return-object
          v-on:change="get_count_people"
        ></v-autocomplete>
      </v-col>
      <v-col cols="3"></v-col>
    </v-row>
    <template v-if="erea != null">
      <v-card class="mx-auto my-10"
        max-width="450" outlined>
        <v-card-title>
          {{greeting}}
        </v-card-title>
        <v-card-text>
          現在、{{erea.erea_name}}では 
          <v-avatar color="primary" size="40" class="white--text">
            <h3>{{res.wakeup_people}}</h3>
          </v-avatar>
          人の方が起きています。
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
    ereas : [],
    erea : null,
    res : {}, //{"erea_id": erea_id, "wakeup_people": num}

    greeting : "おはようございます"
  }),
  methods: {
    async set_greeting() {
      console.log("set_greeting");
      const now = new Date().toLocaleString({ timeZone: 'Asia/Tokyo' });
      var hour = new Date(now).getHours();
      if (4 < hour && hour <= 10) {
        this.greeting = "おはようございます"
      } else if (10 < hour && hour <= 18) {
        this.greeting = "こんにちは"
      } else {
        this.greeting = "こんばんは"
      }
    },
    async get_erea_all() {
      return [
        {"erea_id":0, "erea_name":"東京"},
        {"erea_id":1, "erea_name":"大阪"}
      ]
    },
    async get_count_people() {
      console.log("get_count_people");
      const that = this;
      var res = 1;
      this.$axios.$get("http://localhost:5000/erea/"+that.erea.erea_id+"/wakeup_people")
        .then(function (response) {
          console.log(response);
          that.res = response;
        });
    },
  },
  async mounted() {
    await this.set_greeting();
    this.ereas = await this.get_erea_all();
  }
}
</script>
