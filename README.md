# Java-Developer-Roadmap


26 January 2026
14:57

# 🚀 JAVA BACKEND DEVELOPER ROADMAP
## For 3 Years Experience | Role-Based | Interview-Ready

---
# 📌 PHASE 1: CORE JAVA (Weeks 1-3)




---

## 1️⃣ Java Memory Model & JVM (⭐ VERY IMPORTANT)

🔹 **Heap vs Stack**
- Stack: Method calls, local variables, thread-specific
- Heap: Objects, shared across threads
- 👉 Interview: "Where does String pool reside?" → Heap (since Java 7)

🔹 **Garbage Collection**
- Types: Serial, Parallel, G1GC, ZGC
- Young Gen → Old Gen flow
- Minor GC vs Major GC vs Full GC
- 👉 Interview: "How would you tune GC for a high-throughput app?"

🔹 **Memory Leaks**
- Common causes: Static collections, unclosed resources, inner class references
- Tools: VisualVM, JProfiler, MAT
- 👉 Interview expects you to explain real debugging scenarios

🔹 **JVM Flags You Must Know**
```
-Xms512m        → Initial heap size
-Xmx2g          → Maximum heap size
-XX:+UseG1GC    → Use G1 Garbage Collector
-XX:MaxGCPauseMillis=200
```

---

## 2️⃣ Collections Framework (⭐ VERY IMPORTANT)

🔹 **HashMap Internals** ⭐⭐⭐
- How it works: hashCode() → bucket → equals()
- Collision handling: LinkedList → TreeNode (Java 8+, threshold 8)
- Load factor: 0.75 (why?)
- Rehashing: What happens when capacity exceeded?
- 👉 Interview: "What happens if two keys have same hashCode?"

🔹 **ConcurrentHashMap vs HashMap**
- HashMap: Not thread-safe
- ConcurrentHashMap: Segment locking (Java 7) → Bucket locking (Java 8+)
- 👉 Interview: "Why not just use synchronized HashMap?"

🔹 **ArrayList vs LinkedList**
- ArrayList: O(1) access, O(n) insert middle
- LinkedList: O(n) access, O(1) insert if pointer known
- 👉 Interview: "When would you prefer LinkedList?" (Almost never in practice!)

🔹 **TreeMap vs LinkedHashMap**
- TreeMap: Sorted by keys, Red-Black tree, O(log n)
- LinkedHashMap: Insertion order OR access order (LRU cache!)
- 👉 Interview: "Implement LRU cache" → LinkedHashMap with accessOrder=true

🔹 **Set Implementations**
- HashSet: Backed by HashMap
- TreeSet: Sorted, O(log n)
- LinkedHashSet: Insertion order maintained

---

## 3️⃣ Multithreading & Concurrency (⭐ VERY IMPORTANT)

🔹 **Thread Basics**
- Creating threads: Thread class vs Runnable vs Callable
- Thread states: NEW → RUNNABLE → BLOCKED → WAITING → TERMINATED
- start() vs run() difference
- 👉 Interview: "What happens if you call run() directly?"

🔹 **Synchronization**
- synchronized keyword (method level vs block level)
- Object-level lock vs Class-level lock
- 👉 Interview: "Can two threads enter two different synchronized methods?"

🔹 **Locks (java.util.concurrent.locks)**
- ReentrantLock: tryLock(), lockInterruptibly()
- ReadWriteLock: Multiple readers OR single writer
- 👉 Interview: "When to use ReentrantLock over synchronized?"

🔹 **ExecutorService** ⭐
- Fixed thread pool: Executors.newFixedThreadPool(n)
- Cached thread pool: Creates threads as needed
- Scheduled thread pool: For delayed/periodic tasks
- 👉 Interview: "How to handle thread pool rejection?"

🔹 **CompletableFuture** ⭐⭐
- Async programming without blocking
- thenApply(), thenCompose(), thenCombine()
- Exception handling: exceptionally(), handle()
- 👉 Interview: "How to combine results of 3 async API calls?"

