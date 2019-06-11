---
layout: post
title:      " "Building my CLI Data Gem""
date:       2019-06-11 02:54:42 +0000
permalink:  building_my_cli_data_gem
---


Starting to build this CLI was a bit intimidating. Completing labs is a bit like working through a worksheet, the answers aren't there but the framework is. This project was like a blank sheet of paper. It really took all my resources and knowledge to work through it. 

I decided that my Gem should allow a user to input a dog breed and receive detailed information about that dog breed. I scraped from the American Kennel Club website, and I think getting the scrape just right was probably the most difficult part. 

The first challenge I encountered was that the AKC website page that lists all the breeds is separated out with a "load more" link. Clicking the link loads more dog breeds to the same page, BUT it changes the url to the next page. There was no option to load all the breeds on a single page, so I needed to find a way to set my base Nokogiri doc as ALL the breed pages, without typing out all 23 pages. 

![](https://drive.google.com/open?id=1qB3MnmOSL6aOosjkKF8Zb02izcOp88GG)

Googling how to scrape from multiple pages at once didn't help me much, unlike in other areas of this project. All the solutions I could find suggested a gem called "Mechanize" that I've never dealt with and was having trouble understanding.


```
  def scrape_breeds
    breeds = []

    page_numbers = (1..23).to_a
    page_numbers.each do |page_number|

       doc = Nokogiri::HTML(open("https://www.akc.org/dog-breeds/page/#{page_number}"))
       dog_breeds = doc.css('div.breed-type-card')
       dog_breeds.each do |dog_breed|
         breeds << dog_breed
    end
  end
    breeds
end
```

My solution seem obvious to me now, looking back, but it took some trial and error to get it right. I just defined an array of my page numbers then iterated through them and interpolated each one into my open-uri link, and it worked!

I also had trouble scraping some of my info. The detailed info that I wanted for each breed was found inside a table with clickable tabs. 

![](https://drive.google.com/open?id=1O9yLDHV9K5kbon3qKItBaEujrGCoX7XS)

Not every dog breed had every trait, so I couldn't specify the css selector by index, and the info blurbs were in no way connected with their headings, which were only defined in the clickable tabs. (For example, the blurb about a specific breed's nutrition needs was in no way connected to the tab the said "Nutrition.") 

What I had was a series of info blurbs, in no certain order on any given page, and what I wanted were neatly defined categories that I could attach cleanly to an instance of my DogBreed class, and output appropriately in my CLI. 

new_info = doc.css('div.tabs__tab-panel-content p').each do |info|
                new_details = info.text.strip
                new_info_array << new_details

                new_info_array.each do |new_traits|

                  if new_traits.include?("dog food")
                    breed_info[:nutrition] = new_traits
                  elsif new_traits.include?("coat")
                    breed_info[:grooming] = new_traits
                  elsif new_traits.include?("exercise")
                    breed_info[:exercise] = new_traits
                  elsif new_traits.include?("train")
                    breed_info[:training] = new_traits
                  elsif new_traits.include?("health")
                    breed_info[:health] = new_traits

I ended up iterating through all the p tags under the appropriate div class, and pushing them into a hash as the value for each heading as the key if they contained specific words that ensured they belonged under that heading.

It seems messy and it's not always 100 % accurate, though I got it as close as I possibly could.

I'm eager to receive feedback in my project review, and I'm hoping to hear that there's a more efficient way to do this. 

I had so many ideas for this project that I couldn't quite get to in a week's time. I would like for the user to be able to request specific information about the dog breed, rather than getting a page of all the information at once. (Essentially I would have liked to have gone one level deeper.) My dream for this project at the start was for the user to be able to define traits they wanted in a pet (i.e. low exercise or easy to groom) and receive a list of breeds that fit their criteria. 

I didn't quite get there yet, but I think I'll be coming back to this project and tweaking it to make it better as I learn more. Still, I'm very happy with what it is already. It was nothing, a blank canvas, and now it's a fully functioning CLI that can tell you all about any dog breed you desire.
