JAVA
## Opakovanie

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.List;
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) throws IOException {

            String filename = "word.txt";
            // mozem dat aj absolutnu cestu C:\Users\student\IdeaProjects\Java_Proj\words.txt
            // alebo relativnu cestu ak by som mal words.txt napr v src: src/words.txt
            Path filePath = Path.of(filename);
            try (Stream<String> lines = Files.lines(filePath)){

                List<String> words = lines.filter(word -> word.length()== 3).toList();
                words.forEach(System.out::println);
        }
    }
}
```
