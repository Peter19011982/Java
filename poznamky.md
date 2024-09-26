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
    // mozem dat aj absolutnu cestu C:\Users\student\IdeaProjects\Java_Proj\words.txt
    // alebo relativnu cestu ak by som mal words.txt napr v src: src/words.txt
    Path filePath = Path.of(filename);
    List<String> lines = Files.readAllLines(filePath);
    for (String line: lines) {
        System.out.printf(" The word %s has %d %n", line, line.length());
    }
}
```

Polia


https://github.com/janbodnar/Java-Skolenie/blob/main/collections/arraylist.md

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<String> langs = new ArrayList<>();

    langs.add("Java");
    langs.add("Python");

    //pozicia, ostatne sa posunu
    langs.add(1, "C#");
    langs.add(0, "Ruby");
    System.out.println(langs.size());
    for (String lang : langs) {

        System.out.printf("%s ", lang);
    }

    System.out.println();

    //nemodifikovatelne listy - pocas behu programu sa nemenia
    var words = List.of("wood", "forest", "falcon", "eagle");
    System.out.println(words);

    var values = List.of(1, 2, 3);
    System.out.println(values);
    
}
```

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<String> items = new ArrayList<>();
    fillList(items);
    //metody
    items.set(3, "watch");
    items.add("bowl");
    items.remove(0);
    items.remove("pen");
    items.removeFirst()
    items.removeLast();

    for (Object el : items) {

        System.out.println(el);
    }

    items.clear();

    if (items.isEmpty()) {

        System.out.println("The list is empty");
    } else {
        System.out.println("The list is not empty");
    }
}

void fillList(List<String> data) {

    data.add("coin");
    data.add("pen");
    data.add("pencil");
    data.add("clock");
    data.add("book");
    data.add("spectacles");
    data.add("glass");
}
```

Podmienecne vymazanie cisel/slov z Listu:

```java
import java.util.ArrayList;
import java.util.List;
//podmienecne vymazanie cisel/slov z Listu
void main() {
    List<String> words = new ArrayList<>();
   // zakomnetovane je varianta s lListom cisel
   // List<Integer> values = new ArrayList<>();
//    values.add(5);
//    values.add(-3);
//    values.add(2);
//    values.add(8);
//    values.add(-2);
//    values.add(6);

    words.add("sky");
    words.add("atom");
    words.add("wall");
    words.add("wral");

    //values.removeIf(val -> val < 0);

    words.removeIf(word -> word.startsWith("w"));
    // varianta ked nezacina na w
    //words.removeIf(word -> !word.startsWith("w"));
    System.out.println(words);

    //system.out.println(values);
}
```

Program nacita words.txt a vypise najprav slova zacinajuce na w a porom zacinajuce na w alebo c:

```
import java.io.IOException;
import java.lang.reflect.Array;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

// program nacita words.txt a vypise najprav slova zacinajuce na w a porom zacinajuce na w alebo c
void main() throws IOException {
    List<String> w_words = new ArrayList<>();
    List<String> w_c_words = new ArrayList<>();

    String filename = "words.txt";
    // mozem dat aj absolutnu cestu C:\Users\student\IdeaProjects\Java_Proj\words.txt
    // alebo relativnu cestu ak by som mal words.txt napr v src: src/words.txt
    Path filePath = Path.of(filename);
    List<String> lines = Files.readAllLines(filePath);

    for (String line: lines) {
        if (line.startsWith("w")){
            w_words.add(line);
        }
        //System.out.printf(" The word %s has %d %n", line, line.length());
    }

    for (String line: lines) {
        if (line.startsWith("w") || line.startsWith("c")){
            w_c_words.add(line);
        }
        //System.out.printf(" The word %s has %d %n", line, line.length());
    }
    System.out.println(w_words);
    System.out.println(w_c_words);
}
```

Hashe = mapy a praca s nimi
https://github.com/janbodnar/Java-Skolenie/blob/main/collections/hashmap.md

```
import java.util.HashMap;
import java.util.Map;

