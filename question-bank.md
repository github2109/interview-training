# .NET Backend Interview Question Bank

# 1. Junior Level

## 1.1 C# Fundamentals

### 1. What are the four main principles of OOP?

**Follow-ups** - Can you explain encapsulation with a real example? -
What is the difference between abstraction and encapsulation? - What is
polymorphism? Can you give a C# example? - When would inheritance be
useful, and when would composition be preferable?

### 2. What is the difference between a class and an object?

**Follow-ups** - What happens when you instantiate a class? - Can a
class exist without any instances? - What is the difference between
static and instance members?

### 3. What is the difference between a value type and a reference type?

**Follow-ups** - What are some examples of each? - What happens when you
assign one value type variable to another? - What happens when you
assign one object variable to another? - Is a `string` a value type or
reference type? - Are value types always stored on the stack?

### 4. What is the difference between `class` and `struct`?

**Follow-ups** - When would you choose a struct? - What problems can
large structs cause? - Can a struct implement an interface? - Can a
struct inherit from another struct/class?

### 5. What is the difference between `const` and `readonly`?

**Follow-ups** - When is a `const` value determined? - Can a readonly
field be assigned in a constructor? - What happens when a library
changes a public `const` value?

### 6. What are access modifiers in C#?

**Follow-ups** - Difference between `private`, `protected`, and
`internal`? - What does `protected internal` mean? - What does
`private protected` mean?

### 7. What is the difference between an abstract class and an interface?

**Follow-ups** - Can an abstract class contain implemented methods? -
Can an interface contain implementations in modern C#? - Can a class
inherit from multiple classes? - Can a class implement multiple
interfaces? - Give an example where you would choose an interface.

### 8. What is method overloading?

**Follow-ups** - Can overloaded methods differ only by return type? -
How does overload resolution work? - What is the difference between
overloading and overriding?

### 9. What is the difference between `override`, `virtual`, and `new`?

**Follow-ups** - What happens if a derived class uses `new` instead of
`override`? - Why can this produce surprising behavior when using a
base-class reference? - What does `sealed override` do?

### 10. What are nullable types?

**Follow-ups** - What is the difference between `int` and `int?`? - What
is nullable reference type support? - What is the difference between
`null`, `Nullable<T>`, and `default`? - What does the null-coalescing
operator `??` do?

------------------------------------------------------------------------

## 1.2 Collections and Generics

### 11. What is the difference between an array and `List<T>`?

**Follow-ups** - How does a `List<T>` grow? - What is the complexity of
accessing an element? - What happens when you insert into the middle of
a list? - When would you prefer an array?

### 12. What are `Dictionary<TKey,TValue>` and `HashSet<T>` used for?

**Follow-ups** - What is the average complexity of lookup? - What
happens if two dictionary keys are equal? - How does hashing work at a
high level? - What makes a good dictionary key?

### 13. What is the difference between `IEnumerable<T>`, `ICollection<T>`, and `IList<T>`?

**Follow-ups** - Why might returning `IEnumerable<T>` be useful? - Does
`IEnumerable<T>` guarantee random access? - Does an `IEnumerable<T>`
necessarily represent an in-memory collection?

### 14. What are generics and why are they useful?

**Follow-ups** - What problem do generics solve compared with
`object`? - What is type safety? - What is a generic constraint? - Have
you used `where T : class`, `struct`, or `new()`?

### 15. What is boxing and unboxing?

**Follow-ups** - What happens when an `int` is assigned to an
`object`? - Why can boxing affect performance? - Can generics avoid
boxing?

### 16. What does `yield return` do?

**Follow-ups** - Is the entire result generated immediately? - What is
deferred execution? - What happens if the caller only consumes the first
few items? - What problems can occur if the underlying resource is
disposed before enumeration?

------------------------------------------------------------------------

## 1.3 LINQ

### 17. What is LINQ?

**Follow-ups** - What is the difference between `Where`, `Select`, and
`SelectMany`? - What is the difference between `First`,
`FirstOrDefault`, `Single`, and `SingleOrDefault`? - When would `Any()`
be preferable to `Count() > 0`?

### 18. What is deferred execution in LINQ?

**Follow-ups** - When does a LINQ query actually execute? - What changes
if you call `ToList()`? - Can deferred execution cause a query to
execute multiple times? - Why can this matter with database queries?

### 19. What is the difference between `IEnumerable<T>` and `IQueryable<T>`?

**Follow-ups** - Where is the filtering performed? - What happens when
an EF Core query is converted to `IEnumerable` too early? - Why can
`AsEnumerable()` change performance?

------------------------------------------------------------------------

## 1.4 Exceptions and Error Handling

### 20. What is an exception?

**Follow-ups** - What is the purpose of `try`, `catch`, and `finally`? -
When might `finally` not execute? - What is the difference between
`throw;` and `throw ex;`? - Should you catch every exception?

### 21. When should you create a custom exception?

**Follow-ups** - When is a custom exception useful? - When would a
result/error object be preferable? - Should business validation always
use exceptions?

### 22. How should exceptions be handled in a Web API?

**Follow-ups** - Should controllers contain large `try/catch` blocks? -
What is centralized exception handling? - How would you return a
consistent error response? - What information should not be exposed to
clients?

