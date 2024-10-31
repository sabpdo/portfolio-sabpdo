---
title: "Assignment 6: User Testing & Analysis"
layout: doc
---

# Assignment 6: User Testing & Analysis

## 1. Prepopulate Data

Link To Website: https://goldenbookofficial.vercel.app/

To prepopulate the website, I created a number of real potential users. For each of the users, I enabled a number of different features, ranging from creating conversations between a couple of users, managing authorizations, sending nudges, and creating posts.

You can log into my account @sabpdo, password: "password" to see one of the example profiles!

I also have four other false accounts besides my sample. I have populated the app with real messages to the accounts, posts, reminders/nudges, and authorizations. 

Sample Conversation:
![Messages](/assets/images/Assignments/A6/SampleMessage.png)

Posts on my Community Board:
![Posts](/assets/images/Assignments/A6/SamplePost.png)

Habit Tracking for Sample User:
![Habit](/assets/images/Assignments/A6/SampleHabit.png)

Authorizations Between Users:
![Authorization](/assets/images/Assignments/A6/SampleAuthorization.png)

(nudges can be found in the documents of my vercel deployment page but also periodically appear)

## 2. Task List
<table>
    <thead>
        <tr>
            <th>Title of Task</th>
            <th>Instruction to User</th>
            <th>Rationale of Task</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Create a post</td>
            <td>
                1. Register for an account and create your account. <br>
                2. Post an event, like a meetup or virtual gathering, that you'd like to share with the community. <br><br>
                <b>Follow-up:</b> Was the posting process intuitive? Did you feel that there were enough options for expressing yourself in the post? <br>
                What additional features might help you discover community events?
            </td>
            <td>
                Tests ease of use in creating and publishing posts. <br><br>
                Evaluates user ability to express themselves and interact effectively on the community board.
            </td>
        </tr>
        <tr>
            <td>Send a Message</td>
            <td>
                1. Browse the community board for an event that interests you. <br>
                2. Send a message to the host to express your interest or ask any questions. <br><br>
                <b>Follow-up:</b> Was it easy to locate and contact the event host? What could make messaging feel more welcoming? Did you encounter any limitations while messaging?
            </td>
            <td>
                Assesses ease of use and clarity in the messaging function.<br><br>
                Ensures that messaging supports seamless and comfortable interactions for elderly users.
            </td>
        </tr>
        <tr>
            <td>Track a Streak for a Habit</td>
            <td>
                1. Set up a meaningful habit to track, like a daily check-in or reminder to connect with friends.<br>
                2. Enable the automatic messaging and posting tracking feature to make the most of it!
                <br><br>
                <b>Follow-up:</b> Are reminders and tracking options useful for staying on track? What improvements could make them more effective? <br>
                Did the visual indicators encourage you to continue? <br>
            </td>
            <td>
                Aims to understand how design supports elderly users in establishing, tracking, and sustaining healthy habits. <br><br>
                Learn if the setup process is clear and features like reminders are accessible and motivating. <br><br>
                Aims to get insights into unique needs/preferences of users in how to best support establishing habits.
            </td>
        </tr>
        <tr>
            <td>Send a Nudge</td>
            <td>
                1. Send a nudge to remind another user to stay connected with friends or family. <br>
                2. Set it up so that you also receive social wellness reminders regularly. <br><br>
                <b>Follow-up:</b> Was it easy to find and send a nudge? Did sending a nudge feel meaningful for building connections? Were there any confusing aspects?
            </td>
            <td>
                Gauges user understanding and motivation for the nudge feature.<br><br>
                Identifies how nudges support connections and community engagement.
            </td>
        </tr>
        <tr>
            <td>Authorize another user</td>
            <td>
                1. Log into a prepopulated user account that has multiple authorizations. <br><br>
                <b>Username:</b> sabpdo <br>
                <b>Password:</b> password <br><br>
                2. Authorize another user to help manage your account (e.g., posting events or tracking habits).
                <br><br>
                <b>Follow-Up:</b> Was it easy assigning permissions?
                How did managing another user’s permissions make you secure that the other user was protected from security/privacy concerns?
            </td>
            <td>
                Tests user ease and comfort with authorization settings. <br><br>
                Measures understanding of privacy and security considerations when assigning permissions.
            </td>
        </tr>
    </tbody>
