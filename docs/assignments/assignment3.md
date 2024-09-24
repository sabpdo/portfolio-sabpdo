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
__Name__: Authorizing (Item)

__Purpose__: provide access to perform specified action

__Operational Principle__:
    after authorizing user u
    to perform action a, a
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

### Concept 2: 
__Name__: Authenticating

__Purpose__: authentaticate users so that app users correspond to people

__Operational Principle__: 
    
    after a user u registers with a username u and a password p and 
    a verification code v, they can authenticate by providing the unique pair
    (u, p)

__State__:

    registered: __set__ User
    username, password: registered -> __one__ String

__Actions__:

    register(name, pass: String, verificationCode: String, __out__ user:User)
        registered += (name, pass)

    authenticate(name, pass:String, __out__ user:User)
        (name, pass) in registered


### Concept 3:
__Name__: Nudging (Item)

__Purpose__: deliver a notification

__Operational Principle__: 

    a user/the system a can nudge another user b
    to complete an action a

__State__: 

    nudges: (user, user) -> __set__ String s

__Actions__: 

    nudge(a: User, b: User, action: String)
        nudges[a, b] += action


### Concept 4:

__Name__: Messaging (Item)

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

### Concept 5:

__Name__: Posting (Item)

__Purpose__: share and save content

__Operational Principle__:

    user a can post a post p
    to their account

__State__:

    user_posts: (user) -> __set__ Posts

__Actions__:

    post(a: User, p: Post)
        user_posts[a] += p

    edit(a: User, oldPost: Post, newPost: Post)
        user_posts[a] -= oldPost
        user_posts[a] += newPost
    
    delete(a: User, p: Post)
        user_posts[a] -= oldPost

### Concept 7: 

__Name__: Tracking

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

    stop_tracking(u: User, action: String, time: T)
        tracked_users -= u


### Synchronizations of Concept Actions 



### Dependency Diagram

## Wireframes

## Design iteration

## Design tradeoffs

### Design Decision I

### Design Decision II

### Design Decision III