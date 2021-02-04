<template>
<div>
  <div v-if="staff.length == 0">
    {{getData}}
  </div>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6" v-for="member in staff" :key="member">
      <v-card>
        <v-card-title>
          <v-row justify="center" align="center">
            <v-col cols="12" sm="8" md="6">
            <v-avatar size="62" color="white">
            <v-img :alt="member.name" :src="member.avatar"></v-img>
          </v-avatar>
            </v-col >
            <v-col cols="12" sm="8" md="6">
              {{member.name}}
            </v-col>
          </v-row>
        </v-card-title>
        <v-card-subtitle>
          <v-row justify="center" align="center">
              <v-col cols="12" sm="8" md="6" v-for="role in member.roles" :key="role">
                <v-chip :color="role.color">{{role.name}}</v-chip>
              </v-col>
          </v-row>
        </v-card-subtitle>
      </v-card>
    </v-col>
  </v-row>
</div>

</template>

<script>
export default {
  data: () =>(
  {
    staff: []
  }),
  computed: {
    getData() {
      this.$axios.get("https://pokemon-backend.netlify.app/.netlify/functions/api/staff/", {withCredentials: true}).then(({data}) =>
      {
        this.staff = data;
      }).catch(error => console.error(error));
    }
  }
}
</script>
