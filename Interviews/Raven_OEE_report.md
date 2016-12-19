### What toolchains or approaches do you use to validate and debug your code and system expression at runtime? Comment on the different approaches for when things are going right, and when things go wrong.  

First of all, I would use the embedded debug systems in IDEs to narrow down where the problem occurs in code. (In addition, I might also use print statements and make some small changes of the code to narrow down the problem further. Manual debug is more flexible in some cases.)


Under most circumstances, especially when the possible inputs and results are well defined, I would write tests to help me validate and debug my code. I would write as many tests as possible.


(If possible, I prefer to writing test cases for every functionality of the system. When it comes to locate the problem of a system, test cases would be very helpful. )



### Please describe your contributions to the project. What components were you personally responsible for, and what were their interfaces to the other components? How did those interfaces get defined?###


OEE(Overall Equipment Effectiveness) waterfall report is widely used by manufacturing to aggregate the time loss and up time of the machines in factories. Previously, all the reports were generated by hand. The customer sent a request email to Raven, then we generated a report according to the request, and sent it back. The whole process was slow and annoying.


Thus I was given the task to automate the generation of the OEE waterfall report. I was mainly responsible for the frontend development and build/deployment system. I spent a week to learn all the technologies needed such as React, Redux, D3 and Storybook. It was not easy at first, because I was the only one working on this project and things have been changing a lot since I worked on web development last time.


I first used static data to generate the report using React component and tested the UI using Storybook. Then I realized that the whole system was much more complicated than we thought, so I booked a meeting with the team to discuss about the implementation details. For example, when should we retrieve the data from the database and push to client side (push daily or push as request)? How to fetch the data and information needed asynchronously and still be Restful? How to design the interfaces? How to structure the code?


- When should we retrieve the data from the database and push to client side (push daily or push as request)?

I created a batch job on server to fetch the data on daily basis and store the data on the server. On the client side, the data will only be fetched if the requested data is not present on the client side.


- How to fetch the data and information needed asynchronously?

In Redux, action(Controller) is used to control the behavior of all the components(View) and stores(Model). I created asynchronous actions to fetch the data from server, and when the data was ready, then inform all the related components to update the UI and the store to update the data.


- How to design the interfaces?

I created container components in React to separate UI from the backend. Containers were connected to the store directly, so whenever an update action fired and store updated then the container would inform the UI component to refresh. Thus, people worked on UI did not need to worry about any backend details, all the information needed would be passed in by containers.



- How to structure the code?

I used the idea of MVC. In terms of the implementing MVC in redux/react. Models corresponds to redux stores. Views correspond to UI components. Controllers correspond to actions.



- What development environment and programming language did you use? Why?


  - WebStorm: Since I’ve been using intelliJ and PyCharm from JetBrain, it makes my life much easier to use a web development IDE from the same company. WebStorm provides intelligent auto completion, quick-fix suggestion and smart navigation.


  - Firefox & Chrome: The debug system is ideal for web development. Both support react+redux.


  - React: React helps build encapsulated components and it operates on virtual DOM(an abstraction of abstraction), so developers no longer need to call the HTML DOM(abstraction of a structured HTML: in-memory representation of the text/ time-consuming and bug-risky, inefficient searching) API explicitly. You simply declare how a component should look like. React does the low-level job for you.


  - Redux: React only handles the view layer and managing state of the data is left to developer. However, state management can be really troublesome and it’s hard to keep track of the state update as the web app has been increasingly complicated. Thus, Redux is needed for state management.


  - D3: Previously, plotly was used to draw the diagrams. However, it was really slow to load the diagrams. So I rewrote the code in d3.


  - Webpack: I used webpack to bundle JavaScript for the sake of future improvements. By the time I worked on the project, there were not many non-code static staff such as CSS, images, fonts. However, as those staff grows, it would be much easier to handle those files with webpack. Webpack can help manage all the dependencies in a dependency graph and bundle files. It allows you to lazy load bundle files dynamically and load dependencies as needed. Webpack-dev-server supports hot page reloading.


  - Npm: reuse code, package management


  - Storybook: for UI testing, comes with react. But only for eyeballing tests. Test each UI component separately.

  - Karma: for UI and functional testing(for a specific requirement of the software). I used it for functional tests mainly.


  - Thunk: Redux Thunk middleware allows you to write action creators that return a function instead of an action. The thunk can be used to delay the dispatch of an action, or to dispatch only if a certain condition is met.


  - Ansible: web deployment. Immutable server architecture: we can create, destroy, and replaces servers at any time without causing service disruption. Easy to learn, easy to code, easy to read.