------------------------------------------------------------------------

## 1.5 Async / Await

### 23. What are `async` and `await`?

**Follow-ups** - Does `async` automatically create a new thread? - What
happens while an async I/O operation is waiting? - What does `await`
actually do? - What is the difference between asynchronous and parallel
execution?

### 24. What is the difference between `Task` and `Thread`?

**Follow-ups** - When would you actually need a dedicated thread? - What
does the ThreadPool do? - Why are asynchronous I/O operations usually
preferable for web APIs?

### 25. What happens if you forget to `await` a Task?

**Follow-ups** - What does the method return? - What happens to
exceptions? - What is fire-and-forget? - Why is fire-and-forget
dangerous in ASP.NET Core?

### 26. What is `Task.WhenAll()`?

**Follow-ups** - How is it different from awaiting tasks one at a
time? - When is parallel execution appropriate? - What happens if one of
the tasks fails? - What if the operations modify the same shared state?

------------------------------------------------------------------------

## 1.6 .NET Runtime

### 27. What is the CLR?

**Follow-ups** - What responsibilities does the CLR have? - What is
managed code? - What is JIT compilation? - What is the difference
between .NET runtime and the C# compiler?

### 28. What is the Garbage Collector?

**Follow-ups** - Why does .NET need a GC? - What are GC generations? -
What are Gen 0, Gen 1, and Gen 2? - What is a large object heap? - Can a
managed application still have memory leaks?

### 29. What is `IDisposable`?

**Follow-ups** - Why does `Dispose()` exist if .NET has garbage
collection? - What resources normally need disposal? - What does the
`using` statement do? - What is `IAsyncDisposable`?

------------------------------------------------------------------------

## 1.7 ASP.NET Core

### 30. What is ASP.NET Core?

**Follow-ups** - How is ASP.NET Core different from classic ASP.NET? -
What is middleware? - What is dependency injection? - What is the
request pipeline?

### 31. What is middleware?

**Follow-ups** - How does middleware execute? - What happens if
middleware does not call the next delegate? - Where would you put
logging middleware? - Where would authentication/authorization
middleware be placed?

### 32. What is dependency injection?

**Follow-ups** - Why use DI instead of `new` everywhere? - What are
constructor injection, method injection, and property injection? - What
makes a dependency easy or difficult to test? - What is dependency
inversion?

### 33. Explain Singleton, Scoped, and Transient lifetimes.

**Follow-ups** - Which lifetime is commonly used for request-scoped
services? - What happens if a singleton depends directly on a scoped
service? - When would a singleton be appropriate? - What problems can
shared mutable state create in singleton services?

### 34. What is REST?

**Follow-ups** - What makes an API RESTful? - What is the difference
between a resource and an action? - When should you use GET, POST, PUT,
PATCH, and DELETE? - Which HTTP methods are idempotent?

### 35. What is the difference between GET and POST?

**Follow-ups** - Should GET have a request body? - Is POST always
non-idempotent? - Can GET change server state? - When would you use
query parameters versus a request body?

------------------------------------------------------------------------

## 1.8 HTTP and Web Basics

### 36. What are common HTTP status codes?

**Follow-ups** - Difference between `400`, `401`, `403`, and `404`? -
When would you return `409 Conflict`? - When is
`422 Unprocessable Entity` useful? - What is the difference between
`500` and `503`?

### 37. What is JSON?

**Follow-ups** - What are its advantages and disadvantages? - What is
serialization/deserialization? - How does ASP.NET Core serialize objects
by default? - What can go wrong when serializing circular references?

### 38. What happens at a high level when a browser requests an HTTPS API?

**Follow-ups** - What does DNS do? - What is TCP? - What does TLS
provide? - Why does HTTPS use certificates? - Where does HTTP fit into
the stack?

------------------------------------------------------------------------

## 1.9 Databases and SQL

### 39. What is the difference between a relational and a non-relational database?

**Follow-ups** - When would you choose SQL over NoSQL? - What are
transactions? - What does consistency mean? - What are common reasons to
use a document database?

### 40. What is a database index?

**Follow-ups** - Why does an index make reads faster? - Why can too many
indexes be bad? - What happens to INSERT/UPDATE performance? - What
makes a column a good index candidate?

### 41. What are SQL JOINs?

**Follow-ups** - Difference between INNER JOIN and LEFT JOIN? - What
happens when a row has no matching record? - Can JOINs produce duplicate
rows? - How would you investigate a slow JOIN?

### 42. What is a primary key?

**Follow-ups** - What makes a good primary key? - Can a table have
multiple primary keys? - What is a composite primary key? - What is the
difference between a primary key and a unique constraint?

------------------------------------------------------------------------

## 1.10 Testing

### 43. What is a unit test?

**Follow-ups** - What makes a unit test different from an integration
test? - What are Arrange, Act, Assert? - What should you mock? - Should
you mock every dependency?

### 44. What is an integration test?

**Follow-ups** - What would you test with an integration test in an
ASP.NET Core API? - Should an integration test use a real database? -
What are the advantages and disadvantages of test containers?

### 45. What makes a good test?

**Follow-ups** - What does deterministic mean? - What makes a test
brittle? - Should tests verify implementation details or behavior? -
What is the difference between test coverage and test quality?

