<template>
 <div class="container-fluid">
   <nav class="navbar navbar-light bg-light">
    <span class="navbar-brand mb-0 h1">Participants</span>
  </nav>
  <div class="app-content">
    <participants-list v-bind:participants="participants" v-on:remove-participant="onRemove($event)"></participants-list>
    <participant-add-form v-on:addParticipant="addParticipant($event)"></participant-add-form>
  </div>
 </div>
</template>

<script>
  import ParticipantsList from './components/ParticipantsList.vue';
  import ParticipantAddForm from './components/ParticipantAddForm.vue';

  export default {
    components: {
      ParticipantsList,
      ParticipantAddForm
    },
    data: function () {
      return {
        participants: [],
      }
    },
    methods: {
      addParticipant: function(newParticipant){
        this.$http.post('participants', newParticipant).then(response => {
          this.participants.push(newParticipant);
        });

      },
      onRemove: function (participantToRemove){
        this.$http.post('participants', newParticipant).then(response => {
          this.participants.push(newParticipant);
        });
        this.participants = this.participants.filter((participant) => {
          return participant.id !== participantToRemove.id;
        });
      }
    },
    mounted() {
      this.$http.get('participants').then(response => {
        this.participants = response.body;
      });
    }
  };
</script>

<style>
.container-fluid {
  margin: 0;
  padding: 0;
}

.app-content {
  margin: 30px;
}
</style>