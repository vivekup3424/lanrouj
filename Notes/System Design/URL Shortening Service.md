**Problem Statement :**

Design a URL Shortener system that converts long URLs into short, easy-to-share links while ensuring efficient redirection to the original URL. The system should support link creation, retrieval, and tracking of usage metrics. It must be scalable, fault-tolerant, and capable of handling high traffic with minimal latency.

**What is a URL Shortening service ?**

A URL shortening service takes a long, complex web address and converts it into a shorter, more manageable link. This shorter URL redirects users to the original destination, making sharing links easier and cleaner

For example, shortening a given url will look like :

Old URL : `https://leetcode.com/discuss/interview-question/system-design?currentPage=1&orderBy=hot&query=`

Short URL : `https://bit.ly/4izy9Dn`

**Requirements for URL Shortner Service System Design :**

**1.) Functional Requirements :**

1. Generate a short and unique URL for a given Long URL.
2. When user hits the short URL, it should redirect to the Original URL
3. Retrieve the Original URL from the Short URL

**2.) Non-Functional Requirements :**

1. The system should have a very low latency.
2. The system should have high availability.
3. The system should have good fault tolerance.
4. The system should be scalable.

**API Design :**

1. **Create Short URL :**

- Description : Since we are creating a new short URL from the original URL, this operation is implemented as a POST request. It takes a long URL and returns a shortened URL. Optional fields like a custom alias or expiration date can be included.
    
- Endpoint : `POST /api/v1/createShortUrl`
    
- Request Body: `{ "url": "https://leetcode.com/discuss/interview-question/system-design?currentPage=1&orderBy=hot&query=" }`
    
- Response : `{"shortUrl" : ''https://bit.ly/4izy9Dn"}`
    
- Status Code : 1.) 201: Created successfully.  
    2.) 400: Bad request. An error occurred. (In-case of an error)
    

2. **Redirect to Original URL :**

- Description : When a user accesses the short URL, they are redirected to the original URL.
    
- Endpoint :`GET /api/v1/{shortUrl}`
    
- Request Parameteres: `{shortUrl}`
    
- Response : `Redirect to the Original URL`
    
- Status Code : 301: Permanent Redirect.
    

3. **Update Short URL :(Optional)**

- Description : Updates the destination URL for an existing short URL.
    
- Endpoint : `PUT /api/v1/updateShortUrl/{shortUrl}`
    
