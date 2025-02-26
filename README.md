# Apache Kafka on Windows - Setup Guide

This guide provides step-by-step instructions to install, configure, and run **Apache Kafka on Windows**.

## **Prerequisites**

- Windows 10/11 (64-bit)
- PowerShell or Command Prompt
- Java 8 or later

---

## **Step 1: Install Java**

### **Check if Java is Installed**
```powershell
java -version
```
If Java is **not installed**, install it using:
```powershell
winget install --id Microsoft.OpenJDK.17 -e
```
Verify the installation:
```powershell
java -version
```

---

## **Step 2: Download and Install Apache Kafka**

### **Download Kafka Binary Package**
1. Go to the [Apache Kafka Downloads Page](https://kafka.apache.org/downloads)
2. Download the latest **binary version** (e.g., `kafka_2.13-3.6.0.tgz`)
3. Extract the downloaded file to `C:\kafka`

---

## **Step 3: Configure Kafka**

### **Enable Topic Deletion**
1. Open `C:\kafka\config\server.properties`
2. Find this line:
   ```properties
   #delete.topic.enable=true
   ```
3. Remove the `#` to enable topic deletion:
   ```properties
   delete.topic.enable=true
   ```
4. Save and close the file.

---

## **Step 4: Start Zookeeper**
```powershell
cd C:\kafka
bin\windows\zookeeper-server-start.bat config\zookeeper.properties
```
**Keep this window open.**

---

## **Step 5: Start Kafka Server**
```powershell
cd C:\kafka
bin\windows\kafka-server-start.bat config\server.properties
```
**Keep this window open.**

---

## **Step 6: Create a Kafka Topic**
```powershell
cd C:\kafka
bin\windows\kafka-topics.bat --create --topic test-topic --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
```
Verify the topic:
```powershell
bin\windows\kafka-topics.bat --list --bootstrap-server localhost:9092
```

---

## **Step 7: Send Messages to Kafka (Producer)**
```powershell
bin\windows\kafka-console-producer.bat --topic test-topic --bootstrap-server localhost:9092
```
Type a message and press **Enter**:
```
Hello Kafka!
Welcome to real-time messaging!
```

---

## **Step 8: Read Messages from Kafka (Consumer)**
```powershell
bin\windows\kafka-console-consumer.bat --topic test-topic --from-beginning --bootstrap-server localhost:9092
```
Messages sent by the producer will appear here.

---

## **Step 9: Manage Kafka Topics**

### **List All Topics**
```powershell
bin\windows\kafka-topics.bat --list --bootstrap-server localhost:9092
```

### **Describe a Topic**
```powershell
bin\windows\kafka-topics.bat --describe --topic test-topic --bootstrap-server localhost:9092
```

### **Delete a Topic**
```powershell
bin\windows\kafka-topics.bat --delete --topic test-topic --bootstrap-server localhost:9092
```

---

## **Step 10: Stop Kafka and Zookeeper**
```powershell
bin\windows\kafka-server-stop.bat
bin\windows\zookeeper-server-stop.bat
```

---

## **Bonus: Using Kafka with Kafkacat**
Install Kafkacat using Chocolatey:
```powershell
choco install kafkacat
```
Fetch the last 5 messages from a topic:
```powershell
kafkacat -C -b localhost:9092 -t test-topic -o -5 -e
```

---

## **Troubleshooting Kafka on Windows**

| Issue | Solution |
|-------------------------------|------------------------------------------------------------------|
| `Classpath is empty` error | Ensure you downloaded the **binary version** of Kafka. |
| `java` not recognized | Install Java and set the `JAVA_HOME` environment variable. |
| Kafka topics not creating | Ensure **Zookeeper and Kafka are running** before creating topics. |
| Cannot delete topic | Ensure `delete.topic.enable=true` is set in `server.properties`. |
| Consumer not receiving messages | Check if the **correct topic name** is used when consuming. |

---

## **Summary**
| Step | Command |
|------|---------|
| **Install Java** | `winget install --id Microsoft.OpenJDK.17 -e` |
| **Start Zookeeper** | `bin\windows\zookeeper-server-start.bat config\zookeeper.properties` |
| **Start Kafka** | `bin\windows\kafka-server-start.bat config\server.properties` |
| **Create Topic** | `bin\windows\kafka-topics.bat --create --topic test-topic --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1` |
| **Send Messages** | `bin\windows\kafka-console-producer.bat --topic test-topic --bootstrap-server localhost:9092` |
| **Read Messages** | `bin\windows\kafka-console-consumer.bat --topic test-topic --from-beginning --bootstrap-server localhost:9092` |
| **Stop Kafka** | `bin\windows\kafka-server-stop.bat` |
| **Stop Zookeeper** | `bin\windows\zookeeper-server-stop.bat` |

This guide ensures you can **install, configure, and run Kafka** on Windows without issues. Happy coding!
