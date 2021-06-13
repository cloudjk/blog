---
title: mysql error
sidebar: mydoc_sidebar
permalink: mysql_error.html
folder: mysql
---
## Illegal mix of collations for operation 'concat'  
#### This is due to collections difference, you can solve by converting the two strings or columns to one collection say UTF8
```java
CONCAT(CAST(fName AS CHAR CHARACTER SET utf8),CAST('' AS CHAR CHARACTER SET utf8))
```