---
title: "Project Phase 3: Convergent Design"
layout: doc
---


# Project Phase 3: Convergent Design


## Functional Design


### Concept I:


__Name__: Posting [User]


__Purpose:__ Enable users to share content with other users on the app.  Allows users to publish items of interest in a structured and purposeful manner.


__Operational Principle:__ If a restaurant user posts a food donation `p` with expiration time `t` and quantity `q`, food_item `food`, and the posted food_item `food` becomes available for food-insecure users to request in the food listings feed until the expiration time `t` passes. After expiration time `t` passes, the post will be only visible for another day to users before it is no longer available to view.


__State:__


    posts: __set__ Post
    food_item: Post → __one__ String
    author: Post → __one__ User
    expiration_time: Post → __one__ Date
    quantity: Post → __one__ number


__Actions:__


    createPost(author: User, expiration_time: Date, food_item: String, quantity: number):
        posts += new Post(food_item, author, expiration_time, quantity)

    editPost(oldPost: Post, newPost: Post)
        ``` in editing a post, the relevant fields that are updated will be updated in the states as well```
        posts -= oldPost
        posts += newPost
    
    deletePost(p: Post):
        posts -= p

    getUserPosts(u: User):
        return post for post in posts if posts.author == u

    getAllPosts():
        return posts

    isPostExpired(p:Post):
        return p.expiration_time < now

    assertPostIsNotExpired(p: Post):
        if p.expiration_time > now:
            error

    assertAuthorIsUser(p: Post, u: User):
        if p.author != u:
            error


Side Note: In our application, we plan that users will claim an entire post for the purpose of achieving an MVP. That means if a restaurant has a single post that lists 3 pizzas, and a user claims that post, the user is putting a request for all those 3 pizzas.

### Concept II:

__Name__: Claiming [User, Item]

__Purpose:__ Users can reserve an item as their own.

__Operational Principle:__ User `user` can select an `item` for themself, after which other users cannot claim it unless the item is unclaimed. When a user claims an item, they can request for the item to be claimed via “Pickup” or “Delivery.” When an `item` is claimed, it means the user is requesting the item for themself; however, only when the claim is changed to `completed` does it mean that the user has successfully received the item.

__State:__


    claims: Item -> __one__ Claim
    status: Claim → __one__ “Requested”|”Completed”
    claim_user: Claim → __one__ User
    method: Claim -> __one__ “Pickup”| “Delivery”
    delivery_address: Claim → __one__ string (optional)

__Actions:__


    createPickupClaim(u: User, i: Item):
        if i not in claims:
            claims[i] = new Claim(claim_user: u, “Requested”, “Pickup”)
        else:
            error

    createDeliveryClaim(u: User, i: Item, delivery_address: String):
        if i not in claims:
            claims[i] = new Claim(claim_user: u, “Requested”, “Delivery”, delivery_address)
        else:
            error

    deleteClaim(i: Item):
        if i not in claims:
            error
        else:
            Return del claims[i]

    completeClaim(c: Claim):
        c.status = “Completed”

    getUserClaims(u: User):
        return [i for i in claims if claims[i].claim_user == u]

    getItemClaimer(i: Item):
        return claims[i]

    assertClaimerIsUser(u: User, claim: Claim):
        if claim.claim_user != u
            raise Error

    assertIsNotClaimed(i: Item):
        if claims[i] != None:
        Raise Error


    assertIsNotCompleted(c: Claim):
        if c.status == “completed”:
            Raise Error

    isItemClaimed(i: Item):
        return claims[i] != None

    assertIsPickup(c: Claim)
        if c.method != “Pickup”:
            Raise Error

    assertIsDelivery(c: Claim)
        if c.method != “Delivery”:
            Raise Error


### Concept III:


**Name**: Delivering [User, Request]


**Purpose:** A user can deliver a specific Item to a designated user by a certain time.


**Operational Principle:** User `deliverer` will deliver a specific food donation to a User `receiver` that is designated in a Request `delivery_request` by a designated time `t`. When a volunteer `deliverer` initially volunteers to complete a delivery, it will be marked as `not started` until they pick up the item from the restaurant, which its status will then become `in progress`. After the delivery is marked completed, the designated item `item` should have been `delivered` to the `receiver`.


**State:**

    deliveries: __set__ Delivery
    delivery_status: Delivery → __one__ “Not Started” |“In Progress”|”Completed”
    delivery_request: Delivery → __one__ Request
    time: Delivery → __one__ Date
    deliverer: Delivery → __one__ User

