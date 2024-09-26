# Java 

Moje poznamky   


```java
import java.lang.reflect.Array;
import java.util.Arrays;


void main() {
    int[] vals = {1,2,3,4,5,6};
    //calculate sum
    //print first and last element
    // itterate from last to front
    int sum=0;

    for (int val : vals){
        sum+=val;

    }

    System.out.println("Suma: "+sum);
    System.out.println("Prvy: " +vals[0]);
    System.out.println("Posledny: " +vals[vals.length-1]);
    int sum2 = Arrays.stream(vals).sum();
    System.out.println(sum2);

    for (int j= vals.length- 1; j >= 0; j-- ){
        System.out.println(vals[j]);
    }

}
```

Nacitanie zo suboru, pridali sme Exception 'throws IOException'


```java
import java.io.IOException;
import java.lang.reflect.Array;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.Arrays;
import java.util.List;


void main() throws IOException {
    String filename = "words.txt";
    Path filePath = Path.of(filename);
    List<String> lines = Files.readAllLines(filePath);
    for (String line: lines) {
        System.out.printf(" The word %s has %d %n", line, line.length());
    }
}
```
