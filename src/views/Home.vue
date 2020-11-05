<template>
  <div class="container home">
    <h1 class="page-title">Browse Character Profiles</h1>

    <div class="row justify-content-between mb-2">
      <div class="col-auto">
        <h4>Profiles found: {{ this.shownProfiles.length }}</h4>
      </div>
      <div class="col-auto">
        <input v-model="search" placeholder="search profiles">
      </div>
    </div>

    <div class="row person" v-for="profile in this.shownProfiles" :key="profile.id">
      <div class="col-md-3 name">
        <h2>{{ profile.name }}</h2>
      </div>
      <div class="col occupation">
        <h6>{{ profile.occupation }}</h6>
      </div>
      <div class="col-2 text-right view">
        <router-link :to="'/profile/' + profile.id"><strong>View Profile</strong></router-link>
      </div>
      <div class="col-1 text-center delete">
        <a href="#" id="delete" title="Delete Profile" @click="deleteProfile(profile)">X</a>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Home',
  data() {
    return {
      search: "",
      profiles: this.$root.$data.profiles,
    }
  },
  computed: {
    shownProfiles() {
      return this.profiles.filter(v =>
          v.name.toLowerCase().search(this.search.toLowerCase()) >= 0 ||
          v.occupation.toLowerCase().search(this.search.toLowerCase()) >= 0 ||
          v.profile.toLowerCase().search(this.search.toLowerCase()) >= 0);
    }
  },
  methods: {
    deleteProfile(profile) {
      let index = this.profiles.findIndex(v => v === profile);
      console.log(index);
      this.profiles.splice(index, 1);

      this.profiles.forEach(v => {
        if (v.id >= index) v.id--;
      });
    }
  }
}
</script>

<style scoped>

  .person {
    background-color: #e9ecef;
    margin-bottom: 1em;
    align-items: center;
  }
  .name {
    background-color: #497575;
    padding: 5px;
    color: white;
  }
  .name h2 {
    margin: 0;
  }
  .occupation h6 {
    margin: 0;
  }
  .view a {
    color: black;
  }
  .delete a {
    color: red;
  }
</style>