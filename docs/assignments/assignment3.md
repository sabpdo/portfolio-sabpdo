---
title: "Assignment 3: Convergent Design"
layout: doc
---

# Assignment 3: Convergent Design

## Pitch

Are you looking for a way to connect with others and build a vibrant community? Introducing __GoldenBook__, the innovative social media and community-building app designed specifically for elderly individuals. Unlike traditional social media platforms, GoldenBook prioritizes your security while making connections effortless and enjoyable.

Key Features of GoldenBook:

__Trusted Caregiver Setting:__ With user authorization, trusted caregivers can manage certain actions on the primary user's device, ensuring peace of mind and support when needed.

__Streak-Tracking for Healthy Habits:__ GoldenBook helps users stay on top of important habits, like updating privacy settings or taking medications, by tracking their progress and sending gentle reminders.

__Community Event Posting Board:__ Join a lively community by sharing and discovering local events tailored for your interests, fostering connections and social engagement.

__Social Wellness Notifications:__ To combat social isolation, GoldenBook sends timely reminders to users, encouraging them to reach out to friends and family, ensuring they stay connected.

GoldenBook is crafted with input from elderly users to ensure accessibility and ease of use. Everyone deserves a safe and supportive space to connect and thrive. Join us in creating a vibrant community with GoldenBook—where your connections matter!


## Functional Design

### Concept 1:

__Name__: Authorizing \[Action]

__Purpose__: provide access to perform a specified action

__Operational Principle__:
    after authorizing user u
    to perform action a,
    user u can perform action a
    until access is revoked

__State__: 

    denied: User -> __set__ action

__Actions__: 

    allow(u:user, action: String)
        u in denied - action

    deny(u:user, action: String)
        denied[u] += action
    
    isAllowed(u: user, action: String)
        action not in denied[u]

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
    role: User -> __one__ Role

__Actions__:

    register(name, pass: String, role: String (optional))
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

    a user/the system `fromUser` can nudge another user `toUser`
    to complete an action `a`

__State__: 

    nudge: (User, User) -> __set__ Action
    nudges: __set__ Nudge
    nudge_times: User -> __set__ (nudge, Time)

__Actions__: 

    notify(fromUser: User, toUser: User, action: String)
        nudges[fromUser, toUser] += action
    
    setPeriodicNotify(user: User, action: String, time: Time)
        nudges[System User, user] += action
        nudge_times[user] += (Action, Time)


### Concept 4:

__Name__: Messaging \[User]

__Purpose__: deliver a communication

__Operational Principle__:
    user `sender` can deliver a message
    with content `content` to user `receiver`

__State__:

    messages: (User, User) -> __set__ Message

__Actions__:
    send(sender: User, receiver: User, message: Message)
        messages[sender, receiver] += message
    
    getMessages(user: User)
        message for message in messages if message[0] == user or message[1] == user

### Concept 5:

__Name__: Posting \[Item]

__Purpose__: share and save content

__Operational Principle__:

    user `a` can post a post `p`
    to their account

__State__:

    posts: one User -> __set__ Posts

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

    user_actions: one User -> __set__(Action, Time)

__Actions__:
    
    record(u: User, action: String, time: Time)
        if u in tracked_users:
            user_actions[u] += (action, time)
    
    get_tracked_activities(u: User, __out__: actions)
        actions in user_actions[u]
    
    get_tracked_user_activity(u: User, action: String, __out__: actions)
        action for actions in user_actions[u] if action[0] == action

### Concept 7: 

__Name__: Session-ing \[Action]

__Purpose__: enable authenticated actions for a period

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

\{Tracking, Messaging, Session-ing, Authenticating\}

\{Tracking, Posting, Session-ing, Authenticating\}

\{Authorizing, Messaging, Session-ing, Authenticating\}

\{Authorizing, Posting, Session-ing, Authenticating\}

\{Authorizing, Nudging, Session-ing, Authenticating\}

\{Authorizing, Tracking, Messaging, Posting, Session-ing, Authenticating\}

### App Level & Synchronizations

include Authenticating, Session-ing[Authenticating.User], Messaging[Session-ing.User], Posting[Session-ing.User], 
Nudging[Messaging], Tracking[Messaging.Messages], Tracking[Posting.Posts], 
Authorizing[Messaging], Authorizing[Tracking], Authorizing[Posting]

