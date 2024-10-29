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
                Register for an account and create your account! <br>
                Then advertise an upcoming event that you would like to broadcast to the community, such as a local meetup or an online meeting. <br>
                Follow-up: Did you find the posting process intuitive? What are some limitations that you feel exist in the post creation and expressing yourself in the post? What are some additional features that would make it easier to find community events?
            </td>
            <td>
                Tests the ease of use and accessibility in the posting process. <br>
                Assesses if users have enough creative control/personal expression/engagement on the community board.
            </td>
        </tr>
        <tr>
            <td>Send a message to another user whose event you are interested in</td>
            <td>
                Browse the community board for an event that interests you. When you find one, send a message to the host expressing your interest in attending. Share any questions or details you’d like to know about the event. <br>
                Follow-ups: Was it easy to find and contact the event host? What would make this interaction more welcoming/helpful for you? What are some limitations that you feel exist in the messaging process?
            </td>
            <td>
                Tests ease of use and clarity of messaging function, ensuring it meets the needs of elderly users for seamless and comfortable interactions. <br>
                Tests extent users are able to connect with other users through messaging.
            </td>
        </tr>
        <tr>
            <td>Record a Streak-Tracked Habit</td>
            <td>
                Set up a habit you'd like to track, like a daily check-in or reminder to connect with friends or stay active. Choose something meaningful to you, and start tracking your progress. <br>
                Activate and enable the automatic messaging/posting tracking feature. Take advantage of this feature then!
                <br>
                Follow-ups: To what extent do you feel that reminders and tracking options are helpful for staying on track? If not, what would make them more useful? What limitations exist in the tracking of habits? <br>
                How motivating do you find the progress indicators or streak visuals? Do they encourage you to keep up with your habit? <br>
                Is there any way we could make it easier or more rewarding to mark each habit as complete? Are there any additional habit options or customization choices you would find helpful?
            </td>
            <td>
                Aims to understand how design supports elderly users in establishing, tracking, and sustaining healthy habits. <br>
                Learn if the setup process is clear and features like reminders are accessible and motivating. <br>
                Aims to get insights into unique needs/preferences of users in how to best support establishing habits.
            </td>
        </tr>
        <tr>
            <td>Send a Social Wellness Nudge</td>
            <td>
                Send a nudge to another user. A nudge will remind them to message/stay connected with family and friends 2 days in the future. <br>
                Set it up so that you also send social wellness reminders. <br>
                Follow-ups: How easy was it for you to find and send a social wellness nudge? To what extent did you feel that sending a nudge allowed you to improve your connection/support of others? Were there any limitations/confusing aspects in sending nudges?
            </td>
            <td>
                Tests if users understand the purpose and value of sending nudges. <br>
                Gauges whether users feel motivated to use the feature. <br>
                Tests can uncover how nudges allow users to foster connection and support.
            </td>
        </tr>
        <tr>
            <td>Authorize another user</td>
            <td>
                Log into a prepopulated user account that has multiple authorizations. <br>
                Username: sabpdo <br>
                Password: password <br>
                Authorize another user/caregiver who can help you manage your account, such as posting events or tracking habits. <br>
                Follow-Ups: How control the permissions on another user’s account. <br>
                Follow-Ups: How comfortable did you feel assigning permissions? How did managing another user’s permissions make you secure that the other user was protected in terms of security/privacy concerns?
            </td>
            <td>
                Tests ease of use of authorization features. <br>
                Determines users’ extent of understanding/familiarity of the purpose and functionality of authorizations. <br>
                Tells extent users feel that they are able to maintain/assert privacy and security over their own account and another account through authorizations.
            </td>
        </tr>
    </tbody>
</table>

## 3/4 Study Report & Opportunities for Improvement

### Report 1

#### Study Report

For my first user study, I interviewed Kartik Pingle, another undergraduate at MIT (not in 6.1040). Kartik comes from a bit more of a technical background (he is a 6-3 and 8 double major). However, throughout the interview, I found many interesting behaviors as he explored.

