---
title: "Assignment 4: Backend Design & Implementation"
layout: doc
---

# Assignment 4: Backend Design & Implementation

## Data Modeling

### Concept 1:

__Name__: Authorizing \[Action]

__State Variables__: 

    action: String
    denied_actions: User -> __set__ action

### Concept 2: 

__Name__: Authenticating

__State__:

    registered: __set__ User
    username, password: registered -> __one__ String
    role: User -> __one__ String


### Concept 3:
__Name__: Nudging \[Action]

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
    
    include Authenticating, Session-ing[Authenticating.User], Messaging[Session-ing.User], Posting[Session-ing.User], Nudging[Messaging], Tracking[Messaging.Messages, Posting.Posts], Authorizing[Messaging, Tracking, Posting]
```

## Data Model 
![Data Model](/assets/images/Assignments/DataModel.png)

## Deployed Website Link

## Design Reflection