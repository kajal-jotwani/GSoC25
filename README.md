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

Since Brahma involves both client-side and server-side logic in a bipartite npm package structure, I also spent time learning how npm packages are published and maintained, along with best practices to manage them effectively.

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
I refactored the server-side code into a BrahmaServer class, providing two main methods: `initialize()` and `run()`.This makes server setup modular and reusable. Configuration constants such as IP addresses, ports, and SSL paths were parameterized for flexibility. The `server-example/main.js` demonstrates usage:

```
const brahmaServer = new BrahmaServer();
brahmaServer.initialize();
brahmaServer.run();
```


### 2. Documentation 

Documentation plays a crucial role in any open-source project, and for Brahma, it is particularly important due to its bipartite npm packages. Clear documentation is necessary to explain the package architecture, how to initialize and use them, the responsibilities of client- and server-side code, and the available API endpoints.

I explored various static documentation site generators, and with guidance from my mentor, we decided to implement the documentation using JSDoc with the Docdash theme. The current documentation provides a comprehensive contribution guide for contributors, detailed references for the BrahmaServer class including its constructor, methods, parameters, and usage examples along with API references, and information on the Brahma class.

![alt text](/Images/Documentation.png)

### 3. Example Gallery 
Brahma’s example are fully fledged, networked multi-user WebXR applications that are visual by nature. The goal was to showcase these examples on a dedicated gallery page, similar to how projects like three.js and deck.gl present theirs.

**As part of the process, I explored different approaches to routing and integration.** 

- **[Three.js](https://github.com/mrdoob/three.js) (hash-based routing)**:
Each demo is a standalone HTML file. A metadata file lists titles, thumbnails, and IDs. Clicking a thumbnail updates the URL hash (e.g., `#/webgl_animation_keyframes`), and an **iframe** dynamically loads the corresponding example. This approach is lightweight, framework-free, and keeps examples self-contained. [Example from the Three.js Repository](https://github.com/mrdoob/three.js/blob/0f246617770fac88855ce916f3f5b234d4f1d032/examples/index.html)

- **[Deck.gl](https://github.com/visgl/deck.gl) (React + client-side routing)**:
Each example is a standalone React component, with routing handled by react-router-dom. Metadata maps thumbnails to routes like `/examples/heatmap` or `/examples/scatterplot`. When a user clicks a card, React dynamically renders the component within the SPA without a full page reload, allowing seamless navigation.

- **Concurrent servers (multi-port approach)**:
Instead of building each example into a static HTML file and updating the metadata, each demo could run on a separate server/port, with the gallery embedding them via iframe by pointing the metadata url field to the corresponding port. While technically feasible, this approach adds unnecessary overhead.

After evaluating different options, we adopted the iframe-based hash routing approach, inspired by Three.js. Each example is built separately, with metadata in examples.json (id, title, thumbnail, URL). The gallery uses this JSON to render clickable cards, updating a single iframe to display the selected example. I also tried the Deck.gl React-based method, but since Brahma’s examples are static HTML builds, it wasn’t suitable. The iframe method works seamlessly, keeping examples self-contained and easy to use.

![alt text](/Images/Examples-page.png)


## Challenges and Key Learnings

- **Learning the fundamentals of Three.js** – During the community bonding period, I focused on gaining an in-depth understanding of Three.js: how 3D rendering works, setting up scenes, working with materials, cameras, and animations. Along the way, I also explored Blender and shaders to strengthen my foundation. I documented my learnings in [this repo](https://github.com/kajal-jotwani/Learning_three.js)
 and created a basic example for the project to put theory into practice.

- **Learning open-source practices** – I also learned about best practices such as writing clear documentation, maintaining clean commits, and effective communication.

- **Adapting examples for the project** – One key challenge was figuring out how to represent examples effectively. Brahma’s examples are full-fledged, multi-user WebXR applications, so I spent time exploring how other open-source projects structure and showcase their work. This not only gave me new technical insights but also helped me shape an approach that worked for Brahma’s use case.

## Acknowledgements 
I would like to sincerely thank my mentor **Samir Ghosh** for giving me the opportunity to be part of this project and for his unwavering guidance and constant support throughout the summer. This being my first open-source project, the experience has been both exciting and full of learning. His mentorship helped me not only understand how to structure and document a project effectively but also gave me the confidence to contribute meaningfully to a new codebase. Working on this project has been a truly enriching experience, and I am grateful for all the knowledge, encouragement, and support I received along the way.