// Hashe = mapy a praca s nimi
void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    System.out.println(capitals);
    // podmienecne pridavanie do mapy aj chyba , doplni
    capitals.putIfAbsent("rus", "Moscow");
    capitals.putIfAbsent("ita", "Rome");

    int size = capitals.size();

    System.out.println(capitals);
    System.out.println(size);
    capitals.remove("pol");
    capitals.remove("ita");
    size = capitals.size();
    System.out.println(capitals);
    System.out.println(size);
    String cap1 = capitals.get("ita");
    //resp. ak sa tam nenadzadza vypise NA (NotAvailabled))
    cap1 = capitals.getOrDefault("ita", "NA");
    String cap2 = capitals.get("rus");
    System.out.println(cap1);

    System.out.println(cap1);
    System.out.println(cap2);


}
```


program, ktory spocita znaky v danej vete a vypise ich pocet:


```
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;
// program, ktory spocita znaky v danej vete a vypise ich pocet
void main() {
    // pretransformovat vetu do znakov
    String message = "there is an old falcon in the sky";
    char[] letters = message.toCharArray();
    System.out.println(Arrays.toString(letters));
    char[] chars = message.toCharArray();

    //zadefinovanie mapy
    Map<Character, Integer> charFreq = new HashMap<>();

    for (Character c : chars) {

        // Check if the character already exists in the map
        if (charFreq.containsKey(c)) {
            // Increment the frequency count for the existing character
            charFreq.put(c, charFreq.get(c) + 1);
        } else {
            // Add the character to the map with a frequency of 1
            charFreq.put(c, 1);
        }
    }

    System.out.println(charFreq);
}
```

Iteracia cez pary:


```
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    capitals.forEach((k, v) -> System.out.format("%s: %s%n", k, v));
}
```

Iteracia cez kluc:

```
import java.util.HashMap;
import java.util.Map;
import java.util.Set;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    Set<String> keys = capitals.keySet();

    keys.forEach(System.out::println);
}
```


Iterovanie cez hodnoty:

```
import java.util.Collection;
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<String, String> capitals = new HashMap<>();

    capitals.put("svk", "Bratislava");
    capitals.put("ger", "Berlin");
    capitals.put("hun", "Budapest");
    capitals.put("czk", "Prague");
    capitals.put("pol", "Warsaw");
    capitals.put("ita", "Rome");

    Collection<String> vals = capitals.values();

    vals.forEach(System.out::println);
}
```


https://github.com/janbodnar/Java-Skolenie/blob/main/scope.md


Main trieda (k nej este vytvorime triedu User s privatnou premennou name)


```java
String name = "Peter";

String name = "Peter";

void main() {
    // nastavenie premennej v z setName, getName z inej triedy, viem k nej pristupovat len cez metody
    var user = new User();
    user.setName("Pavol");
    System.out.println(user.getName());

    String name = "Jozef";
    System.out.println("This is main function");

    System.out.printf("Hello %s!%n", name);
    hello();
}

void hello() {

    System.out.println("This is greet function");
    System.out.printf("Hello %s!%n", name);
}
```

druha trieda User,kde je zadefnovana privatna premenna name

```
public class User {

    private String name;
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

}
```

## DATABAZY 
Novy Java projek v Int.Idea  - Maven (nie intIdea)

https://mvnrepository.com/artifact/org.xerial/sqlite-jdbc/3.46.1.0

![image](https://github.com/user-attachments/assets/77bc70ab-20d2-42bb-9f63-a25f6daad6b0)

```

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.logging.Level;
import java.util.logging.Logger;

void main() {

    String query = "SELECT SQLITE_VERSION()";

    try (Connection con = DriverManager.getConnection("jdbc:sqlite:test.db");
         Statement st = con.createStatement();
         ResultSet rs = st.executeQuery(query)) {

        if (rs.next()) {

            System.out.println(rs.getString(1));
        }

    } catch (SQLException ex) {

        Logger lgr = Logger.getLogger(getClass().getName());
        lgr.log(Level.SEVERE, ex.getMessage(), ex);
    }
}
```

dole vypis, ze pouzivame DB SQLite 3.46.1

https://github.com/janbodnar/Java-Skolenie/blob/main/db/sqlite.md
![image](https://github.com/user-attachments/assets/999d0087-be5b-4a75-aa28-f537b6ed4cba)