------------------------------------------------------------------------

# 2. Mid-Level

A mid-level candidate should move beyond definitions and explain
**trade-offs, runtime behavior, production failure modes, and practical
design decisions**.

## 2.1 Advanced C

### 46. What is the difference between `ref`, `in`, and `out`?

**Follow-ups** - When would you use each? - Does `ref` always improve
performance? - What restrictions apply to `in` parameters? - Why should
these features not be used just because they exist?

### 47. What are delegates and events?

**Follow-ups** - What is the difference between a delegate and an
event? - Why can't arbitrary consumers invoke an event from outside its
declaring type? - Where have you used delegates in real code? - How do
delegates relate to LINQ?

### 48. What are extension methods?

**Follow-ups** - How does the compiler resolve an extension method? -
Can an extension method override an instance method? - When can
extension methods make code worse?

### 49. What are records and when would you use them?

**Follow-ups** - How are records different from classes? - What does
value-based equality mean? - What is the `with` expression? - When would
a normal class be more appropriate?

### 50. What are primary constructors in modern C#?

**Follow-ups** - Are primary constructor parameters automatically
properties? - How do they work with dependency injection? - When would a
traditional constructor be clearer?

### 51. What are pattern matching features in modern C#?

**Follow-ups** - Explain type patterns, property patterns, and switch
expressions. - How can pattern matching improve validation or command
handling? - When can a complex pattern become harder to read than normal
code?

------------------------------------------------------------------------

## 2.2 Async, Concurrency, and Parallelism

### 52. Explain the difference between asynchronous programming, concurrency, and parallelism.

**Follow-ups** - Can async code run on one thread? - Can parallel code
be asynchronous? - Which approach is normally useful for
database/network I/O? - Which approach is useful for CPU-heavy work?

### 53. What is a synchronization context?

**Follow-ups** - Does ASP.NET Core have the same synchronization-context
behavior as older ASP.NET? - Why can `.Result` and `.Wait()` be
dangerous? - What is sync-over-async?

### 54. Why should ASP.NET Core code generally avoid blocking on async operations?

**Follow-ups** - What is thread-pool starvation? - How can `.Result`
create latency under load? - How would you detect thread-pool
starvation?

### 55. What is a race condition?

**Follow-ups** - Give a real backend example. - How would you protect
shared state? - What are `lock`, `SemaphoreSlim`, and concurrent
collections used for? - When is a distributed lock necessary?

### 56. What is `CancellationToken`?

**Follow-ups** - Why should APIs accept cancellation tokens? - How would
cancellation propagate from an HTTP request to a database call? - What
happens if a dependency ignores cancellation? - Should cancellation be
logged as an error?

### 57. When would you use `Task.WhenAll()` versus sequential awaits?

**Follow-ups** - What if operations depend on each other? - What if
there are 10,000 operations? - Would you start all 10,000 tasks
immediately? - How would you limit concurrency?

------------------------------------------------------------------------

## 2.3 LINQ and Performance

### 58. Explain deferred execution in more depth.

**Follow-ups** - Can a LINQ query enumerate a database multiple times? -
What happens if the source collection changes between enumerations? -
When would you materialize a query?

### 59. What is the difference between `IEnumerable` and `IQueryable` in EF Core?

**Follow-ups** - What happens if you call `ToList()` too early? - Which
parts of a query are translated to SQL? - What happens when EF cannot
translate an expression? - How would you inspect the generated SQL?

### 60. How would you optimize a LINQ query that is unexpectedly slow?

**Follow-ups** - Would you start by rewriting the LINQ? - How would you
determine whether the problem is CPU, database, network, or
allocation? - How would you inspect the generated SQL? - What metrics
would you collect?

------------------------------------------------------------------------

## 2.4 ASP.NET Core Architecture

### 61. Explain the ASP.NET Core request pipeline.

**Follow-ups** - Where does routing happen? - Where does authentication
happen? - Where does authorization happen? - Where should exception
handling happen? - What is endpoint middleware?

### 62. What is the difference between middleware, filters, and endpoint filters?

**Follow-ups** - When would you use middleware? - When would an MVC
action filter be more appropriate? - What belongs in a global exception
handler? - What logic should not be implemented as middleware?

### 63. How would you structure a medium-sized .NET Web API?

**Follow-ups** - Would you use controllers, services, repositories,
handlers, or something else? - Which layers should know about EF Core? -
Where should business rules live? - How do you avoid creating
abstractions for everything?

### 64. What is the difference between a DTO, domain model, and persistence model?

**Follow-ups** - Should EF entities be returned directly from APIs? -
Why can exposing database entities become a problem? - When is using the
same type acceptable? - How would you handle versioning?

### 65. What is dependency inversion, and how does it affect application architecture?

**Follow-ups** - What is the difference between an abstraction and an
interface created just for mocking? - Can excessive abstraction make a
system harder to understand? - How do you decide where an interface
belongs?

------------------------------------------------------------------------

## 2.5 Dependency Injection

### 66. Explain DI lifetimes with a real web request example.

**Follow-ups** - Why is `DbContext` normally scoped? - Can a singleton
safely depend on a scoped service? - How can a singleton create a scope
when it genuinely needs scoped work? - What problems can captured scoped
dependencies cause?

