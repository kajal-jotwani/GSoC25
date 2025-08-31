![alt text](/Images/Banner.png)
---

# Google Summer of Code 2025 - Final Report
- **Name** : Kajal Jotwani
- **Organization** : UC OSPO
- **Project Description**: [Brahma / Allocentric WebXR Interfaces](https://ucsc-ospo.github.io/project/osre25/ucsc/brahma/)
- **Mentor** : [Samir Ghosh ](https://github.com/smrghsh)
- **Pull Request** : [Routing system for documentation and examples](https://github.com/smrghsh/brahma-xr/pull/3) **(awaiting merge)**

## About the project 
Brahma-XR is a library and framework for building collaborative WebXR rooms with spatial data. The same code runs directly in the browser and works across devices like Apple Vision Pro, Meta Quest 3, and VARJO, which makes it really useful for quick prototyping and on-the-fly demos.

This project was developed as part of **Google Summer of Code 2025**. Since Brahma is moving from a private research repository to a public open-source project, my work during the summer mainly focused on shaping the project structure, setting up a static documentation site, and creating a clean system to run and showcase examples. These contributions were aimed at laying the foundation so that future users and contributors can easily get started with the project.

## Work Done
During the initial phase of the project, I focused on understanding how code is structured in larger Three.js projects. This helped me get a clear picture of how Brahma’s example applications are built. I spent time exploring **Networked-Aframe** to understand its architecture, how client-server communication is handled, and how the backend manages rooms. Studying it helped me understand about how to structure Brahma’s networked code to get it running efficiently.

Since Brahma involves both client- and server-side logic in a bipartite npm package structure, I also spent time learning how npm packages are published and maintained, along with best practices to manage them effectively.

**Intended Project structure:**

```
brahma-xr/
├── build/                      # Build outputs (dist files)
├── docs/                       # Jsdoc generated documentation
├── examples/                   # Individual example apps (WebXR demos)
│   ├── wildfire/               
│   ├── basic/                  
│   └── seal                    
├── files/                      
├── public/                     # Static assets 
├── server-example/             # Server-side example
├── src/                        # Core Brahma-XR library source files
│   └──index.js			        #client side code 
|   └──server.js			    #server side code for npm package            
├── examples.html               # Entry point for example gallery(iframe-based)
├── examples.json               # Metadata for examples (id, title, thumbnail, url)
├── index.html                  # Project landing page
├── jsdoc.json                  # Configuration for JSDoc documentation generation
├── main.js                     
└── style.css                   # Global or gallery styles
```

### 1. Server-Side Code 
This PR restructures the existing server-side code into a BrahmaServer class. The class, defined in server.js, provides two main methods: initialize() and run(), making the server setup cleaner and reusable. The **main.js** file inside the **server-example** folder demonstrated the usage:

```
const brahmaServer = new BrahmaServer();
brahmaServer.initialize();
brahmaServer.run();
```

Constants such as IP addresses, ports, and SSL paths were also parameterized, allowing the server to be configured easily.

### 2. Documentation 

Documentation plays a crucial role in any open-source project, and for Brahma, it is particularly important due to its bipartite npm packages. Clear documentation is necessary to explain the package architecture, how to initialize and use them, the responsibilities of client- and server-side code, and the available API endpoints.

I explored various static documentation site generators, and with guidance from my mentor, we decided to implement the documentation using JSDoc with the Docdash theme. The current documentation provides a comprehensive contribution guide for contributors, detailed references for the BrahmaServer class including its constructor, methods, parameters, and usage examples along with API references, and information on the Brahma class.

![alt text](/Images/Documentation.png)

### 3. Example Gallery 
Brahma’s example are fully fledged, networked multi-user WebXR applications that are visual by nature. The goal was to showcase these examples on a dedicated gallery page, similar to how projects like three.js and deck.gl present theirs.

As part of the process, I explored different approaches to routing and integration. One option was the way three.js handles it, using hash-based routing with iframes where each example is a static HTML page, and navigation is managed through a metadata file that updates the iframe source. Another approach was the method used by deck.gl, where each demo is implemented as a standalone React component, with routing handled by react-router-dom to provide clean, semantic URLs like /examples/scatterplot. A third possibility was to run each demo on separate ports and concurrently display them in the gallery, though this would have added unnecessary overhead.

After testing different options, we chose to adopt the iframe-based hash routing approach similar to three.js. Each example is seperately built, with metadata stored in an examples.json file that defines the id, title, thumbnail, and URL. The gallery page reads this JSON to render clickable cards, and on selection, updates an iframe to display the chosen example. I initially experimented with the React-based method used by deck.gl, but since Brahma’s examples and docs are static HTML pages, this approach wasn’t a good fit. The iframe method worked seamlessly and aligned with Brahma’s vanilla JavaScript foundation, keeping the examples self-contained and easy to maintain.

![alt text](/Images/Examples-page.png)


## Acknowledgements 
I would like to sincerely thank my mentor **Samir Ghosh** for giving me the opportunity to be part of this project and for his unwavering guidance and constant support throughout the summer. This being my first open-source project, the experience has been both exciting and full of learning. His mentorship helped me not only understand how to structure and document a project effectively but also gave me the confidence to contribute meaningfully to a new codebase. Working on this project has been a truly enriching experience, and I am grateful for all the knowledge, encouragement, and support I received along the way.