# Week 4, Day 2 Discussion

Take 30 minutes and discuss the following with your table group. Try whiteboarding out different solutions and ideas!

1. Map the CRUD actions (create, read, update, delete) to their matching Sinatra routes and HTTP verbs. For example: In a blog app, displaying the content of one particular blog post corresponds to the "Read" CRUD action and the *show* RESTful route. The matching route would be an HTTP Get request to '/posts/:id' where the id is that particular post's id i.e. '/posts/6' . 
2. Build an HTML form to create a new blog post. Then, build a form to edit a post. What are the differences between the two? What routes do they send requests to? What type of requests should each form make?
3. Revisit your CRUD action-to-route map. What view files, if any, does each action/route correspond to? 
4. Write out the Active Record code to preform CRUD actions on a Post model. 
5. Let's think about the domain model for a To-Do list application. Let's say you have a List model and an Item model. 
  * What is the relationship between a list and an item?
  * A user needs to be able to visit your app, create a new list and then add items to that list. What route would bring the user to the the page to make a new list? What route would take them to the page to make a new item?
  * How and where would you write the code that associates a new item to its list?
<p class='util--hide'>View <a href='https://learn.co/lessons/week-4-day-2-discussion'>Week 4 Day 2 Discussion</a> on Learn.co and start learning to code for free.</p>
