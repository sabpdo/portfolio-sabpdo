---
title: "Project 6: User Testing and Final Release"
layout: doc
---


# Project 6: User Testing and Final Release

## Link to Website

Link To Website: https://leftover-love.vercel.app/welcome

## Repo 

https://github.com/emilymchen/leftover-love


## Study Report

### Interview I: Luis (Focusing on Volunteer/Recipient Experiences)
My test subject was a friend in Course 6 but not in 6.104, one of the friends I used during my individual A6. He found that the three sign up buttons were self explanatory for their roles, and he created an account and logged in without any qualms, both for volunteer and for recipient, which are what we tested today. They saw the sidebar icon and were able to go to account settings to update their information without any hints, completing task one. Moving on to task 2, once logged in he returned to available donations, and effortlessly claimed for pickup. When prompted to message the donor, he went to messages first, only to find that you can’t initiate a new message from there, only continue existing conversations. He then went to my claims and found the button there. I roleplayed as the donor from my device and he saw that the messages showed up just fine. Unlike the two prior reports, unclaiming did work for him seamlessly. For task 3, he claimed an item after filtering by tags. Despite the hint text, the dropdown arrow was not immediately obvious, he was trying to type the tags first. While add tag works just fine, he suggested that we should integrate the cleaner filters in other apps, where you type and then a plus shows up at the end to add it as a filter. That is not a critical bug though, just a minor enhancement. However, he found it slightly inconsistent that when selecting from the dropdown, the tag automatically shows up, while for typing, you have to click add tag. He said that maybe the dropdown selection should appear in the text box to click add tag, while it’s one more click, it’s more consistent.

For tasks four and five, the user was able to do everything, though he said that the maps felt a little cramped and tiny in the form. “Imagine this on a phone,” he said on our laptops. Regardless, he did everything without any difficulties, and followed the intuitive flows to message the driver and track his order in the order tracker, though his gripe is that he has to manually check the donor / driver messages for a reply as there is no notification system. I tell him that a notification system would be hard to implement at this stage and would require more advanced programming. 
Moving onto volunteers, a lot of the tasks are similar to the recipients, but in the ones that differ, he liked that the pickup and delivery location and distance were clearly shown. Though he thinks the delivery requests should be sorted by distance or expiration date instead of the somewhat arbitrary order it is now, which is a valuable suggestion. He also thinks the maps should be bigger here, as they are crucial for the driver.

But aside from these suggestions, we found no serious bugs, and he was able to guide himself throughout the interface largely without hints or suggestions.

### Interview II: Nicole (Focusing on Restaurant Side)

I believe the overall test with Nicole was successful and we were able to get more insight into a Restaurant associated individual potential use of this app. Nicole is a college student whose family owns a restaurant, and she has spent large amounts of her time helping out there, so we decided to interview Nicole both as a Restaurant user and as a Recipient user. I initially asked her to create an account with his real age and then asked her to create an account as a Restaurant. Initially, she clicked on the login button, attempting to enter a username and password, but then realized after seeing the popup message that she had to create a Restaurant account. The popup message was able to help Nicole easily navigate from her initial detour and properly register her Restaurant account.

Moving on to posting donation items, Nicole was able to smoothly navigate through the functionalities of item posting. An instance where she hesitated, we when she entered two words “spicy, meat” separated by a comma as a tag in her donation post. She saw an error message popup and realized that each tag had to be entered separately as a singular word. This demonstrated that our error messages were properly placed and also informative enough for the user to know how to adjust their actions accordingly. 

Nicole was able to pick up messaging for both Restaurant and Recipient users relatively easily. She swiftly navigated to both the “my messages” tab in the sidebar as well as “message recipient” and “message driver” under each claimed post. Throughout this process, she was able to converse and answer questions smoothly from recipients and volunteers.
Moving on to the Recipient user, she gravitated towards using tags to filter the posts that were being displayed. Although she only selected tags from the dropdown bar and did not attempt to use manual input. When I asked her why she didn’t choose to do manual entry, she told me that she actually did not know that feature existed since the add tag button was a bit small. It will be important for us to consider tweaking the UI to make it more obvious to the user that both manual entry and dropdown selection are viable options for adding tags for donation filtering. 

Overall, Nicole had a positive user experience and could see her family possibly using this app from time to time.


## Opportunities for Improvement

