<script>

  import Header from "../lib/assets/Header.svelte";


  // import user from "../data/user.json";

  // import books from "../data/test.json";

  let books = $state({
    books: [
      {
        title: "Emma",
        author: "Jane Austen",
        isbn: "9780141439587",
        pages: 512,
        readStatus: "read",
        currentPage: 100,
        coverURL: "https://covers.openlibrary.org/b/isbn/9780141439587-M.jpg",
      },
      {
        title: "Little Women",
        author: "Louisa May Alcott",
        isbn: "9780140390698",
        pages: 504,
        readStatus: "read",
        currentPage: 300,
        coverURL: "https://covers.openlibrary.org/b/isbn/9780140390698-M.jpg",
      },
      {
        title: "Pride and Prejudice",
        author: "Jane Austen",
        isbn: "9780141439518",
        pages: 435,
        readStatus: "currentlyReading",
        currentPage: 200,
        coverURL: "https://covers.openlibrary.org/b/isbn/9780141439518-M.jpg",
      },
    ],
  });

  let user = $state({
    "name": "Kelly Deal",
    "accountCreated": "",
    "goal": 0,
    "customGoals": [
        "Read a sequel",
        "Finish a series",
        "Read 5 Non Fiction Books"
    ]
});

let journalEntry = $state({
    "journalEntry": [{
        "id": 1,
        "bookTitle": "Little Women",
        "date": "9/1/2025",
        "pagesFrom": "25",
        "pagesTo": "55",
        "message": "test1"
    },
    {
        "id": 2,
        "bookTitle": "Little Women",
        "date": "9/2/2025",
        "pagesFrom": "55",
        "pagesTo": "125",
        "message": "test2"
    },
    {
        "id": 3,
        "bookTitle": "Little Women",
        "date": "9/3/2025",
        "pagesFrom": "125",
        "pagesTo": "160",
        "message": "test3"
    },
    {
        "id": 4,
        "bookTitle": "Emma",
        "date": "9/4/2025",
        "pagesFrom": "1",
        "pagesTo": "25",
        "message": "test4"
    },
    {
        "id": 5,
        "bookTitle": "Little Women",
        "date": "9/4/2025",
        "pagesFrom": "160",
        "pagesTo": "175",
        "message": "test2"
    }
    ]
}
);

  function getDate() {
    let today = new Date();

    let month = today.getMonth()

    let day = today.getDate()

    let year = today.getFullYear()

    return (month + 1) + "/" + day + "/" + year
  }

  getDate()

  let isOverlayVisHidden = $state(true);

  let readingGoal = 20;

  let isGoalVisHidden = $state(true);

  let isCustomGoalVisHidden = $state(true);

  let isNewEntryHidden = $state(true);

  let custom_goals = user.customGoals;

  function toggleGoalVis() {
    isGoalVisHidden = !isGoalVisHidden;
  }

  let updateGoal = "";

  function newGoal() {
    if (updateGoal != readingGoal) {
      readingGoal = updateGoal;
    }
  }

  function progressBar() {
    let count = 0;
    for (let i = 0; i < books.books.length; i++) {
      if (books.books[i].readStatus == "read") {
        count++;
      }
    }

    return count;
  }

  let update_progress_bar = (progressBar() / readingGoal) * 100;
  function updateProgressBar() {
    update_progress_bar = (progressBar() / readingGoal) * 100;
  }

  function currentlyReading() {
    let currentlyReading = [];

    for (let i = 0; i < books.books.length; i++) {
      if (books.books[i].readStatus == "currentlyReading") {
        currentlyReading.push(books.books[i].title);
      }
    }

    return currentlyReading;
  }

  let isNewJournalEntryHidden = $state(true);

  function toggleJournalEntryVis() {
    isNewJournalEntryHidden = !isNewJournalEntryHidden;
  }

  let bookTitle = "";
  console.log(bookTitle);

  let booksCurrent = currentlyReading();

  let selected = "";

  let isNewBookHidden = $state(true);

  function toggleNewBookEntryVis() {
    isNewBookHidden = !isNewBookHidden;
  }

  let isEditJournalEntryVis = $state(true);

  let bookTitleTest = "";

  function editJournalEntry(journalEntry) {
    console.log("edit");

    document.querySelector("#journalEntryBookTitle").value =
      journalEntry.bookTitle;
    document.querySelector("#journalEntryPagesFrom").value =
      journalEntry.pagesFrom;
    document.querySelector("#journalEntryPagesTo").value = journalEntry.pagesTo;
    document.querySelector("#journalEntryMessage").value = journalEntry.message;

    isEditJournalEntryVis = !isEditJournalEntryVis;
    isOverlayVisHidden = !isOverlayVisHidden;
  }

  let isbn = "";

  let newBookEntry = {
    title: "",
    author: "",
    pageCount: "",
    readStatus: "",
    progress: "",
  };

  let new_journal_entry = {
          "id": 1,
        "bookTitle": "",
        "date": "",
        "pagesFrom": "",
        "pagesTo": "",
        "message": ""
  }

  let newJournal

  function search() {
    console.log(isbn);

    //let entry = newBookEntry;

    let request = "https://openlibrary.org/isbn/" + isbn + ".json";
    fetch(request, {
      mode: "cors",
    })
      .then((response) => {
        if (!response.ok) {
          throw new Error(`HTTP error ${response.status}`);
        }
        return response.json();
      })
      .then((responseData) => {
        newBookEntry.pageCount = responseData.pagination;
        newBookEntry.title = responseData.title;
      });

    request = "https://openlibrary.org/search.json?q=" + isbn + ".json";
    fetch(request, {
      mode: "cors",
    })
      .then((response) => {
        if (!response.ok) {
          throw new Error(`HTTP error ${response.status}`);
        }
        return response.json();
      })
      .then((responseData) => {
        newBookEntry.author = responseData.docs[0].author_name[0];
      });

    console.log(newBookEntry);
  }

  function manualEntry() {
    newBookEntry.readStatus = "currentlyReading";
    newBookEntry.progress = 0;

    console.log(newBookEntry);

    books.books.push(newBookEntry)
  }

  function newCustomGoal() {
    console.log("new custom goal");
  }
</script>

<main style="background-color: #efefef">
  <header>
    <Header />
  </header>

  <container style="padding: 20px;">
    <div class="mainView" style="background-color: #efefef">
      <div class="newJournalEntry">
        <h2>New Journal Entry</h2>
        <!-- <a href="/journal-entry/new"><button>I read today!</button></a> -->
        <button class="main-btn" onclick={toggleJournalEntryVis}
          >I read today!</button
        >
        <div
          hidden={isNewJournalEntryHidden}
          style="
                        position: absolute;
                        top: 0;
                        left: 0;
                        width: 500px;
                        height: 550px;
                        margin-top: 80px;
                        /* height: calc(100% - 80px);*/
                        z-index: 100;
                        background-color: cornflowerblue"
        >
          <label for="bookTitle">Book:</label><br />

          <select
            bind:value={selected}
            onchange={() => {
              console.log(selected);
              if (selected == "newBook") {
                isNewBookHidden = false;
                isNewEntryHidden = true;
              } else if (selected != "") {
                isNewBookHidden = true;
                isNewEntryHidden = false;
              } else {
                isNewBookHidden = true;
                isNewEntryHidden = true;
              }
            }}
          >
            <option value="">Select...</option>
            <option value="newBook">I started a new book</option>
            {#each booksCurrent as book}
              <option value={book}>{book}</option>
            {/each}
          </select><br />

          <div hidden={isNewBookHidden}>
            <!-- <input type="text" bind:value={isbn} /><button onclick={search}
              >Submit</button
                                ><br /> -->

            <!-- <input type="text" bind:value={newBookEntry.title} /> -->
            <label>Title:</label><br />
            <input type="text" bind:value={newBookEntry.title} /><br />

            <label>Autor:</label><br />
            <input type="text" bind:value={newBookEntry.author} /><br />

            <label>Page Count:</label><br />
            <input
              style="width: 300px"
              type="int"
              bind:value={newBookEntry.pageCount}
            /><br />

            <button
              class="main-btn"
              onclick={() => {
                manualEntry();
                isNewBookHidden = true;
                isNewEntryHidden = false;
              }}>Add New Book</button
            >
          </div>

          <div hidden={isNewEntryHidden}>
            <h3>New Journal Entry for {newBookEntry.title}</h3>
            <div
              style="display: grid; grid-template-columns: 1fr 1fr; max-width: 300px"
            >

              <div style="grid-column: 1;">
                <label>Pages From:</label><br />
                <input id="newEntryPagesFrom" type="int" /><br />
              </div>
              <div style="grid-column: 2; padding-left: 10px">
                <label>Pages To:</label><br />
                <input id="newEntryPagesTo" type="int" /><br />
              </div>
            </div>
            <label>Message:</label><br />
            <textarea id="newEntryMessage"></textarea><br />
            <button onclick={() => {
              new_journal_entry.bookTitle = newBookEntry.title
              new_journal_entry.pagesFrom = document.querySelector("#newEntryPagesFrom").value
              new_journal_entry.pagesTo = document.querySelector("#newEntryPagesTo").value
              new_journal_entry.message = document.querySelector("#newEntryMessage").value
              new_journal_entry.date = getDate()

              console.log(new_journal_entry)

              journalEntry.journalEntry.push(new_journal_entry)
            }}>Submit</button>
          </div>
        </div>
      </div>

      <div class="currentlyReading">
        <h2>Currently Reading</h2>
        <div class="bookDetails">
          {#each books.books as book}
            {#if book.readStatus == "currentlyReading" && books.pagesFrom}
              <div class="bookCover">
                <img src={book.coverURL} style="height: 150px" />
              </div>

              <div class="bookInfo">
                <p class="bookTitle">{book.title}</p>
                <p>{book.author}</p>
                <p
                  class="bookProgress"
                  style="width: {Math.round(
                    (book.currentPage / book.pages) * 100
                  ) + 50}px"
                >
                  {Math.round((book.currentPage / book.pages) * 100)}
                </p>
              </div>
            {/if}
          {/each}
        </div>
        <br />
      </div>

      <div class="readingGoal">
        {#if readingGoal}
          <h2>Reading Goal</h2>
          <div>
            <p>{progressBar()} out of {readingGoal}</p>
            <progress id="progressBar" max="100" value={update_progress_bar}
            ></progress>
          </div>

          <button
            class="main-btn"
            onclick={() => {
              isGoalVisHidden = false;
              isOverlayVisHidden = false;
            }}>Change your goal</button
          >
          <div
            class="popup"
            style="height: 250px; width: 550px; margin-left: 35.3%"
            hidden={isGoalVisHidden}
          >
            <button
              class="icon-btn"
              onclick={() => {
                isGoalVisHidden = true;
                isOverlayVisHidden = true;
              }}
              ><i
                class="bi bi-x-lg"
                style="top: 0; right: 0; position: absolute; margin-top: 15px; margin-right: 15px; font-size: 20px"
              ></i></button
            >

            <h2>Update Reading Goal</h2>
            <input style="width: 300px" type="int" bind:value={updateGoal} /><br
            />
            <button
              class="main-btn"
              onclick={() => {
                newGoal();
                updateProgressBar();
                isOverlayVisHidden = true;
                isGoalVisHidden = true;
              }}>Update</button
            >
          </div>
        {:else}
          <button onclick={yearlyReadingGoal}>Pick a Goal</button>
          <p>pick goal</p>
        {/if}

        <div
          class="popup"
          style="height: 250px; width: 550px; margin-left: 35.3%"
          hidden={isCustomGoalVisHidden}
        >
          <button
            class="icon-btn"
            onclick={() => {
              isCustomGoalVisHidden = true;
              isOverlayVisHidden = true;
            }}
            ><i
              class="bi bi-x-lg"
              style="top: 0; right: 0; position: absolute; margin-top: 15px; margin-right: 15px; font-size: 20px"
            ></i></button
          >

          <h2>New Custom Goal</h2>
          <input id="newCustomGoal" type="text" /><br />
          <button
            class="main-btn"
            onclick={() => {
              let temp = custom_goals;
              temp.push(document.querySelector("#newCustomGoal").value);
              console.log(temp);
              custom_goals = temp;
              isCustomGoalVisHidden = true;
              isOverlayVisHidden = true;
            }}>Add New Goal</button
          >
        </div>

        <h2>Custom Goals</h2>
        <button
          class="new-goal-btn"
          onclick={() => {
            isCustomGoalVisHidden = false;
            isOverlayVisHidden = false;
          }}>+ New Goal</button
        ><br />

        {#each custom_goals as goal}
          <div style="padding-top: 10px;">
            <input id="goal" type="checkbox" />
            <label class="custom-goal" for="goal">{goal}</label><br />
          </div>
        {/each}
      </div>

      <div class="journalEntries" style="background-color: white">
        <h2>Journal Entries</h2>

        {#each journalEntry.journalEntry.slice().reverse() as entry}
          <div class="journalEntry">
            <div class="journalInfo">
              <h3><b>{entry.bookTitle}</b></h3>
              <p>{entry.date}</p>
            </div>

            <div class="editJournal">
              <button class="icon-btn" onclick={() => editJournalEntry(entry)}
                ><i class="bi bi-pencil-square"></i>
              </button>
            </div>
          </div>
        {/each}

        <!-- will not do anything -->
        <a style="margin-left: 40%" href="/journal">See older entries</a>

        <div
          class="popup"
          hidden={isEditJournalEntryVis}
          style="
                                                    width: 500px;
                                                    height: 550px;
                                                    /*height: calc(100% - 80px);*/
                                                    margin-left: 35.3%"
        >
          <button
            class="icon-btn"
            onclick={() => {
              isEditJournalEntryVis = true;
              isOverlayVisHidden = true;
            }}
            ><i
              class="bi bi-x-lg"
              style="top: 0; right: 0; position: absolute; margin-top: 15px; margin-right: 15px; font-size: 20px"
            ></i></button
          ><br />
          <div style="margin-left: 100px;">
            <h2
              style="padding-top: 50px; margin-right: 100px; padding-bottom: 20px"
            >
              Edit Journal Entry
            </h2>
            <label>Book Title:</label><br />
            <input id="journalEntryBookTitle" type="text" readonly /><br />

            <div
              style="display: grid; grid-template-columns: 1fr 1fr; max-width: 300px"
            >
              <div style="grid-column: 1;">
                <label for="journalEntryPagesFrom">Pages From:</label><br />
                <input id="journalEntryPagesFrom" type="int" readonly /><br />
              </div>

              <div style="grid-column: 2; padding-left: 10px">
                <label for="journalEntryPagesTo">Pages To:</label><br />
                <input id="journalEntryPagesTo" type="int" /><br />
              </div>
            </div>

            <label for="journalEntryMessage">Message:</label><br />
            <textarea id="journalEntryMessage"></textarea><br />

            <button
              class="main-btn"
              onclick={() => {
                for (let i = 0; i < journalEntry.journalEntry.length; i++) {
                  if (
                    journalEntry.journalEntry[i].bookTitle ==
                      document.querySelector("#journalEntryBookTitle").value &&
                    journalEntry.journalEntry[i].pagesFrom ==
                      document.querySelector("#journalEntryPagesFrom").value
                  ) {
                    journalEntry.journalEntry[i].pagesTo =
                      document.querySelector("#journalEntryPagesTo").value;
                    journalEntry.journalEntry[i].message =
                      document.querySelector("#journalEntryMessage").value;
                  }
                }

                alert("Successfully Updated.");

                isEditJournalEntryVis = true;
                isOverlayVisHidden = true;
              }}>Update</button
            >
          </div>
        </div>
      </div>

      <!-- <div class="gallery">
      <h2>Gallery</h2>
                                                        </div> -->
    </div>
  </container>

  <div class="overlay" hidden={isOverlayVisHidden}></div>
</main>

<style>
  @import "../app.css";

  .custom-goal {
    font-size: 20px;
  }

  input[type="checkbox"] {
    width: 25px;
    height: 25px;
  }

  input[type="checkbox"],
  .custom-goal {
    vertical-align: middle;
  }

  .popup {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 100;
    background-color: white;
    margin-top: 150px;
  }

  .overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: calc(100% - 80px);
    margin-top: 80px;
    background-color: rgba(0, 0, 0, 0.5);
  }
</style>
