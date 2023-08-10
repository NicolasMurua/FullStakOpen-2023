# Summary

So the main idea of this part is to start knowing more about how a browser and a server interacts with each other and how the exchange of information happens, diving into concepts like 'How request and responses works', 'What is the HTTP protocol used for', 'Chrome devtools used to debug', 'DOM-API', etc.

There is no need to write code in this part, You will only need to create a few sequence diagrams.

You can use any tool available, I will just the suggested one from the course, Mermaid on Markdown files.

Below i will put my answers, so if you don't want to be spoiled skip ahead.

If the next content isn't rendered right by github, you can use https://mermaid.live/ and see it online.

# 0.4

```mermaid

sequenceDiagram
participant Browser
participant Server

    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate Server
    Server-->>Browser: Server Response: notes.html, main.css, main.js and data.json
    deactivate Server

    activate Browser
    Note over Browser:  User writes a note
    Note over Browser:  User presses the Save Button
    Browser ->> Server: HTTP POST new_note with data payload
    deactivate Browser

    activate Server
    Note over Server: Creates a new note with the data from the browser
    Note over Server: Sends a URL redirect, so the data can be render
    Server-->>Browser: 301 response, with URL redirect '/exampleapp/notes'
    deactivate Server

    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate Server
    Server-->>Browser: Server Response: notes.html, main.css, main.js and data.json
    deactivate Server

    Note right of Browser: The browser now has rerender the hole page and it's shows the new notes.
```

# 0.5

```mermaid
sequenceDiagram
participant browser
participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-->>browser: spa.html
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    server-->>browser: spa.js
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: the data.json file where the notes are.
    deactivate server

    Note right of browser: This time there is actually no css file.

```

# 0.6

```mermaid
sequenceDiagram
participant Browser
participant Server

    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate Server
    Server-->>Browser: Server Response: spa.html, spa.js and data.json
    deactivate Server

    activate Browser
    Note over Browser:  User writes a note
    Note over Browser:  User presses the Save Button
    Browser ->> Server: HTTP POST new_note with body {"message":"note created"}
    deactivate Browser

    activate Server
    Note over Server: Creates a new note with the data from the browser
    Note over Server: Returns a 201 Created response
    Server-->>Browser: HTTP 201 response
    deactivate Server

    activate Browser
    note over Browser: The browser modifies it's own HTMl through the DOM-API to add the new note.
    note over Browser: The server doesn't sends any new data.json
    deactivate Browser

    Note right of Browser: The browser now has rerender the new note

```
