<template>
  <div>
    <header class='landing'>
      <nav class='navbar navbar-expand-lg navbar-light bg-dark'>
        <router-link class='back' to='/tj'>
          <div class='logo'>
            <img class='logo-img' src='https://imgur.com/FIIcw2K.png' alt='Nooble Creative Logo Dark'>
          </div>
        </router-link>
        <button class='navbar-toggler navbar-dark' type='button' data-toggle='collapse' data-target='#navbarSupportedContent' aria-controls='navbarSupportedContent' aria-expanded='false' aria-label='Toggle navigation'>
    <i class='navbar-toggler-icon'></i>
  </button>
  
        <div class='collapse navbar-collapse' id='navbarSupportedContent'>
          <ul class='navbar-nav ml-auto'>
            <li class='nav-item'>
              <a class='nav-link'>
                <router-link v-bind:to='"/tj"'>Home</router-link>
              </a>
            </li>
            <li class='nav-item'>
              <a class='nav-link'>
                <router-link v-bind:to='"/tj-designers"'>Our Designers</router-link>
              </a>
            </li>
          </ul>
        </div>
      </nav>
    </header>
  
    <TjBio :userdata='userdata' />
    <TjProjectList :projectdata='projectdata' :userdata='userdata' />
  </div>
</template>

<script>
  import TjProjectList from './TjProjectList';
  import TjBio from './TjBio';
  
  export default {
    name: 'TjProjects',
    data: function() {
      return {
        projectdata: {},
        userdata: {},
        userId: ''
      };
    },
    components: {
      TjProjectList,
      TjBio
    },
    created: function() {
      this.getProjectData();
      this.getUserData();
    },
    methods: {
      getProjectData() {
        if (this.$route.params.userId) {
          this.userId = this.$route.params.userId;
          this.$http
            .get(
              'https://behance-mock-api.glitch.me/api/users/' +
              this.userId +
              '/projects'
            )
            .then(function(data) {
              this.projectdata = data.body;
            });
        }
      },
      getUserData() {
        if (this.$route.params.userId) {
          this.userId = this.$route.params.userId;
          this.$http
            .get(
              'https://behance-mock-api.glitch.me/api/users/' +
              this.userId
            )
            .then(function(data) {
              this.userdata = data.body;
            });
        }
      },
  
    }
  };
</script>

<style scoped>
  @import url('https://fonts.googleapis.com/css?family=Merriweather|Montserrat:300,300i,400,600');
  a {
    font-family: 'Montserrat', sans-serif;
    font-weight: 300;
    color: #fff;
  }
  
  .container {
    margin-top: 70px;
  }
  
  .img-border img {
    border-radius: 10px;
  }
  
  .landing {
    background-image: url('../../../assets/tj_img/tossware_behance.jpg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
    height: 25vh;
  }
  
  .logo-img {
    height: 50px;
  }
  
  .navbar {
    background-color: transparent !important;
    color: #ffffff;
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    z-index: 2;
  }
</style>