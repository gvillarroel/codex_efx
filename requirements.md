**Node Chat Monorepo Requirements Document**

**1. Introduction**
This document defines the functional and technical requirements for a Node.js monorepo containing two distinct subprojects: an Angular standalone chat component and an Astro-based frontend. It is intended for front‑end developers familiar with modern JavaScript frameworks, ensuring that both parts integrate smoothly and follow the Google Assistant A2A protocol for messaging.

**2. Prerequisites**
Developers must use the latest long‑term support version of Node.js (v22.x) to ensure compatibility with workspace tools and package ecosystems. All development dependencies should target the most recent stable releases of Angular, Tailwind CSS, and Astro to take advantage of the latest features and performance improvements.

**3. Architecture Overview**
The project is organized as a monorepo managed by a workspace tool such as npm or Yarn workspaces. Two sibling packages live under a shared packages directory. The root configuration declares workspace paths and the Node.js engine version. This setup allows simultaneous development, testing, and deployment of both subprojects.

**4. Subproject A: Angular Standalone Chat Component**

- **Framework and Styling**: Build a standalone Angular component using the most recent Angular major release. Styling must rely solely on Tailwind CSS utilities, avoiding external Angular module dependencies.

- **Component API**: The component should expose a configuration input property to receive connector settings and protocol details. It must emit events when the user sends messages or uploads files. All user interactions—typing text, attaching files, and toggling a settings panel—should trigger clearly defined output events.

- **User Interface Requirements**: The chat interface must include an accessible text input field with send controls and a file attachment mechanism supporting both drag‑and‑drop and manual selection. A collapsible settings area should allow the user to configure connectors and endpoints.

- **Protocol Compliance**: Implement full support for the Google Assistant A2A message schema. The component must recognize and render every variant of A2A message parts, including plain text, media, cards, and suggestion chips. Incoming and outgoing messages should be validated against the protocol schema to ensure interoperability.

**5. Subproject B: Astro Frontend**

- **Framework and Styling**: Create an Astro application that shares the same Tailwind CSS theme tokens as the chat component. Integrate the Angular component either as a web component or through a framework-specific hosting mechanism.

- **Chat History Management**: Implement client‑side storage of conversation sessions, using a browser storage API or a mock service. Display a list of past sessions with human‑readable timestamps and preview snippets.

- **Session Playback**: Clicking a session entry should dynamically mount the Angular chat component and replay the stored A2A payloads in sequence, reconstructing the original conversation with placeholder data.

- **Routing Structure**: Define two primary views: one for listing sessions and another for displaying an individual session detail. The session detail view must mount the chat component and feed it the historical messages.

**6. Documentation Requirements**

- **Root Overview**: Provide a high‑level overview of the monorepo structure, installation steps, development workflow, and build process.

- **Chat Component Guide**: Document the component’s public API, including expected configuration formats, event payloads, and supported A2A message part types. Include examples of typical JSON payloads and instructions for extending or theming the UI.

- **Frontend Guide**: Explain how to register and embed the Angular component within the Astro environment. Describe the chat history storage model, session object schema, and the mechanism for replaying conversations. Provide guidance for connecting to a real agent service conforming to the A2A protocol.

**7. Design and Theming**

Use a centralized set of CSS custom properties for fonts, colors, and spacing. Define variables for primary brand colors, gray palettes, status indicators, and accessibility focus highlights. Tailwind configuration should extend the theme with these custom properties, ensuring visual consistency across both subprojects. Include instructions for loading a material symbol font for UI icons.

**8. Development Workflow**

Explain how to install dependencies at the root, run both subprojects concurrently in development mode, and build them for production. Describe the role of workspace commands and how to execute linting and testing tasks across the entire monorepo.

**9. Acceptance Criteria**

- The chat component builds successfully and can be consumed as a standalone package.
- The Astro frontend lists and replays chat sessions accurately, rendering all A2A parts.
- Documentation is comprehensive, enabling any developer to set up, run, and extend both subprojects without additional guidance.
