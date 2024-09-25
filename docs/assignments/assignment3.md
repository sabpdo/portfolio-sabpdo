---
title: "Assignment 3: Convergent Design"
layout: doc
---

# Assignment 3: Convergent Design

## Pitch

Are you looking for a way to connect with others and build a vibrant community? Introducing GoldenBook, the innovative social media and community-building app designed specifically for elderly individuals. Unlike traditional social media platforms, GoldenBook prioritizes your security while making connections effortless and enjoyable.

Key Features of GoldenBook:

Trusted Caregiver Setting: With user authorization, trusted caregivers can manage certain actions on the primary user's device, ensuring peace of mind and support when needed.

Streak-Tracking for Healthy Habits: GoldenBook helps users stay on top of important habits, like updating privacy settings or taking medications, by tracking their progress and sending gentle reminders.

Community Event Posting Board: Join a lively community by sharing and discovering local events tailored for your interests, fostering connections and social engagement.

Social Wellness Notifications: To combat social isolation, GoldenBook sends timely reminders to users, encouraging them to reach out to friends and family, ensuring they stay connected.

GoldenBook is crafted with input from elderly users to ensure accessibility and ease of use. We believe that everyone deserves a safe and supportive space to connect and thrive. Join us in creating a vibrant community with GoldenBook—where your connections matter!


## Functional Design

### Concept 1:

__Name__: Authorizing \[Action]

__Purpose__: provide access to perform specified action

__Operational Principle__:
    after authorizing user u
    to perform action a,
    user u can perform action a
    until access is revoked

__State__: 

    allowed: user -> __set__ action
    denied: user -> __set__ action

__Actions__: 

    allow(u:user, action: String)
        allowed[u] += action
        u in denied - action

    deny(u:user, action: String)
        denied[u] += action
        u in allowed - action
    
    isAllowed(u: user, action: String)
        action in allowed[u]

### Concept 2: 

__Name__: Authenticating \[Item]

__Purpose__: authentaticate users so that app users correspond to people

__Operational Principle__: 
    
    after a user u registers with a username u and a password p and 
    a verification code v, they can authenticate by providing the unique pair
    (u, p)

__State__:

    registered: __set__ User
    username, password: registered -> __one__ String
    active_users: __set__ User

__Actions__:

    register(name, pass: String, verificationCode: String)
        registered += (name, pass)
    
    unregister(user: User)
        registered -= (user.name, user.password)
        active_users -= user

    login(name, pass:String)
        (name, pass) in registered
        active_users += user

    logout(user: User)
        (name, pass) in registered
        active_users -= user
    
    isLoggedIn(user:User, __out__ user: User)
        user in active_users
    
    isRegistered(user: User, __out__ user: User)
        user in registered


### Concept 3:
__Name__: Nudging \[Action]

__Purpose__: deliver a notification

__Operational Principle__: 

    a user/the system a can nudge another user b
    to complete an action a

__State__: 

    nudges: (user, user) -> __set__ String s

__Actions__: 

    notify(a: User, b: User, action: String)
        nudges[a, b] += action


### Concept 4:

__Name__: Messaging \[Item]

__Purpose__: deliver a communication

__Operational Principle__:
    user a can deliver a message
    with content c to user b

__State__:
    message: (user, user) -> String s
    mesages: __set__ message

__Actions__:
    send(a: User, b: User, c: String)
        message[a, b] = c
        messages += message

    unsend(a: User, b: User, c: String)
        messages -= message[a, b, c]
    
    deleteAll(a: User)
        messages -= message[a, b, c] for any b, c
    
    getMessages(a: User)
        message for message in messages if message[0] == a

### Concept 5:

__Name__: Posting \[Item]

__Purpose__: share and save content

__Operational Principle__:

    user a can post a post p
    to their account

__State__:

    posts: (user) -> __set__ Posts

__Actions__:

    post(a: User, p: Post)
        posts[a] += p

    edit(a: User, oldPost: Post, newPost: Post)
        posts[a] -= oldPost
        posts[a] += newPost
    
    delete(a: User, p: Post)
        posts[a] -= oldPost
    
    getPosts(a: User)
        post in posts[a]

### Concept 6: 

__Name__: Tracking \[Item]

__Purpose__: monitor and track statistics

__Operational Principle__:

    a user u can track action a
    over a period of time t

__State__:

    actions: __set__(String s, Integer t)
    user_actions: User -> actions
    tracked_users: __set__ User

__Actions__:

    start_tracking(u: User, action: String, time: T)
        user_actions[u] = {}
        tracked_users += u
    
    record(u: User, action: String, time: T)
        if u in tracked_users:
            user_actions[u] += (action, time)

    stop_tracking(u: User, action: String)
        tracked_users -= u
    
    get_tracked_activities(u: User, __out__: actions)
        actions in user_actions[u]
    
    get_tracked_user_activity(u: User, action: String, __out__: actions)
        action for actions in user_actions[u] if action[0] == action



