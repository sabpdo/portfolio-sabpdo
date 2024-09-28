---
title: "Assignment 4: Backend Design & Implementation"
layout: doc
---

# Assignment 4: Backend Design & Implementation

## Data Modeling

### Concept 1:

__Name__: Authorizing \[Action]

__State Variables__: 

    denied: User -> __set__ action

### Concept 2: 

__Name__: Authenticating

__State__:

    registered: __set__ User
    username, password: registered -> __one__ String
    role: User -> __one__ Role


### Concept 3:
__Name__: Nudging \[Action]

__State Variables__: 

    fromUser: Nudge -> one User
    toUser: Nudge -> one User
    nudge: (fromUser, toUser) -> __set__ (Action, Time)
    nudges: __set__ Nudge


### Concept 4:

__Name__: Messaging \[User]

__State__:

    toUser: Message -> one User
    fromUser: Message -> one User
    messages: (toUser, fromUser) -> __set__ Message
    time: Message -> one Date
    message_content: Message -> one String


### Concept 5:

__Name__: Posting \[Item]

__State__:

    posts: one User -> __set__ Posts
    date: Post -> one Date
    content: Post -> one String

### Concept 6: 

__Name__: Tracking \[Action]

__State__:

    user_actions: one User -> __set__(Action, Time)

### Concept 7: 

__Name__: Session-ing \[Action]

__State__:

    active: __set__ Session
    user: active -> one User

```
app GoldenBook
    
    include Authenticating, Session-ing[Authenticating.User], Messaging[Session-ing.User], Posting[Session-ing.User], Nudging[Messaging], Tracking[Messaging.Messages], Tracking[Posting.Posts], Authorizing[Messaging], Authorizing[Tracking], Authorizing[Posting]
```

![Data Model](/assets/images/Assignments/DataModel.png)
Questions

1. is this how i properly include things as generalizable parameters?
2. I'm conufsed on the labels of the arrows? what if have duplicate values (e.g. time)
3. if i have a separae user that nudges but it points towards messaging which has a user too how do i manage this. 
4. is this the data model we want?