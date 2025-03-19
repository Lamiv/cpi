# 📌 SAP CPI Routing Interview Questions & Answers  

## 🔹 Basic Routing Questions  

### 1. What is **Routing** in SAP CPI, and why is it important?  
**Answer:**  
Routing in SAP CPI is the process of determining the **target system** where a message should be sent based on **business rules** and **message content**. It ensures:  
- **Efficient data flow** between multiple systems.  
- **Conditional processing** of messages based on headers, payload, or properties.  
- **Optimization of API calls** by directing messages only to relevant systems.  

### 2. What are the different **types of routing** available in CPI?  
**Answer:**  
- **Static Routing** → Fixed destination, no condition required.  
- **Content-Based Routing** → Based on payload values (e.g., Order Type).  
- **Header-Based Routing** → Uses HTTP or custom headers.  
- **Property-Based Routing** → Uses dynamic properties set within the iFlow.  
- **XPath-Based Routing** → Uses XPath expressions for XML payloads.  
- **Multicast Routing** → Sends a message to multiple recipients.  
- **Dynamic Routing** → Uses Groovy scripts or external lookups for decisions.  

### 3. How do you implement **content-based routing** in an iFlow?  
**Answer:**  
1. Add a **Router** component in the iFlow.  
2. Configure **conditions** using **XPath expressions** or **header values**.  
3. Define multiple target endpoints and set conditions for message flow.  
4. Deploy and test the routing logic.  

### 4. What is a **Router** component in SAP CPI, and how does it work?  
**Answer:**  
A **Router** in SAP CPI is used for **conditional message processing**. It evaluates incoming messages and directs them to the appropriate **branch** based on configured conditions (e.g., order type, country, amount).  

### 5. How do you configure **Static Routing** in an integration flow?  
**Answer:**  
- In an iFlow, connect the sender to a **single, predefined receiver**.  
- No conditions or rules are needed.  
- Used when messages always go to the same endpoint.  

---

## 🔹 Intermediate Routing Questions  

### 6. What is **Dynamic Routing**, and how is it different from Static Routing?  
**Answer:**  
- **Static Routing** → Messages always go to a fixed endpoint.  
- **Dynamic Routing** → The endpoint is determined at runtime based on message content (e.g., using **Groovy scripting** or **external lookups**).  

### 7. How do you use **XPath expressions** in a Router to control message flow?  
**Answer:**  
- XPath expressions allow **XML-based routing**.  
- Example: If an order XML contains `<Country>US</Country>`, route it to the US system.  

```html
<xsl:if test="/Order/Country = 'US'">
    <xsl:value-of select="https://us.api.com/orders"/>
</xsl:if>
```
### 8. What is **Header-Based Routing**, and how do you implement it?  
**Answer:**  
- Messages are routed based on **header values** instead of the payload.  
- Example: If the **HTTP Header `Region = EU`**, send it to the **Europe API**.  
- Implemented using a **Router** or **Groovy script** to evaluate headers.  

### 9. Can you explain **Value-Based Routing**? Give an example.  
**Answer:**  
- Routes messages based on **specific field values**.  
- Example: If **OrderType = ‘Urgent’**, send it to a high-priority system.  

### 10. How do you **handle default routing** when no condition matches in a Router?  
**Answer:**  
- SAP CPI allows a **Default Route** in the Router.  
- If no conditions match, the message is sent to the default destination.  

---

## 🔹 Advanced Routing Questions  

### 11. How do you implement **multilevel routing** in an iFlow?  
**Answer:**  
- Use **multiple Router components** in a **sequential flow**.  
- Example: First, route by **Order Type**, then by **Country**.  

### 12. What is **Conditional Routing**, and how do you set up multiple conditions?  
**Answer:**  
- Conditional Routing applies **multiple conditions** to direct messages.  
- Example:  
  - If `Amount > 5000`, send to **Finance System**.  
  - If `Country = UK`, send to **UK API**.  
  - Else, send to **Default API**.  

### 13. How do you use **Groovy scripting for dynamic routing** in SAP CPI?  
**Answer:**  
- Read a **field value** from the message.  
- Set the **target endpoint dynamically**.  

```java
import com.sap.gateway.ip.core.customdev.util.Message

def Message processData(Message message) {
    def headers = message.getHeaders()
    def country = headers.get("CountryCode")

    def targetURL
    switch (country) {
        case "US": targetURL = "https://us.api.com/orders"; break
        case "IN": targetURL = "https://in.api.com/orders"; break
        default: targetURL = "https://global.api.com/orders"
    }

    message.setHeader("TargetEndpoint", targetURL)
    return message
}
```
# 📌 Advanced & Expert-Level SAP CPI Routing Questions & Answers  