### 67. What is the captive dependency problem?

**Follow-ups** - Give an example. - How would you detect it? - Why is it
especially dangerous with `DbContext` or request context?

### 68. What is the difference between `IServiceProvider` usage and constructor injection?

**Follow-ups** - When does service location become an anti-pattern? -
Are there legitimate cases for creating a scope manually? - How would
you prevent a large class from turning into a service locator?

------------------------------------------------------------------------

## 2.6 Entity Framework Core

### 69. What is `DbContext`?

**Follow-ups** - Is `DbContext` thread-safe? - Why is it usually
scoped? - What is change tracking? - What happens when a `DbContext` is
disposed?

### 70. What is the difference between tracking and `AsNoTracking()`?

**Follow-ups** - When does tracking help? - When does it hurt
performance? - What happens if you modify an entity returned by a
no-tracking query?

### 71. What is the N+1 query problem?

**Follow-ups** - Give an example. - How can eager loading, projection,
or explicit loading help? - Is `Include()` always the best solution? -
How would you verify that N+1 is happening?

### 72. What is optimistic concurrency?

**Follow-ups** - What happens if two requests update the same record? -
What is a concurrency token/row version? - How should an API respond to
a concurrency conflict? - When would pessimistic locking be appropriate?

### 73. What is a database transaction?

**Follow-ups** - What are atomicity, consistency, isolation, and
durability? - When should multiple operations be in the same
transaction? - What happens if an external API call is made inside a
database transaction? - Why can long transactions be problematic?

------------------------------------------------------------------------

## 2.7 SQL and Database Design

### 74. Explain database normalization.

**Follow-ups** - What problems does normalization solve? - When might
denormalization be useful? - What is the trade-off between normalized
writes and read performance?

### 75. What are transaction isolation levels?

**Follow-ups** - What are dirty reads? - What are non-repeatable
reads? - What are phantom reads? - What does snapshot isolation
provide? - What isolation level does your database normally use?

### 76. How would you investigate a slow SQL query?

**Follow-ups** - Would you look at the execution plan? - What is an
index scan versus an index seek? - How can a function applied to a
column affect index usage? - How can parameterization affect
performance? - How would you determine whether the database or
application is the bottleneck?

### 77. What is connection pooling?

**Follow-ups** - Why don't applications normally create a new
TCP/database connection for every query? - What happens when the pool is
exhausted? - How can connection leaks happen? - How can long-running
queries affect the pool?

------------------------------------------------------------------------

## 2.8 API Design

### 78. How would you design a REST endpoint for creating a resource?

**Follow-ups** - What should the response status be? - What should
happen if the resource already exists? - How would you validate input? -
How would you make the operation idempotent?

### 79. What is idempotency?

**Follow-ups** - Which HTTP methods are normally idempotent? - Why does
idempotency matter for payment/order APIs? - How would you implement an
idempotency key? - Where would you store idempotency state?

### 80. How would you version a public API?

**Follow-ups** - URL versioning vs header versioning? - How long should
old versions remain supported? - What is a breaking API change? - How
would you evolve a response without breaking clients?

### 81. How would you implement pagination?

**Follow-ups** - Offset pagination vs cursor/keyset pagination? - What
happens when records are inserted while a user is paging? - How would
you sort results deterministically? - What indexes would you need?

------------------------------------------------------------------------

## 2.9 Caching

### 82. Why use caching?

**Follow-ups** - What makes something a good cache candidate? - What are
cache invalidation problems? - What is cache-aside? - What is the
difference between local memory cache and distributed cache?

### 83. How would you cache data in a multi-instance API?

**Follow-ups** - Why might `IMemoryCache` be insufficient? - When would
Redis be useful? - What happens if the cache is unavailable? - How do
you prevent a cache stampede?

### 84. What is cache stampede/thundering herd?

**Follow-ups** - How can it happen? - How can locking or request
coalescing help? - What are stale-while-revalidate strategies?

------------------------------------------------------------------------

## 2.10 Messaging and Background Processing

### 85. Why use a message queue?

**Follow-ups** - What problems does asynchronous messaging solve? - What
are the trade-offs compared with synchronous HTTP? - What is eventual
consistency? - What happens if the consumer is temporarily down?

### 86. What is at-least-once delivery?

**Follow-ups** - Can a message be processed twice? - How should
consumers handle duplicates? - What is idempotent message processing? -
How would you design a deduplication mechanism?

### 87. What is a dead-letter queue?

**Follow-ups** - When should a message be dead-lettered? - How many
retries would you allow? - What is exponential backoff? - How would you
investigate a growing dead-letter queue?

### 88. How would you implement a background worker in ASP.NET Core?

**Follow-ups** - What is `BackgroundService`? - How should it handle
cancellation? - How should exceptions be handled? - How do you prevent
overlapping executions? - What changes when you run multiple application
instances?

------------------------------------------------------------------------

## 2.11 Logging and Observability

### 89. What should a backend service log?

**Follow-ups** - What should never be logged? - What is structured
logging? - Why is a correlation/request ID useful? - How would you trace
one request across multiple services?

### 90. What is the difference between logs, metrics, and traces?

