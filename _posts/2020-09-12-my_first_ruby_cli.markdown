---
layout: post
title:      "My First Ruby CLI"
date:       2020-09-12 00:15:29 -0400
permalink:  my_first_ruby_cli
---


Where do I start...?

It most definitely wasn't and hasn't been an easy week but I must say that all my brain-pain was totally worth it.
I never knew till building this CLI that it was possible to feel your brain hurt 😂 .

It took me 3 start-overs but in the end I got there. Initially I wanted to create something themed around food but, what I love as much as food is gaming and so on my 3rd try I decided to go with that. Behold - **Ultra Gamer**


The first website that came to my head was Playstation, and as i went through the site, i found a page of deals and thought, who wouldn't love a great game deal(PS4 Lovers). So I decided to create a CLI to scrape the PlayStation website to collect some information. I found that they had:

1. 5 Deal Categories 

2. Upon selecting a category, the category page displays games along with their pricing info, game type and console type.

**My Ruby Gem provides:**

1 . A CLI with an interface that users can interact with,

2. Scrape data from PlayStation's Website,

3. Provides two levels of data! First, the CLI displays 5 Deal Categories. User will select a category and the top 30 games will be shown (second level) alongside their pricing information, game type and console type.

4. The Ruby Gem is a game themed application.

5. Following the Single Responsibility Principle (SRP), I split my code up to four files:

**cli.rb** : code handling CLI display logic and user input
**deal_category.rb** : code scraping first level of data, displaying 5 deal categories for user selection
**game_list.rb** : code scraping second level of data, displaying 30 games/theme deals for user viewing

**You can view my [repo code here](https://github.com/Bri8102/cli-project-ultragamer-briana) ! **





```def select_deal(deal_arr)
            input = nil

            while true
                input = Readline.readline("Select Deal or type exit:", true).strip

                goodbye if input.downcase === "exit"
                input = input.to_i

               
                if input > 0 && input < 6
                    puts "--------------------------------------------".black.on_white
                    deal_name = deal_arr[input-1].name.strip
                    puts "Here are the games on sale for #{deal_name.upcase}\n".blue.bold
                    list_games(deal_name)
                else
                    puts "That selection is not valid. Please select a Game Deal from 1 - 5, or type exit."
                end
            end

        end

        def list_games(deal_name)
            # binding.pry
            # puts "Please select a game from 1 - 30".blue.bold
            game_arr = UltraGamer::Game_deals.list_games(deal_name)
 
            puts game_arr.map.with_index {|g, index|
            "\t#{index+1}. #{g.name}: #{g.price} | #{g.console} | #{g.type} \n"}
            # "\t#{index+1}. #{g.name}"}
            puts "--------------------------------------------".black.on_white
            # select_game(game_arr)
        end```

As you can see above, there’s a lot of commenting out! Don't be afraid to make mistakes and challenge yourself. You don't understand something, ASK ! That's one thing I've always struggled with, asking for help. With this choice I had no option but to learn to depend on my cohort lead and my cohort and I must say - smartest decision ever. They helped me understand Object Relationships better and also taught me to re-think my approach to problem-solving.
I have definitely beefed up my knowledge on arguments and object relationships, all the endless googling was all for a great cause.

This project definitely had it's challenges, but overcoming each stage was like winning a medal. I had to remind myself to take breaks and walk away. Walking away definitely helped, most times I would come back having a clearer idea of what it is I was trying to make my code do. The answers are really at your fingertips and it's usually the smallest error!

Can't to see what lies ahead... i'm very excited and terrified 😂.

