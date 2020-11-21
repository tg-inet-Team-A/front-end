<template>
  <div>
    <v-card class="mx-auto my-10"
    max-width="400">
      <v-card-title>
        おはようございます
      </v-card-title>
      <v-card-text>
        現在、{{count}} 人の方が起きています。
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  components: {
  },
  data: () => ({
    count : 0,
  }),
  methods: {
    async get_count_people(){
      return 8;
    }
  },
  async mounted() {
    this.count = await this.get_count_people();
  }
}
</script>
