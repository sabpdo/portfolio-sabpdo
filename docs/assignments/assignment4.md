---
title: "Assignment 4: Backend Design & Implementation"
layout: doc
---

# Assignment 4: Backend Design & Implementation

## Data Modeling

### Concept 1:

__Name__: Authorizing \[User, Action]

__State Variables__: 

    user: Authorization -> one User
    action: Authorization -> one String
    denied_actions: User -> __set__ Authorization
    user_control_map: User -> __set__ User

Note: all users are automatically allowed to do all actions by default.
Action is a generic type that maps to different concepts in my implementation. More specifically, 
the actions will be represented as a string in the implementation such that 
```Action = "Message"|"Friend"|"Nudge"|"Record"|"Post"```.

### Concept 2: 

__Name__: Authenticating

__State__:

    registered: __set__ User
    username, password: registered -> __one__ String


### Concept 3:
__Name__: Nudging \[User, Action]

__State Variables__: 

    from: Nudge -> one User
    to: Nudge -> one User
    time: Nudge -> one Date
    action: Nudge -> one String
    nudges: __set__ Nudge


### Concept 4:

__Name__: Messaging \[User]

__State__:

    to: Message -> one User
    from: Message -> one User
    time: Message -> one Date
    content: Message -> one String
    messages: __set__ Message


### Concept 5:

__Name__: Posting \[User]

__State__:

    time: Post -> one Date
    content: Post -> one String
    author: Post -> one User
    posts: __set__ Post

### Concept 6: 

__Name__: Recording \[Action]
(was previously tracking in A3)
__State__:
    
    time: Record -> one Date
    action: Record -> one String
    user: Record -> one User
    records: __set__ Record

### Concept 7: 

__Name__: Session-ing \[User]

__State__:

    active: __set__ Session
    user: active -> one User

```
app GoldenBook
    
    include Authenticating, Session-ing[Authenticating.User], Messaging[Session-ing.User], Posting[Session-ing.User], Nudging[Messaging], Tracking[Messaging.Messages, Posting.Posts], Authorizing[Messaging, Tracking, Posting, Nudging]
```

## Data Model 
![Data Model](/assets/images/Assignments/DataModel.png)

## Deployed Website Link

Link: https://golden-book-px12ov4gv-sabrina-dos-projects.vercel.app/

Link to Github Repo: https://github.com/sabpdo/GoldenBook

## Design Reflection

During implementation, several design issues arose, particularly concerning user authorization (aka the management of permissions on accounts). Initially, I had not addressed who should control these permissions, leading to two main options: role-based authorization and explicit authorization.

In role-based authorization, specific users, if given a specific role, would automatically gain control over another user’s settings, creating clear relationships and a straightforward implementation. However, this approach could lead to challenges as user roles change over time, potentially resulting in confusion about who holds authority.

Conversely, explicit authorization allows users to manually designate individuals to manage their account settings. While this offers greater flexibility and personalization, it can also introduce complexity, especially for elderly users who may struggle with nuanced controls. Ultimately, I chose explicit authorization, granting the designated "controller" full access to all settings to simplify the user experience and minimize potential confusion.

Another critical design decision involved the format of posts—text or image-based. While many social platforms leverage images for engagement, I prioritized text to safeguard the privacy of elderly users, who are more susceptible to misinformation. This trade-off emphasizes the app's functionality of using posting for community notifications and  prioritization of privacy.

Lastly, I had to make a decision regarding messaging restrictions. I concluded that users who are unable to send messages should also be prevented from receiving them. While this approach ensures consistency, it does limit communication flexibility for users. However, in the long run, this decision prioritizes user security by protecting them from potentially malicious messages, such as those containing deceptive links.