Most surprising was his incredible struggle with Task 3, particularly with automatic tracking of messaging/posting. When he first was given the task, he was incredibly confused -- with visible frustration, he frantically pressed the tracking buttons on and off in confusion, reflecting a gap in the system's intentionality and user interpretation. Kartik speculated “Maybe it logs messaging history but I have no idea how it works or what it does”. This behavior suggests that the feature lacked clarity in both feedback and instructions, leaving users unclear on how to engage effectively with automatic tracking. Only after 5-7 minutes was he able to finally understand it’s functionality; however, this suggests a large disconnect from my intentionality for the app to be easy to use and understandable and the actual reality.

Kartik found the "Create Post" interface intuitive, noting that it resembled familiar social media layouts, but experienced friction while submitting a post. He attempted to submit by pressing "Enter," expecting an automatic submission, but nothing happened as the functionality wasn't implemented. He most likely anticipated using the “Enter” button as it reflects the common/easy way to submit items in other applications. Additionally, he mentioned that the absence of features like emojis, image uploads, and comments made the platform feel less engaging.

While attempting to contact other users, Kartik initially tried clicking on names within posts, assuming they were direct links. Upon realizing this wasn’t possible, he had to navigate the messaging feature through the top navigation bar. This interaction indicated a need for more intuitive navigation options and clearer access points for user interactions.

The “nudge” feature caused some initial confusion. While more apparent than automatic post tracking for him, he did spend some time trying to figure out its function and expressed a preference for tooltips explaining nudges' purpose. He also suggested customizability in nudges (e.g., cancellation options) to make them feel more relevant.

Kartik found the authorization feature useful, specifically appreciating password changes and message review options for authorizees. However, he was puzzled/hesitated for a bit over the title of “Authorizees”, saying the term “authorizee” was unclear. He also scrolled up and down the "Settings" page multiple times. During our debrief, he mentioned that the page felt cluttered which added to his confusion about “authorizees.” He also expected some of the items in settings to not be in settings such as “Social Wellness Notifications.”


#### Opportunities for Improvement


1. Clarify Habit Tracking & Nudging Functionality
    - __Level:__ Conceptual
    - __Severity:__ Major
    - __Flaw/Opportunity:__ Kartik’s difficulty understanding the automatic tracking feature and nudges suggests a lack of clarity in the features and their functionality/purpose. He expected immediate feedback or an explanation on how the tracking and nudging worked, leading to frustration as he tried to engage with it repeatedly without results.
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
    - __Flaw/Opportunity:__ While attempting to contact another user, Kartik clicked on the username within a post, expecting it to open a direct message window. The current setup requires him to navigate to the messaging feature manually, disrupting the interaction flow.
    - __Why It’s Occurring:__ The application currently lacks embedded links in posts that allow for easy redirection to messaging, likely due to a simplified initial layout design.
    - __Proposed Solution:__ Adding clickable usernames within posts that open the messaging feature directly could reduce navigational friction and streamline the user’s journey when attempting to contact others, enhancing overall ease of use.
4. Redesign Settings Page for Better Organization
    - __Level:__ Physical
    - __Severity:__ Moderate
    - __Flaw/Opportunity:__ Kartik noted that the "Settings" page felt cluttered, with excessive scrolling needed to find wellness tracking amidst other settings and to understand some of the authorization features. He also suggested that wellness tracking could be separated to improve navigation and accessibility.
    - __Why It’s Occurring:__ The settings are currently arranged in a single, extended list, without separation or categorization by related features, resulting in a visually overwhelming layout.
    - __Proposed Solution:__ Redesign the settings page with categorized sections or collapsible dropdowns to reduce visual clutter (perhaps aligning better by gestalt princiiples and capitalizing on fitt's law). I can also abstract some of the sections that do not fit as well to other pages (e.g. moving social wellness notifications to habit tracking). This would simplify navigation, especially for frequently used settings, making the page more user-friendly and efficient and reducing scrolling.


### Report 2

#### Study Report

#### Opportunities for Improvement


Questions:
1. Is it okay if it's over?
2. Confirm understanding of conceptual vs. linguistic