**Actions:**

    acceptDelivery(deliverer, receiver: User, delivered_item: item, time: Date):
        deliveries += new Delivery(deliverer, receiver, time, delivered_item, “Not Started”)

    unacceptDelivery(d: Delivery):
        if d in deliveries:
            del d
        else:
            error

    deleteDelivery(request: Request):
        del delivery for deliveries if delivery.delivery_request == request

    getAllUserDeliveries(u: User):
        return [i for i in deliveries if deliveries.deliverer == u]

    getActiveUserDeliveries(u: User):
        return [i for i in deliveries if deliveries.deliverer == u and i.status != “Completed”]

    getCompletedUserDeliveries(u: User):
        return [i for i in deliveries if deliveries.deliverer == u and i.status != “Completed”]

    getItemDeliverer(i: Item):
        return delivery where delivery.delivered_item == i

    startDelivery(d: Delivery):
        d.status = “In Progress”

    completeDelivery(d: Delivery):
        d.status = “Completed”

    assertDelivererIsUser(u: User, d: Delivery):
        if d.deliverer != u:
            raise Error

    getDeliveryRequest(d:Delivery):
        return d.delivered_request

    assertIsNotDelivered(d: Delivery)
        if d.delivery_status == “Completed”:
            raise Error

    assertDeliveryHasNotStarted(d: Delivery)
        if d.delivery_status != “Not Started”:
            raise Error

    assertDeliveryIsInProgress(d: Delivery)
        if d.delivery_status != “In Progress”
            raise Error


### Concept IV:


**Name:** Messaging [User]


**Purpose:** Allows messaging between respective Users.


**Operational Principle:** User `sender` can deliver a message with content `content` to User `receiver` to get information regarding food donations.


**State:**

    sender: Message → __one__ User
    recipient: Message → __one__ User
    time: Message → __one__ Date
    content: Message → __one__ String
    messages: __set__ Message

**Actions:**

    sendMessage(sender: User, recipient: User, time: Date, content: String):
        messages += new Message(sender, recipient, time, content)

    getMessagesBetween(u1: User, u2: User):
        return message for message in messages if (message.sender == u1 and
        message.receiver == u2) or (message.sender == u2 and message.receiver == u1)

    getUserConversations(u: User):
        ```
        got all messages that user u was involved with, returned set of other users from those messages
        ```
        conversationUsers = empty set

        for (sender, recipient), messageSet in messages:
            if sender == u:
                conversationUsers.add(recipient)
            else if recipient == u:
                conversationUsers.add(sender)

        return conversationUsers


### Concept V:

**Name:** Tagging [Item]

**Purpose:** Allows tags to be added to an Item to designate/provide information about that item.

**Operational Principle:** Once an Item `i` is created, string `t` (a tag) can be added to aid in further filtering or categorizing the food donation Item `i`.


**State:**

    tags: one Item -> **set** Tags
    tag_content: Tag -> **one** string


**Actions:**

    addTag(t: string, i: Item):
        if (t not in tags[i]):
            tags[i] += t
            tags[i].push(t)
        else:
            error

    delTag(t: Tag):
        if t in tags:
            del tag

    deleteItem(i: Item)
        del tags[i]


### Concept VI:


**Name**: Session-ing \[Action\]


**Purpose**: enable authenticated actions for a period


**Operational Principle**:


after a session starts (and before it ends),
the getUser action returns the user identified at the start:
start(u,s); getUser(s, u') \{u'=u\}


**State**:

    active: __set__ Session
    user: active -> one User


**Actions**:

    start(user: User, __out__ sess: Session)
        active += user

    getUser(sess: Session, __out__ user: User)
        user in active if Session.user == user

    userIsActive(sess: Session, user: User)
        user in active

    end(sess: Session)
        active -= user


### Concept VII:


**Name**: Authenticating

**Purpose**: authenticate users so that app users correspond to people

**Operational Principle**:

after a user u registers with a username u and a password p and
a verification code v, they can authenticate by providing the unique pair
(u, p). Upon registration, a user will register as a single `role` of either `Volunteer`|`Donor`|`Recipient`. If a user is a `Donor`, they must also list a location.

**State**:

    registered: __set__ User
    username, password: registered -> __one__ String
    role: User -> __one__ Role “Donor” | “Recipient” | “Volunteer”
    location: User -> __one__ String (optional)