**Follow-ups** - What would you use to investigate high latency? - What
would you use to identify error-rate increases? - What is distributed
tracing? - What is a dependency span?

### 91. An API suddenly becomes slow. How would you investigate it?

**Follow-ups** - What metrics do you check first? - How do you
distinguish application latency from database latency? - How would you
identify an external API causing the delay? - What if average latency is
normal but p95/p99 is high?

------------------------------------------------------------------------

# 3. Senior Level

Senior interviews should focus on **system behavior, trade-offs,
reliability, scalability, security, architecture, and production
debugging**.

## 3.1 Architecture and Design

### 92. How would you design a backend service expected to handle high traffic?

**Follow-ups** - Where are the likely bottlenecks? - How would you scale
horizontally? - Which components would be stateless? - Where would
caching help? - What would you monitor?

### 93. How do you decide whether a system should be a monolith or microservices?

**Follow-ups** - What problems do microservices introduce? - When is a
modular monolith preferable? - How do you identify service boundaries? -
What does independent deployment actually require?

### 94. What is the difference between horizontal and vertical scaling?

**Follow-ups** - What are the limits of each? - What happens to
in-memory state when horizontally scaling? - How do sessions and caches
change the architecture?

### 95. How would you design a system that must remain available if one application instance dies?

**Follow-ups** - What state can safely live in process memory? - What
should be externalized? - How would load balancing work? - What happens
to in-flight requests? - What happens to background jobs?

### 96. Explain eventual consistency.

**Follow-ups** - When is eventual consistency acceptable? - Give a real
business example. - How should the UI/API communicate temporarily stale
data? - How would you reconcile inconsistent state?

------------------------------------------------------------------------

## 3.2 Distributed Systems

### 97. What problems occur when a system is distributed across multiple services?

**Follow-ups** - Network failures? - Timeouts? - Duplicate requests? -
Partial failures? - Clock differences? - Data consistency? - Service
discovery?

### 98. Why should every external HTTP call have a timeout?

**Follow-ups** - What happens if you don't? - Should all dependencies
have the same timeout? - What is the relationship between timeout and
retry? - How can retries make an outage worse?

### 99. Explain retry, timeout, circuit breaker, and bulkhead patterns.

**Follow-ups** - When should you retry? - Which errors should not be
retried? - Why should retries use backoff and jitter? - What is retry
amplification? - What happens when the downstream system is completely
unavailable?

### 100. How would you design an idempotent distributed operation?

**Follow-ups** - Where does the idempotency key come from? - What state
must be persisted? - What happens if the first request succeeds but the
response is lost? - What if two requests with the same idempotency key
arrive concurrently?

### 101. What is the distributed transaction problem?

**Follow-ups** - Why is a normal database transaction insufficient
across two services? - What is the Saga pattern? - What are compensating
actions? - What are the trade-offs of eventual consistency?

------------------------------------------------------------------------

## 3.3 Messaging at Scale

### 102. How would you design a reliable message consumer?

**Follow-ups** - What happens if processing fails? - How do you handle
duplicate messages? - How do you handle poison messages? - How do you
preserve ordering when ordering matters? - How do you scale consumers?

### 103. What is the difference between competing consumers and pub/sub?

**Follow-ups** - When would multiple consumers share the same queue? -
When would each subscriber need its own copy? - How does partitioning
affect throughput and ordering?

### 104. How would you guarantee that a database update and message publication stay consistent?

**Follow-ups** - What is the transactional outbox pattern? - Why can
"update DB, then publish message" lose events? - What happens if the
message is published but DB commit fails? - How would you process the
outbox reliably?

------------------------------------------------------------------------

## 3.4 Performance

### 105. An API endpoint takes 10 seconds in production but 500 ms locally. How do you investigate?

**Follow-ups** - What evidence would you collect before changing code? -
How would you separate network, database, CPU, and dependency latency? -
Would you profile first? - What production-only factors could explain
the difference?

### 106. CPU usage is high on a .NET service. What would you investigate?

**Follow-ups** - What is consuming CPU? - How would you distinguish
application CPU from GC CPU? - Could excessive serialization cause it? -
Could inefficient LINQ cause it? - Could a busy loop or retry loop cause
it?

### 107. Memory usage keeps increasing. What would you investigate?

**Follow-ups** - How do you distinguish a real memory leak from normal
GC behavior? - What kinds of objects commonly remain rooted
unexpectedly? - How can event handlers cause object retention? - What
tools can you use to inspect managed memory?

### 108. What causes thread-pool starvation?

**Follow-ups** - How can synchronous I/O cause it? - How can excessive
blocking calls cause it? - What symptoms would appear in production? -
How would you verify the diagnosis?

------------------------------------------------------------------------

## 3.5 Database Architecture

### 109. How would you design a database for a high-volume transactional system?

**Follow-ups** - How would you choose primary keys? - What indexes are
needed? - How would you handle hot rows? - Would you partition tables? -
Where would caching fit?

### 110. When would you denormalize a database?

**Follow-ups** - What problem are you trying to solve? - How do you keep
duplicated data consistent? - Could a cache solve the same problem? -
What are the long-term maintenance costs?

### 111. What is database partitioning?

**Follow-ups** - Horizontal vs vertical partitioning? - When does
partitioning help? - What problems can partitioning introduce? - How
would you choose a partition key?