```
__sync__ register(username, password: String, __out__ user: User)

    Authenticating.register(username, password, user)
```
```
__sync__ login(username, password: String, __out__ user: User, out session: Session)

    Authenticating.authenticate(username, password, user)
    Session-ing.start(user, session)
```
```
__sync__ logout(session: Sessin)

    Session-ing.end(session)
```
```
__sync__ authenticate(username, password: String, __out__ user: User, out session: Session)

    Authenticating.authenticate(username, password, user)
    Session-ing.start(user, session)
```
```
__sync__ sendMessage(sender: User, receiver: User, message: Message)
    
    Session-ing.userIsActive(sender)
    Authorizing.isAllowed(sender, Messaging)
    Messaging.send(sender, receiver, message)
```
```
__sync__ post(user: User, p: Post)
    
    Session-ing.userIsActive(user)
    Authorizing.isAllowed(user, Posting)
    Post.post(user, p)
```
```
__sync__ edit(user: User, oldPost: Post, newPost: Post)
    
    Session-ing.userIsActive(user)
    Authorizing.isAllowed(user, Posting)
    Post.edit(user, oldPost, newPost)
```
```
__sync__ delete(user: User, p: Post)
    
    Session-ing.userIsActive(user)
    Authorizing.isAllowed(user, Posting)
    Post.delete(user, p)
```
```
__sync__ nudgeForMessage(sender: User, receiver: User)

    Session-ing.userIsActive(sender)
    Authorizing.isAllowed(sender, Nudging)
    Nudging.notify(sender, receiver, Message)
```
```
__sync__ setPeriodicNudgeForMessage(user: User)

    Session-ing.userIsActive(user)
    Authorizing.isAllowed(user, Nudging)
    Nudging.setPeriodicNotify(user, Message)
```
```
__sync__ allowMessage(user: User)

    Session-ing.userIsActive(user)
    Authorizing.allow(Messaging.send)
```
```
__sync__ denyMessage(user: User)

    Session-ing.userIsActive(user)
    Authorizing.deny(Messaging.send)
```
```
__sync__ allowTracking(user: User)

    Session-ing.userIsActive(user)
    Authorizing.allow(Tracking.record)
```
```
__sync__ denyTracking(user: User)

    Session-ing.userIsActive(user)
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
__sync__ recordMessageActivity(user: User)

    Session-ing.userIsActive(user)
    Authorizing.isAllowed(user, Tracking)
    Tracking.record(user, "message")
```
```
__sync__ recordPostingActivity(user: User)

    Session-ing.userIsActive(user)
    Authorizing.isAllowed(user, Tracking)
    Tracking.record(user, "post")
```
```
__sync__ unregister(user: User)

    Session-ing.userIsActive(user)
    Authenticating.unregister(user)
```

## Dependency Diagram

![Dependency Diagram](/assets/images/Assignments/DependencyDiagram.png)

## Wireframes

Link to WireFrames: https://www.figma.com/design/FrijeU0YcwSkAAbuCnNssg/GoldenBook?node-id=0-1&t=YkF3by5es3HbNfjm-1


## Design Tradeoffs

### Decision I: Session/Authentication Dependency for Secure Messaging/Posting

**Options Considered**: 
- Require authentication and session initialization before messaging/posting. (Chosen)
- Allow messaging/posting without session dependency.

**Rationale**:  
Given the app’s focus on privacy and security for elderly users, it's crucial to ensure that all interactions (messaging/posting)  occur within authenticated sessions. This prevents unauthorized use and reduces the risk of anonymous attacks or fraudulent activity. By requiring users to authenticate before posting/messaging, we create a safer environment where elderly users are less likely to encounter malicious interactions.


### Decision II: Restricting Notification Nudges to Improve Usability

**Options Considered**:  
- Allow nudges for all actions.
- Limit nudges to essential actions. (Chosen)
- Provide adjustable settings for nudge frequency. (Chosen)

**Rationale**:  
While nudges can help promote social engagement, overwhelming users with excessive notifications can lead to frustration—especially for elderly users who may be less familiar with frequent app interactions. I decided to restrict nudges to the most critical actions, primarily messaging, while allowing users to adjust the frequency of notifications.


### Decision III: Ethical Control Over User Accounts for Trusted Caregivers

**Options Considered**:  
- Provide caregivers full or view access to a user’s account.
- Restrict caregivers to only allow or deny user actions. (Chosen)

**Rationale**:  
To preserve the autonomy of elderly users while providing necessary support, I decided to limit the level of access trusted caregivers have. Instead of granting full control or access to private conversations, caregivers can only allow or deny specific actions, like approving critical posts or messages. This avoids potential ethical concerns around surveillance and privacy violations, as full access could reduce the user’s independence. By striking this balance, the app empowers elderly users while still offering a safeguard against harmful or unsafe behavior. 