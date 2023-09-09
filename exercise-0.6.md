Here is a diagram showing the user creating a new note using the single-page version of the app:

    participant Browser as browser
    participant Server as server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-->>browser: HTML document (SPA version)
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    server-->>browser: JavaScript file (SPA version)
    deactivate server

    Note right of browser: Browser starts executing JavaScript code which fetches JSON from the server.

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: Browser executes JavaScript functions to control operation of the SPA, and displays loaded notes.

    browser->browser: User enters text into form and clicks "Save"
    Note right of browser: User's action triggers event listener on "Save" button.

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new-note-spa (with user's text as HTTP body)
    activate server

    Note over server: Server processes POST request, creates a new note in its data.json, and returns 201 Created
    server-->>browser: 201 Created
    deactivate server

    Note right of browser: SPA JavaScript pushes the new note to the notes list without reloading the page.


This sequence diagram extends the earlier sequence for accessing the SPA with steps specifically for creating a new note. After the SPA loads and the notes are displayed, the user interacts with the form to create the new note. This triggers a POST request, which contains the user's note as text in the HTTP body, sent to the server. Once the server finishes processing the request and updating data.json, it sends a 201 Created response back to the SPA. Finally, the SPA's JavaScript takes the new note and adds it to the already rendered list of notes, without needing to reload the entire page.