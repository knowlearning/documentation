# Recommended Application Scaffold

## Goal

The goal of this scaffold isn't to prescribe exactly how you should structure an app. Many apps won't need all the flexibility that this scaffold allows for, so they'll probably be better served by much simpler main scripts.

The goal of this scaffold is to demonstrate, as simply as possible, a fully fleshed out structure that provides clear places to make all important top-level application architecture decisions. This structure should work well with any front-end web application framework you want to use.

## 3 Answers Required for Initialization

Lets talk about 3 questions an app needs to answer before initialization:

1.  What user is running our app? ```@knowlearning/agents``` handles authentication for you:
    ```js
       const { auth: { user, provider } } = await Agent.environment()
    ```
    Now ```user``` will be the UUID that uniquely identifies your user (no matter who the provider is), and ```provider``` will be the single-sign-on provider the user logged in with (WARNING! ```provider``` may be ```"anonymous"```, in which case you probably want to show a login page).
2.  What content should the user see? Usually we use 2 pieces of information to decide. Both of those pieces are found in the URL of the app: the domain the user is using, and the "resource path" (all parts after the domain).
    1. We recommend that your app first checks if the path is a UUID. If it is a UUID, we recommend inspecting its metadata, then using its type to decide what kind of content you want to show.
    2. If the path is not a UUID, then your app makes the decision to show whatever component or content as it normally would (using a router for your framework, or whatever implementation you like best).
3. What data do we use as the "props" for the content?
    1. If the path is a UUID, then we recommend you use the data of that UUID to initialize the content.
    2. If the path is not a UUID, then the app decides as it normally would (perhaps using query parameters, hardcoded values, or even requesting specially named scopes for the user).

Once these questions are answered, an app has everything it needs to initialize. The recommended scaffold implementation we will dive into now will explicitly show how to answer these questions. As we're doing so we will discuss the many flexibilities and possible decisions for your unique app.