🔹 **Atomic Variables**
- AtomicInteger, AtomicReference
- CAS (Compare-And-Swap) operation
- 👉 Interview: "How does AtomicInteger achieve thread safety without locks?"

🔹 **Common Concurrency Issues**
- Deadlock: How to detect and prevent
- Race condition: When it occurs
- Starvation: Thread never gets CPU
- 👉 Interview: "Write code that creates deadlock"

---

## 4️⃣ Java 8+ Features (⭐ MUST KNOW)

🔹 **Lambda Expressions**
- Functional interfaces: Single abstract method
- Method references: Class::method
- 👉 Interview: "Difference between Predicate, Function, Consumer, Supplier?"

🔹 **Streams API** ⭐⭐
- Intermediate: filter(), map(), flatMap(), sorted(), distinct()
- Terminal: collect(), reduce(), forEach(), count()
- Parallel streams: When to use, when to avoid
- 👉 Interview: "Find second highest salary using streams"

🔹 **Optional**
- Why: Avoid NullPointerException
- Methods: of(), ofNullable(), orElse(), orElseGet(), orElseThrow()
- 👉 Interview: "Difference between orElse() and orElseGet()?"
  - orElse(): Always evaluates argument
  - orElseGet(): Lazy evaluation

🔹 **Date/Time API (java.time)**
- LocalDate, LocalTime, LocalDateTime
- ZonedDateTime for timezone handling
- Period vs Duration
- 👉 Interview: "How to calculate days between two dates?"

🔹 **Java 11+ Features**
- var keyword (local variable type inference)
- String methods: isBlank(), lines(), strip()
- Files.readString(), Files.writeString()

🔹 **Java 17 Features** (LTS - Important!)
- Records: Immutable data classes
- Sealed classes: Controlled inheritance
- Pattern matching for instanceof

---

## 5️⃣ Exception Handling

🔹 **Checked vs Unchecked**
- Checked: Must handle (IOException, SQLException)
- Unchecked: Runtime exceptions (NullPointer, ArrayIndexOutOfBounds)
- 👉 Interview: "Should you create checked or unchecked custom exceptions?"

🔹 **Best Practices**
- Never catch Exception/Throwable generically
- Don't swallow exceptions (empty catch block)
- Use try-with-resources for AutoCloseable
- Custom exceptions for business logic

🔹 **Exception in Multithreading**
- Thread.UncaughtExceptionHandler
- CompletableFuture exception handling

---

## 6️⃣ String Handling

🔹 **String Immutability**
- Why immutable: Security, caching, thread safety
- String pool concept
- 👉 Interview: "How many objects created: String s = new String("hello")?"

🔹 **String vs StringBuilder vs StringBuffer**
- String: Immutable
- StringBuilder: Mutable, not thread-safe, faster
- StringBuffer: Mutable, thread-safe, slower
- 👉 Interview: "Which one in single-threaded loop concatenation?"

🔹 **equals() vs ==**
- ==: Reference comparison
- equals(): Content comparison
- hashCode() contract with equals()
- 👉 Interview: "What breaks if hashCode not overridden with equals?"

---

# 📌 PHASE 2: SPRING FRAMEWORK (Weeks 4-7)

---

## 1️⃣ Spring Core (⭐ VERY IMPORTANT)

🔹 **IoC (Inversion of Control)**
- Traditional: You create objects
- IoC: Container creates objects
- 👉 Interview: "Explain IoC with real example"

🔹 **Dependency Injection (DI)** ⭐⭐⭐
- What: Container injects dependencies
- Why: Loose coupling, testability
- Types:
  - Constructor Injection ⭐ (Recommended)
  - Setter Injection
  - Field Injection (NOT recommended - why?)
- 👉 Interview: "Why is constructor injection preferred?"
  - Immutability
  - Required dependencies clear
  - Easier testing
  - Fails fast if dependency missing

🔹 **Bean Scopes**
- Singleton (default): One instance per container
- Prototype: New instance every request
- Request: One per HTTP request
- Session: One per HTTP session
- 👉 Interview: "What happens when Singleton depends on Prototype?"

