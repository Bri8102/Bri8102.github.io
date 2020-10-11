---
layout: post
title:      "Fantasy Features with Sinatra"
date:       2020-10-10 21:41:15 -0400
permalink:  fantasy_features_with_sinatra
---


Even though it's just our second project, this has been my favorite. The processes are now automated in a sense and we don't have to do so much of the coding. However, I think learning the fundamentals was defintely neccessary to understand the brains behind the magic.

There are so many things we don't pay attention to until we do. Sinatra has been particularly interesting, especially the CRUD section which is all about the HTTP Requests. It's crazy because, how many times in our lives have we 'surfed the web'? SO MANY & not until now have I understood routes are the brains that direct you to the information you wish to see and in the back end there are HTTP verbs used as requests to give you the particular information you're asking for. Allowing you to perform certain tasks such as to **Deleting and Updating ** information within forms.


**My Project - Fantasy Feature World**

On starting this project, I wanted it to be centered around Music because it is something that I am passionate about. I have always wondered about collaborations of different artists and what it would sound like if it were actually to happen.  So I thought this would be a great opportunity to create a Web Application that allows users to create a list of some of the features they have been fantasizing about.

# PLAN
![](https://firebasestorage.googleapis.com/v0/b/damioniru-web.appspot.com/o/Screenshot%202020-10-10%20at%2021.08.36.png?alt=media&token=ed862c6a-8e44-42d7-bd77-79728b70ba8d)


# Models, Views and Controllers
**1. *MODELS*** a.k.a The Back-End


After creating my plan which you see above. I created my *Model *files, in order to create *Objects* that would serve as a "Real World Representation" of my *Users and the Features they would create, this also sets the scene for the database. After this I went on to create migrations for each user, creating two tables along with the data and data types they would be populated with(seen in picture above).

a. *User* - this class *has_many* :features

b. *Feature* - this class *belongs_to* :user

***2. VIEWS***  a.k.a The Front-End


This consists of codes that show your User what you want them to see, based on helper methods or not ! You can specify what you want the user to see and depict whether or not you would like for them to be logged in to view the information or if it is free for all. In this project, we focused on the ability of the user to *Sign up or Log In*  and stay logged in with the help of Session cookies which i enabled in my Application Controller (see below)

``` 
     configure do
         set :public_folder, 'public'
        set :views, 'app/views'
       enable :sessions
       set :session_secret, "featureworld"
    end
```

***3. CONTROLLERS***  a.k.a The Middle-Man


The real brains of the operation through the use of CRUD methods. These methods allow users to **Create**, **Read**, **Update** or **Delete**. 

This snippets of code below allows the implenation of the Create Function. When you access the '/features/new' route, It checks if the current_user is logged in and renders a form to create a Feature from the ERB file 'new', if they are. Otherwise, they will be redirected to the '/login' route and prompted to login. ERB stands for Embeded Ruby & allows us to Integrate Ruby and HTML to display information to a user.

```    
     get  '/features/new' do
        if logged_in?
        erb :"features/new"
        else  
            redirect to '/login'
        end
    end
```

Once the form is created, the information filled into the form is submit through a POST request which sends all the information from the form to * '/features'* route. It checks to see if the user is logged in and then checks to see if the song field has been left empty (if empty, redirects back to the form for user to fill out again). If the song field isn't empty, it checks to see if there is an existing song by that name and finds the user by their session id and the song parameter and redirects them to a page where they can view all the features they have created. Otherwise it allows them to create a new feature with the information they have entered into the fields of the form. if they are not logged in, it redirects them to the log in page and prompts them to log in.

```    
         post  '/features' do
        if logged_in?
            if params[:song] == ""
                redirect to "features/new"
            else
                if @feature = Feature.find_by(user_id: session[:user_id], song: params[:song])
                    redirect to "/features/#{@feature.id}"
                else
                 @feature = Feature.create(song: params[:song],artist1: params[:artist1], artist2: params[:artist2], user_id: session[:user_id])
								 
             if @feature.save
       
                redirect to "/features/#{@feature.id}"
             else
                redirect to "/features"
             end
            end
        end
       else
        redirect to '/login'
    end
```

The snippets below represents the part of my Web Application that I found specifically difficult until I was able to figure it out with the help of a peer from my cohort. I wanted my users to be able to see all the features they had created and that was specific to them . I found that I had to create an entirely new route for that to happen. I also wanted the user to have a DELETE & EDIT function for every feature they created; to do this i had to embed the delete & edit forms within a button to implement those actions. 

My GET request route uses *.where* class method to call all the Features where the user_id = params[:id] and maps through to create an array then select each feature to display on the page from the array; It then renders the *show.erb* which gives the user a list of all their features as well as a two button option to delete that specific post and an Edit button directing the user to the * '/features/:id/edit'* route which displays a form for the user to change information about their feature. 

I also included an option for the user to Create anoter feature. Once they click on this it directs them to the *'/features/new'* route and renders the form to create a new Feature.

```    
     get  '/features/user/:id' do
        @features = Feature.where("user_id=#{params[:id]}").map {|f| f}
        erb :'features/show'
    end
```

```
   <h5>Here are your features</h5>
   <% @features.each do |f| %>

  <div>
    <%= f.song %> - <%= f.artist1 %> ft. <%= f.artist2 %>
   <button type ="button"> <form method="POST" action="/features/<%=f.id%>/delete">
     <input type="hidden" id="hidden" name="_method" value="DELETE">
     <input type="submit" value="Delete Feature">
   </button>
   <button >
     <a href="/features/<%=f.id%>/edit"> Edit Feature</a>
   </button><br>

  </div>
 <% end %> 
```

Hopefully, with time I can work to develop this Web Application and make it look better and add more functionality for the user as well as make my code neater. I have most definitely enjoyed learning Sinatra, it has been a lovely learning experience. I now appreciate how routes within Web Application work on a deeper level. 

Even with all the challenges I faced and the amount of times i broke my code , it was fun to be able to work through all of them and figure out exactly what code was needed to carry out certain actions and display very specific information. I am looking forward to learning Rails.




