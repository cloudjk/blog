---
title: What is NODE_ENV and How to set in Express
sidebar: mydoc_sidebar
permalink: node_process_env_node_env.html
folder: node
---

### Production mode, Development mode

1. Production mode : add file caching, hide detailed error message etc...
2. Development mode : disable file caching, show detailed error message etc...

### How to check what mode the current system is in

```javascript
// insert below at the first line app.js(index.js)
process.env.NODE_ENV = (process.env.NODE_ENV && (process.env.NODE_ENV).trim().toLowerCase() == 'production') ? 'production' : 'development';
```

### How to diverge to different mode variables

```javascript
// can put in below anywhere
if (process.env.NODE_ENV == 'production') {
    console.log('Production Mode');
} else {
    console.log('Development Mode');
}
```

### How to set NODE_ENV

```bash
export NODE_ENV=production
```

### How to get NODE_ENV 1

1. printenv
2. echo $NODE_ENV
3. (REPL) node > process.env

### How to delete NODE_ENV

```bash
delete process.env.API_Key;
```