## 🔹 Advanced Routing Questions  

### 14. **Scenario:** You have a business case where an iFlow should send data to **different APIs based on country codes**. How would you design the routing logic?  
**Answer:**  
- Use a **Router** or **Groovy script** to check `CountryCode`.  
- Route to different **API endpoints** based on the value.  
- Ensure a **Default Route** is defined for unexpected values.  
- Example Groovy Script:  

```java
import com.sap.gateway.ip.core.customdev.util.Message

def Message processData(Message message) {
    def headers = message.getHeaders()
    def country = headers.get("CountryCode")

    def targetURL
    switch (country) {
        case "US": targetURL = "https://us.api.com/orders"; break
        case "IN": targetURL = "https://in.api.com/orders"; break
        default: targetURL = "https://global.api.com/orders"
    }

    message.setHeader("TargetEndpoint", targetURL)
    return message
}
```
# 📌 Advanced & Expert-Level SAP CPI Routing Questions & Answers  

## 🔹 Advanced Routing Questions  

### 15. How do you implement **message splitting with routing** in CPI?  
**Answer:**  
- Use the **Splitter** component to divide a batch message into individual messages.  
- Each split message can be processed independently and routed using the **Router** component.  
- Example use case:  
  - A **bulk order XML** is split into individual orders and routed to different fulfillment centers based on region.  

---

## 🔹 Expert-Level & Real-World Scenarios  

### 16. **Scenario:** A message needs to be routed to **multiple destinations** based on business rules. How would you implement **Multicast Routing**?  
**Answer:**  
- Use the **Multicast component** to send messages to **multiple receivers simultaneously**.  
- Example:  
  - A **customer order confirmation** is sent to both the **Inventory System** and **Customer API** at the same time.  
- **Implementation Steps:**  
  1. Add a **Multicast component** in iFlow.  
  2. Define the receivers (e.g., Customer API, Inventory System).  
  3. Configure parallel processing if needed.  

---

### 17. **Scenario:** How do you design a **fallback route** in case the primary receiver system is down?  
**Answer:**  
- Use a **Fault Handling branch** in the iFlow.  
- If the primary API fails, use an **Exception Subprocess** to send the message to a **backup API**.  
- **Example:**  
  - If the **main payment gateway** fails, route the request to a **secondary gateway**.  
- **Implementation Steps:**  
  1. Add an **Exception Subprocess**.  
  2. Inside it, add a **Router** or **Groovy script** to determine the fallback route.  

---

### 18. **Scenario:** Your client wants to **route messages dynamically based on database lookup values**. How would you achieve this?  
**Answer:**  
- Use a **Request-Reply component** to fetch routing information from a database.  
- Store the **resulting endpoint** in a **property** or **header**.  
- Use a **Router** or **Groovy script** to apply the database lookup result.  

**Example Groovy Script for Database Lookup-Based Routing:**

```java
import com.sap.gateway.ip.core.customdev.util.Message;

def Message processData(Message message) {
    def properties = message.getProperties();
    def orderType = properties.get("OrderType");

    def targetEndpoint;
    if (orderType == "HighPriority") {
        targetEndpoint = "https://fast-processing.api.com";
    } else {
        targetEndpoint = "https://standard-processing.api.com";
    }

    message.setHeader("TargetEndpoint", targetEndpoint);
    return message;
}
```

### 19. **Scenario:** If a message needs to be **sent to different endpoints at different times of the day**, how would you implement **time-based routing**?  
**Answer:**  
- Use **Groovy scripting** to determine the **current time** and select the appropriate endpoint.  
- **Example:**  
  - Messages between **9 AM - 5 PM** are sent to a **primary processing system**.  
  - Messages **after hours** are sent to a **backup queue** for later processing.  

```java
import java.time.LocalTime;

def Message processData(Message message) {
    def currentTime = LocalTime.now();
    def targetEndpoint = (currentTime.getHour() < 17) ? "https://day.api.com" : "https://night.api.com";

    message.setHeader("TargetEndpoint", targetEndpoint);
    return message;
}

```

### 20. **Scenario:** You are working with a **large volume of transactions** and need to optimize routing performance. What are the best practices?  
**Answer:**  
- **Use parallel processing** to handle multiple messages at once.  
- **Minimize script execution time** in routing logic by avoiding unnecessary loops.  
- **Use caching** for database lookups instead of querying every time.  
- **Optimize network latency** by reducing API calls and using message queues.  
- **Compress large payloads** before transmission.  

