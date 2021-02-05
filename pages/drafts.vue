<template>
  <div>
    <div v-if="drafts.length == 0">
      {{getDraftsForSeason7}}
    </div>
    <v-row justify="center" align="center">
      <v-col cols="12" sm="8" md="6" v-for="draft in drafts" :key="draft">
        <v-card>
          <v-card-title>
            Season {{draft.season.split("season_")[1]}} {{draft.name}}
          </v-card-title>
          <v-card-subtitle >
          <v-row justify="center" align="center">
            <h4>Liaisons</h4>
            <v-spacer/>
            <div v-for="liaison in draft.liaisons" :key="liaison">
              <v-chip :color="liaison.color">{{liaison.name}}</v-chip>
            </div>
          </v-row>
          <br>
          <br>
          <v-row justify="center" align="center">
          <h4>Status</h4>
          <v-spacer/>
          <v-chip v-if="draft.isCurrent" color="green">
            Ongoing
          </v-chip>
          <v-chip v-else color="brown lighten-3">
            Old
          </v-chip>
          </v-row>
          </v-card-subtitle>
          <v-btn :href="draft.draft_doc">View Doc</v-btn>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>
<script>
export default {
  data: () => ({
    drafts: []
  }),
  computed: {
    async getDraftsForSeason7() {
      await this.$axios.get("https://pokemon-backend.netlify.app/.netlify/functions/api/draft/")
        .then(({data}) =>
        {
          this.drafts = data;
          console.log(data);
        }).catch(error => console.error(error));
    }
  }
}
</script>
