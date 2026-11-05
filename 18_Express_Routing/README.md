# 🚀 PART 5 — EXPRESS.JS

# Chapter 18 — Express Routing



Chapter 18

Beginner to Advanced



In Chapter 17, you learned how to install Express.js and create your first Express server.

Now let's learn Express Routing.

Routing is one of the most important concepts in backend development. It helps your application decide what to do when a client requests a particular URL.

In this chapter, you will learn:

- What is routing?
- Why do we need routing?
- `app.get()`
- `app.post()`
- `app.put()`
- `app.patch()`
- `app.delete()`
- Route parameters
- Query parameters
- Request body
- Route handlers

## 📖 Interactive learning icons

# 📖

Read

Learning guidance

# 💡

Important

Remember this

## 🔑 Requires Before Starting

Before learning Express Routing, understand:

| Concept        | What you should know          |
| -------------- | ----------------------------- |
| Node.js        | JavaScript runtime            |
| Express        | Backend web framework         |
| `express()`    | Creates Express application   |
| `app.listen()` | Starts the server             |
| HTTP           | Request and response          |
| HTTP methods   | GET, POST, PUT, PATCH, DELETE |
| JSON           | Data exchange format          |
| Functions      | Creating callback functions   |

### Quick revision

In Chapter 17, you created this route:

```
app.get("/", (req, res) => {

    res.send("Welcome to Express");

});
```

Here:

- `app.get()` registers a GET route.
- `/` is the URL path.
- `req` contains request information.
- `res` sends the response.
- The callback is the route handler.

Now let's understand routing deeply.

# 1. What is Express Routing?

Express Routing is the process of defining how an application responds to client requests for different URLs and HTTP methods.

In simple words:

Routing decides which code should execute when a user requests a particular URL.

### Real-world example

Imagine you are building an online shopping application.

Your application needs different pages and operations:

| URL          | Purpose           |
| ------------ | ----------------- |
| `/`          | Home page         |
| `/products`  | Display products  |
| `/customers` | Display customers |
| `/orders`    | Display orders    |
| `/login`     | User login        |

Each URL can have a different route handler.

### Basic syntax

```
app.METHOD(PATH, HANDLER);
```

Where:

- `app` = Express application.
- `METHOD` = HTTP method.
- `PATH` = URL path.
- `HANDLER` = Function that processes the request.

Example:

```
app.get("/students", (req, res) => {

    res.send("Student List");

});
```

# 2. Why do we need Express Routing?

Imagine you are creating a Student Management System.

You need to perform these operations:

1. Get all students.
2. Get one student.
3. Create a student.
4. Update a student.
5. Delete a student.

Without proper routing, you may write many `if...else` conditions to check the requested URL and HTTP method.

### Without Express routing

```
if (req.url === "/students" && req.method === "GET") {

    // Get students

} else if (req.url === "/students" && req.method === "POST") {

    // Create student

} else if (req.url === "/students/1" && req.method === "GET") {

    // Get one student

}
```

### With Express routing

```
app.get("/students", (req, res) => {
    res.send("Get students");
});

app.post("/students", (req, res) => {
    res.send("Create student");
});

app.get("/students/1", (req, res) => {
    res.send("Get one student");
});
```

Express routing makes code:

- Easier to understand.
- Easier to maintain.
- Easier to organize.
- Easier to test.
- Easier to expand.

# 3. Real-world analogy

Imagine a railway station.

