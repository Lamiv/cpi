# 📌 **Reliability & Message Persistence Patterns in SAP CPI**  

## 🔹 **Message Reliability & Delivery Guarantees**  
1. What are **message reliability and delivery guarantees** in SAP CPI?  
2. What is the difference between **At-Most-Once, At-Least-Once, and Exactly-Once** delivery?  
3. How does SAP CPI ensure **message persistence and durability**?  
4. What is the **Idempotency pattern**, and how do you implement it in SAP CPI?  
5. How can you prevent **duplicate message processing** in SAP CPI?  

## 🔹 **JMS Queues & Asynchronous Processing**  
6. What is **JMS (Java Message Service)**, and why is it used in SAP CPI?  
7. What is the difference between **JMS Queues and Topics**?  
8. How does the **Guaranteed Delivery pattern** work with JMS queues in CPI?  
9. How do you handle **message ordering in JMS-based integrations**?  
10. What are the best practices for **tuning and scaling JMS-based integrations** in CPI?  

## 🔹 **SAP Event Mesh & Event-Driven Architecture (EDA)**  
11. What is **SAP Event Mesh**, and how does it integrate with SAP CPI?  
12. How does **event-driven integration** differ from traditional point-to-point integration?  
13. What is the **publish-subscribe (pub-sub) pattern**, and how is it implemented in Event Mesh?  
14. How do you handle **event retries and dead-letter queues in SAP Event Mesh**?  
15. What is the best approach for **handling high-throughput events** in SAP CPI?  

## 🔹 **Error Handling & Resilience**  
16. What is the **Dead Letter Queue (DLQ) pattern**, and how does it work?  
17. How do you implement **retry mechanisms** in SAP CPI?  
18. What is the **Circuit Breaker pattern**, and how does it improve integration resilience?  
19. How do you use **backpressure handling in event-driven architectures**?  
20. How can you monitor and troubleshoot **JMS queues and Event Mesh integrations**?  

## 🔹 **Real-World Scenarios & Expert-Level Reliability Design**  
21. **Scenario:** You need to guarantee that messages are **processed exactly once** even in case of failures. How would you implement this?  
22. **Scenario:** Your SAP CPI integration must handle **large message bursts efficiently** without losing data. What strategy would you use?  
23. **Scenario:** An external system sends duplicate messages due to API issues. How would you prevent processing them twice in CPI?  
24. **Scenario:** Your integration depends on a **third-party API** that is occasionally down. How do you ensure **reliable message delivery**?  
25. **Scenario:** You need to design a **high-availability integration** using SAP CPI, Event Mesh, and JMS queues. What architecture would you propose?  

---
