---
title: SOLID Principles
sidebar: mydoc_sidebar
permalink: javascript_solid_principle.html
folder: javascript
---

### Single Responsibility Principle

    - Every method/class should handle a single responsibility

    - 
    ```java
    import fetch from "node-fetch";

    const getPosts = async (userId: number) => {
    try {
        const response = await fetch(
        `https://jsonplaceholder.typicode.com/users/${userId}/posts`
        );
        const posts = await response.json();
        // Do some cleanup; remove UserID from post since it's not really needed
        const cleanedPosts = posts.map((post) => {
        delete post["userId"];
        return post;
        });
        return cleanedPosts;
    } catch (e) {
        // Log error in some kind of Error Logging Service, here we just do console log
        console.log(e);
        // Send a meaningful but non-technical error message back to the end-user
        throw Error("Error while fetching Posts!");
    }
    };

    const main = async () => {
    const result = await getPosts(1);
    console.log(result);
    };

    main();
    ```
