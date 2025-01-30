I always have been questioning on how does discord work and design choices required to make it have such a low latency??
Well its time to find out.

Here is what I have gather from their tech blogs
1. They have a cluster of NoSQL database servers (powered by ScyllaDB), each one serving a different data set
2. There is a need of low latency (that is database should respond to high frequencies of queries as fast as possible)
3. 