🔹 **Bean Lifecycle**
- Instantiation → Populate Properties → BeanNameAware → BeanFactoryAware → PreInitialization → InitializingBean → Custom init → Ready → DisposableBean → Custom destroy
- @PostConstruct, @PreDestroy
- 👉 Interview: "How to execute code after bean initialization?"

🔹 **ApplicationContext vs BeanFactory**
- BeanFactory: Lazy loading, basic
- ApplicationContext: Eager loading, enterprise features
- 👉 Interview: "When to prefer BeanFactory?"

---

## 2️⃣ Spring Boot Essentials (⭐ VERY IMPORTANT)

🔹 **Auto-Configuration**
- @SpringBootApplication = @Configuration + @EnableAutoConfiguration + @ComponentScan
- How it works: spring.factories, @Conditional annotations
- 👉 Interview: "How does Spring Boot know to configure DataSource?"

🔹 **Starters**
- spring-boot-starter-web
- spring-boot-starter-data-jpa
- spring-boot-starter-security
- 👉 Interview: "What's inside a starter?"

🔹 **Configuration**
- application.properties vs application.yml
- @Value("${property.name}")
- @ConfigurationProperties (type-safe)
- 👉 Interview: "How to load config from external file?"

🔹 **Profiles**
- @Profile("dev"), @Profile("prod")
- spring.profiles.active=dev
- Profile-specific files: application-dev.yml
- 👉 Interview: "How to have different DB for dev and prod?"

🔹 **Actuator**
- Health checks: /actuator/health
- Metrics: /actuator/metrics
- Custom endpoints
- 👉 Interview: "How to check if app is healthy in production?"

---

## 3️⃣ Spring MVC & REST APIs (⭐ VERY IMPORTANT)

🔹 **Annotations**
- @RestController = @Controller + @ResponseBody
- @RequestMapping, @GetMapping, @PostMapping, etc.
- @PathVariable, @RequestParam, @RequestBody
- 👉 Interview: "Difference between @PathVariable and @RequestParam?"

🔹 **HTTP Status Codes You Must Know**
```
200 OK           → Success
201 Created      → Resource created
204 No Content   → Success, no body
400 Bad Request  → Client error (validation)
401 Unauthorized → Authentication required
403 Forbidden    → Authenticated but no permission
404 Not Found    → Resource doesn't exist
500 Internal Server Error → Server error
```

🔹 **Request Validation**
- @Valid, @NotNull, @NotBlank, @Size, @Email
- Custom validators
- 👉 Interview: "How to validate nested objects?"

🔹 **Exception Handling** ⭐
- @ControllerAdvice + @ExceptionHandler
- Custom error response structure
- 👉 Interview: "How to handle all exceptions globally?"

```java
@RestControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleNotFound(ResourceNotFoundException ex) {
        return ResponseEntity.status(404).body(new ErrorResponse(ex.getMessage()));
    }
}
```

🔹 **Response Handling**
- ResponseEntity for full control
- Consistent response structure
- Pagination: Page, Pageable

---

## 4️⃣ Spring Data JPA (⭐ VERY IMPORTANT)

🔹 **Repository Pattern**
- JpaRepository, CrudRepository, PagingAndSortingRepository
- Derived query methods: findByNameAndAge()
- @Query for custom JPQL/Native
- 👉 Interview: "How does Spring Data generate queries from method names?"

🔹 **Entity Relationships** ⭐
- @OneToOne
- @OneToMany / @ManyToOne
- @ManyToMany
- mappedBy: Owning side vs Inverse side
- 👉 Interview: "Difference between unidirectional and bidirectional?"

🔹 **Fetch Types** ⭐⭐
- LAZY (default for collections): Load when accessed
- EAGER: Load immediately
- 👉 Interview: "What is N+1 problem and how to solve?"
  - Problem: 1 query for parent + N queries for children
  - Solutions: JOIN FETCH, @EntityGraph, @BatchSize

🔹 **LazyInitializationException**
- Cause: Accessing lazy collection outside transaction
- Solutions:
  - EAGER fetch (not recommended)
  - JOIN FETCH
  - @Transactional on service method
  - DTO projection
- 👉 Interview expects real solution, not just definition

