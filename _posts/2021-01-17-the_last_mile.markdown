---
layout: post
title:      "THE LAST MILE"
date:       2021-01-17 21:55:35 +0000
permalink:  the_last_mile
---


A breath of fresh air, to be writing what shall be my final blog about my final project with FlatIron School, but really the first of many more blogs to come once i step out into the big world of Software Engineers and claim my place.

This bootcamp is honestly one of the best decisions i have made. It has completely changed the way i handle problem solving, both in thought and execution. I am a different person from when i started and i am so grateful to have been given this opportuniy.

Lets get into the technicalities.


## Bon Voyage

Ironically that is the title of my final project, which was created with a Rails API Backend and a React Frontend with Redux as the Middleware.

Personally, i found this project to be very challenging. I guess, that is why it was saved for last, a test of faith - well it worked because i almost gave up. My App was inspired by my travel habits and lack thereof for most of last year. Although i was able to visit some amazing countries... i was, well we were all stuck at home for most of the year.

So i decided to create an App that allowed me daydream about destinations i would like to visit as well as provide informaiton on countries i have visited, Anyone Can.

### Challenge

The most challenging part of this putting this project together was connecting my Rails API to my React frontend. 
My Assumption was that with my  ```gem rack-cors``` installed in my Rails App and my Fetch Request (see below) clearly stated in my ```src/actions/destinationActions.js``` folder, with a seeded database in Rails, i would be good to go.

```export const fetchDestinations = () => {
    return (dispatch) => {
      fetch('http://localhost:3000/destinations')
      .then(res => res.json())
      .then(destinations => dispatch({
        type: 'FETCH_DESTINATIONS',
        payload: destinations
      }))
    };
  };
	``` 
	
	In reality, i spent a good 4 hours, trying to understand why i was able to seed the data in Rails and See all my data in JSON format once my api was fired up and and i visited ```localhost:3000/destinations```. However, my fetch request was not grabbing any of the data.

Cue Redux DevTools and Chrome DevTools  - A LIFE SAVER! The whole time there was an error i had overlooked (see below)
```
Access to fetch at 'http://localhost:3000' from origin 'http://localhost:3001' has been blocked by CORS policy: Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource. If an opaque response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disabled.
```

### The Fix

After hours of reading numerous stack overflow answers for this error above; although very helpful.. none of them seemed to help solve this error - and ofcourse - frustration kicked in, coupled with the thought of giving up at the very last lap of what has a been a long journey.

After a couple of walks, I decided to give it one last try and Go through all individual files for my rails app. I found that in 'config/initializers/cors.rb' i had failed to add a wildcard for **Origin** such as below:

```
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins '*'

    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end
```

I restarted my server after adding my wildcard, and everything came together and my app was fully functioning, and this definitely topped the excitemenet of passing my very first review. I dont have much advice to give, but to Take regular walks, Pay attention to detail, and dont forget, It's literally the little things that can make or break (literally) your app.

**Thanks for coming to my TedxTalk.**