**Actions**:

    registerRecipient(name, pass: String)
       registered += new User(name, pass, “Recipient”)

    registerDonor(name, pass, location: String)
       Registered += new User(name, pass, “Donor”, location)

    registerVolunteer(name, pass: String)
       registered += new User(name, pass, “Volunteer”)

    unregister(user: User)
       registered -= (user.name, user.password)
       active_users -= user

    authenticate(name, pass: String, __out__ user: User)
       (name, pass) in registered

    getUserRole(user: User):
        return user.role

    getUserLocation(user: User):
        return user.location

    assertIsVolunteer(user: User):
        if user.role != “Volunteer”:
            raise Error

    assertIsDonor(user: User):
        if user.role != “Donor”:
            raise Error

    assertIsRecipient(user: User):
        if user.role != “Recipient”:
            raise Error


### Subsets


\{Authenticating\}


\{Authenticating, Sessioning\}


\{Authenticating, Sessioning, Posting\}


\{Authenticating, Sessioning, Posting, Claiming\}


\{Authenticating, Sessioning, Posting, Claiming, Delivering\}


\{Authenticating, Sessioning, Messaging\}


\{Authenticating, Sessioning, Posting, Messaging\}


\{Authenticating, Sessioning, Posting, Claiming, Messaging\}


\{Authenticating, Sessioning, Posting, Claiming, Delivering, Messaging\}


\{Authenticating, Sessioning, Posting, Tagging\}


\{Authenticating, Sessioning, Posting, Tagging, Claiming\}


\{Authenticating, Sessioning, Posting, Claiming, Delivering, Tagging\}


\{Authenticating, Sessioning, Posting, Tagging, Messaging\}


\{Authenticating, Sessioning, Posting, Claiming, Tagging, Messaging\}


\{Authenticating, Sessioning, Posting,Claiming, Delivering, Tagging, Messaging\}


### Functional Design: Dependency Diagram
![dependency diagram](/assets/images/leftover_love_dependency_diagram.png)


### App-level Synchronizations


```
concept LeftoverLove
   include Authenticating,
   include Sessioning[Authenticating.User],
   include Posting[Sessioning.User],
   include Claiming[Sessioning.User],
   include Delivering[Sessioning.User, Claiming.Claim],
   include Messaging[Sessioning.User],
   include Tagging[Posting.Post]
```


```
__sync__ registerRecipient(username, password, __out__ user: User)
    Authenticating.registerRecipient(username, password)
```


```
__sync__ registerDonor(username, password, role, location: String, __out__ user: User)
    Authenticating.registerDonor(username, password, location)
```


```
__sync__ registerVolunteer(username, password, __out__ user: User)
    Authenticating.registerVolunteer(username, password)
```


```
__sync__ login(username, password: String, __out__ user: User, __out__ session: Session)
    Authenticating.authenticate(username, password, user)
    Sessioning.start(user, session)
```


```
__sync__ logout(session: Session)
    Sessioning.end(session)
```


```
__sync__ authenticate(username, password: string, __out__ user: User, __out__ session: Session)
    Authenticating.authenticate(username, password, user)
    Session-ing.start(user, session)
```


```
__sync__ getAllPosts()
    Return post for posts in Posting.getAllPosts()
```


```
__sync__ getUserPosts(session: Session)
    user = Sessioning.getUser(session)
    return Posting.getUserPosts(user)
```


```
__sync__ getAllNonExpiredPosts()
    Return post for posts in Posting.getAllPosts if !isPostExpired(post)
```


```
__sync__ getAllNonExpiredNonClaimedPosts()
    Return post for posts in Posting.getAllPosts if !Posting.isPostExpired(post) && !Claiming.isItemClaimed(post)
```


```
__sync__ createPost(session: Session, p: Post, food_item: string, expiration_time: Date, t?: string[])
    user = Sessioning.getUser(session)
    Authenticating.assertIsDonor(user)
    Posting.createPost(user, expiration_time, food_item)
    for tag in t:
        Tagging.addTag(p, tag)
```


```
__sync__ editPost(session: Session, oldPost: Post, newPost: Post)
    user = Sessioning.getUser(session)
    Authenticating.assertIsDonor(user)
    Posting.assertAuthorIsUser(post, user)
    Posting.editPost(oldPost, newPost)
```


```
__sync__ deletePost(session: Session, p: Post)
    user = Sessioning.getUser(session)
    Authenticating.assertIsDonor(user)
    Posting.assertAuthorIsUser(post, user)
    Posting.deletePost(user, p)
    Tagging.deleteItem(p)
    deleted_claim = Claiming.deleteClaim(p)
    Delivering.deleteDelivery(deleted_claim)
```