[New Standard Signages to be used at Indian Railways Stations](https://images.openai.com/static-rsc-4/iuJAgBRClETCrPEnP4r0MTtCvmYP0SZDeBOjtjos7T6cWyo_7FGIgPSn8kuXIuYqII1q3nky2v0i7yYIRhP-lHQ3yAmb4vBjh8GJ2mO6brxscL2b4PdPUFmcha_XmVhPeN3aUnstgUYgZBER1QfzAYK8P3bioD2L8FOfy0VTX-M?purpose=inline)

[mysuruinfrahub.com](https://mysuruinfrahub.com/new-standard-signages-to-be-used-at-indian-railways-station/?utm_source=chatgpt.com)

Passengers need to reach different platforms.

| Railway station               | Express routing |
| ----------------------------- | --------------- |
| Passenger                     | Client          |
| Destination                   | URL path        |
| Ticket type / journey request | HTTP method     |
| Platform direction            | Route matching  |
| Platform staff                | Route handler   |

For example:

- Passenger wants Platform 1.
- Another passenger wants Platform 2.
- Station staff direct them to the correct platform.

Similarly, Express routes direct requests to the correct handler.

# 4. Architecture / flow

### Express routing flow

\#chatgpt-mermaid-\_r_4o5\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_4o5\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_4o5\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_4o5\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_4o5\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4o5\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_4o5\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_4o5\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_4o5\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_4o5\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_4o5\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_4o5\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4o5\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4o5\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_4o5\_ p{margin:0;}#chatgpt-mermaid-\_r_4o5\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4o5\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4o5\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4o5\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_4o5\_ .label text,#chatgpt-mermaid-\_r_4o5\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4o5\_ .node rect,#chatgpt-mermaid-\_r_4o5\_ .node circle,#chatgpt-mermaid-\_r_4o5\_ .node ellipse,#chatgpt-mermaid-\_r_4o5\_ .node polygon,#chatgpt-mermaid-\_r_4o5\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_4o5\_ .rough-node .label text,#chatgpt-mermaid-\_r_4o5\_ .node .label text,#chatgpt-mermaid-\_r_4o5\_ .image-shape .label,#chatgpt-mermaid-\_r_4o5\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_4o5\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_4o5\_ .rough-node .label,#chatgpt-mermaid-\_r_4o5\_ .node .label,#chatgpt-mermaid-\_r_4o5\_ .image-shape .label,#chatgpt-mermaid-\_r_4o5\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_4o5\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_4o5\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4o5\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4o5\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_4o5\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_4o5\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_4o5\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_4o5\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_4o5\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_4o5\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_4o5\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4o5\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4o5\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_4o5\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4o5\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_4o5\_ .icon-shape,#chatgpt-mermaid-\_r_4o5\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_4o5\_ .icon-shape p,#chatgpt-mermaid-\_r_4o5\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_4o5\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_4o5\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_4o5\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_4o5\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_4o5\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_4o5\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_4o5\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_4o5\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_4o5\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4o5\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_4o5\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_4o5\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_4o5\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4o5\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_4o5\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_4o5\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4o5\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_4o5\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_4o5\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4o5\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_4o5\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4o5\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_4o5\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_4o5\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_4o5\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_4o5\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_4o5\_ .node rect,#chatgpt-mermaid-\_r_4o5\_ .node circle,#chatgpt-mermaid-\_r_4o5\_ .node ellipse,#chatgpt-mermaid-\_r_4o5\_ .node polygon,#chatgpt-mermaid-\_r_4o5\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_4o5\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_4o5\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_4o5\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_4o5\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4o5\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Client / PostmanHTTP RequestExpress ServerMatch HTTP Method + URLGet Students HandlerCreate Student HandlerReplace Student HandlerUpdate Student HandlerDelete Student Handler404 Not FoundHTTP ResponseGET /studentsPOST /studentsPUT /students/1PATCH /students/1DELETE /students/1No Match

### GitHub README diagram

Route HandlerExpress ServerClientRoute HandlerExpress ServerClient#chatgpt-mermaid-\_r_4of\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_4of\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_4of\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_4of\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_4of\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_4of\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_4of\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_4of\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_4of\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_4of\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_4of\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_4of\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4of\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4of\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_4of\_ p{margin:0;}#chatgpt-mermaid-\_r_4of\_ .actor{stroke:rgb(83, 154, 248);fill:rgb(222, 234, 251);stroke-width:1;}#chatgpt-mermaid-\_r_4of\_ rect.actor.outer-path[data-look="neo"]{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4of\_ rect.note[data-look="neo"]{stroke:rgb(107, 198, 127);fill:rgb(243, 243, 243);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4of\_ text.actor>tspan{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_4of\_ .actor-line{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4of\_ .innerArc{stroke-width:1.5;stroke-dasharray:none;}#chatgpt-mermaid-\_r_4of\_ .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4of\_ .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4of\_ [id$="-arrowhead"] path{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4of\_ .sequenceNumber{fill:#707070;}#chatgpt-mermaid-\_r_4of\_ [id$="-sequencenumber"]{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4of\_ [id$="-crosshead"] path{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_4of\_ .messageText{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_4of\_ .labelBox{stroke:rgba(0, 0, 0, 0.1);fill:rgb(252, 252, 252);filter:none;}#chatgpt-mermaid-\_r_4of\_ .labelText,#chatgpt-mermaid-\_r_4of\_ .labelText>tspan{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_4of\_ .loopText,#chatgpt-mermaid-\_r_4of\_ .loopText>tspan{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_4of\_ .sectionTitle,#chatgpt-mermaid-\_r_4of\_ .sectionTitle>tspan{fill:rgb(13, 13, 13);stroke:none;}#chatgpt-mermaid-\_r_4of\_ .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:rgba(0, 0, 0, 0.1);fill:rgba(0, 0, 0, 0.1);}#chatgpt-mermaid-\_r_4of\_ .note{stroke:rgb(107, 198, 127);fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_4of\_ .noteText,#chatgpt-mermaid-\_r_4of\_ .noteText>tspan{fill:rgb(13, 13, 13);stroke:none;font-weight:normal;}#chatgpt-mermaid-\_r_4of\_ .activation0{fill:rgb(243, 243, 243);stroke:hsl(0, 0%, 85.2941176471%);}#chatgpt-mermaid-\_r_4of\_ .activation1{fill:rgb(243, 243, 243);stroke:hsl(0, 0%, 85.2941176471%);}#chatgpt-mermaid-\_r_4of\_ .activation2{fill:rgb(243, 243, 243);stroke:hsl(0, 0%, 85.2941176471%);}#chatgpt-mermaid-\_r_4of\_ .actorPopupMenu{position:absolute;}#chatgpt-mermaid-\_r_4of\_ .actorPopupMenuPanel{position:absolute;fill:rgb(222, 234, 251);box-shadow:0px 8px 16px 0px rgba(0,0,0,0.2);filter:drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));}#chatgpt-mermaid-\_r_4of\_ .actor-man circle,#chatgpt-mermaid-\_r_4of\_ line{fill:rgb(222, 234, 251);stroke-width:2px;}#chatgpt-mermaid-\_r_4of\_ g rect.rect{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_4of\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_4of\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_4of\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_4of\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_4of\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4of\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_4of\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_4of\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_4of\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4of\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_4of\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_4of\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4of\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_4of\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_4of\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4of\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_4of\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_4of\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}GET /studentsMatch GET /studentsProcess requestStudent dataHTTP 200 JSON

### Suggested folder structure

```
18_Express_Routing/
│
├── README.md
│
├── 01_get_route.js
├── 02_post_route.js
├── 03_put_route.js
├── 04_patch_route.js
├── 05_delete_route.js
├── 06_route_params.js
├── 07_query_params.js
├── 08_request_body.js
├── 09_route_handlers.js
├── 10_student_routes.js
│
└── images/
    ├── routing-flow.png
    ├── route-parameters.png
    └── query-parameters.png
```

GitHub image reference:

```
![Express Routing](./images/routing-flow.png)
```

Add the actual image file to GitHub for it to appear. Mermaid diagrams render directly in GitHub.

# 5. Express Routing syntax

Let's understand the five main HTTP methods.

## A. GET route

Used to retrieve information.

```
app.get("/students", (req, res) => {

    res.send("Get all students");

});
```

## B. POST route

Used to create a resource or submit data.

```
app.post("/students", (req, res) => {

    res.send("Create new student");

});
```

## C. PUT route

Used to replace an existing resource representation.

```
app.put("/students/:id", (req, res) => {

    res.send("Replace student");

});
```

## D. PATCH route

Used to partially update a resource.

```
app.patch("/students/:id", (req, res) => {

    res.send("Update student");

});
```

## E. DELETE route

Used to request deletion of a resource.

```
app.delete("/students/:id", (req, res) => {

    res.send("Delete student");

});
```

### HTTP methods comparison

| Method | Purpose        | Example       |
| ------ | -------------- | ------------- |
| GET    | Read           | `/students`   |
| POST   | Create         | `/students`   |
| PUT    | Replace        | `/students/1` |
| PATCH  | Partial update | `/students/1` |
| DELETE | Delete         | `/students/1` |

# 6. Basic examples

Let's create separate examples for each HTTP method.

First, create a project.

### Step 1 — Create folder

```
mkdir 18_Express_Routing

cd 18_Express_Routing
```

### Step 2 — Initialize project

```
npm init -y
```

### Step 3 — Install Express

```
npm install express
```

### Step 4 — Create file

```
01_get_route.js
```

## A. GET example

```
// Import Express
const express = require("express");

// Create Express application
const app = express();

// GET route
app.get("/students", (req, res) => {

    // Send response
    res.send("Getting all students");

});

// Start server
app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

Run:

```
node 01_get_route.js
```

Open:

[Test GET /students](http://localhost:3000/students?utm_source=chatgpt.com)

Output:

```
Getting all students
```

## B. POST example

Create `02_post_route.js`.

```
const express = require("express");

const app = express();

// POST route
app.post("/students", (req, res) => {

    res.send("Student created successfully");

});

app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

Test using Postman:

- Method: POST
- URL: `http://localhost:3000/students`

Output:

```
Student created successfully
```

## C. PUT example

Create `03_put_route.js`.

```
const express = require("express");

const app = express();

app.put("/students/:id", (req, res) => {

    res.send("Student replaced successfully");

});

app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

Test:

```
PUT http://localhost:3000/students/1
```

Output:

```
Student replaced successfully
```

## D. PATCH example

Create `04_patch_route.js`.

```
const express = require("express");

const app = express();

app.patch("/students/:id", (req, res) => {

    res.send("Student updated successfully");

});

app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

Test:

```
PATCH http://localhost:3000/students/1
```

Output:

```
Student updated successfully
```

## E. DELETE example

Create `05_delete_route.js`.

```
const express = require("express");

const app = express();

app.delete("/students/:id", (req, res) => {

    res.send("Student deleted successfully");

});

app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

Test:

```
DELETE http://localhost:3000/students/1
```

Output:

```
Student deleted successfully
```

# 7. Dry run

Let's understand how Express handles a GET request.

Code:

```
app.get("/students", (req, res) => {

    res.send("Student List");

});
```

Assume the client sends:

```
GET /students
```

Execution:

| Step | Action                   | Explanation              |
| ---- | ------------------------ | ------------------------ |
| 1    | Client sends request     | Requests `/students`     |
| 2    | Express receives request | Checks registered routes |
| 3    | Express matches route    | Finds GET `/students`    |
| 4    | Handler executes         | Callback function runs   |
| 5    | `res.send()` executes    | Sends response           |
| 6    | Client receives response | Displays Student List    |

Output:

```
Student List
```

### Important

If you send a POST request to `/students`, the GET route does not match.

Express checks both the HTTP method and the route path.

# 8. Output

Let's understand the expected responses.

| Request              | Expected output  |
| -------------------- | ---------------- |
| GET `/students`      | Get all students |
| POST `/students`     | Create student   |
| PUT `/students/1`    | Replace student  |
| PATCH `/students/1`  | Update student   |
| DELETE `/students/1` | Delete student   |

These are example response messages. Actual applications perform the required operations on their data.

# 9. Line-by-line explanation

Now let's understand the important routing concepts in detail.

## A. Route parameters — `req.params`

Route parameters are values included in a URL path.

Example:

```
/students/101
```

Here, `101` is a route parameter.

We define it using `:id`.

```
app.get("/students/:id", (req, res) => {

    console.log(req.params);

    res.send("Student ID: " + req.params.id);

});
```

Visit:

[Test route parameter](http://localhost:3000/students/101?utm_source=chatgpt.com)

Output:

```
Student ID: 101
```

### Multiple route parameters

```
app.get("/students/:studentId/courses/:courseId", (req, res) => {

    const studentId = req.params.studentId;

    const courseId = req.params.courseId;

    res.json({
        studentId: studentId,
        courseId: courseId
    });

});
```

URL:

```
/students/101/courses/501
```

Output:

```
{
    "studentId": "101",
    "courseId": "501"
}
```

💡 Important: Route parameter values are strings by default. Convert them when you need numeric values.

Example:

```
const id = Number(req.params.id);
```

## B. Query parameters — `req.query`

Query parameters are additional values sent after `?` in a URL.

Example:

```
/students?name=Ramesh
```

Here:

- `name` is the query parameter key.
- `Ramesh` is the query parameter value.

Example code:

```
app.get("/students", (req, res) => {

    const name = req.query.name;

    res.send("Student Name: " + name);

});
```

Visit:

[Test query parameter](http://localhost:3000/students?name=Ramesh\&utm_source=chatgpt.com)

Output:

```
Student Name: Ramesh
```

### Multiple query parameters

URL:

```
/students?name=Ramesh&course=Node.js
```

Code:

```
app.get("/students", (req, res) => {

    const name = req.query.name;

    const course = req.query.course;

    res.json({
        name: name,
        course: course
    });

});
```

Output:

```
{
    "name": "Ramesh",
    "course": "Node.js"
}
```

### Query parameters use cases

- Searching.
- Filtering.
- Pagination.
- Sorting.

Example:

```
/products?category=electronics&page=1&limit=10
```

## C. Request body — `req.body`

The request body contains data sent by the client.

For example, when registering a new student, the frontend sends:

```
{
    "name": "Ramesh",
    "course": "Node.js"
}
```

Express needs middleware to parse JSON request bodies.

Use:

```
app.use(express.json());
```

Complete example:

```
const express = require("express");

const app = express();

// Parse incoming JSON request bodies
app.use(express.json());

// POST route
app.post("/students", (req, res) => {

    // Read request body
    const student = req.body;

    res.status(201).json({
        message: "Student received successfully",
        data: student
    });

});

app.listen(3000, () => {

    console.log("Server running on port 3000");

});
```

### Test using Postman

Method:

```
POST
```

URL:

```
http://localhost:3000/students
```

Select:

```
Body → raw → JSON
```

Send:

```
{
    "name": "Ramesh",
    "course": "Node.js"
}
```

Expected response:

```
{
    "message": "Student received successfully",
    "data": {
        "name": "Ramesh",
        "course": "Node.js"
    }
}
```

💡 Important: `express.json()` parses JSON request bodies. Without it, `req.body` will generally be `undefined` for incoming JSON requests.

## D. Route handlers

A route handler is a function that executes when a request matches a route.

Basic example:

```
app.get("/students", (req, res) => {

    res.send("Student List");

});
```

Here, the arrow function is the route handler.

### Multiple route handlers

Express allows multiple handler functions for a route.

```
app.get(
    "/students",

    (req, res, next) => {

        console.log("First handler");

        next();

    },

    (req, res) => {

        res.send("Student List");

    }
);
```

Execution:

1. First handler runs.
2. `next()` passes control to the next handler.
3. Second handler sends the response.

Output in terminal:

```
First handler
```

Browser output:

```
Student List
```

Remember: If a handler neither sends a response nor calls `next()`, the request may remain unfinished.

# 10. Practical example — Complete Student Routing API

Now let's combine all five HTTP methods, route parameters, query parameters and request body.

### Requirements

Build a Student Management API.

It should support:

1. Get all students.
2. Get one student by ID.
3. Create a student.
4. Replace a student's details.
5. Partially update student details.
6. Delete a student.
7. Search students using query parameters.

File: `10_student_routes.js`

```
// Import Express
const express = require("express");

// Create application
const app = express();

// Parse JSON request body
app.use(express.json());

// Sample student data
let students = [
    { id: 1, name: "Ramesh", course: "Node.js" },
    { id: 2, name: "Kumar", course: "React.js" }
];

// ===================================
// GET - Get all students
// ===================================

app.get("/students", (req, res) => {

    const searchName = req.query.name;

    let result = students;

    // Search by name if query parameter exists
    if (searchName) {

        result = students.filter((student) =>
            student.name.toLowerCase().includes(searchName.toLowerCase())
        );

    }

    res.status(200).json({
        success: true,
        data: result
    });

});

// ===================================
// GET - Get student by ID
// ===================================

app.get("/students/:id", (req, res) => {

    const id = Number(req.params.id);

    const student = students.find((item) => item.id === id);

    if (!student) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    res.status(200).json(student);

});

// ===================================
// POST - Create student
// ===================================

app.post("/students", (req, res) => {

    const { name, course } = req.body;

    // Basic validation
    if (!name || !course) {

        return res.status(400).json({
            message: "Name and course are required"
        });

    }

    const newStudent = {
        id: students.length
            ? Math.max(...students.map(student => student.id)) + 1
            : 1,
        name,
        course
    };

    students.push(newStudent);

    res.status(201).json({
        message: "Student created successfully",
        data: newStudent
    });

});

// ===================================
// PUT - Replace student
// ===================================

app.put("/students/:id", (req, res) => {

    const id = Number(req.params.id);

    const { name, course } = req.body;

    const index = students.findIndex((item) => item.id === id);

    if (index === -1) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    if (!name || !course) {

        return res.status(400).json({
            message: "Name and course are required"
        });

    }

    students[index] = {
        id,
        name,
        course
    };

    res.status(200).json({
        message: "Student replaced successfully",
        data: students[index]
    });

});

// ===================================
// PATCH - Partially update student
// ===================================

app.patch("/students/:id", (req, res) => {

    const id = Number(req.params.id);

    const student = students.find((item) => item.id === id);

    if (!student) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    const { name, course } = req.body;

    if (name !== undefined) {
        student.name = name;
    }

    if (course !== undefined) {
        student.course = course;
    }

    res.status(200).json({
        message: "Student updated successfully",
        data: student
    });

});

// ===================================
// DELETE - Delete student
// ===================================

app.delete("/students/:id", (req, res) => {

    const id = Number(req.params.id);

    const index = students.findIndex((item) => item.id === id);

    if (index === -1) {

        return res.status(404).json({
            message: "Student not found"
        });

    }

    const deletedStudent = students.splice(index, 1)[0];

    res.status(200).json({
        message: "Student deleted successfully",
        data: deletedStudent
    });

});

// Start server
app.listen(3000, () => {

    console.log("Student API running on port 3000");

});
```

### Test all endpoints using Postman

| Method | URL                     | Purpose                  |
| ------ | ----------------------- | ------------------------ |
| GET    | `/students`             | Get all students         |
| GET    | `/students/1`           | Get student by ID        |
| GET    | `/students?name=Ramesh` | Search student           |
| POST   | `/students`             | Create student           |
| PUT    | `/students/1`           | Replace student          |
| PATCH  | `/students/1`           | Partially update student |
| DELETE | `/students/1`           | Delete student           |

### POST body

```
{
    "name": "Suresh",
    "course": "Python"
}
```

### PUT body

```
{
    "name": "Ramesh Kumar",
    "course": "FastAPI"
}
```

### PATCH body

```
{
    "course": "Express.js"
}
```

### Test execution flow

\#chatgpt-mermaid-\_r_515\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_515\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_515\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_515\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_515\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_515\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_515\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_515\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_515\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_515\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_515\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_515\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_515\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_515\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_515\_ p{margin:0;}#chatgpt-mermaid-\_r_515\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_515\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_515\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_515\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_515\_ .label text,#chatgpt-mermaid-\_r_515\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_515\_ .node rect,#chatgpt-mermaid-\_r_515\_ .node circle,#chatgpt-mermaid-\_r_515\_ .node ellipse,#chatgpt-mermaid-\_r_515\_ .node polygon,#chatgpt-mermaid-\_r_515\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_515\_ .rough-node .label text,#chatgpt-mermaid-\_r_515\_ .node .label text,#chatgpt-mermaid-\_r_515\_ .image-shape .label,#chatgpt-mermaid-\_r_515\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_515\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_515\_ .rough-node .label,#chatgpt-mermaid-\_r_515\_ .node .label,#chatgpt-mermaid-\_r_515\_ .image-shape .label,#chatgpt-mermaid-\_r_515\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_515\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_515\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_515\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_515\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_515\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_515\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_515\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_515\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_515\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_515\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_515\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_515\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_515\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_515\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_515\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_515\_ .icon-shape,#chatgpt-mermaid-\_r_515\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_515\_ .icon-shape p,#chatgpt-mermaid-\_r_515\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_515\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_515\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_515\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_515\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_515\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_515\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_515\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_515\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_515\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_515\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_515\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_515\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_515\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_515\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_515\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_515\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_515\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_515\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_515\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_515\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_515\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_515\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_515\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_515\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_515\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_515\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_515\_ .node rect,#chatgpt-mermaid-\_r_515\_ .node circle,#chatgpt-mermaid-\_r_515\_ .node ellipse,#chatgpt-mermaid-\_r_515\_ .node polygon,#chatgpt-mermaid-\_r_515\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_515\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_515\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_515\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_515\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_515\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Client RequestExpress RoutingHTTP MethodRead StudentCreate StudentReplace StudentUpdate StudentDelete StudentSend JSON ResponseGETPOSTPUTPATCHDELETE

Note: This practical example stores records in memory. Data disappears when you restart the server. We will use a database in later chapters.

# 11. Common mistakes

## Mistake 1 — Forgetting `express.json()`

Wrong

```
const app = express();

app.post("/students", (req, res) => {

    console.log(req.body);

});
```

If JSON parsing middleware has not been configured, `req.body` will generally be undefined.

Correct

```
const app = express();

app.use(express.json());

app.post("/students", (req, res) => {

    console.log(req.body);

    res.json(req.body);

});
```

## Mistake 2 — Using `req.params` for query parameters

Wrong:

```
const name = req.params.name;
```

For this URL:

```
/students?name=Ramesh
```

Correct:

```
const name = req.query.name;
```

## Mistake 3 — Using `req.query` for route parameters

For this URL:

```
/students/101
```

Correct:

```
const id = req.params.id;
```

## Mistake 4 — Forgetting `return` after an error response

Wrong:

```
if (!student) {

    res.status(404).json({
        message: "Not found"
    });

}

res.json(student);
```

This can attempt to send two responses when the student is missing.

Correct:

```
if (!student) {

    return res.status(404).json({
        message: "Not found"
    });

}

res.json(student);
```

## Mistake 5 — Confusing PUT and PATCH

| PUT                                        | PATCH                        |
| ------------------------------------------ | ---------------------------- |
| Replaces the resource representation       | Applies a partial update     |
| Usually sends all required resource fields | Can send only changed fields |

# 12. Best practices

1. Use meaningful resource-based URLs.
2. Use the correct HTTP methods.
3. Use route parameters for resource identification.
4. Use query parameters for filtering, searching and pagination.
5. Use the request body for submitted resource data.
6. Always validate incoming data.
7. Return appropriate status codes.
8. Use `express.json()` for JSON request bodies.
9. Use `return` after sending an early error response.
10. Avoid writing all routes in one large file as your application grows.
11. Keep route handlers focused and readable.
12. Do not trust client input without validation.

### Professional route naming

Good:

```
GET    /api/students
GET    /api/students/101
POST   /api/students
PUT    /api/students/101
PATCH  /api/students/101
DELETE /api/students/101
```

Avoid inconsistent endpoint naming such as:

```
GET /getAllStudents
POST /createNewStudent
```

# 13. Interview questions

## Beginner level

Q1. What is routing in Express.js?

Routing defines how the application responds to a particular HTTP method and URL.

Q2. What is `app.get()`?

It registers a route to handle GET requests.

Q3. What is `app.post()`?

It registers a route to handle POST requests.

Q4. What is a route parameter?

A dynamic value included in the URL path, such as `/students/:id`.

Q5. What is `req.params`?

It contains the route parameter values.

## Intermediate level

Q6. What is `req.query`?

It contains query string parameters from the URL.

Q7. What is `req.body`?

It contains the parsed request body, provided the appropriate middleware is configured.

Q8. Why do we use `express.json()`?

It parses incoming JSON request bodies.

Q9. What is a route handler?

A callback function that processes a matching request.

Q10. What is the difference between PUT and PATCH?

PUT generally replaces the resource representation, while PATCH applies partial changes.

## Advanced level

Q11. Can we have multiple route handlers for one route?

Yes. Express supports multiple handlers, and `next()` can pass control to the next handler.

Q12. What happens when no route matches?

Express continues looking for a matching route or middleware. If nothing handles the request, the default response is generally 404 Not Found.

Q13. Why should we validate `req.body`?

Because client input may be missing, incorrect or malicious.

Q14. What is the difference between route parameters and query parameters?

Route parameters identify a resource in the path. Query parameters provide additional information such as filtering and pagination.

Q15. Can the same URL have GET and POST routes?

Yes. For example, GET `/students` retrieves students and POST `/students` creates a student.

# 14. Practice problems

Try these exercises in VS Code.

Your practice checklist

0/8

Exercise 1: Create GET /employees to return all employees.

💡 Show hint

Exercise 2: Create POST /employees to receive employee information.

💡 Show hint

Exercise 3: Create GET /employees/:id to read an employee ID.

💡 Show hint

Exercise 4: Create GET /products?category=mobile to read the category.

💡 Show hint

Exercise 5: Create PUT /employees/:id to replace employee details.

💡 Show hint

Exercise 6: Create PATCH /employees/:id to update only the employee email.

💡 Show hint

Exercise 7: Create DELETE /employees/:id to delete an employee.

💡 Show hint

Exercise 8: Create a route with two parameters: /orders/:orderId/items/:itemId.

💡 Show hint

# 15. Mini challenge — Employee Management API

Practical challenge

Build an Employee Management API using Express routing.

### Requirements

Your API should support:

| Method | Endpoint                   | Function                  |
| ------ | -------------------------- | ------------------------- |
| GET    | `/employees`               | Get all employees         |
| GET    | `/employees/:id`           | Get employee by ID        |
| GET    | `/employees?department=IT` | Filter by department      |
| POST   | `/employees`               | Create employee           |
| PUT    | `/employees/:id`           | Replace employee          |
| PATCH  | `/employees/:id`           | Update employee partially |
| DELETE | `/employees/:id`           | Delete employee           |

### Starter code

```
const express = require("express");

const app = express();

app.use(express.json());

// Sample employees
let employees = [
    {
        id: 1,
        name: "Ramesh",
        department: "IT"
    },
    {
        id: 2,
        name: "Kumar",
        department: "HR"
    }
];

// 1. GET all employees


// 2. GET employee by ID


// 3. Filter employees by department


// 4. POST new employee


// 5. PUT employee


// 6. PATCH employee


// 7. DELETE employee


// Start server
```

### Expected output

For:

```
GET /employees?department=IT
```

Expected response:

```
[
    {
        "id": 1,
        "name": "Ramesh",
        "department": "IT"
    }
]
```

Try building it yourself. Focus on understanding how `req.params`, `req.query` and `req.body` work.

# 16. Chapter summary

| Topic            | What you learned                  |
| ---------------- | --------------------------------- |
| Express Routing  | Matching requests to handlers     |
| `app.get()`      | Retrieve information              |
| `app.post()`     | Create or submit data             |
| `app.put()`      | Replace a resource                |
| `app.patch()`    | Partially update a resource       |
| `app.delete()`   | Delete a resource                 |
| `req.params`     | Read route parameters             |
| `req.query`      | Read query parameters             |
| `req.body`       | Read request body                 |
| `express.json()` | Parse JSON request bodies         |
| Route handler    | Function that processes a request |
| `next()`         | Pass control to another handler   |

# 17. Quick revision

Remember these three important request properties:

| Property     | Example URL / Data      |
| ------------ | ----------------------- |
| `req.params` | `/students/101`         |
| `req.query`  | `/students?name=Ramesh` |
| `req.body`   | `{ "name": "Ramesh" }`  |

Important routing syntax

```
const express = require("express");

const app = express();

app.use(express.json());

app.get("/students", (req, res) => {
    res.json({ message: "Get students" });
});

app.post("/students", (req, res) => {
    res.status(201).json(req.body);
});

app.put("/students/:id", (req, res) => {
    res.json({ id: req.params.id });
});

app.patch("/students/:id", (req, res) => {
    res.json({ id: req.params.id });
});

app.delete("/students/:id", (req, res) => {
    res.json({ id: req.params.id });
});

app.listen(3000);
```

## 📁 GitHub README checklist

- Create `18_Express_Routing` folder.
- Create `README.md`.
- Add five HTTP method examples.
- Add route parameter examples.
- Add query parameter examples.
- Add request body examples.
- Add Mermaid diagrams.
- Add actual images inside `images/` if needed.
- Test endpoints using Postman.
- Complete Employee Management API challenge.

Suggested GitHub image references:

```
![Express Routing](./images/routing-flow.png)

![Route Parameters](./images/route-parameters.png)

![Query Parameters](./images/query-parameters.png)
```

Remember that actual image files must be committed to your repository. Mermaid diagrams can render directly in GitHub.

Chapter 18 completed

You have now learned how to create different routes and handle incoming request data in Express.js.

Practice the Employee Management API challenge before moving forward.

When you are ready, type `NEXT` to start:

# Chapter 19 — Express Middleware 🚀