🔹 **Transactions** ⭐
- @Transactional: Where to put? (Service layer)
- Propagation: REQUIRED, REQUIRES_NEW, NESTED
- Isolation: READ_COMMITTED, REPEATABLE_READ, etc.
- 👉 Interview: "What is propagation REQUIRES_NEW?"

🔹 **Auditing**
- @CreatedDate, @LastModifiedDate
- @CreatedBy, @LastModifiedBy
- @EnableJpaAuditing

---

## 5️⃣ Spring Security (⭐ IMPORTANT)

🔹 **Authentication vs Authorization**
- Authentication: Who are you?
- Authorization: What can you do?

🔹 **Security Filter Chain**
- Request → Filters → Authentication → Authorization → Controller
- Key filters: UsernamePasswordAuthenticationFilter, JwtAuthenticationFilter

🔹 **JWT Authentication** ⭐
- Token structure: Header.Payload.Signature
- Flow: Login → Generate JWT → Client stores → Send in Authorization header
- 👉 Interview: "How to invalidate JWT token?"

🔹 **Method-Level Security**
- @PreAuthorize("hasRole('ADMIN')")
- @Secured("ROLE_USER")
- 👉 Interview: "Difference between @PreAuthorize and @Secured?"

🔹 **CORS Configuration**
- Why needed: Browser security
- @CrossOrigin or global config
- 👉 Interview: "How to enable CORS for specific origins?"

---

## 6️⃣ Spring AOP (Aspect-Oriented Programming)

🔹 **Core Concepts**
- Aspect: Cross-cutting concern (logging, security)
- Join Point: Method execution point
- Advice: Action taken (Before, After, Around)
- Pointcut: Where to apply advice

🔹 **Advice Types**
- @Before: Before method execution
- @After: After method (always)
- @AfterReturning: After successful return
- @AfterThrowing: After exception
- @Around: Before + After (most powerful)

🔹 **Use Cases**
- Logging
- Transaction management
- Security checks
- Performance monitoring
- 👉 Interview: "How does @Transactional work internally?" (AOP proxy!)

---

# 📌 PHASE 3: MICROSERVICES (Weeks 8-11)

---

## 1️⃣ Microservices Fundamentals (⭐ VERY IMPORTANT)

🔹 **Monolith vs Microservices**
| Aspect | Monolith | Microservices |
|--------|----------|---------------|
| Deployment | Single unit | Independent |
| Database | Shared | Per service |
| Scaling | Entire app | Individual service |
| Team | Large, coordinated | Small, autonomous |
| Failure | Affects whole app | Isolated |

🔹 **When NOT to use Microservices**
- Small team
- Simple domain
- Tight deadline
- No DevOps maturity
- 👉 Interview: "What are disadvantages of microservices?"

🔹 **Service Decomposition**
- By business capability
- By subdomain (DDD)
- 👉 Interview: "How would you decompose an e-commerce app?"

---

## 2️⃣ Service Discovery (⭐ IMPORTANT)

🔹 **Why Needed**
- Services have dynamic IPs
- Services scale up/down
- Need to find available instances

🔹 **Eureka (Netflix OSS)**
- Eureka Server: Registry
- Eureka Client: Registers itself
- Heartbeat mechanism
- Self-preservation mode
- 👉 Interview: "What happens if Eureka server goes down?"

🔹 **Client-Side vs Server-Side Discovery**
- Client-side: Client decides which instance (Eureka + Ribbon)
- Server-side: Load balancer decides (AWS ALB)

---

## 3️⃣ API Gateway (⭐ VERY IMPORTANT)

🔹 **Why Needed**
- Single entry point
- Cross-cutting concerns
- Protocol translation

🔹 **Spring Cloud Gateway**
- Routes: Predicates + Filters
- Predicates: Path, Method, Header, etc.
- Filters: AddRequestHeader, RateLimiter, CircuitBreaker

🔹 **Responsibilities**
- Routing
- Authentication/Authorization
- Rate limiting
- Load balancing
- Logging/Monitoring
- 👉 Interview: "How does API Gateway handle authentication?"

---

