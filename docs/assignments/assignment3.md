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

    allowed: One user -> __set__ action
    denied: One user -> __set__ action

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

__Name__: Authenticating

__Purpose__: authenticate users so that app users correspond to people

__Operational Principle__: 
    
    after a user u registers with a username u and a password p and 
    a verification code v, they can authenticate by providing the unique pair
    (u, p)

__State__:

    registered: __set__ User
    username, password: registered -> __one__ String

__Actions__:

    register(name, pass: String, verificationCode: String)
        registered += (name, pass)
    
    unregister(user: User)
        registered -= (user.name, user.password)
        active_users -= user
    
    authenticate(name, pass: String, __out__ user: User)
        (name, pass) in registered
    

### Concept 3:
__Name__: Nudging \[Action]

__Purpose__: deliver a notification

__Operational Principle__: 

    a user/the system userA can nudge another user userB
    to complete an action a

__State__: 

    nudges: (user, user) -> __set__ String s

__Actions__: 

    notify(userA: User, userB: User, action: String)
        nudges[userA, userB] += action

a
### Concept 4:

__Name__: Messaging \[User]

__Purpose__: deliver a communication

__Operational Principle__:
    user a can deliver a message
    with content `content` to user b

__State__:
    message: (user, user) -> String s
    mesages: __set__ message

__Actions__:
    send(a: User, b: User, content: String)
        message[a, b] = content
        messages += message

    unsend(a: User, b: User, content: String)
        messages -= message[a, b, c]
    
    deleteAll(a: User)
        messages -= message[a, b, content] for any b, content
    
    getMessages(a: User)
        message for message in messages if message[0] == a

### Concept 5:

__Name__: Posting \[Item]

__Purpose__: share and save content

__Operational Principle__:

    user a can post a post p
    to their account

__State__:

    posts: One user -> __set__ Posts

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

__Name__: Tracking \[Action]

__Purpose__: monitor and track statistics

__Operational Principle__:

    a user u can track action a
    over a period of time t

__State__:

    actions: __set__(String s, Integer t)
    user_actions: One User -> actions
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

### Concept 7: 

__Name__: Session-ing \[Action]

__Purpose__: enable authenticated actions for an extended period of time

__Operational Principle__:

    after a session starts (and before it ends),
    the getUser action returns the user identified at the start:
    start(u,s); getUser(s, u') {u'=u}

__State__:

    active: __set__ Session
    user: active -> one User

__Actions__:

    start(user: User, __out__ sess: Session)
        active += user

    getUser(sess: Session, __out__ user: User)
        user in active if Session.user == user
    
    userIsActive(sess: Session, user: User)
        user in active
    
    end(sess: Session)
        active -= user


## Synchronizations of Concept Actions 

### Subsets

\{Authenticating\}

\{Messaging, Session-ing, Authenticating\}

\{Posting,  Session-ing, Authenticating\}

\{Nudging, Messaging, Session-ing, Authenticating\}

\{Authorizing, Tracking, Messaging, Session-ing,Authenticating\}

\{Authorizing, Tracking, Posting, Session-ing,Authenticating\}

\{Tracking, Messaging, Session-ing, Authenticating\}

\{Tracking, Posting, Session-ing Authenticating\}

### App Level & Synchronizations

include Authenticating, Session-ing[Authenticating.User]  Messaging[Session-ing.User], Posting[Session-ing.User], 
Nudging[Messaging.Message], Tracking[Messaging.Messages], Tracking[Posting.Posts], 
Authorizing[Messaging], Authorizing[Tracking], Authorizing[Posting]

```
__sync__ register(username, password: String, __out__ user: User)

    Authenticating.register(username, password, user)
```
```
__sync__ login(username, password: String, __out__ user: User, out session: Session)

    Authenticating.authenticate(username, password, user)
    Sessioning.start(user, session)
```
```
__sync__ authenticate(username, password: String, __out__ user: User, out session: Session)

    Authenticating.authenticate(username, password, user)
    Sessioning.start(user, session)
```
```
__sync__ sendMessage(userA: User, userB: User, message: String)
    
    Session-ing.userIsActive(userA)
    Authorizing.isAllowed(userA, "message")
    Messaging.sendMessage(userA, userB, message)
```
```
__sync__ unsendMessage(userA: User, userB: User, message: String)
    
    Session-ing.userIsActive(userA)
    Authorizing.isAllowed(userA, "unsend")
    Messaging.unsendMessage(userA, userB, message)
```
```
__sync__ post(user: User, p: Post)
    
    Session-ing.userIsActive(user)
    Authorizing.isAllowed(user, "post")
    Post.post(user, p)
```
```
__sync__ edit(user: User, oldPost: Post, newPost: Post)
    
    Session-ing.userIsActive(user)
    Authorizing.isAllowed(user, "post")
    Post.edit(user, oldPost, newPost)
```
```
__sync__ delete(user: User, p: Post)
    
    Session-ing.userIsActive(user)
    Authorizing.isAllowed(user, "delete")
    Post.delete(user, p)
```
```
__sync__ nudgeForMessage(userA: User, userB: User)

    Session-ing.userIsActive(user)
    Authorizing.isAllowed(user, "nudge")
    Nudging.notify(userA, userB, "message")
```
```
__sync__ allowMessage(user: User)

    Session-ing.userIsActive(user)
    Authorizing.allow(Messaging.sendMessage)
    Authorizing.allow(Messaging.unsendMessage)
```
```
__sync__ denyMessage(user: User)

    Session-ing.userIsActive(user)
    Authorizing.deny(Messaging.sendMessage)
    Authorizing.deny(Messaging.unsendMessage)
```
```
__sync__ allowTracking(user: User)

    Session-ing.userIsActive(user)
    Authorizing.allow(Tracking.start_tracking)
    Authorizing.allow(Tracking.record)
```
```
__sync__ denyTracking(user: User)

    Session-ing.userIsActive(user)
    Authorizing.deny(Tracking.start_tracking)
    Authorizing.deny(Tracking.record)
```
```
__sync__ allowPosting(user: User)

    Session-ing.userIsActive(user)
    Authorizing.allow(Posting.post)
```
```
__sync__ denyPosting(user: User)

    Session-ing.userIsActive(user)
    Authorizing.deny(Posting.post)
```
```
__sync__ trackMessageActivity(user: User)

    Session-ing.userIsActive(user)
    Authorizing.isAllowed(user, "track")
    Tracking.start_tracking(user, "message")
```
```
__sync__ trackPostingActivity(user: User)

    Session-ing.userIsActive(user)
    Authorizing.isAllowed(user, "track")
    Tracking.start_tracking(user, "post")
```
```
__sync__ unregister(user: User)

    Session-ing.userIsActive(user)
    Tracking.stop_tracking(user, activity) for activity in Tracking.get_tracked_activities(user)
    Authenticating.unregister(user)
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
