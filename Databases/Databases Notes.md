A database is just a collection of data. the DBMS is the actual software that manages that data.

the main components of a DBMS are
1. the client communications manager - manages the connection between the client and the database server (where the DBMS runs)
2. the process manager - manages the assignment and scheduling of threads to begin the action
3. the relational query processor - compiles SQL query text into an internal query plan, optimizes the plan, and executes it via a suite of operators.
4. the transactional storage manager - manages all data access and manipulation. has algorithms for disk memory, buffer management, lock management.

To connect to a DBMS [[Connecting to the DB]], you need to form a connection between the database client and the database server, the connection of which is handled by a driver. for example:
- I write a python program using psycopg2 to connect to my postgres database. here,
	- my python program is the database client, issuing commands like SELECT this
	- psycopg2 implements the python DB-API and wraps around libpq, the C library that implements the postgres wire protocol. pyscopg2 is the driver that translates the python level commands into byte level commands (and translates the response back into python objects on return)
		- pyscopg3 and pg8000 are both pure python implementations by contrast
	- the postgres server is the backend which contains those 4 things above.
- I connect to MySQL Workbench to check on my SQL database. here,
	- Workbench itself is the client
	- MySQL C client library ```libmysqlclient``` is the driver that implements the MySQL protocol
	- the server is the server
- I open up DBeaver to look at my various different dbs
	- DBeaver is the client, written in Java and is the caller for the JDBC API...
	- ...which is implemented by the many different drivers that DBeaver can import in. these drivers connect to many different dbs.
	- Many different servers.

Process model options:
- process per DBMS worker
	- isolation and fault tolerant
- thread per DBMS worker
	- os thread per worker
	- userspace thread per worker
- process pool

Keep in mind the textbook was written in 2007, before a lot of modern advances in OSes. [[Evolution of OSes]]

DBMS workers need to be able to share some data with each other, these include:
- Disk I/O buffers
	- Database buffer pool
	- Log tail
- Client communication buffers, used to 
- Lock table