<template>
  <v-container class="search--container">
      <!-- SEARCH BAR FILTER INPUT -->
      <!-- *---------------------------* -->

      <h1>wizard-search-app <img style="height: 40px" src="images/lightning.svg"></h1>
      <v-form @submit.prevent="submitSearch">
       <small> * search bar filters in lowercase </small>
        <v-text-field
          label="Search"
          single-line
          solo
          clearable
          type="text" 
          v-model="searchInput"
        ></v-text-field>
      </v-form>

      <!-- *--------------------------------------------------------* -->
      <!-- this button will show and hide additional API information  -->

      <v-btn @click="showText = !showText" color="orange" elevation="2">click for more info  <v-icon small>mdi-cursor-default-click-outline</v-icon></v-btn>
      
      <!-- RESULTS PAGE DISPLAYED BELOW  -->
      <!-- *---------------------------* -->
      <!-- Loading spinner -->
        <v-progress-circular
          v-if="isLoading"
          indeterminate
          class="mt-5"
        ></v-progress-circular>
        
      <div v-for="result in filteredResults" :key="result.id" class="single-result">
        <v-card elevation="2">
          <v-card-title>{{ result.name }} </v-card-title>
          <v-divider class="mx-4"></v-divider>
          
          <v-card-text>
            <div class="textbox" v-if="showText">
              <!-- RESULTS TABLE -->
              <!-- *-----------* -->
              <table>
                <v-chip-group
                  v-model="selection"
                  active-class="deep-purple accent-4 white--text"
                  column 
                >   
                  <thead>
                    <tr>
                      <th>
                        <v-chip color="white" label>Gender</v-chip>
                      </th>
                    </tr>
                    <tr>
                      <th>
                        <v-chip color="white" label>House</v-chip>
                      </th>
                    </tr>
                    <tr>
                      <th>
                        <v-chip color="white" label>Petronas</v-chip>
                      </th>
                    </tr>
                    <tr>
                      <th>
                        <v-chip color="white" label>Species</v-chip>
                      </th>
                    </tr>
                    <tr>
                      <th>
                        <v-chip color="white" label>Ancestry</v-chip>
                      </th>
                    </tr>
                    <tr>
                      <th>
                        <v-chip color="white" label>Alive</v-chip>
                      </th>
                    </tr>
                    <tr>
                      <th>
                        <v-chip color="white" label>Birth Year</v-chip>
                      </th>
                    </tr>
                  </thead>
                  <!-- TABLE BODY -->
                  <!-- *--------* -->
                  <tbody>
                    <tr>
                      <td>
                        <v-chip color="indigo" label outlined>
                          <v-icon small>mdi-human-male-female</v-icon>{{ result.gender }}
                        </v-chip>
                      </td>
                    </tr>
                    <tr>
                      <td>
                        <v-chip color="indigo" label outlined>
                          <v-icon small>mdi-home</v-icon>{{ result.house }}
                        </v-chip>
                      </td>
                    </tr>
                    <tr>
                      <td>
                        <v-chip color="indigo" label outlined>
                          <v-icon small>mdi-horse</v-icon>{{ result.patronus }}
                        </v-chip>
                      </td>
                    </tr>
                    <tr>
                      <td>
                        <v-chip color="indigo" label outlined>
                          <v-icon small>mdi-dna</v-icon>{{ result.species }}
                        </v-chip>
                      </td>
                    </tr>
                    <tr>
                      <td>
                        <v-chip color="indigo" label outlined>
                          <v-icon small>mdi-family-tree</v-icon>{{ result.ancestry }}
                        </v-chip>
                      </td>
                    </tr>
                    <tr>
                      <td>
                        <v-chip color="indigo" small label outlined>
                          <v-icon small>mdi-auto-fix</v-icon>{{ result.alive }}
                        </v-chip>
                      </td>
                    </tr>
                    <tr>
                      <td>
                        <v-chip color="indigo" label outlined>
                          <v-icon small>mdi-cake-variant</v-icon>{{ result.yearOfBirth }}
                        </v-chip>
                      </td>
                    </tr>
                  </tbody>
                </v-chip-group>
              </table>
              <!-- END OF TABLE -->
              <!-- *----------* -->
            </div>
          </v-card-text>
        </v-card>
      </div>

      <!-- Navigation and exit button -- appear once additional information tables have been activated via @click="showText"      -->

      <!-- *-------------------* -->
      <div v-if="showText">
         <back-to-top visibleoffset="300">
            <v-btn class="fixed--button--scroll--top" fab dark color="orange" elevation="2">
              <v-icon dark>mdi-arrow-up-thick</v-icon>
            </v-btn>
          </back-to-top>

          <v-btn @click="showText = !showText" class="fixed--button" fab dark color="indigo" elevation="2">
            <v-icon dark>mdi-close</v-icon>
          </v-btn>
      </div>
      <!-- *-------------------* -->
    
  </v-container>
</template>

<script>

const CHARACTERS_API_ENDPOINT = 'http://hp-api.herokuapp.com/api/characters/'

  export default {
    name: 'SearchBarInput',
    data() {
      return {
        results: [],
        searchInput: '',
        showText: false,
        isLoading: false
      }
    },
    methods: {
      /**
     * When the user submits their search request (hits enter) query the API endpoint
     */
    searchResponded(response) {
      this.isLoading = false;
        // EXERCISE - Implement logic to handle the API response.
        console.log(response); // eslint-disable-line no-console
      }

    },
    
    created() {
      this.$http.get(CHARACTERS_API_ENDPOINT).then(function(data){
        this.results = data.body.slice(0,20);
        // limits get results to 20 characters at a time ^
      })
      .catch(error => console.log(error))
    },

    computed: {
      filteredResults: function() {
        return this.results.filter((result) => {
          return result.name.toLowerCase().match(this.searchInput); 
        });
      }
    }
  }

</script>



<style lang="scss" scoped>
@import '../style/SearchBarInput.scss'
</style>
