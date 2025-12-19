# Step 20: File I/O (Input/Output)

## What is File I/O?

**File I/O** refers to reading from and writing to files. Java provides multiple ways to handle files through different packages:
- `java.io`: Traditional I/O (streams)
- `java.nio.file`: New I/O (NIO) - Modern approach (Java 7+)

---

## File I/O Methods

### 1. Using java.io (Traditional)

#### Writing to a File

```java
import java.io.*;

public class FileWritingExample {
    public static void main(String[] args) {
        // Method 1: FileWriter
        try (FileWriter writer = new FileWriter("output1.txt")) {
            writer.write("Hello, File I/O!\n");
            writer.write("This is line 2.\n");
            writer.write("This is line 3.");
            System.out.println("Successfully wrote to file using FileWriter");
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Method 2: BufferedWriter (Better performance)
        try (BufferedWriter bw = new BufferedWriter(new FileWriter("output2.txt"))) {
            bw.write("Line 1");
            bw.newLine();
            bw.write("Line 2");
            bw.newLine();
            bw.write("Line 3");
            System.out.println("Successfully wrote to file using BufferedWriter");
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Method 3: FileOutputStream (for binary data)
        try (FileOutputStream fos = new FileOutputStream("output3.txt")) {
            String data = "Writing using FileOutputStream";
            fos.write(data.getBytes());
            System.out.println("Successfully wrote to file using FileOutputStream");
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Method 4: PrintWriter (Convenient methods)
        try (PrintWriter pw = new PrintWriter("output4.txt")) {
            pw.println("Line 1");
            pw.println("Line 2");
            pw.printf("Formatted: %s, %d%n", "Text", 123);
            System.out.println("Successfully wrote to file using PrintWriter");
        } catch (FileNotFoundException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

#### Reading from a File

```java
import java.io.*;