- Request Parameteres: ```{shortUrl}``
    
- Request Body : `{"url" : ""https://leetcode.com/discuss/interview-question/system-design?currentPage=1&orderBy=hot&query="}`
    
- Response : `{"Status : Successfull" , "message : "Short URL updated successfully"}`
    
- Status Code : 200, as we are returning the status message from the server, if we weren't returning a proper response from the server, we would have used 204 status code for no content.
    

**Database Design :**

When designing a URL shortening service, one of the most crucial aspects to consider is the database design. The system needs to efficiently store original URLs, their shortened counterparts, and ensure fast redirection for users. We can choose either an SQL-based or NoSQL-based database, each offering its own set of advantages.

**Why NoSQL Databases Tend to Be a Better Fit :**

1. **Scalability :** URL shortening services can experience rapid growth in traffic and data. NoSQL databases are built for horizontal scalability, meaning they can distribute data across multiple servers. This allows them to handle high volumes of traffic and large datasets much more efficiently than SQL databases, which typically require vertical scaling (adding more power to a single server). For URL shortening services with millions of users and billions of redirects, NoSQL ensures that the database can grow seamlessly without bottlenecks.
    
2. **High Availability and Fault Tolerance :** NoSQL databases like MongoDB or Cassandra are designed with high availability in mind, often offering automatic replication and failover. This means that even if one server goes down, the data is replicated across other servers, ensuring that the URL shortening service remains operational with minimal downtime. In contrast, SQL databases can be more complex and expensive to set up for high availability, especially when dealing with large-scale applications.
    
3. **Flexibility and Schema-less Design :** URL shortening services often evolve over time. Initially, you may only need to store the original URL and its shortened version, but later you might want to track metadata such as expiration times, user access logs, or analytics data. NoSQL databases allow you to store this data without rigid schemas, giving you the flexibility to adjust the database design as needed without affecting existing data. This level of flexibility makes NoSQL databases ideal for services that require rapid changes and scalability.
    

**Database Schema Example :**

Now that we have decided to use a NoSQL-based database, such as MongoDB, let’s explore a basic and simple schema for our URL Shortener system. This schema will serve as the foundation for storing essential data efficiently while supporting the core functionalities of the service.

1. longUrl: The original long URL provided by the user. This field will store the full URL to be shortened.
    
2. shortUrl: The shortened version of the URL, which will be generated and provided to the user. This will be unique for each original URL.
    
3. createdAt: The timestamp when the short URL was created. This allows us to track the creation time for each shortened URL, which could be useful for future enhancements like expiration times or analytics.
    

The database Schema will look like this :

```
{
  "_id": ObjectId("unique_id") (Auto Generated by MongoDB),
  "longUrl": "https://leetcode.com/discuss/interview-question/system-design?currentPage=1&orderBy=hot&query=",
  "shortUrl": "https://bit.ly/4izy9Dn",
  "createdAt": ISODate("2024-12-15T00:00:00Z")
}
```

**High Level Design :**  

![[Pasted image 20241215224357.png]]

**Overview of High Level Design :**

The design focuses on creating a highly scalable, fault-tolerant, and low-latency system for shortening URLs and redirecting users efficiently. The architecture includes several critical components working in coordination to process requests, distribute loads, and provide fast redirections.

1. **User Interaction :**  
    The user initiates a request to the system, such as creating a short URL or accessing a short URL to get redirected to the original URL. The user interacts with the system through an API, which is forwarded to the Load Balancer.
    
2. ***Load Balancer :**  
    The Load Balancer serves as the entry point to the system. Its role is to distribute incoming requests across multiple web servers to ensure even workload distribution. It prevents any single server from becoming a bottleneck and improves fault tolerance.  
    After receiving the processed data from the API gateway, the load balancer sends the response back to the user.
    
3. **API Gateway :**  
    The API Gateway is responsible for routing requests to the appropriate backend server. It adds another layer of abstraction and simplifies request handling.  
    Key tasks of the API Gateway include:
    

- Routing: It selects an available web server from the pool (Web Server 1, 2, or 3).
- Managing Traffic: It handles incoming API requests like creating short URLs or redirections.
- Returning Data: After receiving the processed response, it forwards the data back to the Load Balancer.

4. **Distributed Web Servers :**  
    The system has multiple Web Servers (Web Server 1, Web Server 2, Web Server 3) that process incoming API requests. These servers handle tasks like Generating a short URL for a given long URL.  
    Checking for an existing short URL in the Cache Layer or Database, Redirecting users to the original URL.
    
5. **Cache Layer (Redis / Memcached) :**
    

- The Cache Layer stores frequently accessed URLs to speed up redirection and reduce database load.
    
- When a short URL is accessed, the web server first checks if the corresponding original URL exists in the cache. If the URL is found in the cache, It is returned directly to the user, significantly reducing latency. If the URL is not found in the cache, then the system queries the Database to retrieve the original URL.After retrieving the data, the cache is updated so that subsequent requests for the same URL are served faster.
    

6. **Database (MongoDB) :**  
    The Database is the primary storage system for the URL Shortener. All data, including long URLs, short URLs, and metadata (like creation date), is stored here.

**Work Flow for API Endpoints :**

1. **Create Short URL :**

- The user sends a POST request to create a short URL.
- The request is passed to the Load Balancer → API Gateway → Web Server.
- The Web Server generates a unique short URL and stores the mapping (short URL ↔ original URL) in the Database.
- The Cache Layer is updated to store this mapping for future requests.
- A response containing the short URL is sent back to the user.

2.) **Redirect to Original URL :**

- The user accesses a short URL, triggering a GET request.
- The request is passed through the Load Balancer → API Gateway → Web Server.
- The Web Server checks the Cache Layer:
- If the short URL exists in the cache, the original URL is returned immediately.
- If not, the Web Server retrieves the original URL from the Database and updates the cache.
- The user is redirected to the original URL.

**Design Trade-Offs :**

1. ) **Database Choice (Sql vs NoSql) :**

- Opting for a NoSQL database like MongoDB provides scalability, flexibility, and high throughput for write-heavy workloads. However, it sacrifices strong ACID compliance, which traditional SQL databases provide.
- In our case, we prioritize performance and scalability but may need to manage data integrity manually, especially for edge cases like duplicate URL entries or concurrent writes.

2.) **Vertical Scaling vs Horizontal Scaling :**

- The current system design leverages horizontal scaling by adding more web servers or cache nodes to handle increasing traffic. However, the database (MongoDB) may still require vertical scaling (adding more resources like CPU, memory, or blob storage) as the dataset grows.
    
- Horizontal scaling improves system resilience and load handling, while relying on vertical scaling for the database introduces a bottleneck. While NoSQL databases like MongoDB support distributed scaling, ensuring seamless performance at massive scale requires careful management of resources and potential sharding.
    

3.) **Stateless vs Stateful Architecture :**

- The system follows a stateless architecture, where each request is independent and does not rely on server-side session information. This simplifies scalability, as any web server can handle incoming requests without needing to maintain state.
    
- While stateless design improves scalability and fault tolerance, it requires consistent integration with the database and cache layers to store and retrieve data. This reliance on external components like MongoDB and the cache layer introduces a trade-off, as their failure could affect the overall system performance.