### 112. How would you safely migrate a large production database?

**Follow-ups** - How do you avoid long locks? - What is an
expand-and-contract migration? - How do you deploy schema and
application changes independently? - How would you roll back if the
application deployment fails?

------------------------------------------------------------------------

## 3.6 Security

### 113. What are common security risks in backend APIs?

**Follow-ups** - SQL injection? - Broken authentication/authorization? -
Sensitive data exposure? - SSRF? - Insecure deserialization? -
Rate-limit abuse? - Excessive request payloads?

### 114. Authentication vs authorization: what is the difference?

**Follow-ups** - Where should authentication happen? - Where should
authorization happen? - What are claims? - What are roles and
policies? - How would you implement resource-level authorization?

### 115. How should passwords be stored?

**Follow-ups** - Why should passwords never be encrypted for normal
authentication storage? - What is password hashing? - What are salt and
work factors? - What makes a password-hashing algorithm appropriate?

### 116. How would you protect a public API from abuse?

**Follow-ups** - Rate limiting? - Per-user vs per-IP limits? - What
about distributed rate limiting? - How would you prevent attackers from
bypassing IP-based limits? - How would you monitor abuse?

------------------------------------------------------------------------

## 3.7 Reliability and Production Engineering

### 117. What does graceful degradation mean?

**Follow-ups** - What functionality could be degraded safely? - What if
a recommendation service is unavailable? - What if the cache is
unavailable? - What if the primary database becomes slow rather than
completely unavailable?

### 118. What is a health check?

**Follow-ups** - Liveness vs readiness? - Should a health check call
every dependency? - Can a badly designed health check make an outage
worse? - What should Kubernetes/load balancers use readiness checks for?

### 119. What is graceful shutdown?

**Follow-ups** - What should happen to in-flight HTTP requests? - What
should happen to background workers? - What should happen to messages
currently being processed? - How does cancellation help?

### 120. How would you design an API for zero-downtime deployments?

**Follow-ups** - Can the old and new application versions run
simultaneously? - What does backward-compatible schema evolution mean? -
How do you handle API contract changes? - What happens to queued
messages during deployment?

------------------------------------------------------------------------

## 3.8 System Design Scenarios

### 121. Design a payment API.

**Follow-ups** - How do you prevent duplicate charges? - How do you
handle provider timeouts? - What happens if the provider processes the
payment but your API times out? - How do you reconcile provider state
with your database? - Where would you use idempotency? - What should be
logged?

### 122. Design an order-processing system.

**Follow-ups** - How do you reserve inventory? - What happens if payment
succeeds but inventory reservation fails? - Would you use synchronous or
asynchronous processing? - How do you handle retries? - How do you
guarantee users don't get charged twice?

### 123. Design a notification system.

**Follow-ups** - Email, SMS, push notifications: same pipeline or
separate? - How do you handle provider failures? - How do you retry? -
How do you avoid sending the same notification twice? - How would you
schedule millions of notifications?

### 124. Design a rate limiter for a multi-instance API.

**Follow-ups** - Where is the rate-limit state stored? - Fixed window vs
sliding window vs token bucket? - How does the design behave across
multiple instances? - What happens if Redis is unavailable? - How do you
avoid race conditions?

### 125. Design a URL shortener.

**Follow-ups** - How do you generate unique short IDs? - How do you
handle collisions? - How do you scale reads? - Would you cache
redirects? - How would you collect analytics without slowing down
redirects?

### 126. Design a file-upload service.

**Follow-ups** - Where are files stored? - Would the API server stream
the entire file? - How do you handle very large uploads? - How do you
validate file types? - How do you scan for malicious content? - How
would you support resumable uploads?

------------------------------------------------------------------------

# 4. Cross-Level Practical Questions

These can be used at different levels by changing the depth of the
follow-ups.

## 127. A database query suddenly becomes 20× slower. What do you do?

**Junior** - How would you reproduce the problem? - What information
would you collect?

**Mid** - How would you inspect the generated SQL and execution plan? -
What would you check about indexes and data volume?

**Senior** - How would you determine whether this is a query-plan
regression, infrastructure problem, lock contention, parameter issue, or
data-distribution change? - How would you mitigate it safely in
production?

------------------------------------------------------------------------

## 128. An API returns duplicate records. How would you debug it?

**Follow-ups** - Could the database query contain a JOIN that multiplies
rows? - Could the application be adding duplicates? - Could pagination
cause repeated records? - Could multiple consumers/processors be
producing duplicate data? - What evidence would distinguish each case?

------------------------------------------------------------------------

## 129. A background job occasionally processes the same item twice.

**Follow-ups** - Is duplicate processing necessarily a bug? - What
delivery guarantee does the queue provide? - How would you make the
operation idempotent? - Would you use a distributed lock? - What happens
if the process crashes halfway through?

------------------------------------------------------------------------

## 130. An external API is occasionally slow.

**Follow-ups** - What timeout would you use? - Would you retry? - Which
failures are retryable? - How would you prevent retries from increasing
load? - Would you use a circuit breaker? - What metrics would you
record?

------------------------------------------------------------------------

## 131. A service works perfectly with one instance but fails with five instances.

