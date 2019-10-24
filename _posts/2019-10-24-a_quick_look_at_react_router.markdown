---
layout: post
title:      "A Quick Look at React Router"
date:       2019-10-24 04:16:46 +0000
permalink:  a_quick_look_at_react_router
---



As of React Router V4, routing via component composition has become the norm. This is what allows for dynamic routing. Dynamic routing occurs AS your app is rendering, rather than being declared beforehand, as in static routing. 

Thanks to dynamic routing, everything in your react app, including the route, can be rendered in component composition.
React Router comes with some handy components - Route, Link, and BrowserRouter (usually imported as just Router). These are imported from react-router-dom (because, understandably enough, we are using react router… for the DOM)

![](https://i.ibb.co/Vwddv44/react-router-dom.png)

Then when rendering App, we wrap everything in a Router component. The Router component allows React Router to pass the history and location props to your components, which allow you to do handy things like press the back button on a single page application.

Then we render route components, where we point to a path and then define a component we want to render when that path is called.

![](https://i.ibb.co/cLBkFfw/router-routes.png)

Above you can see I also passed an exact prop to my Route components, to ensure only an exact path match would trigger a rendering of the related component. (This is so that, for example, the path “/my-posts/new” won’t also render the “/my-posts” path component.)

Another detail above is that on two occasions I used the react router “render” prop, which accepts a functional component, allowing me to pass props to those components while still rendering them with react router.

Link components render an anchor tag that will change the route when clicked. In my case, I rendered my links in a separate Nav component.

![](https://i.ibb.co/M5GPhHr/NavLinks.png)

As you can see above, I also used NavLinks rather than just Links, because they allow for styling.

React router allows for a dynamic, logical, react-like experience in your react app.
