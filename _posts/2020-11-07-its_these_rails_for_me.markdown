---
layout: post
title:      "It's these Rails for me"
date:       2020-11-07 19:28:22 -0500
permalink:  its_these_rails_for_me
---


If you're thinking from the look of the title that I'm going to go on a mini rant, well.....you're not completely wrong. But not all rants are negative.

It was really these rails for me. Working on this Rails Project has further solidified my knowledge of the inner-workings of web applications; all the progress I was hoping for, finally came through. 

I kind of have a mild obsession with TO DO LIST applications and thought, I might as well learn how to make one since I use them alot and so I did. I started by mapping out my relationships(see below), with my Join Table being Lists.

![](https://firebasestorage.googleapis.com/v0/b/damioniru-web.appspot.com/o/Screenshot%202020-11-07%20at%2018.47.03.png?alt=media&token=2b67521c-f5e5-41b1-b7c6-e7ff3abeca20)

With this, I was able to successful build out my associations and use nested routes to get my app functioning. However, where it all started to go downhill was when I introduced OminAuth into the mix. This quickly became a 2 day stretch consisting of endless headaches, frustration, a mix of many overwhelming emotions to say the least as I couldn't just figure out what i was doing wrong. Keep in mind that I didn't use Devise, which made it a little more difficult as the instructions for set up were a little different from using OmniAuth coupled with devise.

I realized that when I was trying to login via google (the 3rd party provider i selected), my user wasn't being created. I received the **Error** - ```No route matches {:action=>"show", :controller=>"users"}, missing required keys: [:id]```

After hours of debugging and several minutes on a zoom call with a couple of members from my cohort **(ABSOLUTE LIFESAVERS**). My User model was requiring the presence of username parameter as well as email and because there was no where for omniauth to pull the username information from, my user wasnt being created. I refactored the code to only require the presence of email. 

It looked something like this:                                               refactored to this:
```validates :username, :email, presence: true              validates :email, presence: true         
```

This allowed my sessions#omniauth work, thus creating my user and successfully allowing 3rd party login to function properly.
``` def omniauth
          @user = User.from_omniauth(auth)
          @user.save
          session[:user_id] = @user.id
         redirect_to user_path(@user)
    end
```


In Hindisght, it really seems like an easy fix, but it took myself and 2 of my cohort members on a zoom call to figure this out. This is the importance of peer programming. You can't know it all and that's okay. Turns out 6 eyes are better than 2 and I'm glad they were able to spot what I couldn't. In the end we got it done and I will definitely be building out more apps with my current knowledge on Rails for further Solidify my knowledge and see what new challenges I come accross to help sharpen my growing skillset.