**Follow-ups** - Is there local in-memory state? - Are sessions stored
locally? - Is there a local cache? - Is there a singleton with mutable
state? - Is there a race condition? - Is there a distributed lock or
shared resource problem?

------------------------------------------------------------------------

## 132. Your API receives the same request twice.

**Follow-ups** - How do you determine whether this is a client retry,
network retry, user double-click, or backend retry? - Which operations
require idempotency? - How would you implement an idempotency key? -
What happens if both requests arrive concurrently?

------------------------------------------------------------------------

# 5. Code Review Questions

## 133. Review this code

``` csharp
public async Task<User> GetUser(int id)
{
    var user = await _db.Users.FirstOrDefaultAsync(x => x.Id == id);
    return user;
}
```

**Questions** - What would you change? - What happens if the user does
not exist? - Should this return the EF entity directly? - Should this
query use `AsNoTracking()`? - Should it project directly to a DTO? -
What HTTP status should the controller return?

------------------------------------------------------------------------

## 134. Review this code

``` csharp
public async Task ProcessAsync()
{
    var result = _client.GetAsync("/users").Result;
    Console.WriteLine(result);
}
```

**Questions** - What is wrong with this? - What problems can `.Result`
cause? - How would you rewrite it? - What should happen if the HTTP call
times out? - Should the `HttpClient` be created for every request?

------------------------------------------------------------------------

## 135. Review this code

``` csharp
public class OrderService
{
    private readonly DbContext _db;

    public OrderService(DbContext db)
    {
        _db = db;
    }

    public async Task CreateAsync(Order order)
    {
        _db.Add(order);
        await _db.SaveChangesAsync();
    }
}
```

**Questions** - What would you ask before approving this? - Is the
transaction boundary clear? - How are validation and business rules
handled? - Is the service reusable for multiple operations? - Should
`DbContext` be abstracted? - Would you use a repository here?

------------------------------------------------------------------------

## 136. Review this code

``` csharp
public class CacheService
{
    private readonly Dictionary<string, object> _cache = new();

    public object Get(string key) =>
        _cache.TryGetValue(key, out var value) ? value : null;

    public void Set(string key, object value) =>
        _cache[key] = value;
}
```

**Questions** - Is this thread-safe? - What happens under concurrent
requests? - What happens with multiple application instances? - Does
this need expiration? - What happens when memory grows indefinitely? -
Would `IMemoryCache` or Redis be more appropriate?

------------------------------------------------------------------------

# 6. Behavioral / Experience Questions for Backend Developers

These should not replace technical questions. They are useful for
understanding whether the candidate has actually worked through
production problems.

## 137. Tell me about the most difficult production bug you have investigated.

**Follow-ups** - How did you narrow down the cause? - What evidence did
you use? - What was your first wrong hypothesis? - How did you verify
the final root cause? - What did you change to prevent recurrence?

## 138. Tell me about a performance problem you solved.

**Follow-ups** - What was slow? - How did you measure it? - What did you
initially suspect? - What actually caused it? - What was the measurable
improvement?

## 139. Tell me about a production incident caused by a design decision.

**Follow-ups** - What decision caused the problem? - What assumptions
were wrong? - How did you mitigate the incident? - What would you design
differently now?

## 140. Tell me about a time you disagreed with a technical decision.

**Follow-ups** - What were the competing options? - What evidence did
you use? - How was the decision made? - What happened afterward?

## 141. Tell me about a system you inherited that was difficult to maintain.

**Follow-ups** - What made it difficult? - Did you rewrite it or improve
it incrementally? - How did you decide? - How did you avoid introducing
regressions?

## 142. Tell me about a time you had to debug a problem you could not reproduce locally.

**Follow-ups** - What production evidence did you collect? - Did you add
logging or telemetry? - How did you narrow the search? - How did you
verify the fix?

------------------------------------------------------------------------

# 7. Senior Deep-Dive Topics

Use these when a candidate performs strongly on the senior-level
questions.

## 143. Explain the Outbox Pattern.

**Follow-ups** - What consistency problem does it solve? - Where is the
outbox stored? - How does a publisher know which records are already
processed? - What happens if the publisher crashes? - How do you prevent
duplicate messages? - Does the outbox give exactly-once delivery?

## 144. Explain the Saga Pattern.

**Follow-ups** - What is a choreography-based saga? - What is an
orchestration-based saga? - What are compensating transactions? - What
happens when compensation itself fails? - When would you avoid a
distributed saga?

## 145. Explain the CAP theorem in practical terms.

**Follow-ups** - What does partition tolerance mean? - Why are network
partitions unavoidable in distributed systems? - What trade-off is made
during a partition? - How does this relate to consistency and
availability? - Give an example using a real distributed
database/system.

## 146. How would you design for failure rather than assuming dependencies always work?

**Follow-ups** - Timeouts? - Retries? - Circuit breakers? - Queues? -
Caching? - Fallbacks? - Graceful degradation? - Bulkheads?

## 147. How would you make a service observable enough to debug a production incident?

**Follow-ups** - What metrics? - What structured logs? - What
distributed traces? - What correlation identifiers? - What dashboards? -
What alerts? - How do you avoid logging sensitive information?

## 148. How would you safely introduce a major architectural change into a running production system?

