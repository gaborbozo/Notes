```java
import java.nio.ByteBuffer;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;
import java.util.List;

public class NIOExample {

    public static void main(String[] args) {
        // Define the path of the file to read from and write to
        Path filePath = Path.of("example.txt");

        // Read from the file
        try {
            List<String> lines = Files.readAllLines(filePath, StandardCharsets.UTF_8);
            System.out.println("Contents of the file:");
            for (String line : lines) {
                System.out.println(line);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }

        // Write to the file
        try {
            String content = "Hello, World!";
            byte[] bytes = content.getBytes(StandardCharsets.UTF_8);
            ByteBuffer buffer = ByteBuffer.wrap(bytes);

            // If the file does not exist, it will be created; if it exists, the existing content will be overwritten
            Files.write(filePath, buffer.array(), StandardOpenOption.CREATE, StandardOpenOption.TRUNCATE_EXISTING);
            System.out.println("Successfully wrote to the file.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI5ODE5MjMxOF19
-->