## 4️⃣ Circuit Breaker - Resilience4j (⭐ VERY IMPORTANT)

🔹 **Why Needed**
- Prevent cascade failures
- Fail fast
- Graceful degradation

🔹 **Circuit States** ⭐⭐
```
CLOSED → (failures exceed threshold) → OPEN
OPEN → (wait duration passes) → HALF_OPEN
HALF_OPEN → (success) → CLOSED
HALF_OPEN → (failure) → OPEN
```

🔹 **Configuration**
```yaml
resilience4j:
  circuitbreaker:
    instances:
      userService:
        failureRateThreshold: 50
        waitDurationInOpenState: 5000
        slidingWindowSize: 10
```

🔹 **Other Resilience4j Features**
- Retry: Automatic retry with backoff
- Rate Limiter: Limit requests per time
- Bulkhead: Limit concurrent calls
- Time Limiter: Timeout handling
- 👉 Interview: "Difference between Circuit Breaker and Retry?"

🔹 **Fallback**
```java
@CircuitBreaker(name = "userService", fallbackMethod = "fallback")
public User getUser(Long id) {
    return restTemplate.getForObject(url, User.class);
}

public User fallback(Long id, Exception e) {
    return new User("Default", "User");
}
```

---

## 5️⃣ Inter-Service Communication (⭐ IMPORTANT)

🔹 **Synchronous**
- RestTemplate (legacy)
- WebClient (reactive, recommended)
- OpenFeign (declarative)
- 👉 Interview: "Why prefer WebClient over RestTemplate?"

🔹 **OpenFeign** ⭐
```java
@FeignClient(name = "user-service")
public interface UserClient {
    @GetMapping("/users/{id}")
    User getUser(@PathVariable Long id);
}
```

🔹 **Asynchronous**
- Message Queues: RabbitMQ, Kafka
- Event-driven architecture
- 👉 Interview: "When to use async over sync communication?"

---

## 6️⃣ Message Queues (⭐ IMPORTANT)

🔹 **RabbitMQ vs Kafka**
| Aspect | RabbitMQ | Kafka |
|--------|----------|-------|
| Type | Message Broker | Event Streaming |
| Ordering | Per queue | Per partition |
| Retention | Until consumed | Time-based |
| Use case | Task queues | Event sourcing, logs |

🔹 **Kafka Concepts**
- Topic: Category of messages
- Partition: Parallel processing
- Consumer Group: Load balancing
- Offset: Message position
- 👉 Interview: "How does Kafka guarantee ordering?"

🔹 **Spring Kafka**
```java
@KafkaListener(topics = "orders", groupId = "order-service")
public void consume(OrderEvent event) {
    // Process event
}
```

---

## 7️⃣ Config Server

🔹 **Why Needed**
- Centralized configuration
- Environment-specific configs
- Dynamic refresh without restart

🔹 **Spring Cloud Config**
- Config Server: Serves configurations
- Config Client: Fetches from server
- Git-backed storage
- @RefreshScope for dynamic refresh

---

## 8️⃣ Distributed Tracing (⭐ IMPORTANT)

🔹 **Why Needed**
- Track request across services
- Identify bottlenecks
- Debug distributed issues

🔹 **Concepts**
- Trace ID: Entire request journey
- Span ID: Single service operation
- 👉 Interview: "How to trace a request across 5 services?"

🔹 **Tools**
- Spring Cloud Sleuth (auto-instrumentation)
- Zipkin / Jaeger (visualization)

---

## 9️⃣ Data Management Patterns (⭐ IMPORTANT)

🔹 **Database per Service**
- Each service owns its data
- No direct DB access across services
- 👉 Interview: "How to query data across services?"

🔹 **Saga Pattern** ⭐⭐
- Problem: Distributed transactions
- Solution: Sequence of local transactions
- Types:
  - Choreography: Events trigger next step
  - Orchestration: Central coordinator
- Compensating transactions for rollback
- 👉 Interview: "How to handle order failure after payment success?"

🔹 **CQRS**
- Command Query Responsibility Segregation
- Separate read and write models
- 👉 Interview: "When to use CQRS?"

