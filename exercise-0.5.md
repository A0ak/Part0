A sequence diagram showing the user's process of navigating to the single page application (SPA) version of the notes app at https://studies.cs.helsinki.fi/exampleapp/spa:

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

    Note right of browser: The browser starts executing the JavaScript code which fetches the JSON from the server.

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: The browser executes JavaScript functions to control the operation of the single page application


This diagram shows the browser first sending a GET request to the specified URL. Then, it shows the server responding to this request with the HTML document of the SPA version. The browser continues to request the CSS and JavaScript files from the same server.

When the browser receives the JavaScript file, it sends another GET request to the server. This time, the server responds with JSON data. This data is used by the browser to direct the operation of the SPA. Finally, the browser processes this data and renders the content of the SPA for the user to view.