```
__sync__ createPickupClaim(session: Session, post: Post)
    user = Sessioning.getUser(session)
    Authenticating.assertIsRecipient(user)
    Posting.assertPostIsNotExpired(post)
    Claiming.assertIsNotClaimed(post)
    Claiming.createPickupClaim(user, post)
```


```
__sync__ createDeliveryClaim(session: Session, post: Post, delivery_address: String)
    user = Sessioning.getUser(session)
    Authenticating.assertIsRecipient(user)
    Posting.assertPostIsNotExpired(post)
    Claiming.assertIsNotClaimed(post)
    Claiming.createDeliveryClaim(user, post, delivery_address)
```


```
__sync__ deleteClaim(session: Session, post: Post)
    user = Sessioning.getUser(session)
    Authenticating.assertIsRecipient(user)
    Claiming.assertClaimerIsUser(post, user)
    deleted_claim = Claiming.deleteClaim(post)
    Delivering.deleteDelivery(deleted_claim)
```


```
__sync__ getUserClaims(session: Session)
   user = Sessioning.getUser(session)
   Claiming.getUserClaims(user)
```


```
__sync__ getPostClaimer(session: Session, post: Post)
   Sessioning.getUser(session, user)
   Claiming.getItemClaimer(post)
```


```
__sync__ pickupClaim(session: Session; claim: Claim):
    Sessioning.getUser(session, user)
    Authenticating.assertIsRecipient(user)
    Claiming.assertClaimerIsUser(user, claim)
    Claiming.completeClaim(claim)
```


```
__sync__ acceptDelivery(session: Session, claim: Claim, time: Date)
    user = Sessioning.getUser(session)
    Authenticating.assertIsVolunteer(user)
    Claiming.assertIsNotCompleted(claim)
    Claiming.assertIsDelivery(claim)
    Delivering.acceptDelivery(deliverer: user,  time: Time,  delivery_request: claim)
```


```
__sync__ unacceptDelivery(session: Session, d: Delivery)
    user = Sessioning.getUser(session)
    Authenticating.assertIsVolunteer(user)
    Delivering.assertDelivererIsUser(user, d)
    Delivering.assertIsNotDelivered(d)
    Delivering.unacceptDelivery(d)
```


```
__sync__ getAllUserDeliveries(session: Session)
    user = Sessioning.getUser(session)
    Delivering.getAllUserDeliveries(user)
```


```
__sync__ getActiveUserDeliveries(session: Session)
    user = Sessioning.getUser(session)
    Delivering.getActiveUserDeliveries(user)
```


```
__sync__ getCompletedUserDeliveries(session: Session)
    user = Sessioning.getUser(session)
    Delivering.getCompletedUserDeliveries(user)
```


```
__sync__ getClaimDeliverer(claim: Claim)
    Delivering.getItemDeliverer(claim)
```


```
__sync__ startDelivery(session: Session, d: Delivery)
    user = Sessioning.getUser(session)
    Authenticating.assertIsVolunteer(user)
    Delivering.assertDelivererIsUser(user, d)
    Delivering.assertDeliveryHasNotStarted(d)
    Delivering.startDelivery(d)
```


```
__sync__ completeDelivery(session: Session, d: Delivery)
    user = Sessioning.getUser(session)
    Delivering.assertDelivererIsUser(user, d)
    Delivering.assertDeliveryIsInProgress(d)
    Delivering.completeDelivery(d)
    claim = Delivering.getDeliveryRequest(d)
    Claiming.assertIsDelivery(claim)
    Claiming.completeClaim(claim)
```

```
__sync__ sendMessage(session: Session, u2: User, message_content: String)
    const receiver = (await Authing.getUserByUsername(to))._id;
    const sender = Sessioning.getUser(session);
    Messaging.sendMessage(sender, receiver, new Date now(), message_content)
````


```
__sync__ getMessagesBetween(session: Session, u1: User, u2: User)
    Sessioning.getUser(session)
    Messaging.getMessagesBetween(u1, u2)
```


```
__sync__ getUserConversations(session: Session)
    user = Sessioning.getUser(session)
    Messaging.getUserConversations(user)
```


```
__sync__ getTags(p: Post)
   Posting.assertPostIsNotExpired(post)
   Tagging.getTags(p)