</table>

## 3. Study Report

### Report 1

For my first user study, I interviewed Kartik Pingle, another undergraduate at MIT (not in 6.1040). Kartik comes from a bit more of a technical background (he is a 6-3 and 8 double major). However, throughout the interview, I found many interesting behaviors as he explored.

Most surprising was his incredible struggle with Task 3, particularly with automatic tracking of messaging/posting. When he first was given the task, he was incredibly confused -- with visible frustration, he frantically pressed the tracking buttons on and off in confusion, reflecting a gap in the system's intentionality and user interpretation. Kartik speculated “Maybe it logs messaging history but I have no idea how it works or what it does”. This behavior suggests that the feature lacked clarity in both feedback and instructions, leaving users unclear on how to engage effectively with automatic tracking. Only after 5-7 minutes was he able to finally understand it’s functionality; however, this suggests a large disconnect from my intentionality for the app to be easy to use and understandable and the actual reality.

Kartik found the "Create Post" interface intuitive, noting that it resembled familiar social media layouts, but experienced friction while submitting a post. He attempted to submit by pressing "Enter," expecting an automatic submission, but nothing happened as the functionality wasn't implemented. He most likely anticipated using the “Enter” button as it reflects the common/easy way to submit items in other applications. Additionally, he mentioned that the absence of features like emojis, image uploads, and comments made the platform feel less engaging.

While attempting to contact other users, Kartik initially tried clicking on names within posts, assuming they were direct links. Upon realizing this wasn’t possible, he had to navigate the messaging feature through the top navigation bar. This interaction indicated a need for more intuitive navigation options and clearer access points for user interactions.

The “nudge” feature caused some initial confusion. While more apparent than automatic post tracking for him, he did spend some time trying to figure out its function and expressed a preference for tooltips explaining nudges' purpose. He also suggested customizability in nudges (e.g., cancellation options) to make them feel more relevant.

Kartik found the authorization feature useful, specifically appreciating password changes and message review options for authorizees. However, he was puzzled/hesitated for a bit over the title of “Authorizees”, saying the term “authorizee” was unclear. He also scrolled up and down the "Settings" page multiple times. During our debrief, he mentioned that the page felt cluttered which added to his confusion about “authorizees.” He also expected some of the items in settings to not be in settings such as “Social Wellness Notifications.”

### Report 2

For my second user study, I interviewed Brigitte Nguyen, a pharmacist in her 50s with limited experience using technology. The study aimed to understand her initial impressions of the app and to identify usability challenges that an elderly user might face when accessing it for the first time. Through our conversation, it became clear that several core features were challenging for her to understand, largely due to a lack of contextual guidance and onboarding.

Brigitte frequently asked about the purpose of the app, indicating that an introductory message or onboarding tutorial would be beneficial. Without this context, she felt unprepared to engage fully, often asking, “What is this app for?” This response underscored the need for a guided tour that clearly explains the app's goals and key features to help users feel oriented from the outset.

