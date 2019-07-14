---
layout: post
title:      "My Sinatra Portfolio Project"
date:       2019-07-14 22:10:56 +0000
permalink:  my_sinatra_portfolio_project
---

I have really enjoyed working with sinatra so far. This project was really fun for me. I enjoy being able to see the fruits of my labor in real time as easily as refreshing the page. 

For this project, I decided I wanted users to be able to keep track of Iron Man comics they want to read, and be able to update their list once they had read them. I also wanted them to be able to create new comics, and delete those comics but only if they had created them. 

Determining what models I would need, what their associations would be, and what their data tables would look like was a fun challenge. I ended up sketching out the relationships. 

![](https://drive.google.com/open?id=1HgOLVRMlln7AdNkpNKMnqUCWkZhS74Au)

I knew I wanted users to have many comics, but, thinking about it, though it was my initial thought, it wasn't appropriate for comics to belong to one user. I wanted a universal database of comics that any user could choose from. So comics would have many different users. That's one join table, comic_users. 

Then I had to determine what attributes each comic would have. I settled on a Title, Author(s), Illustrator(s), Release Date, and Volume #. 

I wanted users to be able to view each comic individually, and also be able to view authors and illustrators, and see the comics associated with them. 

Because any given comic book could have many authors and/or illustrators, and because I wanted users to be able to see all comics by a given author or illustrator, that meant two more many-to-many associations, and two more join tables, comic_authors and comic_illustrators. 

Each join table has a belongs_to association with both it's corresponding parent models. 

After this it was fairly standard game-of-catch code, creating controller actions and views that covered all my routes.

I ran into trouble once again when I wanted to limit the users who could delete a comic from the universal list to only the user that had initially created that comic. In labs thus far, we had done something similar when users could delete their own posts. However, because I had a many-to-many relationship between comics and users, the original creator of the comic was not the only user with the comic_id attatched to them. Therefore, if I coded as I had in the past, specifying that only users who had the comic_id in their attributes could delete the comic, it would still allow more than the original poster to delete said comic.

I had to add separate column to my comic table, user_created, into which I could then associate the current_user upon the creation of a new comic object.

```
post '/comics/new' do
    @user = current_user
    @comic = Comic.create(params["comic"])
    if !params[:author][:name].empty? 
      @comic.authors << Author.create(params[:author])
    end

    if !params[:illustrator][:name].empty?
      @comic.illustrators << Illustrator.create(params[:illustrator])
    end
    @comic.update_attributes(:user_created => @user.id)
    flash[:message] = "Successfully created comic!"
    redirect "/profile"
  end

```

Then, when a delete form was posted, I only had to confirm that the current_user.id was equal to the comic.user_created.

```
 delete '/comics/:id' do
    if logged_in?
      @comic = Comic.find(params[:id])
        if @comic.user_created == current_user.id
        @comic.destroy
        flash[:message] = "Successfully updated comic."
        redirect '/comics'
        else
        flash[:error] = 'You can only delete comics that you created'
        redirect '/comics'
        end
    else
      redirect '/'
    end
  end

```

It seems simple now, but getting it to work was a fun challenge for me, and it felt great when it worked.

As I said, I really enjoyed this project. Setting up a functional app that I could follow as if I was a user from beginning to end, seeing it all come together, having fun with styling, it was great and I can't wait to do more.




