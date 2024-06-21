# Reliable, Scalable, Maintainable Applications

<br>

### 1.0.a Data-intensive VS Compute-intensive

| Data-intensive                                               | Compute-intensive                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------------ |
| Amount of data and complexity of data is huge                | Amount of data and complexity of data is relatively less           |
| They devote most of their processing time to I/O operations. | They devote most of their processing time in processing the input. |

<br>

### 1.0.b Standard Building Blocks of DIA (DICk-BullShit)

- **Database** : Store actual data.
- **Indexes** : Search data by key word (like hashtables?).
- **Caches** : Remember result of expensive calculations to reuse it later.
- **Batch processing** : Periodically crunch `(WTF is crunch?)` a large amount of accumulated data.
- **Stream processing** : messages handled asynchronously.

You won't be builing those blocks from scratch. We have many database system for that. The thing is there are various ways to approach each one of them and different tools implement different approaches.

Wisdom lies in identifying what tool or approach to use in a particular project.

<br>

## 1.1 Thinking About Data Systems

Though building blocks in 1.0.b are different tools; for eg, though database and a message queue have very different access and implementation pattern, **why should we lump them together under an umbrella - _data system_?**

Many application have wide-ranging requirements so work is boken down in single-single small tasks to handled by multiple tools and are sitched together using application code. `Figure 1.1`

Because all the building blocks then work together under the application code and they all deal with data, they are together rconsidered under _data system_.

Application Programming Interface (API) usually hides those implementation details from clients.

**What problems arise when we design data systems or services?**

- Ensuring data remains correct and complete
- Consistently good perfirmance to clients
- Scaling or handling an increase in load
- Building good API structure for our services

<br>

## 1.2 Reliability

### 1.2.a Definition

The system should continue to work correctly (performing the correct function at the desired level of performance) even in the face of adversity (hardwae or software faults, and human error).

- The application performs the function that the user expected.
- It can tolerate the user making mistakes or useing the software in unexpected ways.
- Its performance is good enough for the required use case, under the expected load and data volume.
- The system prevents any unauthorized access and abuse.

<br>

### 1.2.b Faults

Things that _CAN_ go wrong are called _faults_.

System that can anticipate faults and can cope with them are called _fault-tolerant_ or _resilient_.

Making a system tolerant of every possible kind of fault is a unicorn chase X. So only talk about certain _types_ of faults.

<br>

### 1.2.c Faults VS Failures

| Faults                                                           | Failures                                              |
| ---------------------------------------------------------------- | ----------------------------------------------------- |
| Fault happens when a component deviates from its specifications. | Failure is entire system stops providing the service. |
| We can design a fault-tolerant system.                           | We cannot design a failure-tolerant system.           |

<br>

Design fault-tolerant machanisms that prevent faults from causing failures.

Increae the rate of faults by triggering then deliberately. By doing this, you ensure that the fault-tolarance machinery is continually exercised and tested so that faults are handled correctly. (Netflix Chaos Monkey)

We generally prefer tolerating faults over prreventing faults. But there are cases where prevention is better than cure because no cure exists. Eg, then attacker gains access to sensitive data. This can't be undone so better prevent.

## Buzzwords

- Crunch 1.0.b
- Redis - message queue - 1.1
- Apache Kafka - message queue - 1.1
- Memchached - caching layer - 1.1
- Elasticsearch - searching - 1.1
- Solr - searching - 1.1
- The Netflix Chaos Monkey - fault handling - 1.2