1. Add Tag Donations Filtering Clarity
    - Make add tag for filtering more intuitive that both dropdown and manual entry are possible 
    - __Level:__ Linguistic
    - __Severity:__ Moderate
    - __Flaw/Opportunity:__ Throughout Nicole’s user testing, she was unaware of the existence of manual tag entry, and only used the dropdown to add items to filter. During Andy’s and Luis’s user testing, we noticed the opposite: he only used the manual input and was not aware that the dropdown was an option. Making that apparent is helpful for users to easily interchange between the two tag input options. 
    - __Why Its Occuring:__ The current way to add tags for donations filtering (on the recipient side) is presented as “Input tags to filter by (one word)” with a dropdown icon located next to it in the same entry box. Recipient user types can choose to manually type a tag into the box and then click the “Add Tag” button to add the tag to filters. Alternatively users could click the dropdown button and select a tag they are interested in including in filters. 
    - __Future Design:__ It is important for the users to be able to easily and quickly realize that there are two options for adding tags. We will change the working for manual input to “Type or select tags to filter by (one word)”. We also will provide users the alternative option to hit Enter after entering a tag. Additionally, to facilitate the process for entering in options, we incorporated a suggestions popup bar upon input typing that users could click.

2. Ensure censored password for the account has the correct number of characters.
    - __Level:__ Physical
    - __Severity:__ Minor
    - __Flaw/Opportunity__: When Andy tried to update his password in the account settings, he attempted to recall his old password by counting the number of characters in the censored placeholder. However, he soon realized that the placeholder was hardcoded and did not reflect the actual length of his password, leading to confusion while resetting his password (since you need the old password to reset the new password).
    - __Why Its Occurring:__ The account settings currently displays a censored string (*********) in the section where the user updates their password. However, this string is currently hard-coded to be the same length, so it isn’t dependent on the actual length of the user’s current password.
    - __Future Design:__ Since it is confusing for users who have passwords that are shorter or longer than the hard-coded length, we will update the censored string to match the length of the user’s current password.

