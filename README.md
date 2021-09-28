# echosec-coding-exercise-hayden-master

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).


### Additional Information

First thing you'll notice, I totally went off script with this exercise. My Vue inexperience really came through and I ran into some issues that I couldn't remedy, and I figured it would be better to just have a decent application than nothing at all. 

<!-- ** ----------------------------------------------------** -->

Second, this is not the API I was asked to use. 
At first I thought there was an issue with fetching the data, but the original API was actually quite empty.

It had a few names of characters, but not much else. So I figured I would just use one that actually had some data to spit out (I hope that's alright).

<!-- ** ----------------------------------------------------** -->

Third, I began with axios, but ran into some issues.
I have worked with axios in the past, and it's extremely easy to use.
However, I ran into some issues with it while trying to filter the get results.

<!-- ** ----------------------------------------------------** -->

ISSUES: 

@submit.prevent="submitSearch" is not working. 
All results are automatically displayed, and filtered on keystrokes. I wanted to at least get the search functionality working, and then will go back and fix the issue. 

As you can tell, I have moved some things around. It's the first time I've ever really worked on a pre-populated project, and the second VueJS project I've worked on, so for the sake of simplicity, I removed Results.vue, and moved the code into the SearchBarInput.vue document. I also couldn't get the data to filter when it was in a different component - I've dealt with this in React, but again, just inexperience with Vue. 

axios is obviously a great solution for retrieving API JSON data, 
but it gave me some issues upon reloading the data once it had been filtered .

<div v-for="result in filteredResults" :key="result.id">

I would loop through filteredResults, and display filter the data just fine. But upon refreshing, the original data: 

( this.list=response.data )

would not load manually, I would manually have to switch the v-for to loop through the original response data:

<div v-for="result in results" :key="result.id">

  submitSearch() {

       axios.get('https://www.anapioficeandfire.com/api/characters/')
        .then((response) => {
            this.list=response.data;
            console.log(response.data)
        })
        .catch(error => console.log(error))
        }
    },

    computed: {
      filteredResults: function() {
        return this.results.filter((result) => {
          return result.name.match(this.searchInput); 
        });
      }
    }

I attempted to write a function that would handle both the original API fetch first, and then filter through the results,
but I just couldn't get to seem to get it working and chome dev console kept yelling at me. 


<!-- **----------------------------------------------------------------** -->

Thank you for the exercise, I enjoyed it!
I welcome any critique's or advice :)