**Follow-ups** - Can you migrate incrementally? - What is the strangler
pattern? - How do you maintain backward compatibility? - How would you
use feature flags? - How do you validate the new implementation? - What
is your rollback strategy?

## 149. What is the difference between scalability, performance, availability, and reliability?

**Follow-ups** - Can a system be fast but unreliable? - Can a system be
highly available but slow? - How would you measure each? - Which
trade-offs would you consider for a payment system versus a reporting
system?

## 150. Describe a backend architecture you would be comfortable owning in production.

**Follow-ups** - What are the major components? - Where does state
live? - How does data flow through the system? - How are failures
handled? - How is it monitored? - How does it scale? - How is it
deployed? - How would you test it? - What are the biggest known
trade-offs?

------------------------------------------------------------------------

# 8. Suggested Interview Progression

## Junior Interview

**Recommended areas** 1. C# fundamentals 2. OOP 3. Collections 4. LINQ
5. Async/await 6. ASP.NET Core basics 7. HTTP/REST 8. SQL basics 9.
Testing basics

**Good junior signal**

The candidate can explain fundamentals clearly, write simple C# code,
understand request/response flow, use async/await correctly, and reason
about basic database operations.

------------------------------------------------------------------------

## Mid-Level Interview

**Recommended areas** 1. Advanced C# 2. Async/concurrency 3. LINQ and EF
Core 4. DI and architecture 5. SQL performance 6. API design 7. Caching
8. Messaging 9. Observability 10. Testing strategy

**Good mid-level signal**

The candidate can explain **why** they chose an approach, recognize
common production problems, reason about performance, and make
reasonable trade-offs without overengineering.

------------------------------------------------------------------------

## Senior Interview

**Recommended areas** 1. System design 2. Distributed systems 3.
Reliability 4. Database architecture 5. Messaging 6. Security 7.
Performance investigation 8. Production debugging 9. API evolution 10.
Architecture trade-offs

**Good senior signal**

The candidate thinks in terms of **failure modes, trade-offs,
operational behavior, scalability, maintainability, and business
requirements**, rather than simply naming patterns.

------------------------------------------------------------------------

# 9. Interviewer Notes

## Avoid treating these as trivia questions

For example:

> "What is dependency injection?"

is much less useful than:

> "You have a singleton service that needs a scoped service. What
> problems could this cause, and how would you design around it?"

The second question tests whether the candidate understands lifetime
management rather than whether they memorized a definition.

## Use progressive follow-ups

A useful pattern is:

1.  **Definition** --- Does the candidate know the concept?
2.  **Example** --- Can they explain it concretely?
3.  **Trade-off** --- Do they understand when it is appropriate?
4.  **Failure mode** --- Do they know how it breaks?
5.  **Production scenario** --- Have they applied it in real systems?

For example:

**Topic: caching**

-   What is caching?
-   When would you use it?
-   What can go wrong with caching?
-   How do you invalidate cached data?
-   What happens when you have five API instances?
-   How would you handle a cache outage?
-   How would you prevent a cache stampede?

## Look for reasoning, not specific vocabulary

A candidate does not necessarily need to use the same terminology or
architecture you use. A strong answer should demonstrate:

-   Correct understanding of the underlying problem.
-   Awareness of trade-offs.
-   Ability to identify failure modes.
-   Appropriate use of abstractions.
-   Practical production experience.
-   Willingness to verify assumptions with measurements.

------------------------------------------------------------------------

# 10. Quick Interview Checklist

### Junior

-   [ ] C# fundamentals
-   [ ] OOP
-   [ ] Value/reference types
-   [ ] Collections
-   [ ] LINQ
-   [ ] Exceptions
-   [ ] async/await
-   [ ] CLR/GC basics
-   [ ] ASP.NET Core basics
-   [ ] DI
-   [ ] HTTP/REST
-   [ ] SQL
-   [ ] Unit/integration testing

### Mid

-   [ ] Advanced C#
-   [ ] Async/concurrency
-   [ ] Cancellation
-   [ ] LINQ execution
-   [ ] EF Core
-   [ ] DI lifetimes
-   [ ] API design
-   [ ] Transactions
-   [ ] SQL performance
-   [ ] Caching
-   [ ] Messaging
-   [ ] Background processing
-   [ ] Observability
-   [ ] Production debugging

### Senior

-   [ ] System design
-   [ ] Scalability
-   [ ] Distributed systems
-   [ ] Failure handling
-   [ ] Idempotency
-   [ ] Messaging guarantees
-   [ ] Outbox/Saga
-   [ ] Database architecture
-   [ ] Security
-   [ ] Reliability
-   [ ] Performance investigation
-   [ ] Zero-downtime deployment
-   [ ] Architecture trade-offs
-   [ ] Production incident experience

------------------------------------------------------------------------

## Source

The question bank incorporates and expands on topics/questions from:

-   Doit Software --- [150 .NET Interview Questions and Answers for
    2026](https://doit.software/blog/net-interview-questions)

The linked article covers Junior, Middle, and Senior .NET questions and
includes C#, ASP.NET Core, databases, testing, architecture, distributed
systems, and Azure topics. This document reorganizes that material into
a more practical interviewer-oriented progression and adds
follow-up/scenario questions.