🔹 **Event Sourcing**
- Store events, not current state
- Rebuild state by replaying events
- 👉 Interview: "Advantages of event sourcing?"

---

## 🔟 Observability

🔹 **Three Pillars**
- Logs: What happened
- Metrics: How much/many
- Traces: Request journey

🔹 **Logging**
- ELK Stack: Elasticsearch, Logstash, Kibana
- Structured logging (JSON)
- Correlation IDs

🔹 **Metrics**
- Micrometer + Prometheus + Grafana
- Key metrics: Latency, Error rate, Throughput

🔹 **Health Checks**
- Spring Actuator /health
- Liveness vs Readiness probes
- 👉 Interview: "Difference between liveness and readiness?"

---

# 📌 PHASE 4: SYSTEM DESIGN (Weeks 12-14)

---

## 1️⃣ SOLID Principles (⭐ VERY IMPORTANT)

🔹 **S - Single Responsibility**
- One class, one reason to change
- ❌ UserService doing email + validation + DB
- ✅ Separate UserService, EmailService, ValidationService

🔹 **O - Open/Closed**
- Open for extension, closed for modification
- Use interfaces and inheritance
- 👉 Example: Payment strategy pattern

🔹 **L - Liskov Substitution**
- Subtypes must be substitutable for base types
- ❌ Square extends Rectangle (width/height issue)

🔹 **I - Interface Segregation**
- Many specific interfaces > one fat interface
- ❌ Worker interface with work() and eat() for Robot
- ✅ Workable and Eatable interfaces

🔹 **D - Dependency Inversion**
- Depend on abstractions, not concretions
- ✅ Inject PaymentGateway interface
- ❌ Inject StripePayment directly

---

## 2️⃣ Design Patterns (⭐ MUST KNOW FOR INTERVIEWS)

🔹 **Creational**
- Singleton: One instance (Spring beans)
- Factory: Object creation abstraction
- Builder: Complex object construction (Lombok @Builder)
- 👉 Interview: "Implement thread-safe Singleton"

🔹 **Structural**
- Adapter: Interface compatibility
- Decorator: Add behavior dynamically (Java I/O)
- Proxy: Access control (Spring AOP)

🔹 **Behavioral**
- Strategy: Algorithm selection at runtime
- Observer: Event handling (pub-sub)
- Template Method: Algorithm skeleton

---

## 3️⃣ HLD - High Level Design (⭐ VERY IMPORTANT)

🔹 **Approach Framework**
1. Requirements clarification (5 min)
2. Capacity estimation (5 min)
3. High-level design (15 min)
4. Deep dive (10 min)
5. Bottlenecks & scaling (5 min)

🔹 **Key Concepts**
- Load Balancing: Round robin, least connections
- Caching: Redis, local cache, CDN
- Database: SQL vs NoSQL, sharding, replication
- Message Queues: Async processing
- 👉 Interview: "Design URL Shortener", "Design Rate Limiter"

🔹 **Scalability Patterns**
- Horizontal vs Vertical scaling
- Database sharding
- Read replicas
- Caching layers

---

## 4️⃣ LLD - Low Level Design (⭐ IMPORTANT)

🔹 **Approach**
1. Clarify requirements
2. Identify classes/entities
3. Define relationships
4. Apply design patterns
5. Write key methods

🔹 **Common Problems**
- Parking Lot System
- Library Management
- Elevator System
- Tic-Tac-Toe
- 👉 Interview expects working code!

---

# 📌 PHASE 5: DSA (Daily Practice)

---

## 📅 Weekly DSA Schedule

| Week | Topic | Problems/Day |
|------|-------|--------------|
| 1-2 | Arrays & Strings | 2 Easy + 1 Medium |
| 3-4 | Two Pointers, Sliding Window | 1 Easy + 2 Medium |
| 5-6 | HashMap & HashSet | 1 Easy + 2 Medium |
| 7-8 | Linked List, Stack, Queue | 2 Medium |
| 9-10 | Trees & BFS/DFS | 2 Medium |
| 11-12 | Binary Search, Sorting | 1 Medium + 1 Hard |
| 13-14 | Dynamic Programming | 2 Medium |
| 15-16 | Revision & Mock Tests | Timed practice |

