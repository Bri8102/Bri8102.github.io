---
layout: post
title:      "JavaScript On The Rocks"
date:       2021-01-26 22:20:42 +0000
permalink:  javascript_on_the_rocks
---


These past couple of weeks has made me want to have a nice glass of whisky after each lesson to cool off from the information overload! it has been quite a journey, but still one i'm not ready to give up on yet.

For my Rails API JavaScript project, I created a Single Page Application(SPA). 

I used HTML, CSS, and JavaScript to build out the Frontend(view) of my application, and Ruby on Rails to build out the Backend a.k.a API. My Frontend(client) and API(server) were able to communicate thanks async JS, using JSON as a means of communication.

I built a Recipe Application where users can submit recipes of their favorite or speciality meals and drinks aswell as search for meal or cocktail(or mocktail) recipe ideas based on different ingredients. Once the new recipe form is filled out with the neccessary information, all attributes are saved to the API and displayed on DOM to the user. They will be able to see the name of the recipe, the ingredients listed out as well as a link to direct them to the website for further instructions. There is also an option to search for recipes by ingredients listed in a drop down list (collected from API through a fetch request).

I think Styling wise, this might be the nicest looking app I have created, thanks to google, other recipe sites and youtube for all the CSS styling tricks. 

One thing I found particularly confusing, was the use of 'event' in ```event.target.parentElement``` . This was the most important part of my code which i had to fix to get my code displaying all recipes aswell as recipes searched for by ingredients on the DOM.

I watched endless Youtube videos, sent my cousin a text for help and Read numerous documentation on how to use ```event.target``` as I initially thought i was using it wrongly. I found that the 'event' keyword was deprecated and this didnt mean it wouldnt work in code, but for some reason it just wasnt working for me. I ended up having to change my from **A** to **B** (see below)

**A** - *Error: Uncaught Type: Target undefined, Event undefined*
```
addRecipe(event) {
      debugger
        const form = event.target.parentElement
        console.log(form)
        const ingredients = form[3].value.split(', ')
        const recipe = new Recipe(form[0].value, form[1].value, form[2].value, ingredients)
        const configurationObject = {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
              "Accept": "application/json"
            },
            body: JSON.stringify({
              "title": form[0].value,
              "image_url": form[1].value,
              "recipe_url": form[2].value,
              "ingredients": ingredients
           })
        };
				....
			```
			
			**B** - I had to directly call formSubmit which was defined in my constructor as 
			```document.getElementById("form-submit");``` in order to access the form button that was bound to a click event somewhere else in my code.
			
			```
			addRecipe() {
      debugger
        const form = this.formSubmit.parentElement;
        debugger
        console.log(form)
        const ingredients = form[3].value.split(', ')
        const recipe = new Recipe(form[0].value, form[1].value, form[2].value, ingredients)
        const configurationObject = {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
              "Accept": "application/json"
            },
            body: JSON.stringify({
              "title": form[0].value,
              "image_url": form[1].value,
              "recipe_url": form[2].value,
              "ingredients": ingredients
           })
        };
           ....
			```
			
			I found that my Search by Ingredients function has the same issue and gave the same error. I ended up changing the code for that function to something similar to my addRecipe() function. With this change, I was able to populate my drop downlist, and upone clicking an ingredient, it displayed a recipe containing that ingredient to the DOM.
			
			```const ingredient = event.target.value``` **TO** ```const ingredient = this.ingredientDropDown.value```


I am glad that even though i know the 'event' keyword should have work had it been passed in as an arg (tried and didnt work), I was able to find an alternative way to implement the same actions. That is what coding is all about, finding new and improved ways to do things. Keyword for this project was Perserverance. However, I am glad to be done.

Perhaps it's time for that glass of Whisky now 😂



