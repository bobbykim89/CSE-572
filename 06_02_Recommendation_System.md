# RECOMMENDATION SYSTEM
Usage of deep learning...

- Movie/video recommendation system (youtube, netflix, etc)

User profile may include
- age
- gender
- preferences

the **user profile** gathers **usage history** such as:
- what movies watched?
- how long did you watch?
- rating?
- if series... what season you are at?

And it gains knowledge about your preferences <u>**without explicitly asking you**</u>.

It <u>**_changes dynamically_**</u>... your tastes change.

Youtube only cares about video view history... and that's it. Netflix does a more comprehensive search.

- Youtube will provide a list of videos **ranked in a specific order.**
- Netflix will provide a list of videos **in a specific categorization**

## Cold start problem
Very important problem in any recommendation subsystem.
- user based: user creates an account (profile available), but usage history not available. What will you show on first page?
  - You can match the user profile with millions of other users... you can use deep learning systems.
- Item based: new movie is released, to who do I recommend the movie? 
  - You don't have ratings for this movie because no watch history available.
  - you take characterisitics of item and select salient features and match with other items.
  - you only recommend movie to the users that liked similar movies... millions of data, use deep learning.

