---
title: "Assignment 4: Backend Design & Implementation"
layout: doc
---

# Assignment 4: Backend Design & Implementation

## Data Modeling

### Concept 1:

__Name__: Authorizing \[User, Action]

__Operational Principle__:
    after user a authorizes user b
    to perform action c,
    user b can perform action c
    until user a denies the action c for user b.
    user b can designate who user a is/who has control
    to perform authorizations on their account.

__State Variables__: 

    authorizations: __set__ Authorization
    user: Authorization -> one User
    denied_actions: Authorization -> __set__ allowed_action_type
    allowed_action_type: one action
    user_control_map: User -> __set__ User 

__Actions__ (ones most relevant/changed from A3):

    allow(u:user, action: string)
        u in denied - action

    deny(u:user, action: string)
        denied[u] += action
    
    isAllowed(u: user, action: string)
        action not in denied_actions[u]
    
    addAuthorizer(authorizer: user, authorizee: user)
        if authorizer in user_control_map:
            user_control_map[authorizer] += authorizee
        else:
            user_control_map[authorizer] = Set(authorizee)
        
    removeAuthorizer(authorizer: user, authorizee: user)
        if authorizer not in user_control_map or not authorizee in user_control_map[authorizer]:
            throw Error
        else:
            del authorizee in user_control_map[authorizer]
    
    ... 

Note: all users are automatically allowed to do all actions by default.
Action is a generic type that maps to different concepts in my implementation. More specifically, 
the actions will be represented as a string in the implementation such that action could equal any of the following allowed action types
```"Message"|"Nudge"|"Record"|"Post"``` (but these actions are only specified in the syncs).

Also, user_control_map is a map of a User ("Authorizer") to all their Authorizee's.

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

__Name__: Recording \[User, Action]

__State__:
    
    time: Record -> one Date
    action: Record -> one String
    user: Record -> one User
    autotracked: User -> __set__ action
    records: __set__ Record

This was previously "Tracking" in A3, but I re-named it to "Recording" to make it more clear. Recording in my app (later for synchronizations) allows for the functionality 
for both (1) allowing a user to manually record their own actions (any action) and (2) to automatically record/track messaging & posting information if needed.

For automatic recording of messaging and posting, the syncs __startAutomaticRecordForMessaging__ and __startAutomaticRecordForPosting__
work such that when a message is sent/a post is posted, a record will automatically be created. (Similar logic exists for stop).

### Concept 7: 

__Name__: Session-ing \[User]

__State__:

    active: __set__ Session
    user: active -> one User



```
app GoldenBook
    
    include Authenticating, Session-ing[Authenticating.User], Messaging[Session-ing.User], Posting[Session-ing.User], Nudging[Sessioning-ing.User, Messaging.Message], Tracking[Session-ing.User, Messaging.Message, Posting.Post], Authorizing[Session-ing.User, Messaging.Message, Recording.Record, Posting.Post, Nudging.Nudge]
```

## Data Model 
![Data Model](/assets/images/Assignments/DataModel.png)

## Deployed Website Link

Link: https://golden-book-two.vercel.app/

Link to Github Repo: https://github.com/sabpdo/GoldenBook

## Design Reflection
During implementation, several design issues emerged that required careful consideration and resolution.

First, in handling authorization, I had not initially defined how "authorizers" would be designated. I debated between two approaches: a flexible mapping of authorizers to authorizees or creating specific "caregiver/authorizer" accounts limited to managing only one authorizee’s account (and these caregivers would be solely limited to this functionality). I opted for the more flexible mapping, allowing for easier reassignment of roles as users' needs evolve. This resolved ambiguities around how people might fill multiple or changing roles over time.

Next, I had to address the format of posts—text or image-based. While images typically boost engagement on social platforms, I prioritized text to protect the privacy of elderly users, who are more vulnerable to misinformation. This decision reflected a trade-off between engagement and privacy, with the latter taking precedence to ensure the app focused on community notifications and safeguarding user information.

Also, I faced the issue of messaging restrictions. I decided that users who cannot send messages should also be unable to receive them. While this ensures consistent restrictions, it limits communication flexibility. However, the decision prioritizes user security by minimizing the risk of harmful messages, such as those containing deceptive links.

Lastly, there was an issue with how to track actions automatically. I initially considered using a boolean property in each record, checking the most recent record for tracking status. However, this was too time-dependent. Instead, I opted for mapping users to the actions automatically tracked for them. This solution was more flexible and streamlined state management by eliminating reliance on individual records.