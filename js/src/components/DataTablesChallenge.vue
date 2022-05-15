<template>
    
  <v-row>
    <v-col>
      <h2>Data Tables Challenge</h2>
       <v-data-table
       data-test-id="the-data-table"
    :headers="headers"
    :sort-by="['lastNoteByCurrentUser']"
    :sort-desc="[true]"
    :items="allLoanApplications"
    :items-per-page="10"
    class="elevation-1"
  >
  <template v-slot:item.updatedAt="{ item }">{{formatDate(item.updatedAt)}}</template>
  <template v-slot:item.lastNoteByCurrentUser="{ item }">{{formatDate(item.lastNoteByCurrentUser)}}</template>
  <template v-slot:item.timeInStatus="{ item }">{{formatDate(item.timeInStatus)}}</template>
  </v-data-table>
    </v-col>
  </v-row>
</template>

<script>
import { mapActions, mapGetters } from 'vuex';
import { DateTime } from "luxon";

export default {
  data: () => ({
    // declare initial data here
     headers: [
                {
                    text: "App Id",
                    value: "id",
                },
                {
                    text: "Last Name",
                    value: "lastName",
                },
                {
                    text: "First Name",
                    value: "firstName",
                },
                {
                    text: "State",
                    value: "state",
                },
                {
                    text: "Status",
                    value: "status",
                },
                {
                    text: "My Last Note",
                    value: "lastNoteByCurrentUser",
                },
                {
                    text: "Time In Status",
                    value: "timeInStatus",
                },
                {
                    text: "Task",
                    value: "oldestOpenTask",
                },
                {
                    text: "Last Updated",
                    value: "updatedAt",
                },
            ]
  }),
  mounted() {
        this.loadLoanApplications()
    },

  computed: {
    ...mapGetters({
      allLoanApplications: 'allLoanApplications'
    })
  },

  methods: {
    ...mapActions({
      loadLoanApplications: 'loadLoanApplications'
    }),
    formatDate(date) {
return DateTime.fromISO(date).toRelative()
    }
  }
};
</script>
