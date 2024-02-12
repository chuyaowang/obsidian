# Work with .json files

## Reading

To read as a list:
``` R
library(rjson)
data <- fromJSON(file = "dir")
```

To read as a data.frame:
``` R
library(jsonlite)
data <- fromJSON(txt = "dir", flatten=TRUE)
```

