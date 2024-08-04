
-               +--------------------------------------+ 
+-----+           +---------+     +-------+       +-----+          +----------+
|client| <--> |   |controller|<-> | service | <-> | repo |  | <--> | Database |
+-----+           +---------+     +-------+       +-----+          +----------+
-               +--------------------------------------+ 

- client can be a browser or mobile app.
- client sends http requests to controller
- controller routes those requests to service layer which generates results
- if service needs to get data from database it sends the requests of data to repo layer which talks with database
- finally controller sends the result back to client
- 