```java
import com.sap.gateway.ip.core.customdev.util.Message;
import java.util.concurrent.*;

def Message processData(Message message) {
    def executor = Executors.newFixedThreadPool(10);
    executor.execute(() -> {
        def headers = message.getHeaders();
        def orderID = headers.get("OrderID");
        def log = message.getLogger();
        log.info("Processing order: " + orderID);
    });

    executor.shutdown();
    return message;
}
```

### 21. Scenario: A business requirement needs routing logic where orders from specific customers go to different ERP systems dynamically. How would you handle this?  
**Answer:**  
- Use a **Value Mapping Table** to store customer-to-ERP mappings.  
- Use **Groovy scripting** to retrieve the ERP system dynamically based on the customer ID.  

```java
import com.sap.gateway.ip.core.customdev.util.Message;
import java.util.HashMap;

def Message processData(Message message) {
    def headers = message.getHeaders();
    def customerID = headers.get("CustomerID");

    def erpMapping = new HashMap<>();
    erpMapping.put("CUST001", "https://erp1.api.com");
    erpMapping.put("CUST002", "https://erp2.api.com");

    def targetERP = erpMapping.getOrDefault(customerID, "https://default-erp.api.com");
    message.setHeader("TargetERP", targetERP);

    return message;
}
```
### 22. Scenario: A company has multiple warehouses, and messages should be routed based on stock availability. How would you implement this?  

**Answer:**  
- Use a **Request-Reply component** to query the warehouse API for stock availability.  
- Use **Groovy scripting** to select the warehouse dynamically.  

```java
import com.sap.gateway.ip.core.customdev.util.Message;
import groovy.json.JsonSlurper;

def Message processData(Message message) {
    def body = message.getBody(String);
    def json = new JsonSlurper().parseText(body);

    def stockAvailability = json.stockAvailable;
    def targetWarehouse = (stockAvailability > 0) ? "https://warehouse1.api.com" : "https://backup-warehouse.api.com";

    message.setHeader("TargetWarehouse", targetWarehouse);
    return message;
}
```
### 23. Scenario: How do you handle routing based on priority orders in SAP CPI?  
**Answer:**  
- Assign priority based on an **Order Type** field in the message.  
- Use a **Router** to send high-priority orders to a **fast-processing API**.  
- **Example Groovy Script:**  

```java
import com.sap.gateway.ip.core.customdev.util.Message;

def Message processData(Message message) {
    def headers = message.getHeaders();
    def orderType = headers.get("OrderType");

    def targetEndpoint;
    if (orderType == "HighPriority") {
        targetEndpoint = "https://fast-processing.api.com";
    } else {
        targetEndpoint = "https://standard-processing.api.com";
    }

    message.setHeader("TargetEndpoint", targetEndpoint);
    return message;
}
```

### 24. Scenario: How can you implement failover logic for an integration where the primary API is unreliable?  

 **Answer:**  
- Implement a **Retry Mechanism**.  
- If the **primary API fails**, route the message to a **backup API**.  
- **Example Groovy Script for Failover:**  

```java
import com.sap.gateway.ip.core.customdev.util.Message;
import java.net.HttpURLConnection;
import java.net.URL;

def Message processData(Message message) {
    def primaryAPI = "https://primary.api.com";
    def backupAPI = "https://backup.api.com";

    def targetAPI = checkAPIStatus(primaryAPI) ? primaryAPI : backupAPI;
    message.setHeader("TargetEndpoint", targetAPI);

    return message;
}

boolean checkAPIStatus(String apiUrl) {
    try {
        def url = new URL(apiUrl);
        def connection = (HttpURLConnection) url.openConnection();
        connection.setRequestMethod("HEAD");
        return (connection.getResponseCode() == 200);
    } catch (Exception e) {
        return false;
    }
}

```
### 25. Scenario: You need to implement routing logic where a message should be processed only if a mandatory field is present. How would you handle this?  

**Answer:**  
- Use **Groovy scripting** to validate if the required field is present.  
- If the field is missing, **throw an exception** or **route it to an error handling API**.  

```java
import com.sap.gateway.ip.core.customdev.util.Message;

def Message processData(Message message) {
    def body = message.getBody(String);

    if (!body.contains("<MandatoryField>")) {
        throw new Exception("Mandatory field missing in message");
    }

    return message;
}

```
### 25. Scenario: You need to implement routing logic where a message should be processed only if a mandatory field is present. How would you handle this?  

 **Answer:**  
- Use **Groovy scripting** to validate if the required field is present.  
- If the field is missing, **throw an exception** or **route it to an error handling API**.  

```java
import com.sap.gateway.ip.core.customdev.util.Message;

def Message processData(Message message) {
    def body = message.getBody(String);

    if (!body.contains("<MandatoryField>")) {
        throw new Exception("Mandatory field missing in message");
    }

    return message;
}

```
