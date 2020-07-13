# AlStarApp-Project-Plan

# EXAMPLE GROUP PROJECT README

# TUNIN

## Table of Contents
1. [Overview](#Overview)
1. [Product Spec](#Product-Spec)
1. [Wireframes](#Wireframes)
1. [Schema](#Schema)

## Overview
### Description
Help users find and write reviews of products they have already or trying to purchase. Could be potentially used as a social platform where people talk, connect with each other concerning the product they have purchased and how was the experience like to them.Also it can be a way of connecting the users to the online shop with the best products.

### App Evaluation
- **Category:** Market/ Social Networking
- **Mobile:** This app would be primarily developed for mobile but would perhaps be just as viable on a computer, such as tinder or other similar apps. Functionality wouldn't be limited to mobile devices, however mobile version could potentially have more features.
- **Story:** Allows users to look and write reviews basing on other people's experiences with the particular procucts.
- **Market:** Any individual could choose to use this app, and to keep it a safe environment, people would be organized into age groups.
- **Habit:** This app could be used as often, anytime wants to shop, before buying or shopping for anything, helping them find a product and whether it is worth the run for their money.
- **Scope:** First we would start with having users write reviews and storing them in database where others could find them and use them as referrence while shopping, then perhaps this could evolve into a social and application as well to broaden its usage. Large potential for use with amazon and other online shopping platforms, Facebook, or other social applications.

## Product Spec
### 1. User Stories (Required and Optional)

**Required Must-have Stories**
* User is able to login if they are signed up but taken back to sign up if not
* User logs in and navigated to the welcome/home screen
* User picks whether they want to write or find reviews of specific items
* User is able to be navigates smoothly from one screen to the other and write a review succesfully.
* User is able to search for review of an item they are looking for with ease,depending on which category the item they are looking for falls under
* User is able to find the reviews of an item if it exists on the database.

**Optional Nice-to-have Stories**

* Connect the user to the store with goods with high reviews.
* Connect the user to the people who wrote reviews
* Profile Add-On: Shows the profile of the users, the reviews they have written and messages from people wanting to know more about the item
* Notification button with  notification of messages,best sell deals and so on


### 2. Screen Archetypes

* Login 
* Register - User signs up or logs into their account
   * Upon Download/Reopening of the application, the user is prompted to log in to gain access to their profile information to be properly matched with another person. 
   * ...
* Home Screen - The users is asked whether he wants to find or write review for a particular item
   * With a welcome message the user he asked whether he wants to add or find a review
* Selection Screen for users writing the reviews.
   * If the user is into giving reviews for a given app, this screen allow them to enter the logistics of the item so it is easier to be found by the other user    who will be looking for this particular reviews. The logistics category include:
          *Enter the product type
          *Enter the name of the brand
          *Enter the mode of purchase and cost
          *Enter the store 
* Selection Screen for users looking for reviews.
   * Allows users to search for reviews and to make it easier, the user is given option which include:
        *Search by location
        *Reviews
        *Product type   
* Search By Location Screen 
   *Asks the user to allow the app access their location
*Search By Reviews Screen
  *Asks users whether or higly reviewed items or
* Search By Prodcut Type/Name Scree
   *Allows users to check out reviews for different items by their product name or type directly
* Rating Screen
  *Allows users to take the pictures and rate the product out of 10
* Customer Experience and Anyother Thing the user wants to write about the product
  *Allows the user to write about the customer experience and any other good or bad thing while purchasing and consuming 
* Review preview and Submission Screen
* Search result screen
### 3. Navigation

**Tab Navigation** (Tab to Screen)

* Action selection
* Review submission
* Review search
* Search results

Optional:
* Messages to other users
* Link to the shopping platforms

**Flow Navigation** (Screen to Screen)
* Forced Log-in -> Account creation if no log in is available
* Action Selection (Or Queue if Optional) -> Jumps to Either writing or giving reviews
* Review Conclusion -> Review Submission. 
* Search By Specific Category -> Search Results

## Wireframes
<img src=https://imgur.com/6bhZc8Y.gif

### [BONUS] Digital Wireframes & Mockups
<img src=https://www.figma.com/file/AXV7VKFZXF6nE6u2men6wY/Untitled?node-id=0%3A1

### [BONUS] Interactive Prototype
<img src=https://www.figma.com/proto/AXV7VKFZXF6nE6u2men6wY/Untitled?node-id=2%3A0&scaling=scale-down
## Schema 
### Models
#### Post

   | Property      | Type     | Description |
   | ------------- | -------- | ------------|
   | objectId      | String   | unique id for the user post (default field) |
   | author        | Pointer to User| image author |
   | image         | File     | image that user posts |
   | caption       | String   | image caption by author |
   | commentsCount | Number   | number of comments that has been posted to an image |
   | likesCount    | Number   | number of likes for the post |
   | createdAt     | DateTime | date when post is created (default field) |
   | updatedAt     | DateTime | date when post is last updated (default field) |
### Networking
#### List of network requests by screen
   - Home Feed Screen
      - (Read/GET) Query all posts where user is author
         ```swift
         let query = PFQuery(className:"Post")
         query.whereKey("author", equalTo: currentUser)
         query.order(byDescending: "createdAt")
         query.findObjectsInBackground { (posts: [PFObject]?, error: Error?) in
            if let error = error { 
               print(error.localizedDescription)
            } else if let posts = posts {
               print("Successfully retrieved \(posts.count) posts.")
           // TODO: Do something with posts...
            }
         }
         ```
      - (Create/POST) Create a new like on a post
      - (Delete) Delete existing like
      - (Create/POST) Create a new comment on a post
      - (Delete) Delete existing comment
   - Create Post Screen
      - (Create/POST) Create a new post object
   - Profile Screen
      - (Read/GET) Query logged in user object
      - (Update/PUT) Update user profile image
#### [OPTIONAL:] Existing API Endpoints
##### An API Of Ice And Fire
- Base URL - [http://www.anapioficeandfire.com/api](http://www.anapioficeandfire.com/api)

   HTTP Verb | Endpoint | Description
   ----------|----------|------------
    `GET`    | /characters | get all characters
    `GET`    | /characters/?name=name | return specific character by name
    `GET`    | /houses   | get all houses
    `GET`    | /houses/?name=name | return specific house by name

##### Game of Thrones API
- Base URL - [https://api.got.show/api](https://api.got.show/api)

   HTTP Verb | Endpoint | Description
   ----------|----------|------------
    `GET`    | /cities | gets all cities
    `GET`    | /cities/byId/:id | gets specific city by :id
    `GET`    | /continents | gets all continents
    `GET`    | /continents/byId/:id | gets specific continent by :id
    `GET`    | /regions | gets all regions
    `GET`    | /regions/byId/:id | gets specific region by :id
    `GET`    | /characters/paths/:name | gets a character's path with a given name