public class FileReadingExample {
    public static void main(String[] args) {
        // Method 1: FileReader
        System.out.println("=== Using FileReader ===");
        try (FileReader reader = new FileReader("output1.txt")) {
            int character;
            while ((character = reader.read()) != -1) {
                System.out.print((char) character);
            }
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Method 2: BufferedReader (Better performance, read line by line)
        System.out.println("\n\n=== Using BufferedReader ===");
        try (BufferedReader br = new BufferedReader(new FileReader("output2.txt"))) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Method 3: FileInputStream (for binary data)
        System.out.println("\n=== Using FileInputStream ===");
        try (FileInputStream fis = new FileInputStream("output3.txt")) {
            int data;
            while ((data = fis.read()) != -1) {
                System.out.print((char) data);
            }
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

### 2. Using java.nio.file (Modern - Java 7+)

```java
import java.nio.file.*;
import java.io.IOException;
import java.util.List;

public class NIOFileExample {
    public static void main(String[] args) {
        // Writing to file
        System.out.println("=== Writing using NIO ===");
        String content = "Line 1\nLine 2\nLine 3\nLine 4";
        Path path = Paths.get("nio_output.txt");
        
        try {
            Files.writeString(path, content);
            System.out.println("Successfully wrote to file");
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Reading entire file as String
        System.out.println("\n=== Reading as String ===");
        try {
            String fileContent = Files.readString(path);
            System.out.println(fileContent);
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Reading file as List of lines
        System.out.println("\n=== Reading as List of Lines ===");
        try {
            List<String> lines = Files.readAllLines(path);
            for (int i = 0; i < lines.size(); i++) {
                System.out.println("Line " + (i + 1) + ": " + lines.get(i));
            }
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Appending to file
        System.out.println("\n=== Appending to File ===");
        try {
            Files.writeString(path, "\nAppended line", StandardOpenOption.APPEND);
            System.out.println("Successfully appended to file");
            System.out.println("Updated content:");
            System.out.println(Files.readString(path));
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## File Operations

```java
import java.io.File;
import java.io.IOException;
import java.nio.file.*;

public class FileOperationsExample {
    public static void main(String[] args) {
        // Creating a file
        System.out.println("=== Creating File ===");
        File file = new File("test.txt");
        try {
            if (file.createNewFile()) {
                System.out.println("File created: " + file.getName());
            } else {
                System.out.println("File already exists");
            }
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // File information
        System.out.println("\n=== File Information ===");
        if (file.exists()) {
            System.out.println("Name: " + file.getName());
            System.out.println("Absolute Path: " + file.getAbsolutePath());
            System.out.println("Writable: " + file.canWrite());
            System.out.println("Readable: " + file.canRead());
            System.out.println("Size: " + file.length() + " bytes");
            System.out.println("Is Directory: " + file.isDirectory());
            System.out.println("Is File: " + file.isFile());
        }
        
        // Creating directory
        System.out.println("\n=== Creating Directory ===");
        File dir = new File("testdir");
        if (dir.mkdir()) {
            System.out.println("Directory created: " + dir.getName());
        } else {
            System.out.println("Directory already exists or couldn't create");
        }
        
        // Listing files in directory
        System.out.println("\n=== Listing Files ===");
        File currentDir = new File(".");
        String[] files = currentDir.list();
        if (files != null) {
            System.out.println("Files in current directory:");
            for (String filename : files) {
                System.out.println("  " + filename);
            }
        }
        
        // Copying file (NIO)
        System.out.println("\n=== Copying File ===");
        try {
            Path source = Paths.get("test.txt");
            Path destination = Paths.get("test_copy.txt");
            Files.copy(source, destination, StandardCopyOption.REPLACE_EXISTING);
            System.out.println("File copied successfully");
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Moving/Renaming file (NIO)
        System.out.println("\n=== Moving/Renaming File ===");
        try {
            Path source = Paths.get("test_copy.txt");
            Path destination = Paths.get("test_renamed.txt");
            Files.move(source, destination, StandardCopyOption.REPLACE_EXISTING);
            System.out.println("File moved/renamed successfully");
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Deleting file
        System.out.println("\n=== Deleting File ===");
        File fileToDelete = new File("test_renamed.txt");
        if (fileToDelete.delete()) {
            System.out.println("Deleted: " + fileToDelete.getName());
        } else {
            System.out.println("Failed to delete file");
        }
    }
}
```

---

## Try-with-Resources (Automatic Resource Management)

```java
import java.io.*;

public class TryWithResourcesExample {
    public static void main(String[] args) {
        // Old way (manual close)
        BufferedReader reader = null;
        try {
            reader = new BufferedReader(new FileReader("file.txt"));
            String line = reader.readLine();
            System.out.println(line);
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (reader != null) reader.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        
        // New way (try-with-resources - Java 7+)
        // Automatically closes resource
        try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
            String line = br.readLine();
            System.out.println(line);
        } catch (IOException e) {
            e.printStackTrace();
        }  // br is automatically closed here
        
        // Multiple resources
        try (FileReader fr = new FileReader("file1.txt");
             BufferedReader br = new BufferedReader(fr);
             FileWriter fw = new FileWriter("file2.txt")) {
            
            String line;
            while ((line = br.readLine()) != null) {
                fw.write(line + "\n");
            }
        } catch (IOException e) {
            e.printStackTrace();
        }  // All resources closed automatically
    }
}
```

---

## 2025 Interview Questions

**Q1: What is the difference between FileReader and BufferedReader?**
**A:**
- **FileReader**: Reads characters one by one (slower)
- **BufferedReader**: Uses buffer for efficient reading, can read line by line

**Q2: What is try-with-resources?**
**A:** Automatic resource management (Java 7+). Resources implementing AutoCloseable are automatically closed.

**Q3: What is the difference between java.io and java.nio?**
**A:**
- **java.io**: Stream-based, blocking I/O, traditional
- **java.nio**: Buffer-based, non-blocking I/O, better performance

**Q4: How do you read a file line by line?**
**A:**
```java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
}
```

**Q5: How do you append to a file?**
**A:**
```java
// java.io
FileWriter fw = new FileWriter("file.txt", true);  // true = append

// java.nio
Files.writeString(path, content, StandardOpenOption.APPEND);
```

**Q6: What is the difference between FileWriter and PrintWriter?**
**A:**
- **FileWriter**: Basic writing, write() method
- **PrintWriter**: Convenient methods like println(), printf()

**Q7: How to check if a file exists?**
**A:**
```java
File file = new File("file.txt");
boolean exists = file.exists();

// Or NIO
boolean exists = Files.exists(Paths.get("file.txt"));
```

---

**Next:** [Step 21: Multithreading Basics](../Step-21-Multithreading-Basics/README.md)