3. Button Ordering to Increase User Experience Intuition
    - Place buttons in order of importance from right to left, since users instinctively navigate to the bottom right of a modal to complete actions
    - __Level:__ Physical
    - __Severity:__ Minor 
    - __Flaw/Opportunity:__ Throughout the interview with Andy, we saw that his gut instinct was to keep moving the bottom right of the modal (e.g. the add/edit post modal) to complete the action (e.g. posting). However, the current design afforded such that the modal had the ‘close’ button instead at the bottom right which was not his expected/gut reaction button he had expected to click. Thus, switching around the order of the buttons will better align with the user's expectations.
    - __Why Its Occuring__: Buttons are currently not placed in order of importance for many modals. For example, the ‘cancel’ button is placed to the rightmost location instead of the core action related to the modal.
    - __Future Design:__ Since users naturally gravitate to the bottom right of a modal when completing actions, we will update the button placement to be in order of importance from right to left to minimize friction when looking for default actions. We thus rearranged all our modals to have buttons rearranged in increasing order of importance (e.g. switching [`cancel`, `save`, `delete`] to [`cancel`, `delete`, `save`].

4. Prepopulate My Messages with Individuals involved in Order Process 
    - __Level:__ Conceptual/Physical
    - __Severity:__ Moderate
    - __Flaw/Opportunity__: When first given the task for messaging the donor/volunteer, Andy had struggled to complete the task. He first navigated to the messages tab instead of my claims and expected to see the restaurant in the messages tab users list but did not and was confused where to go from there.
    - __Why Its Occuring:__ The messages page is currently only a page where you can continue conversations initiated in the recipient claims / volunteer deliveries pages, and not initiate new ones. We did this to control against the ability to message everyone on the app. However, this means that individuals in the order process do not show in messages until you start a conversation with them through the unnatural modals, which can only be found in the claim / delivery pages.
    - __Future Design:__ Aside from querying all users with past conversation history, the messages view can also query the current donor and driver and put them at the top of the stack with (Driver) and (Donor) parentheses for easy retrieval, regardless of whether they have a message history or not. However, if there are multiple simultaneous claims by the same user, it would be rough to include many Drivers and Donors that can’t be told apart from each other, so this is not an easy fix either.

5. Make the add button color more intuitive
    - __Level__: Linguistic
    - __Severity__: Moderate
    - __Flaw/Opportunity__: All users initially stated that the add button’s color was a bit unintuitive, as it resembled more of a delete button.
    - __Why Its Occuring__: The color red is usually associated with actions like deletion, which doesn’t match the function of the add button. However, our add button was previously dark-orange, which made it resemble the delete button. Also, the delete button was also red as well which added to the confusion.
    - __Future Design__: We will change our add button to be pink instead of red, which still fits within the overall color scheme of our app, while also not confusing users by looking too similar to the style of a delete button.


## Design Revisions

### Change I: Limits on Quantity of Food in Food Posting
__Updated Design:__
Previously, the `quantity` parameter in Posting was unrestricted. While we retained `quantity` as a state parameter, we implemented a cap of 5 for its maximum value, preventing users from inputting a number greater than 5 for `quantity.`During the design process, we faced two primary options: (1) cap the `quantity` value or (2) allow users to specify any number, with the option for recipients to claim subsets of the total quantity (e.g., multiple people claiming portions of a single post).

__Reasoning:__
We chose the first option for two key reasons:

- Implementation simplicity: Capping the value to 5 was more feasible within our project timeline, avoiding the complexity of managing multiple claims per post.

- Focus on small-scale restaurants/donors: We decided to shift our focus/target audience to smaller restaurants, which, as revealed through interviews, face fewer legal challenges than larger corporations and typically deal with smaller portions. Because they face fewer legal challenges, they are also more likely to engage with the application compared to larger established corporations.

While this limitation narrows the potential scale of individual donations, it strengthens the case for our app’s focus on serving small businesses and promoting sustainability at a community level.

### Change II: Adding Instructions as a State for Claiming
__Updated Design:__
In our initial design, we did not include `instructions` as a state for claiming. However, we have now added this feature, allowing recipients to provide specific instructions (e.g., "leave it at the door") when requesting a delivery.

__Reasoning:__
During development, we recognized that including an `instructions` parameter would enhance user experience by offering recipients greater flexibility and clarity in specifying delivery preferences. This feature aligns with the functionality of similar applications, such as DoorDash, which improves familiarity and usability for users.


### Change III: Removal of `delivery_time` as a State for Delivering
__Updated Design:__
In our initial design, `delivery_time` was included as a state for Delivering. However, we removed it during implementation due to practical and usability considerations. The app now relies solely on the inherent `expiration_time` associated with each food donation.

__Reasoning:__
We identified several issues with including `delivery_time`:
- Redundant information: Each donation already has an expiration time, making a separate `delivery_time` parameter unnecessary and adding unnecessary complexity to the interface. We also have a messaging feature, which makes it easier for the volunteer and recipient to communicate and agree on an established delivery time.

- Deciding who determines the delivery_time poses significant challenges. Assigning this responsibility to restaurants is impractical since their involvement ends after food pickup. Similarly, requiring recipients to set delivery times could lead to unrealistic expectations and scheduling conflicts for volunteers.

- Volunteer experience: Allowing recipients to specify arbitrary or inconvenient delivery times could deter volunteers from participating, undermining their critical role in the app's success.

This modification simplifies the app’s design, reduces cognitive load for users, and ensures the process remains practical for all those who use the app.

### Change IV: Adding Preset Tags to Select On Top of Self Defined Tags for Filtering
__Updated Design:__
In our initial design, we did not include a series of the most common preset tags for recipient users to select from to filter their available donations. We have now added this preset tags feature as an add on to the previously established self defined tags.

__Reasoning:__
In the feedback we received from the previous assignment, we realized that adding another easy and efficient way for recipient users to add tags for filtering would greatly improve the user experience. This offers users greater sense of flexibility and increases efficiency, allowing users to directly select from a list of commonly appearing tags.


### Change V: Removing Image Upload for Food Postings
__Updated Design:__
In our initial design, we had food donors upload an image while posting food, which would then be displayed in the feed along with other details about a food listing. We have removed image uploading, so instead, the food name and details are the only things displayed in the feed.

__Reasoning:__
We wanted to reduce the amount of friction for donors to list food as much as possible, and for restaurants who may be listing tens of plates of food, having to take pictures for each of these items would be tedious and time-consuming. Additionally, it allows us to display more useful information such as the food’s tags and expiration time in a more compact manner.

### ~Changes from Beta Release~

### Change VI: Allow Enter Button for Adding Tags

__Updated Design:__
In our initial design, when the user has selected the tag input text box and presses enter, the food listing will post rather than adding the tag the user had input into the box. We updated this so that users can press the enter button after typing in a tag, and the tag gets added to the food listing, rather than posting altogether.

__Reasoning:__
During our user tests, we found that users would often instinctively press enter after they had finished typing in something like a tag, which resulted in them posting food listings prematurely before they had finished adding all the tags they wanted to. Allowing users to press enter to add tags rather than having to click the ‘add tag’ button makes posting food more efficient.

### Change VII: Clarify Filter Tags Component (by adding suggested tags and changing the wording)

__Updated Design:__
In our initial design, when recipients were filtering food listings by tags, the wording of the text input said “Input tags to filter by (one word)” along with a dropdown arrow on the side. We updated this wording to instead read “Type or select tags to filter by (one word)”. Additionally, as users type tags, we show suggested tags based on the initial characters they write (e.g. if they type “veg”, we suggest “vegetarian” or “vegan” in the dropdown). 

__Reasoning:__
During our user tests, we found some users were confused by the wording and thought that they could only use the dropdown menu to add tags to filter by, rather than being able to add their own custom tags as well. By updating this wording, we made it more clear to our users that they have two options for adding tags to filter posts. Additionally, by adding the suggested tags, we save time for users who see the option they’re looking for so they don’t have to type out the whole tag each time.

### Change VIII: Prepopulate Messages Tab With Order-Related Users

__Updated Design:__
We adjusted our messages tab to also allow recipients to message other users (e.g. drivers/donors) that they had not messaged before but was either a driver or a donor associated with their claim.

__Reasoning:__
In our user interviews, we found that it was frustrating to not be able to start new conversations with relevant users in the messages tab, and thus incorporating it into the tab made it more convenient. While that messaging functionality was available in the claim tab, incorporating this into the messaging tab as well makes it more accessible/visible.

### Change IX: Fix Delete Account Functionality

__Updated Design:__
Our initial delete account endpoint just removed the given user from the database, but didn’t delete the associated posts/claims/deliveries/messages. We updated this endpoint to remove these entries as well so that there are no items that are dependent on the removed user.

__Reasoning:__
When we deleted accounts that had previously made posts, it caused errors in other existing users’ pages since the endpoints returning any claims or deliveries or messages with that deleted user would throw errors. Updating this fixed these errors and made the app more stable.

### Change X: Add nut-free/contains nuts for food as a dropdown filter

__Updated Design:__
Our initial list of default tags did not include “nut-free”. We added a new default tag, “nut-free”, in the dropdown filter. 

__Reasoning:__
We received feedback from our user tests that our list of default tags was missing “nut-free”, which is a very common allergy/food restriction. We added this tag so as to better accommodate as many people with our app as possible. 

### Change XI: Changed censored password to same number of characters as the original password

__Updated Design:__
In our initial design, the censored password preview in the account settings displayed a hardcoded number of asterisks rather than a number of asterisks matching the number of characters actually in the password. We updated this to instead match the number of asterisks with the length of the user’s current password.

__Reasoning:__
When users go to update their password, seeing a hardcoded censored password that doesn't match the number of characters they are expecting in their password causes confusion, since you need your old password to create a new password. Updating the censored password to match the number of characters makes the design less confusing and more intuitive for users, since they are also able to see more visual confirmation that their password gets correctly updated when the length of this censored password changes.

### Change XII: Reorder buttons at the end of modal in increasing importance
__Updated Design:__
Modals now arrange buttons in order of importance from right to left to better align with user expectations. For example, buttons previously ordered as [cancel, save, delete] will be updated to [cancel, delete, save]. This ensures the primary action (e.g., save) is placed at the bottom-right corner of the modal, where users instinctively look to complete actions.

__Reasoning:__
We noticed users’ natural inclination to click the bottom-right button to complete actions (e.g., posting). However, the current design places the close button in that position, leading to confusion. By rearranging buttons to prioritize core actions, we reduce friction and better align with user expectations.

### Change XIII: Sort delivery requests by distance or expiration date

__Updated Design:__
Previously, delivery requests were displayed in the order they were populated. In our updated design, requests are now sorted by expiration date by default, with the soonest-to-expire requests appearing first.

__Reasoning:__
Sorting by expiration date ensures a more intuitive and efficient experience when searching through delivery requests. Prioritizing requests based on their proximity to expiration makes it easier to identify and address the most urgent tasks promptly. Additionally, this change supports better decision-making by emphasizing requests that require immediate attention


### Change IXX: Change button colors to better reflect functionality
__Updated Design:__
The add button color was changed from dark-orange to pink. This adjustment maintains the app’s overall color scheme while distinguishing the add button from the delete button.

__Reasoning:__
Users reported that the dark-orange add button closely resembled the red delete button, causing confusion since red typically signifies deletion actions. By switching to pink, the add button becomes more intuitive and clearly differentiates its function from deletion.



## Demo Video Link

https://drive.google.com/file/d/1HmPJTvV0oKi3eDhTaHSeDtDwsRJx5A4O/view?usp=sharing