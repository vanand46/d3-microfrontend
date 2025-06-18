## What are microfrontends?

- A design pattern where a web application (often a monolith) is divided into multiple, smaller, and independently deployable applications.
- Each smaller application, or microfrontend (MFE), is responsible for a distinct feature or business domain of the product.

### Why use them?

- **Team Autonomy:** Multiple engineering teams can work on their features in isolation, with their own release cycles.
- **Maintainability:** Each smaller application is easier to understand, develop, and test.
- **Technology Freedom:** Teams can choose the best technology stack for their specific feature without impacting other teams.

---

### Microfrontend Integration Strategies

Here are the major ways to integrate microfrontends into a host application.

**1. Build-Time Integration**

The microfrontend is included as a dependency and bundled with the host application *before* it is deployed.

**How it works:**
1.  An engineering team develops the MFE as a component or library.
2.  They publish the MFE as a package (e.g., to NPM).
3.  The host application team installs the MFE package as a dependency.
4.  The host application's build process includes all the code for the MFE in its final bundle.

-   **Pros:**
    -   Relatively easy to set up and understand.
    -   Ensures type safety and dependency management through standard tooling.
-   **Cons:**
    -   **Tight Coupling:** The host application and MFE are locked to a specific version.
    -   **Slow Deployments:** The entire host application must be rebuilt and redeployed every time even a single MFE is updated.

**2. Run-Time Integration (Client-Side)**

The host application fetches and renders the microfrontend *after* the host has already loaded in the browser. This is the most common and flexible approach.

**How it works:**
1.  An engineering team develops and deploys their MFE to a separate location (e.g., a CDN).
2.  The host application is loaded in the user's browser.
3.  The host application then dynamically fetches the MFE's code from its deployed URL and renders it in the appropriate place. (e.g., via Webpack Module Federation).

-   **Pros:**
    -   **Independent Deployments:** MFEs can be updated and deployed at any time without requiring the host application to be redeployed.
    -   **Resilience:** An MFE can fail to load without breaking the entire application.
-   **Cons:**
    -   The initial setup and tooling (like Webpack Module Federation) can be more complex.
    -   Managing shared dependencies and application state between the host and MFEs requires careful planning.

**3. Server-Side Integration (Server-Side Rendering - SSR)**

A server assembles the final HTML document by fetching content from different microfrontends *before* sending the page to the browser.

**How it works:**
1.  A user requests a page.
2.  A server-side application (the "app shell" or "composition layer") receives the request.
3.  It determines which MFEs are needed for the page and fetches their HTML fragments from their respective services.
4.  The server combines these fragments into a single HTML document and sends it to the browser.

-   **Pros:**
    -   **Improved Performance:** Faster initial page load (First Contentful Paint) because the browser receives a fully-formed HTML page.
    -   **Better SEO:** Search engine crawlers can easily index the content.
-   **Cons:**
    -   Increased server-side complexity and infrastructure costs.
    -   The server can become a performance bottleneck if not managed correctly.
