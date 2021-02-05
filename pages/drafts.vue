<template>
  <div>

    <!-- <div v-if="drafts.length == 0">
      {{getDraftsForSeason7}}
    </div> -->

    <div>
      <v-data-table
      :headers="headers"
      :items="drafts"
      item-key="name"
      class="elevation-1"
      :search="search"
      :custom-filter="filterDrafts">
      <template v-slot:top>
        <v-text-field
        v-model="search"
        label="Search For Draft"
        class="mx-4"></v-text-field>
      </template>
      <template v-slot:body.append>
        <tr>
          <td></td>
        </tr>

      </template>
      </v-data-table>
    </div>
  </div>
</template>
<script>
export default {
  data: () => ({
    search: "",
    drafts: []
  }),
  computed: {
    headers() {
      return [
        {
          text: 'League',
          align: 'start',
          sortable: false,
          value: 'name'
        },
        {
          text: 'Season',
          value: 'season',
        },
        {
          text: 'Liaisons',
          value: 'liaisons'
        },
        {
          text: 'Doc',
          value: 'draftDoc'
        }
      ]
    },
    async getDraftsForSeason7() {
      await this.$axios.get("https://pokemon-backend.netlify.app/.netlify/functions/api/draft/")
        .then(({data}) =>
        {
          this.drafts = data;
          console.log(data);
        }).catch(error => console.error(error));
    }
  },
  methods: {
    filterDrafts(value, search, item)
    {
      return value != null &&
       search != null &&
        typeof value === 'string' &&
         value.toString().toLocaleUpperCase().indexOf(search.toUpperCase()) !== -1
    }
  }
}
</script>