```


```
__sync__ addTag(session: Session, p: Post, t: string)
    user = Sessioning.getUser(session)
    Authenticating.assertIsDonor(user)
    Posting.assertAuthorIsUser(p, user)
    Posting.assertPostIsNotExpired(p)
    Tagging.addTag(p, t)
```


```
__sync__ deleteTag(session: Session, p: Post, t: string)
    user = Sessioning.getUser(session)
    Authenticating.assertIsDonor(user)
    Posting.assertAuthorIsUser(p, user)
    Posting.assertPostIsNotExpired(p)
    Tagging.deleteTag(p, t)
```


## Wireframes


Link to WireFrames: https://www.figma.com/design/4jja6UpmibCmcGxuCgmQk0/LeftoverLove?node-id=0-1&t=alOJNKqwPkQAMcDt-1


## Heuristic Evaluation


### Usability Criteria: Pleasantness
Going by the wireframes, the aesthetic of the website is extremely calming and pleasant to look at. Prospective food recipients need to feel like they are supported and loved, and the warmth of the interface does just that. However, there is a tradeoff between aesthetic and function. The initial menu where it calmingly says “find food”, “join the mission”, “volunteer today” contributes to the aesthetic, but at the expense of the clarity of naming it “Recipient”, “Business”, “Volunteer” portals. It is something to consider.


### Usability Criteria: Accessibility
While our app is definitely mindful in nature, focusing on redistributing food to those in need and fostering a community, there is a considerable lack of accessibility features in our wireframes, as it wasn’t prioritized in our concepts or features. The least we should do is add a light mode / dark mode, alternative color-blind-friendly color schemes, text to speech, and also make sure that zooming in or out works correctly and maintains the proportions of the app without introducing any bugs, keeping it easy to use for all levels and abilities. However, we have to keep in mind the tradeoff between more accessibility features and potential performance overhead, as the key functionality of the app cannot be overshadowed by these features alone.


### Physical Criteria: Situational Context 
There are plenty of examples of situational context in our wireframes – as described in more detail in the user’s language section, the flowchart of the delivery tells the user exactly where they are in the delivery process. Likewise, in claiming food, there is a tab that shows you if you are in “delivery” or “pickup” mode, an easy toggle for the user. And for volunteers, a job they accept is then moved upwards into the “My deliveries” section, accurately showing a new situation and adapting to the new context of the user input. However, this type of context could use some more consistency, as for businesses, claimed food is simply colored as “claimed!” instead of being moved into its own section. My biggest improvement would be at least a one word indicator if you are using the app in business, recipient, or volunteer mode, as lack of proper signposting could be confusing in the long run. We have to consider what type of situational context each of our three use cases wants – business, recipient, or volunteer, and also the tradeoffs of information overload when considering adding more context clues.  


### Physical Criteria: Accelerators 
One thing that the app is lacking is in accelerators, which are shortcuts for expert users. So far, we have authentication flow and intuitive flows for businesses, volunteers, and recipients. For businesses, a way to tabulate their most frequent past listings, and relist more of them in one tap, in order to not have to fill out the whole prompt again. Or even advance scheduled postings if they are sure they will have at least a baseline number of leftovers at a certain time of day. And while not currently in the wireframes, the recipients should be able to only see food that matches their preferences, or at least filter with one tap. There are many little opportunities throughout.


### Linguistic Level: Consistency 
Our app’s design is consistent with those of other applications in similar domains, such as deliveries and ridesharing. Specifically, the “awaiting pickup” screen shows an intuitive flow between requested delivery, confirmed delivery, and other steps in the food delivery process, and a map, something we see in Uber Eats, Domino’s, etc. Together with the other screens, they form an environment intuitive to a new user with existing domain experience.


### Linguistic Level: Speak a User’s Language 
In general, the wireframes exhibit language that is easy to understand for the user. Simple prompts such as “Confirm delivery details” and “Confirm pickup location” in the pickup confirmations provide a clear indication into what the user has to do, as well as the messages to List a Meal and Edit Your Meal. There is nothing technical about this website’s messages that would only be understandable by developers. But when choosing the language, we have to balance clarity and concision, they can’t be too dense and ruin the immersion, and they can’t be too short to the point the phrasing is vague.








## Visual Design Study


https://docs.google.com/presentation/d/1I1n29u_gzrYPGGBNMdZqZgLpg0n7CCoAn4ui2D2Y9q0/edit?usp=sharing





## Implementation Plan

### Concept Ordering

After evaluation, we realized that the tasks must be developed in this order due to dependencies.

- Authenticating
- Sessioning
- Posting
- Claiming
- Delivering, Tagging, Messaging (can be concurrently)

### By Timeline

### Week 1 (Alpha Release)

- Authenticating (can be re-used)
- Session-ing (can be re-used)
- Posting
- Claiming

### Week 2 (Beta Release)

- Delivering
- Tagging
- Messaging

### Task Ordering & Assignments

### Week 1 (Alpha Release)

We structured our tasks to finish the MVP features, pages for tasks 1-3, and 4 is the extra features we wanted to include to improve user experience.

- **Setup + modified auth/sessioning**
  - Deadline: soft deadline **Thursday 11/21**, hard deadline **Friday 11/22**
  - Creating our repository and transferring relevant files/skeleton (includes our backend and frontend for Authenticating and Session-ing) - **Emily**
  - Finish backend for Authentication and Session-ing
    - Add in role as a parameter to Authenticating (plus additional actions to validate roles) - **Emily**
  - Front-end relevant to Authenticating/Session-ing
    - Landing page - **Emily**
    - Login/Registration Pages - **Emily**
    - Navbar based off roles - **Emily**
    - Account Settings - **Claire**
- **Posting**
  - Deadline: **Friday 11/22**
  - Assigned To: **Sabrina**
  - Backend for Posting
    - Implement concept and routes for Posting, while validating that only donors can claim - **Sabrina**
  - Frontend
    - Create Posts - **Sabrina**
    - View Posts - **Sabrina**
    - Pickup page with map - **Matt**
    - Filter by pickup vs delivery - **Claire**
    - Page to filter for your own food listings - **Claire**
- **Claiming**
  - Deadline: **Saturday 11/23**
  - Backend
    - Implement concept and routes for Claiming, while validating that only recipients can claim - **Matt**
  - Frontend (depends on posting frontend)
    - Recipients should be able to claim items and see it in their claims list, and designate items for pickup - **Matt**
    - Donors should be able to view if an item has been claimed (either as pickup or delivery) - **Matt**
    - Volunteers should be able to view claimed items with a method of ‘Delivery - **Sabrina**
- Misc
  - Sidebar with logout button - **Claire**

### Week 2 (Beta Release)

- **Delivering**
  - Deadline: **Friday 12/1**
  - Assigned To: **Sabrina**
  - Backend
    - Implement concept and routes for Delivering - **Sabrina**
  - Frontend
    - Volunteers should be able to deliver items and see them in their pending deliveries - **Sabrina**
    - Volunteers should be able to mark deliveries as completed - **Sabrina**
- **Tagging**
  - Deadline: **Friday 12/1**
  - Backend
    - Implement concept and routes for Tagging, while validating that only donors can modify tags (but recipients can view tags) - **Emily**
  - Frontend
    - Recipients and donors should be able to filter both the pickup & delivery pages by tags - **Claire**
- **Messaging**
  - Deadline: **Friday 12/1**
  - Backend
    - Implement concept and routes for Messaging - **Sabrina**
  - Frontend
    - All users should be able to view a Messaging/Inbox page in the sidebar, from which they can view their messages or compose a message to a new user - **Matt**
    - Recipients should be able to start a new message with a food donor from a pickup confirmation page - **Matt**
    - Recipients should be able to start a new message with a volunteer from a delivery confirmation page - **Matt**
    - Volunteers should be able to start a new message with a recipient from a delivery request page - **Matt**
- **Styling & UI Overhaul**
  - Deadline: **Wednesday 12/3**
  - Assigned To: **Claire** & **Emily**

### Final Week (User Tests)

- Each team member will find a respective user and conduct interviews!

### Contingency Plan (What will happen if something goes wrong):

- We’ve created general soft and hard deadlines for the important tasks with a lot of dependencies, along with leaving in extra ‘padding’ days for when things get behind. In case something goes wrong, we will prioritize the most important features/concepts to achieve a functioning app, which are Authenticating, Sessioning, Posting, Claiming, and Delivering. Prior to the beta release, if we find we are very behind, we will remove messaging and tagging as concepts for the app to cut down on the requirements for an MVP.
- While Week 1 has more dependencies, all the concepts/work in Week 2 can be done concurrently so there is less room for error.
- Other superfluous items that can be dropped are some of the styling components, some of the “nice to have” pages such as the pages that filter for “Your Posts”/”Your Donations”. Additionally, the map can be dropped on the pickup page.

### Our Concepts:

Authenticating, Sessioning, Posting,Claiming, Delivering, Tagging, Messaging


