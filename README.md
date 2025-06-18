## What are microfrontends?
- Divide a monolithic app into multiple, smaller apps.
- Each smaller app is responsible for a distinct feature of the product.

### Why use them?
- Multiple engineering teams can work in isolation
- Each smaller app is easier to understand and make changes to.

### Major Categories of Integration of the Microfrontends in an application

1. **Build-Time Integration**

   Before the host app gets loaded in the browser, it gets access to MFE component.

   **Timeline 1**: Engineering team develops the MFE component.

   **Timeline 2**: Publish MFE component as NPM package.

   **Timeline 3**: The host app team install the MFE component as a dependency.

   **Timeline 4**: The host app build includes the all the code for the  MFE component 
   
   
3. **Run-Time Integration**

   After the host gets app loaded in the browser, it gets access to the MFE component.

4. **Server Integration**

   While sending down JS to load up the host app, a server decides on whether or not to include MFE component.  