---

## 🎯 Must-Solve LeetCode Problems

🔹 **Arrays**
- Two Sum
- Best Time to Buy and Sell Stock
- Product of Array Except Self
- Maximum Subarray

🔹 **Strings**
- Valid Anagram
- Longest Substring Without Repeating
- Group Anagrams

🔹 **Linked List**
- Reverse Linked List
- Merge Two Sorted Lists
- Linked List Cycle

🔹 **Trees**
- Maximum Depth of Binary Tree
- Level Order Traversal
- Validate BST
- Lowest Common Ancestor

🔹 **DP**
- Climbing Stairs
- House Robber
- Coin Change
- Longest Increasing Subsequence

---

# 📌 INTERVIEW QUESTION BANK

---

## Core Java Questions
1. HashMap internal working?
2. Why String is immutable?
3. Difference between == and equals()?
4. How does garbage collection work?
5. Explain thread lifecycle
6. What is deadlock? How to prevent?
7. Difference between Callable and Runnable?
8. What is volatile keyword?
9. Explain CompletableFuture methods
10. Stream API: filter vs map vs flatMap?

## Spring Questions
1. What is IoC and DI?
2. Bean scopes? Singleton vs Prototype?
3. @Component vs @Service vs @Repository?
4. How @Transactional works internally?
5. What is AOP? Real use cases?
6. Spring Boot auto-configuration?
7. How to handle exceptions globally?
8. N+1 problem and solutions?
9. @Primary vs @Qualifier?
10. How to create custom starter?

## Microservices Questions
1. When NOT to use microservices?
2. How services communicate?
3. Explain Circuit Breaker pattern
4. What is Saga pattern? Types?
5. How to handle distributed transactions?
6. Service discovery - how it works?
7. API Gateway responsibilities?
8. How to trace requests across services?
9. Database per service - how to query?
10. Event-driven vs REST?

## System Design Questions
1. Design URL Shortener
2. Design Rate Limiter
3. Design Notification System
4. Design E-commerce Order Flow
5. How to scale read-heavy system?

---

# 📌 WEEKLY STUDY TEMPLATE

---

| Day | Morning (1hr) | Evening (2hrs) | Night (1hr) |
|-----|---------------|----------------|-------------|
| Mon | DSA Practice | Core Java/Spring | Interview Q&A |
| Tue | DSA Practice | Microservices | Interview Q&A |
| Wed | DSA Practice | System Design | Project Work |
| Thu | DSA Practice | Core Java/Spring | Interview Q&A |
| Fri | DSA Practice | Microservices | Project Work |
| Sat | DSA Contest | Project Work | Mock Interview |
| Sun | Revision | System Design | Rest |

---

# 📌 PROJECT IDEAS

---

| Project | Technologies | Level |
|---------|--------------|-------|
| URL Shortener | Spring Boot, Redis, Base62 | Beginner |
| Task Manager API | Spring Boot, JPA, JWT | Beginner |
| E-Commerce Backend | Microservices, Kafka, Eureka | Intermediate |
| Notification Service | RabbitMQ, Email/SMS | Intermediate |
| Banking System | Saga Pattern, Resilience4j | Advanced |

---

# 📌 RESOURCES

---

🔹 **Books**
- Effective Java - Joshua Bloch
- Spring in Action - Craig Walls
- Building Microservices - Sam Newman
- Designing Data-Intensive Applications - Martin Kleppmann

🔹 **Practice**
- LeetCode (Top Interview 150)
- NeetCode.io roadmap
- HackerRank Java

🔹 **System Design**
- ByteByteGo YouTube
- System Design Primer (GitHub)

---

## 💡 Final Tips

```
✅ Consistency > Intensity (1 hour daily > 7 hours weekend)
✅ Understand WHY, not just WHAT
✅ Build projects, don't just read
✅ Practice explaining concepts out loud
✅ Mock interviews are essential
✅ Focus on depth over breadth
```

---

**Good luck with your Java Backend Developer journey! 🚀**

