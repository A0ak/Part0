Here's a sequence diagram showing the process of creating a new note:

    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the CSS file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the JavaScript code which fetches the JSON from the server.

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: The browser executes the callback function that renders the notes to DOM.

    browser->browser: User enters text into form and clicks "Save"
    Note right of browser: User's action triggers event listener on the "Save" button.

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new-note (with user's text in HTTP body)
    activate server

    Note over server: Server processes POST request, creates a new note, and updates its data.json file

    server-->>browser: Redirect (302) to /notes
    deactivate server

    Note over browser: browser automatically follows the redirect

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server

    Note over server: Server returns updated notes page with the new note

    server-->>browser: HTML document with updated notes
    deactivate server

    Note right of browser: The browser renders the updated page


This diagram extends the initial sequence to include the user's action of creating a note, and the consequences thereof. After the initial page load, the browser's user interacts with the form on the page to create a new note. This triggers a POST request, sent to the server, containing the new note's content. After the server processes the request by updating its data.json file and creating a new note, it issues a redirect response, which the browser automatically follows. The server then responds to the subsequent GET request with the updated notes page, which includes the newly created note.