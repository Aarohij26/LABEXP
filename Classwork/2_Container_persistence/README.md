# 🐳 Container Persistence

## 📌 Objective
Understand how to preserve container changes using Docker commands and best practices.

## 1️⃣ Run Base Container
```bash
docker run -it --name java_lab ubuntu:22.04 bash
```
![run container](/Classwork/2_Container_Persistence/Images/image1.png)

## 2️⃣ Install Java
```bash
apt update
apt install -y openjdk-17-jdk
javac --version
```
![install java](/Classwork/2_Container_Persistence/Images/image2.png)

## 3️⃣ Create Java Program
```bash
mkdir -p /home/app
cd /home/app
nano Hello.java
```

Paste:
```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello from Docker container!");
    }
}
```

Compile & Run:
```bash
javac Hello.java
java Hello
```
![java program](/Classwork/2_Container_Persistence/Images/image3.png)

## 4️⃣ Exit Container
```bash
exit
```
![exit](/Classwork/2_Container_Persistence/Images/image4.png)

## 5️⃣ Commit Container to Image
```bash
docker commit java_lab myrepo/java-app:1.0
docker images
```
![commit](/Classwork/2_Container_Persistence/Images/image5.png)

## 6️⃣ Reuse Image
```bash
docker run -it myrepo/java-app:1.0 bash
cd /home/app
java Hello
```
![reuse](/Classwork/2_Container_Persistence/Images/image6.png)

## 7️⃣ Save and Load Image
```bash
docker save -o java-app.tar myrepo/java-app:1.0
docker load -i java-app.tar
```
![save load](/Classwork/2_Container_Persistence/Images/image7.png)

## 8️⃣ Export vs Save
```bash
docker export java_lab > container.tar
docker save -o image.tar myrepo/java-app:1.0
```
![export vs save](/Classwork/2_Container_Persistence/Images/image8.png)

## 🔑 Key Concepts
- Container → Running environment  
- Image → Snapshot of container  
- docker commit → Container to Image  
- docker save/load → Image to File and back  
- docker export → Only filesystem (not recommended)