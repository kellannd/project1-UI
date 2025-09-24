Deployed [here](https://68d35fc7b7cbbeb63d84d2fb--reading-journal-project.netlify.app/)<br>
Video [here](https://drive.google.com/file/d/1prfWGTjAwwIvC0PbyeEQvLfYNOBUSaWM/view?usp=sharing)

# What is this project?
This is a journal for a user to track their reading. As they continue to complete their goals, they will earn a "painting" to put in their digital gallery.

# Interface
## Current User Features
### User Info
The user can hover over the user icon and see their info.<br>
<img src="/journal-project/static/screenshots/Screenshot 2025-09-23 233359.png" height="400px"><br>

### Adding a new Journal Entry
If the user wants to create a new journal entry, they can click on the "I read today!" button. This will open a popup for the new journal entry.<br>
<img src="/journal-project/static/screenshots/image-9.png" height="400px"><br>

The user can pick the book they want to journal about, or enter a new book.<br>
<img src="/journal-project/static/screenshots/Screenshot 2025-09-23 213307.png" height="400px"><br>

If the user wants to enter a new book, the view will change to allow the user to enter the title, author, and page count.
<img src="/journal-project/static/screenshots/image-10.png" height="400px"><br>

After the user clicks "Add new book" the user will then be able to add a journal entry for the new book they added.
<img src="/journal-project/static/screenshots/image-11.png" height="400px"><br>

The user will see the new book they entered show up in their "Currently Reading" section.
<img src="/journal-project/static/screenshots/image-12.png" height="400px"><br>

If the user selects a book they are currently reading, then they will just get the journal entry section.
<img src="/journal-project/static/screenshots/image-13.png" height="400px"><br>

The progress bar for the currently reading books will also update with the new journal entries.
<img src="/journal-project/static/screenshots/image-15.png" height="400px"><br>

The new journal entries will also show up under the "Journal Entries" section.
<img src="/journal-project/static/screenshots/image-14.png" height="400px"><br>

If the user is making a new journal entry when they finish a book, they can mark the book as finished. This will update the Reading Goal section, as well as give the user a new "painting" for their "gallery".
<img src="/journal-project/static/screenshots/image-16.png" height="400px"><br>
<img src="/journal-project/static/screenshots/image-17.png" height="400px"><br>

### View a Journal Entry
The home pages shows the user the 5 most recent journal entries. To view any journal entry, click on the title of the book.
<img src="/journal-project/static/screenshots/image.png" height="400px"><br>

A view with the journal entry opens in a popup. Click the 'X' at the top of the screen to exit the view.
<img src="/journal-project/static/screenshots/image-1.png" height="400px"><br>

### Edit a Journal Entry
To edit a journal entry, click the pencil symbol in the top right corner of the journal entry you want to edit. A popup will open and will allow you to edit and update the entry. Note that you can only update the pages to and message entry, not the title or pages from.
<img src="/journal-project/static/screenshots/image-8.png" height="400px"><br>

### View and Change Overall Reading Goal
This is the user's main goal view. Here, you can see the user's reading goal for the year along with a progress bar.
<img src="/journal-project/static/screenshots/image-6.png" height="400px"><br>

If the user wants to change their goal, they can click "Change your goal" which will open a popup where the user can enter a new goal.
<img src="/journal-project/static/screenshots/image-3.png" height="400px"><br>

The goal view will update with the user's new goal.
<img src="/journal-project/static/screenshots/image-4.png" height="400px"><br>

### Add Custom Reading Goals
If the user clicks "+New goal" a popup will open where a user can enter a new custom goal.
<img src="/journal-project/static/screenshots/image-5.png" height="400px"><br>

When the user submits the new goal, their custom goal list will update.
<img src="/journal-project/static/screenshots/image-6.png" height="400px"><br>

### Gallery
The user can hover over the info symbol next to the gallery header to get info about what the "Gallery" is and how you can earn "paintings".
<img src="/journal-project/static/screenshots/Screenshot 2025-09-23 211151.png" height="400px"><br>

You can click on the Gallery and it would theoretically open a new page for the user to view all of their "paintings". However, for now it displays an alert.
<img src="/journal-project/static/screenshots/image-7.png" height="400px"><br>

New paintings earned will also populate in your gallery.
<img src="/journal-project/static/screenshots/image-18.png" height="400px"><br>

# Design Work
## Interview
I have interviewed 2 people so far that I know casually use other reading trackers, such as Goodreads. I asked them what they like and don’t like in the current tracker that they use. One person indicated that they would like a way to track goals other than book count and would like to create custom goals. They also indicated that having some kind of reward system would make them more likely to log in the journal.

Interview Questions:
What do you currently use to track your reading for the year?
What would be the most important things you would want tracked?
What is the most important element that you look for in a UI?

## Sketching
Sketches can be found [here](/journal-project/static/sketches/)

## Feedback
I originally went with a brighter styling for my website (using an off-white background and brighter accent colors). However, I got some feedback from some of the people I originally interviewed, and they suggested a more muted color scheme. They also suggested a darker background to give it more of an "art gallery" feel.

# Implimentation
Svelte-Kit was used to create the base for this app and was hosted on Netlify.

The [Rijksmuseum API](https://github.com/Rijksmuseum/rijksmuseum.github.io/tree/master) was used to access these paintings from [The Collection](https://www.rijksmuseum.nl/en/collection).

## Styling
All icons used were taken from [Bootstrap Icons](https://icons.getbootstrap.com/).

Styling for text input boxes, popups, and overlays inspired by [w3schools](https://www.w3schools.com/css/default.asp).

# Future Work
One item I tried to include was the ability to search for a book rather than having to manually enter all of the details. However, the API I was using stopped working and I did not have time to fix the feature. This would be one of the first things I would fix in the future.

In addition, there are certain features that, while would work, do not currently have any functionality. An example of this is the "see older entries" button on in the "Journal Entries" section. Currently, this button just triggers an alert that tells the user what this button would do. These are features I would take the time to go in and add actual functionality to.




