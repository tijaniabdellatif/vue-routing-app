<template>
  <section>
    <h2>{{ teamName }}</h2>
    <ul>
      <user-item
        v-for="member in members"
        :key="member.id"
        :name="member.fullName"
        :role="member.role"
      ></user-item>
    </ul>

    <router-link to='/teams/t2'>Go to team 2</router-link>
  </section>
</template>

<script>
import UserItem from '../users/UserItem.vue';

export default {
  components: {
    UserItem
  },

  inject:['users','teams'],

  data() {
    return {

      teamName : "",
      members:[]

    };
  },


  methods:{
     loadTeam(route)
     {

       //this.$route.path //trams/t1
       const teamID = route.params.teamId;
       const selectedTeam = this.teams.find((team) => {

         return team.id === teamID
       });

       const members = selectedTeam.members;
       const selectedMembers = [];


       members.forEach(element => {

         const selectedUser = this.users.find(user => {

           return user.id === element
         })

         selectedMembers.push(selectedUser);
       })

       this.members = selectedMembers;
       this.teamName = selectedTeam.name;
     }
  },


  created() {

          this.loadTeam(this.$route);
  },
  watch:{

    $route(value){


         this.loadTeam(value)
    }
  }
};
</script>

<style scoped>
section {
  margin: 2rem auto;
  max-width: 40rem;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  border-radius: 12px;
}

h2 {
  margin: 0.5rem 0;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
