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

    denied_actions: User -> __set__ action
    action: Action -> one String
    user_control_map: User -> __set__ User 

__Actions__:

    allow(u:user, action: allowed_action_type)
        u in denied - action

    deny(u:user, action: allowed_action_type)
        denied[u] += action
    
    isAllowed(u: user, action: allowed_action_type)
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
    
    ... rest of the functions are get functions

Note: all users are automatically allowed to do all actions by default.
AllowedAction is a generic type that maps to different concepts in my implementation. More specifically, 
the actions will be represented as a string in the implementation such that 
```Action = "Message"|"Friend"|"Nudge"|"Record"|"Post"``` (but these actions are only specified in the syncs).

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
    records: __set__ Record
    automatic_tracked_actions: __set__ Action

This was previously "Tracking" in A3, but I re-named it to "Recording" to make it more clear. Recording in my app allows for the functionality 
for both (1) allowing a user to manually record their own actions (any action) and (2) to automatically record/track messaging & posting information if needed.

The second functionality is uses automatic_tracked_actions to see which actions we are automatically tracking. The default is to 
not track neither "Messaging" nor "Posting" unless enabled.

### Concept 7: 

__Name__: Session-ing \[User]

__State__:

    active: __set__ Session
    user: active -> one User



```
app GoldenBook
    
    include Authenticating, Session-ing[Authenticating.User], Messaging[Session-ing.User], Posting[Session-ing.User], Nudging[Sessioning-ing.User, Messaging], Tracking[Messaging.Messages, Posting.Posts], Authorizing[Messaging, Tracking, Posting, Nudging]
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


1. Ask about the tracking concept to confirm ideas.
Should I have it as an options