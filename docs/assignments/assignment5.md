---
title: "Assignment 5: Frontend Design & Implementation"
layout: doc
---

# Assignment 5: Frontend Design & Implementation

Wireframes for reference from A3: https://www.figma.com/design/FrijeU0YcwSkAAbuCnNssg/GoldenBook?node-id=0-1&t=YkF3by5es3HbNfjm-1


## Heuristic Evaluation

### Heuristic: Usability critieria

#### __Error tolerance__: 

- In terms of error tolerance, my wireframes have many areas of improvements but do incorporate some oppportunities for user to backtrack on mistakes. For example, while users are able to undo accidental clicks (e.g. clicking on a wrong page, turning off notifications and manage authorizations dynamically), there are some areas of improvement to improve the safety. For example, while users can post and send messages, the wireframes do not currently indicate options to delete/undo some actions. 
    - Potential improvements for this include the following:

        (1) Providing the option to unsend/delete messages

        (2) Providing the option to give authorization control to another user and revoke it

        (3) Provide an option to stop recording actions
    - If I incorporate the opportunities to delete posts/messages, I could have a popup that appears that warns the user: "Are you sure you want to delete this?" to prevent the user from accidentally deleting items. 
        - However, adding features to delete messages or posts introduces tradeoffs between safety and efficiency. For instance, implementing confirmation popups (“Are you sure you want to delete this?”) can prevent accidental deletions, but frequent prompts may frustrate users who prefer quicker interactions.

#### __Accessibility__:

- To meet accessibility guidelines, my app could integrate features that cater to a wider range of users. For example, I should implement color-blind-friendly palettes to ensure usability for color-impaired users. 
- Incorporating text-to-speech functionality for community board posts would assist visually impaired users. These features would significantly improve the app’s accessibility and inclusivity. 
- While implementing these features, I need to decide on the correct balance betwen design simplicity and performance overhead. For example, a color-blind-friendly design might limit certain color schemes that could otherwise be more visually appealing to the broader user base.


### Heuristic: Physical

#### __Situational Context__:  
- Currently, there exists many flags to see their context, but there can be features to improved. The current design offers some context cues, such as tags showing ownership of posts and differing headers for actions like posting or editing.
- However, the design could benefit from further differentiation in popups for actions like sending nudges or making posts, as these currently appear too similar. Instead I can make them static forms that differ.
- For improvements, there could also be a sidebar/bar at the top that highlights which page a user is on in the page as well that dynamically changes based on their currently location. However, while implementing this, I need to consider how overloading users with too many indicators may lead to information overload, reducing ease of use.
- Also, the send emoji can be replaced with a more recognizable emoticon instead. 

#### __Fitt's Law__:

- The placement of certain elements in my wireframes adheres to Fitts' Law but could be further optimized. Some areas have too much white space, which can make frequently used buttons feel distant and harder to reach.

- However, one example of a good usage of Fitt's law in my application are the popups: the delete button is located next to the cancel button, and the popups do not expand to the whole page to reduce user's effort. 
    - Additionally, all the names are cenetered in the navigation bar.

- On the manage authorizations page, organizing accounts and buttons into a grid layout would reduce unnecessary space and improve ease of access. 
- Reducing white space overall in all my pages (e.g profile view) will benefit the user in terms of Fitt's law. While reducing white space, I need to reduce enough space to reduce effort to click new buttons, while also not cluttering/making buttons too close together to the point that it is unusable.

### Heuristic: Linguistic Level

#### __Speak the User's Language__: 

- The interface generally uses simple, intuitive labels, but there is room to clarify certain terms. For instance, "Tracking" or "Recording" could be renamed to "Daily Habit Tracking" for better clarity. - Replacing "Nudge" with "Nudge to Socialize" could make the function more intuitive to users. 
- Balancing clarity with brevity is crucial here—while longer phrases may provide more context, they could detract from simplicity. For technical concepts like "authorization," slightly longer explanations may be necessary to ensure understanding without overwhelming users.

#### __Consistency__: 

- My interface maintains a high level of consistency in both design and functionality. Messaging resembles standard formats from popular platforms, with messages on the left side and user profiles similar to Instagram or Facebook. 
- Additionally, visual elements like the "fire" icon resemble streaks in apps like Duolingo, reinforcing familiarity. 
- However, there are areas of consistency that can be improved. For example, I call the notifications "Social Wellness Notifications" in one part of my application, while in another page of my wireframe, I call it "Nudge" which can be confusing. 

## Code Implementation

Github Repo:
https://github.com/sabpdo/goldenbook-frontend 

## Deployed Site

Deployed Site: https://goldenbookofficial.vercel.app/ 

## Visual Design Study

https://docs.google.com/presentation/d/1eaI43w2RmGbkWwBf4GR5imzrCrhYtfS20DjsWakKrbE/edit?usp=sharing