## Synchronizations of Concept Actions 

### Subsets

\{Authenticating\}

\{Messaging, Authenticating\}

\{Posting, Authenticating\}

\{Nudging, Authenticating\}

\{Authorizing, Tracking, Messaging, Nudging, Posting, Authenticating\}

\{Tracking, Messaging, Posting, Authenticating\}

### App Level & Synchronizations

include Authenticating,  Messaging[Authenticating.User], Posting[Authenticating.User], 
Nudging[Messaging.Message], Tracking[Messaging.Messages], Tracking[Posting.Posts], 
Authorizing[Messaging], Authorizing[Tracking], Authorizing[Posting], 
```
__sync__ sendMessage(userA: User, userB: User, message: String)
    
    Authorizing.isLoggedIn(userA)
    Authorizing.isAllowed(userA, "message")
    Messaging.sendMessage(userA, userB, message)
```
```
__sync__ unsendMessage(userA: User, userB: User, message: String)
    
    Authorizing.isLoggedIn(userA)
    Authorizing.isAllowed(userA, "unsend")
    Messaging.unsendMessage(userA, userB, message)
```
```
__sync__ post(user: User, p: Post)
    
    Authorizing.isLoggedIn(user)
    Authorizing.isAllowed(user, "post")
    Post.post(user, p)
    Nudging.notify()
```
```
__sync__ edit(user: User, oldPost: Post, newPost: Post)
    
    Authorizing.isLoggedIn(user)
    Authorizing.isAllowed(user, "post")
    Post.edit(user, oldPost, newPost)
```
```
__sync__ delete(user: User, p: Post)
    
    Authorizing.isLoggedIn(user)
    Authorizing.isAllowed(user, "delete")
    Post.delete(user, p)
```
```
__sync__ nudgeForMessage(userA: User, userB: User)

    Authorizing.isLoggedIn(user)
    Authorizing.isAllowed(user, "nudge")
    Messaging.sendMessage()
    Nudging.notify(userA, userB, "message")
```
```
__sync__ allowMessage(user: User)

    Authorizing.isLoggedIn(user)
    Authorizing.allow(Messaging.sendMessage)
    Authorizing.allow(Messaging.unsendMessage)
```
```
__sync__ denyMessage(user: User)

    Authorizing.isLoggedIn(user)
    Authorizing.deny(Messaging.sendMessage)
    Authorizing.deny(Messaging.unsendMessage)
    Messaging.deleteAll(user)
```
```
__sync__ allowTracking(user: User)

    Authorizing.isLoggedIn(user)
    Authorizing.allow(Tracking.start_tracking)
    Authorizing.allow(Tracking.record)
```
```
__sync__ denyTracking(user: User)

    Authorizing.isLoggedIn(user)
    Authorizing.deny(Tracking.start_tracking)
    Authorizing.deny(Tracking.record)
```
```
__sync__ allowPosting(user: User)

    Authorizing.isLoggedIn(user)
    Authorizing.allow(Posting.post)
```
```
__sync__ denyPosting(user: User)

    Authorizing.isLoggedIn(user)
    Authorizing.deny(Posting.post)
```
```
__sync__ trackMessageActivity(user: User)

    Authorizing.isLoggedIn(user)
    Authorizing.isAllowed(user, "track")
    Tracking.start_tracking(user, "message")
```
```
__sync__ trackPostingActivity(user: User)

    Authorizing.isLoggedIn(user)
    Authorizing.isAllowed(user, "track")
    Tracking.start_tracking(user, "post")
```
```
__sync__ nudgeForPost(user: User)

    Authorizing.isLoggedIn(user)
    Authorizing.isAllowed(user, "nudge")
    Nudging.notify(system, user, "post")
```
```
__sync__ unregister(user: User)

    Authorizing.isLoggedIn(user)
    Tracking.stop_tracking(user, activity) for activity in Tracking.get_tracked_activities(user)
```
```
__sync__ nudgeForInactivePoster(user: User)

    Authorizing.isLoggedIn(user)
    Tracking.get_tracked_user_activity(user, "post")
    Nudging.notify(system, user, "post")
```
```
__sync__ autoPostFromTracking(user: User, post: Post)

    Authorizing.isLoggedIn(user)
    Authorizing.isAllowed(user, "post")
    Tracking.get_tracked_user_activity(user, "message")
    Posting.post(user, post)
```


## Dependency Diagram

![Dependency Diagram](/assets/images/Assignments/DependencyDiagram.png)

## Wireframes

## Design tradeoffs

### Design Decision I
__Title__:

__Various Options__:

__Rationale__:


### Design Decision II

__Title__:

__Various Options__:

__Rationale__:


### Design Decision III

__Title__:

__Various Options__:

__Rationale__:
