<script>
  import Header from "../lib/assets/Header.svelte";

  // test();

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
        readStatus: "currentlyReading",
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
    name: "Kelly Deal",
    accountCreated: "",
    goal: 10,
    customGoals: [
      "Read a sequel",
      "Finish a series",
      "Read 5 Non Fiction Books",
    ],
  });

  let journalEntry = $state({
    journalEntry: [
      {
        id: 1,
        bookTitle: "Little Women",
        date: "9/1/2025",
        pagesFrom: "25",
        pagesTo: "55",
        message: "test1",
      },
      {
        id: 2,
        bookTitle: "Little Women",
        date: "9/2/2025",
        pagesFrom: "55",
        pagesTo: "125",
        message: "test2",
      },
      {
        id: 3,
        bookTitle: "Little Women",
        date: "9/3/2025",
        pagesFrom: "125",
        pagesTo: "160",
        message: "test3",
      },
      {
        id: 4,
        bookTitle: "Emma",
        date: "9/4/2025",
        pagesFrom: "1",
        pagesTo: "25",
        message: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur fringilla interdum velit. Maecenas eu euismod tellus. Ut accumsan ac augue facilisis facilisis. Maecenas eget vulputate neque. Cras dictum sollicitudin turpis nec condimentum. Curabitur nunc ante, aliquet quis vehicula vehicula, sagittis et odio. Ut congue massa sit amet neque placerat vestibulum. Cras eget facilisis enim. Donec eu felis scelerisque, laoreet erat dictum, sollicitudin est. Vestibulum lobortis dui et lacus consequat feugiat.",
      },
      {
        id: 5,
        bookTitle: "Little Women",
        date: "9/4/2025",
        pagesFrom: "160",
        pagesTo: "175",
        message: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc augue felis, malesuada vel vehicula in, facilisis ut ligula. Fusce sagittis tortor elit, et viverra quam tempor venenatis. Quisque ut sem sapien. Sed quis ultrices nisl. Nulla vel laoreet lacus. Aenean tempus lectus vel lorem semper rhoncus. Sed lacinia, dolor id accumsan ornare, leo tellus ullamcorper purus, vitae malesuada erat lacus sed ante.",
      },
    ],
  });

  let gallery = $state({
    gallery: [
      {
        date: "",
        artId: "SK-C-214",
        imgURL:
          "https://lh3.googleusercontent.com/_gkvrwgCC-JpNkZRpv0IM0giM23DnBm8a5kS_dc_nhE1gZmxGM_wJIGnwFr8tVFURhao5SuWUxOkwniEcvWottBGuN4=s0",
      },
      {
        date: "",
        artId: "SK-A-138",
        imgURL:
          "https://lh3.googleusercontent.com/RXnCCOk53g6rXEPxVOWPjgTEqKzU0AUaLtXPT7-6ArjUeYueBsIvVZPnsqx0pEdHni8er7oagIHk2jlB4-U3a_kP5rg=s0",
      },
      {
        date: "",
        artId: "SK-A-2565",
        imgURL:
          "https://lh3.googleusercontent.com/Jq-ZhL8kU6AFoC5F804qAYSG6kmrBKMZRwtYj92wh3KfS_100G1hKXTfLy-Zm5yq2kbCNv6TZRtyVVRGjgidsvtdaO-T=s0",
      },
    ],
  });

  // returns current date as 1/1/2025

  function getDate() {
    let today = new Date();
    let month = today.getMonth();
    let day = today.getDate();
    let year = today.getFullYear();

    return month + 1 + "/" + day + "/" + year;
  }

  // Hidden Divs

  let isOverlayVisHidden = $state(true);

  let isGoalVisHidden = $state(true);

  let isCustomGoalVisHidden = $state(true);

  let isNewEntryHidden = $state(true);

  function toggleGoalVis() {
    isGoalVisHidden = !isGoalVisHidden;
  }

  let isNewJournalEntryHidden = $state(true);

  function toggleJournalEntryVis() {
    isNewJournalEntryHidden = !isNewJournalEntryHidden;
  }

  let isPaintingViewHidden = $state(true);

  let isJournalViewHidden = $state(true);

  // Goal Section

  let readingGoal = user.goal;

  let custom_goals = $state(user.customGoals);

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

  let update_progress_bar = $state((progressBar() / readingGoal) * 100);
  function updateProgressBar() {
    update_progress_bar = (progressBar() / readingGoal) * 100;
  }

  let isCustomGoalChecked = $state(false);

  // Currently Reading

  function currentlyReading() {
    let currentlyReading = [];

    for (let i = 0; i < books.books.length; i++) {
      if (books.books[i].readStatus == "currentlyReading") {
        currentlyReading.push(books.books[i].title);
      }
    }

    return currentlyReading;
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

  let newBookEntry = {
    title: "",
    author: "",
    pages: 0,
    readStatus: "",
    currentPage: 0,
  };

  let new_journal_entry = {
    id: 1,
    bookTitle: "",
    date: "",
    pagesFrom: 0,
    pagesTo: 0,
    message: "",
  };

  let newJournal;

  // Search
  // open books api stopped working :(

  let isbn = "";
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
    newBookEntry.currentPage = 0;
    newBookEntry.pageCount = Number(newBookEntry.pageCount);

    console.log(newBookEntry);
  }

  // New Journal Entry

  let isChecked = false;

  // Journal View

  let currJournalView = {}
  // Gallery
  let paintingURL = $state("");

  let painting = {
    date: "",
    artId: "",
    imgURL: "",
    title: "",
  };

  function rewardPainting() {
    let request =
      "https://www.rijksmuseum.nl/api/en/collection?key="+ RIJK_KEY + "&type=painting&toppieces=true&ps=50";
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
        let i = Math.floor(Math.random() * 49);

        console.log(responseData.artObjects[i]);
        painting.imgURL = responseData.artObjects[i].webImage.url;
        painting.date = getDate();
        painting.artId = responseData.artObjects[i].objectNumber;
        painting.title = responseData.artObjects[i].longTitle;

        console.log(painting);
        paintingURL = painting.imgURL;
        gallery.gallery.push(painting);
        isPaintingViewHidden = false;
        isOverlayVisHidden = false;
      });
  }

  let isGalleryInfoHidden = $state(true);

  function hoverGalleryInfo() {
    isGalleryInfoHidden = !isGalleryInfoHidden;
  }
</script>

<main style="background-color: #443B3D">
  <header>
    <Header />
  </header>

  <container style="padding: 20px;">
    <!-- Overlay for all popups  -->
    <div class="overlay" hidden={isOverlayVisHidden}></div>

    <div class="mainView" style="background-color: #443B3D">
      <div class="newJournalEntry">
        <h2>New Journal Entry</h2>

        <div style="text-align: center">
          <button
            style="margin-top: 30px"
            class="main-btn"
            onclick={() => {
              toggleJournalEntryVis();
              isOverlayVisHidden = false;
            }}>I read today!</button
          >
        </div>
        <div
          hidden={isNewJournalEntryHidden}
          style="
                        position: absolute;
                        top: 0;
                        left: 0;
                        width: 500px;
                        min-height: 200px;
                        max-height: 700px;
                        margin-top: 80px;
                        /* height: calc(100% - 80px);*/
                        z-index: 100;
                        background-color: white;
                        margin-left: 35.3%;
                        margin-top: 150px;"
        >
          <button
            class="icon-btn"
            onclick={() => {
              toggleJournalEntryVis();
              isOverlayVisHidden = true;
            }}
            ><i
              class="bi bi-x-lg"
              style="top: 0; right: 0; position: absolute; margin-top: 15px; margin-right: 15px; font-size: 20px"
            ></i></button
          >

          <h2>New Journal Entry</h2>
          <div style="margin-left: 100px">
            <label for="bookTitle">Book:</label><br />
            <div style="margin-bottom: 15px">
              <select
                id="selectBookTitle"
                style="width: 300px"
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
                {#each books.books as book}
                {#if book.readStatus == "currentlyReading"}
                  <option value={book.title}>{book.title}</option>
                  {/if}
                {/each}
              </select>
            </div>
            <br />

            <div hidden={isNewBookHidden}>
              <!-- <input type="text" bind:value={isbn} /><button onclick={search}
              >Submit</button
                                ><br /> -->

              <!-- <input type="text" bind:value={newBookEntry.title} /> -->
              <label>Title:</label><br />
              <input id="newBookTitle" type="text" bind:value={newBookEntry.title} /><br />

              <label>Autor:</label><br />
              <input id="newBookAuthor" type="text" bind:value={newBookEntry.author} /><br />

              <label>Page Count:</label><br />
              <input
              id="newBookPageCount"
                style="width: 300px"
                type="int"
                bind:value={newBookEntry.pages}
              /><br />

              <button
                style="margin-top: 20px; margin-bottom: 20px; margin-left: 60px"
                class="main-btn"
                onclick={() => {
                  manualEntry();
                  isNewBookHidden = true;
                  isNewEntryHidden = false;
                }}>Add New Book</button
              >
            </div>

            <div hidden={isNewEntryHidden}>
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

              <div style="margin-bottom: 10px; margin-top: 20px">
                <label for="mark-as-finished">Mark as Finished?</label>
                <input
                  if="mark-as-finished"
                  type="checkbox"
                  bind:checked={isChecked}
                />
              </div>

              <br />
              <label>Message:</label><br />
              <textarea id="newEntryMessage"></textarea><br />
              <button
                style="margin-bottom: 20px; margin-top: 20px; margin-left: 95px "
                class="main-btn"
                onclick={() => {
                  if (newBookEntry.title) {
                    new_journal_entry.bookTitle = newBookEntry.title;
                  } else {
                    new_journal_entry.bookTitle = selected;
                  }
                  new_journal_entry.pagesFrom = Number(
                    document.querySelector("#newEntryPagesFrom").value
                  );
                  new_journal_entry.pagesTo = Number(
                    document.querySelector("#newEntryPagesTo").value
                  );
                  new_journal_entry.message =
                    document.querySelector("#newEntryMessage").value;
                  new_journal_entry.date = getDate();

                  newBookEntry.currentPage = Number(
                    document.querySelector("#newEntryPagesTo").value
                  );

                  if (isChecked) {
                    newBookEntry.readStatus = "read";
                  }

                  let isNewBook = true;
                  for (let i = 0; i < books.books.length; i++) {
                    if (books.books[i].title == selected) {
                      isNewBook = false;
                      books.books[i].currentPage = Number(
                        document.querySelector("#newEntryPagesTo").value
                      );

                      if (isChecked) {
                        books.books[i].readStatus = "read";
                      }


                    }
                  }

                  if (isNewBook) {
                        books.books.push(newBookEntry);
                      }

                  journalEntry.journalEntry.push(new_journal_entry);

                  console.log(books.books);

                  toggleJournalEntryVis();
                  isOverlayVisHidden = true;

                  if (isChecked) {
                    rewardPainting();
                    updateProgressBar();
                  }

                  newBookEntry = {
    title: "",
    author: "",
    pages: 0,
    readStatus: "",
    currentPage: 0,
  }

  new_journal_entry =  {
    id: 1,
    bookTitle: "",
    date: "",
    pagesFrom: 0,
    pagesTo: 0,
    message: "",
  }

                  isNewBookHidden = true;
                  isNewEntryHidden = true;

                  document.querySelector("#newEntryPagesFrom").value = ""
                  document.querySelector("#newEntryPagesTo").value = ""
                  document.querySelector("#newEntryMessage").value = ""
                  document.querySelector("#selectBookTitle").value = ""
                  document.querySelector("#newBookTitle").value = ""
                  document.querySelector("#newBookAuthor").value = ""
                  document.querySelector("#newBookPageCount").value = 0

                }}>Submit</button
              >
            </div>
          </div>
        </div>
      </div>

      <div class="currentlyReading">
        <h2>Currently Reading</h2>
        <div class="bookDetails">
          {#each books.books as book}
            {#if book.readStatus == "currentlyReading"}
              <div class="bookCover">
                {#if book.coverURL}
                  <img src={book.coverURL} style="height: 150px" />
                {:else}
                  <div
                    style="display: flex; justify-content: center; align-items: center; width: 100px; height: 150px; border: 3px solid #915B49; background-color: #d4977a"
                  >
                    <i
                      style="font-size: 40px; color: #915B49"
                      class="bi bi-book-half"
                    ></i>
                  </div>
                {/if}
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
            <h3>{progressBar()} out of {readingGoal}</h3>
            <progress id="progressBar" max="100" value={update_progress_bar}
            ></progress>
          </div>

          <button
            class="icon-btn"
            style="text-decoration: underline; font-size: 1em; margin-top: 10px"
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
              custom_goals = temp;
              isCustomGoalVisHidden = true;
              isOverlayVisHidden = true;
            }}>Add New Goal</button
          >
        </div>

        <h2 style="margin-top: 10px">Custom Goals</h2>
        <button
          class="new-goal-btn"
          style="font-size: 20px; margin-top: -30px"
          onclick={() => {
            isCustomGoalVisHidden = false;
            isOverlayVisHidden = false;
          }}>+ New Goal</button
        ><br />

        <div style="margin: 0 auto; padding-left: 180px">
          {#each custom_goals as goal}
            <div style="padding-top: 10px; text-align: left;">
              <input
                id={goal}
                type="checkbox"
                value={goal}
                onchange={() => {
                  for (let i = 0; i < custom_goals.length; i++) {
                    if (custom_goals[i] == goal) {

                      custom_goals = custom_goals.filter(item => item !== goal)

                      document.querySelectorAll('input[type="checkbox"]').forEach(cb => cb.checked = false)

                      rewardPainting();
                    }
                  }
                }}
              />
              <label class="custom-goal" for="goal">{goal}</label><br />
            </div>
          {/each}
        </div>
      </div>

      <div class="journalEntries">
        <h2>Journal Entries</h2>

        {#each journalEntry.journalEntry.slice().reverse().slice(0, 5) as entry}
          <div class="journalEntry">
            <div class="journalInfo">
              <button
                class="icon-btn"
                onclick={() => {
                  isJournalViewHidden = false;
                  isOverlayVisHidden = false;
                  currJournalView = entry

                  console.log(currJournalView)
                }}><h3><b>{entry.bookTitle}</b></h3></button
              >

              <!-- View Journal Entry -->
              <div
                style="height: 550px; width: 500px; background-color: white;
                        margin-left: 35.3%;"
                class="popup"
                hidden={isJournalViewHidden}
              >
                <button
                  class="icon-btn"
                  onclick={() => {
                    isJournalViewHidden = true;
                    isOverlayVisHidden = true;


                  }}
                  ><i
                    class="bi bi-x-lg"
                    style="top: 0; right: 0; position: absolute; margin-top: 15px; margin-right: 15px; font-size: 20px"
                  ></i></button
                >
                  <h2>Journal Entry for {currJournalView.bookTitle}</h2>
                  <h2 style="text-align: center; margin-top: -20px">{currJournalView.date}</h2>

                  <h3 style="text-align: center">Pages {currJournalView.pagesFrom} to {currJournalView.pagesTo}</h3>
                  <p style="margin-left: 50px; margin-right: 50px; margin-top: 20px" id="view-journal-entry-message">{currJournalView.message}</p>

              </div>

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
        <div style="text-align: center">
          <button
            style="text-decoration: underline; font-size: 1em; padding-bottom: 15px"
            class="icon-btn"
            onclick={() => {
              alert(
                "This would route to a new page and show all journal entries"
              );
            }}>See older entries</button
          >
        </div>

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

      <div class="gallery">
        <h2 style="margin-bottom: 20px">
          <a onmouseenter={ hoverGalleryInfo } onmouseleave={hoverGalleryInfo}><i style="font-weight: bold" class="bi bi-info-circle" on></i></a><button style="font-size: 1em; font-weight: bold; margin-left: 5px;" class="icon-btn" onclick={() => {
            alert("This would route to a new page and display all of the art you have 'earned' ")
          }}>Gallery</button>
        </h2>

        <div style="    background-color: white;
    color: black;
    width: 350px;
    position: absolute;
    right: 0;
    top: 0;
    margin-top: 150px;
    margin-right: 90px;
    font-size: 20px;
    padding: 20px;
    box-shadow: 0 0 3px black; z-index: 100;" hidden={isGalleryInfoHidden}>
    <div style="text-align: center">
        <h4>What is the Gallery?</h4>
        </div>
        <p style="text-align: left">  Every time you complete a goal, you earn a painting to put in your gallery. These painting are randomly chosen from the Rijksmuseum database.
        </p><br>
        <div style="text-align: center">
        <h4>How do you earn a painting?</h4></div>
        <p style="text-align: left">  You earn a painting by either (a) Finishing a book or (b) Completing one of your custom goals</p>
        </div>

        {#each gallery.gallery.slice().reverse().slice(0, 3) as painting}
          <div class="painting">
            <img
              src={painting.imgURL}
              style="max-height: 300px; max-width: 300px"
            /><br />
          </div>
        {/each}

        {#if !isPaintingViewHidden}
          <div
            class="popup"
            style="width: 1100px; height: 720px; text-align: center; margin-left: 20%; margin-top: 50px"
          >
            <button
              class="icon-btn"
              onclick={() => {
                isPaintingViewHidden = true;
                isOverlayVisHidden = true;
              }}
              ><i
                class="bi bi-x-lg"
                style="top: 0; right: 0; position: absolute; margin-top: 15px; margin-right: 15px; font-size: 20px"
              ></i></button
            >
            <div style="margin: 3em">
              <img
                style="max-height: 600px; max-width: 900px"
                src={paintingURL}
              />
              <h3 style="padding-bottom: 20px">{painting.title}</h3>
            </div>
          </div>
        {/if}
      </div>
    </div>
  </container>
  <br />
  <br />
</main>

<style>
  @import "../app.css";
</style>