Brigitte also encountered obstacles when trying to use the messaging feature, which she described as “not very intuitive.” Specifically, she expected to access the messaging page of a given user by clicking directly on  the user’s name on the post; however, clicking on the username did not do anything. She likely had this expectation due to the standard linking action that most other social media apps do (e.g. in Instagram, when you click a profile on a post, it will go to that person's profile/message page).

When exploring the habit-tracking feature, Brigitte expressed confusion about its purpose, remarking, “What is this?” She was unsure how it could help her stay accountable, stating that streaks like “Apple health progress are much more motivating for me because of the bar graphs to track progress.” While Brigitte expected the habit-tracking feature to include more metrics and visualizations, the simple presence of a calendar icon didn’t clearly convey its purpose to her. Additionally, the automatic post and message buttons left her feeling completely lost regarding their functionality.

Finally, Brigitte struggled with the Nudge feature, questioning why it required such specific timestamps and how it could support meaningful connections. This feature could benefit from a practical guide explaining how and when to use nudges to foster relationships. She found it difficult to locate the wellness notifications in settings, emphasizing the importance of a cohesive in-app guide. Her observation when asked what was confusing about nudging that “it’s not a terminology issue, but things need context” highlights a consistent theme: the need for structured, context-rich guidance to support her navigation and understanding.

Brigitte’s feedback reflects common usability challenges tied to initial onboarding, feature clarity, and navigational cues.

## 4. Opportunities for Improvement


1. Clarify Habit Tracking & Nudging Functionality
    - __Level:__ Conceptual
    - __Severity:__ Major
    - __Flaw/Opportunity:__ Kartik and Brigitte’s difficulty understanding the automatic tracking feature and nudges suggests a lack of clarity in the features and their functionality/purpose. He expected immediate feedback or an explanation on how the tracking and nudging worked, leading to frustration as he tried to engage with it repeatedly without results.
    - __Why It’s Occurring:__ The habit tracking system and nudges currently lacks descriptive tooltips or onboarding instructions, resulting in confusion, especially for users unfamiliar with automatic tracking. Short labels without context can lead to misinterpretations of functionality.
    - __Proposed Solution:__ Adding a tooltip with a concise description when the user hovers over the tracking/nudging button would help set expectations. Additionally, an optional onboarding screen explaining the tracking feature upon first use could improve understanding and reduce frustration.
2. Enable "Enter" Key for Post Submission
    - __Level:__ Physical
    - __Severity:__ Minor
    - __Flaw/Opportunity:__ Kartik assumed pressing "Enter" would submit a post, a common shortcut in other applications. The lack of this shortcut led to minor friction as he had to find and click the submit button manually.
    - __Why It’s Occurring:__ The interface currently doesn’t recognize the "Enter" key as a trigger for post submission, which may be due to design oversight or differing form submission requirements.
    - __Proposed Solution:__ Integrate "Enter" as an alternate submission option for posts, aligning with standard user expectations on similar platforms. This change could streamline the posting process and reduce friction for users familiar with similar interfaces.
3. Integrate Direct Messaging from Posts
    - __Level:__ Physical
    - __Severity:__ Minor
    - __Flaw/Opportunity:__ While attempting to contact another user, both Kartik and Brigitte clicked on the username within a post, expecting it to open a direct message window. The current setup required them to navigate to the messaging feature manually, disrupting the interaction flow.
    - __Why It’s Occurring:__ The application currently lacks embedded links in posts that allow for easy redirection to messaging, likely due to a simplified initial layout design.
    - __Proposed Solution:__ Adding clickable usernames within posts that open the messaging feature directly could reduce navigational friction and streamline the user’s journey when attempting to contact others, enhancing overall ease of use.
4. Redesign Settings Page for Better Organization
    - __Level:__ Physical
    - __Severity:__ Moderate
    - __Flaw/Opportunity:__ Kartik noted that the "Settings" page felt cluttered, with excessive scrolling needed to find wellness tracking amidst other settings and to understand some of the authorization features. He also suggested that wellness tracking could be separated to improve navigation and accessibility. Similarly, Brigitte had a hard time locating the Social Wellness feature within settings.
    - __Why It’s Occurring:__ The settings are currently arranged in a single, extended list, without separation or categorization by related features, resulting in a visually overwhelming layout.
    - __Proposed Solution:__ Redesign the settings page with categorized sections or collapsible dropdowns to reduce visual clutter (perhaps aligning better by gestalt princiiples and capitalizing on fitt's law). I can also abstract some of the sections that do not fit as well to other pages (e.g. moving social wellness notifications to habit tracking). This would simplify navigation, especially for frequently used settings, making the page more user-friendly and efficient and reducing scrolling.


Questions:
1. Is it okay if it's over?
2. Confirm understanding of conceptual vs. linguistic