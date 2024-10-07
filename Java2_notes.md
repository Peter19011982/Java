# Java 

## Pole int-tov - ulohy


```java
import java.lang.reflect.Array;
import java.util.Arrays;


void main() {
    int[] vals = {1,2,3,4,5,6};
    //calculate sum
    //print first and last element
    //itterate from last to front
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


## Nacitanie zo suboru, pridali sme Exception 'throws IOException'


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

## List-y


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

## Podmienecne vymazanie cisel/slov z Listu:


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

## Program nacita words.txt a vypise najprav slova zacinajuce na w a porom zacinajuce na w alebo c:

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

## Hashe = mapy a praca s nimi
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
    // podmienecne pridavanie do mapy ak chyba, tak doplni
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


## Program, ktory spocita znaky v danej vete a vypise ich pocet:


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

## Iteracia cez pary:


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

## Iteracia cez kluc:

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


## Iterovanie cez hodnoty:


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


```java
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



## pouzite try catch blokov


```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.logging.Level;
import java.util.logging.Logger;

void main() {

    String query = "SELECT SQLITE_VERSION()";
//try/catch sa pouziva ak nmoze nastat nejaka chyba 
    try (Connection con = DriverManager.getConnection("jdbc:sqlite:test.db");
         Statement st = con.createStatement();
         ResultSet rs = st.executeQuery(query)) {

        if (rs.next()) {

            System.out.println(rs.getString(1));
        }
        // uzavrie automaticky spojenia , cize uz netreba uzatvarat
//        con.close();
//        st.close();
//        rs.close();

    } catch (SQLException ex) {

        Logger lgr = Logger.getLogger(getClass().getName());
        lgr.log(Level.SEVERE, ex.getMessage(), ex);
    }
}
```

https://github.com/janbodnar/Java-Skolenie/blob/main/db/sqlite.md
https://github.com/janbodnar/Java-Skolenie/blob/main/db/sql.md

## SQLite DB
https://sqlitebrowser.org/dl/


```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.logging.Level;
import java.util.logging.Logger;

void main() {

    try (Connection con = DriverManager.getConnection("jdbc:sqlite:test.db")) {

        try (Statement st = con.createStatement()) {

            st.addBatch("DROP TABLE IF EXISTS cars");
            st.addBatch("CREATE TABLE cars(id INTEGER PRIMARY KEY, name TEXT, price INT)");

            st.addBatch("INSERT INTO cars(name, price) VALUES('Audi',52642)");
            st.addBatch("INSERT INTO cars(name, price) VALUES('Mercedes',57127)");
            st.addBatch("INSERT INTO cars(name, price) VALUES('Skoda',9000)");
            st.addBatch("INSERT INTO cars(name, price) VALUES('Volvo',29000)");
            st.addBatch("INSERT INTO cars(name, price) VALUES('Bentley',350000)");
            st.addBatch("INSERT INTO cars(name, price) VALUES('Citroen',21000)");
            st.addBatch("INSERT INTO cars(name, price) VALUES('Hummer',41400)");
            st.addBatch("INSERT INTO cars(name, price) VALUES('Volkswagen',21600)");
            st.executeBatch();
        }

    } catch (SQLException ex) {

        Logger lgr = Logger.getLogger(getClass().getName());
        lgr.log(Level.SEVERE, ex.getMessage(), ex);
    }
}
```

![image](https://github.com/user-attachments/assets/8aba794c-d6fc-443b-a486-76a2a2685649)




```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.logging.Level;
import java.util.logging.Logger;

void main() {

    String query = "SELECT * FROM cars";

    try (Connection con = DriverManager.getConnection("jdbc:sqlite:test.db");
         PreparedStatement pst = con.prepareStatement(query);
         ResultSet rs = pst.executeQuery()) {

        while (rs.next()) {
// !!! pristupujeme od 1,nie od 0
            System.out.printf("%d %s %d%n", rs.getInt(1),
                    rs.getString(2), rs.getInt(3));
        }

    } catch (SQLException ex) {

        Logger lgr = Logger.getLogger(getClass().getName());
        lgr.log(Level.SEVERE, ex.getMessage(), ex);
    }
}
```


```java

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.logging.Level;
import java.util.logging.Logger;

void main() {

    int carPrice = 23999;
    String carName = "Oldsmobile";
//spravne zadanie parametrov  VALUES(?, ?)
    String sql = "INSERT INTO cars(name, price) VALUES(?, ?)";

    try (Connection con = DriverManager.getConnection("jdbc:sqlite:test.db")) {

        try (PreparedStatement pst = con.prepareStatement(sql)) {

            pst.setString(1, carName);
            pst.setInt(2, carPrice);
            pst.executeUpdate();

            System.out.println("A new car has been inserted");
        }

    } catch (SQLException ex) {

        Logger lgr = Logger.getLogger(getClass().getName());
        lgr.log(Level.SEVERE, ex.getMessage(), ex);
    }
}
```

## UI Swing
https://github.com/janbodnar/Java-Skolenie/blob/main/ui/swing.md


```java
package com.zetcode;

import java.awt.EventQueue;
import javax.swing.JFrame;

public class SimpleEx extends JFrame {

    public SimpleEx() {

        initUI();
    }

    private void initUI() {

        setTitle("Simple example");
        setSize(400, 350);
        setLocationRelativeTo(null);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {

        EventQueue.invokeLater(() -> {

            var ex = new SimpleEx();
            ex.setVisible(true);
        });
    }
}
```


![image](https://github.com/user-attachments/assets/36c6a8a2-0e5e-433b-98c7-6f11e15da70c)


```java
package com.zetcode;

import javax.swing.*;
import java.awt.EventQueue;

public class QuitButtonEx extends JFrame {

    public QuitButtonEx() {

        initUI();
    }

    private void initUI() {

        var quitButton = new JButton("Show message");
        quitButton.addActionListener((_) -> JOptionPane.showMessageDialog(this,"button clicked"));

        createLayout(quitButton);

        setTitle("Quit button");
        setSize(400, 350);
        setLocationRelativeTo(null);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
    }

    private void createLayout(JComponent... arg) {

        var pane = getContentPane();
        var gl = new GroupLayout(pane);
        pane.setLayout(gl);

        gl.setAutoCreateContainerGaps(true);

        gl.setHorizontalGroup(gl.createSequentialGroup()
                .addComponent(arg[0])
        );

        gl.setVerticalGroup(gl.createSequentialGroup()
                .addComponent(arg[0])
        );
    }

    public static void main(String[] args) {

        EventQueue.invokeLater(() -> {

            var ex = new QuitButtonEx();
            ex.setVisible(true);
        });
    }
}
```


![image](https://github.com/user-attachments/assets/a26c903a-2df5-4a13-80c2-dbd096efa237)


## vytvorenie jar suboru:
Artifact:
1. hamburger menu
2. Project structure
3. Artifacts
4. + a JAR  -> From modules with dependeces
5. Vybrat main class + OK
6. Apply + OK

Build:
1. Hamburger menu
2. Build -> Build Artifacts - Build
3. jar subor najdem v out/artifacts

Spustenie v prikazovom riadku:  (predtym pridat java path do premennych prostredia windows)
cd C:\Users\student\IdeaProjects\UISwingEx\out\artifacts\UISwingEx_jar\
C:\Users\student\IdeaProjects\UISwingEx\out\artifacts\UISwingEx_jar> java -jar .\UISwingEx.jar


![image](https://github.com/user-attachments/assets/7ff2a17c-23ca-4b9c-a472-bfea004f8726)


## Label multiline string v okne


```java
package com.zetcode;

import javax.swing.GroupLayout;
import javax.swing.JComponent;
import javax.swing.JFrame;
import javax.swing.JLabel;
import java.awt.Color;
import java.awt.EventQueue;
import java.awt.Font;

public class LabelEx extends JFrame {

    public LabelEx() {

        initUI();
    }

    private void initUI() {

        var lyrics =  """
                <html>It's way too late to think of<br> 
                Someone I would call now<br> 
                And neon signs got tired<br> 
                Red eye flights help the stars out<br> 
                I'm safe in a corner<br> 
                Just hours before me<br> 
                <br> 
                I'm waking with the roaches<br> 
                The world has surrendered<br> 
                I'm dating ancient ghosts<br> 
                The ones I made friends with<br> 
                The comfort of fireflies<br> 
                Long gone before daylight<br> 
                <br> 
                And if I had one wishful field tonight<br> 
                I'd ask for the sun to never rise<br> 
                If God leant his voice for me to speak<br> 
                I'd say go to bed, world<br> 
                <br> 
                I've always been too late<br> 
                To see what's before me<br> 
                And I know nothing sweeter than<br> 
                Champaign from last New Years<br> 
                Sweet music in my ears<br> 
                And a night full of no fears<br> 
                <br> 
                But if I had one wishful field tonight<br> 
                I'd ask for the sun to never rise<br> 
                If God passed a mic to me to speak<br> 
                I'd say stay in bed, world<br> 
                Sleep in peace</html>""";

        var label = new JLabel(lyrics);
        label.setFont(new Font("Arial", Font.PLAIN, 14));
        label.setForeground(new Color(50, 50, 25));

        createLayout(label);

        setTitle("No Sleep");
        setLocationRelativeTo(null);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
    }

    private void createLayout(JComponent... arg) {

        var pane = getContentPane();
        var gl = new GroupLayout(pane);
        pane.setLayout(gl);

        gl.setAutoCreateContainerGaps(true);

        gl.setHorizontalGroup(gl.createSequentialGroup()
                .addComponent(arg[0])
        );

        gl.setVerticalGroup(gl.createParallelGroup()
                .addComponent(arg[0])
        );

        pack();
    }

    public static void main(String[] args) {

        EventQueue.invokeLater(() -> {

            var ex = new LabelEx();
            ex.setVisible(true);
        });
    }
}
```

![image](https://github.com/user-attachments/assets/0bc8d1dd-8d47-4b1e-972b-a6c3fffe4232)


## Stahovanie projektov z GITHUB

![image](https://github.com/user-attachments/assets/315d3b19-b895-47fb-aa8a-86008278eecf)

##Sorting


```java
import java.util.Comparator;
import java.util.List;

void main() {

    List<String> words = List.of("sky", "pen", "new", "rock", "war", "water");
    System.out.println(words);

    List<String> filtered = words.stream().filter(word -> word.startsWith("w")).toList();
    System.out.println(filtered);

    List<String> sorted = words.stream().sorted(Comparator.naturalOrder()).toList();
    System.out.println(sorted);

    List<String> reversed = words.stream().sorted(Comparator.reverseOrder()).toList();
    System.out.println(reversed);
}
```

##forEach

```java
import java.util.Arrays;
import java.util.List;

void main() {

    List<String> words = List.of("sky", "pen", "new", "rock", "war", "water");

    System.out.println(words);

//    words.forEach(word -> System.out.println(word));
    words.forEach(System.out::println);
    
//    for (String word: words) {
//        System.out.println(word);
//    }

    int[] vals = {1, 2, 3, 4, 5};
    Arrays.stream(vals).forEach(System.out::println);
}
```


##Filtrovanie slov zo suboru


```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;
import java.util.List;

void main() throws IOException {

    List<String> w_words = new ArrayList<>();
    List<String> w_c_words = new ArrayList<>();

    String fileName = "words.txt";
    Path filePath = Path.of(fileName);

    List<String> lines = Files.readAllLines(filePath);

    for (String line: lines) {

        if (line.startsWith("w")) {
            w_words.add(line);
        }
    }

    for (String line: lines) {

        if (line.startsWith("w") || line.startsWith("c") ) {
            w_c_words.add(line);
        }
    }

    System.out.println(w_words);
    System.out.println(w_c_words);
}
```


## OOP

https://github.com/janbodnar/Java-Skolenie/blob/main/oop/objects.md


```java
import java.util.List;
import java.util.Random;

class Base {}
class Planet {}

void main() {

    //rozne typy objektov ... dame predka = Object
    List<Object> obs = List.of(new Base(), new Planet(), new Base(), new Planet(),
            new Base(), new Planet(), new Base(), new Base(), new Planet() );

    var r = new Random();

    for (int i = 0; i < 10; i++) {
    //nahodne indexy hadze od 1 az po obs.size()-1
        int idx = r.nextInt(obs.size());

        System.out.println(idx);
        var o = obs.get(idx);
    //zistuje akej triedy je objekt Base alebo Planet
        if (o instanceof Base) {
            System.out.println("Base");
        }

        if (o instanceof Planet) {
            System.out.println("Planet");
        }
    }
}
```



##User trieda - treba vytvorit equals() and hashCode(); set, get, toString


```java
import java.util.Objects;

public class User {
    private String name;
    private int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
//Generate -> equals() and hasCode()
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        User user = (User) o;
        return age == user.age && Objects.equals(name, user.name);
    }


    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

## main trieda


```java
import java.util.List;
import java.util.Random;

class Base {}
class Planet {}

//hash
//equalc

void main() {
User u1 = new User("Joe Doe",34);
User u2 = new User("Joe Doe",34);
    System.out.println(u1);
    System.out.println(u2);


    System.out.println(u1.equals(u2));
    System.out.println(u1 == u2);

}
```

## nahradenie samostatnej triedy User jednym riadom: main triede
##//automaticky vytvori equals() and hashCode(); set, get, toString
##record User(String name, int age){


```java
import java.util.List;
import java.util.Random;

class Base {}
class Planet {}

//hash
//equalc

void main() {
User u1 = new User("Joe Doe",34);
User u2 = new User("Joe Dee",34);
User u3= new User("Joe Doe",34);
    System.out.println(u1);
    System.out.println(u2);
    System.out.println(u3);


    System.out.println(u1.equals(u2));
    System.out.println(u1.equals(u3));
    System.out.println(u1 == u2);

}
//automaticky vytvori equals() and hashCode(); set, get, toString
record User(String name, int age){}




## Sorting record


https://github.com/janbodnar/Java-Skolenie/blob/main/record.md


```java
void main() {

    var users = List.of(
            new User("John", "Doe", 1230),
            new User("Lucy", "Novak", 670),
            new User("Ben", "Walter", 2050),
            new User("Robin", "Brown", 2300),
            new User("Amy", "Doe", 1250),
            new User("Joe", "Draker", 1190),
            new User("Janet", "Doe", 980),
            new User("Albert", "Novak", 1930));

    var sorted = users.stream().sorted(Comparator.comparing(User::lastName).reversed()).toList();

    sorted.forEach(System.out::println);
}

record User(String firstName, String lastName, int salary) {
}
```

##ENUM
https://github.com/janbodnar/Java-Skolenie/blob/main/enum.md

```java
enum Day {

    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY,
    SUNDAY
}

void main() {
    //ciselna hodnota volby ordinal();
    System.out.println(Day.MONDAY.ordinal());
    System.out.println(Day.THURSDAY.ordinal());

    Day day = Day.MONDAY;

    if (day == Day.MONDAY) {

        System.out.println("It is Monday");
    }

    System.out.println(day);

    for (Day d : Day.values()) {

        System.out.println(d);
    }
}
```

## dalsi priklad na ENUM, kde doplnime ENUM  MaritalStatus 


```java
import java.util.List;

void main() {

    List<User> users = List.of(
            new User("Jack", "jack234@gmail.com"),
            new User("Peter", "pete2@post.com"),
            new User("Lucy", "lucy17@gmail.com"),
            new User("Robert", "bob56@post.com"),
            new User("Martin", "mato4@imail.com")
    );

    List<User> res = users.stream()
            .filter(user -> user.email().matches(".*post.com"))
            .toList();

    res.forEach(p -> System.out.println(p.name()));
}

record User(String name, String email) {
}
```



##zmenene vyssie : pridane ENUM  MaritalStatus a vypis MARRIED


```java
import java.util.List;

void main() {

    List<User> users = List.of(
            new User("Jack", "jack234@gmail.com", MaritalStatus.SIVORCED),
            new User("Peter", "pete2@post.com", MaritalStatus.SINGLE),
            new User("Lucy", "lucy17@gmail.com", MaritalStatus.SIVORCED),
            new User("Robert", "bob56@post.com", MaritalStatus.MARRIED),
            new User("Martin", "mato4@imail.com",MaritalStatus.SINGLE)
    );

     List<User> res = users.stream().filter(user -> user.maritalStatus()==MaritalStatus.MARRIED).toList();

    res.forEach(p -> System.out.println(p.name()));
}

record User(String name, String email, MaritalStatus maritalStatus) {
}

enum MaritalStatus{
    SINGLE,
    MARRIED,
    SIVORCED
}
```


## pretypovanie


```java
import java.util.List;

void main() {
    int i= 15000;
    long n=i;
    System.out.println(i);
    System.out.println(n);

    long n2= 150000L;
    int i2= (int) n2; //ak som si isty, ze sa zmesti, tak mozem nasilu pretypovat; ak je vacsie ako int, tak dojde k preteceniu
    System.out.println(n);
    System.out.println(i2);

    //pretypovanie Srting na Int
    String val="1234";
    int val2 = Integer.parseInt(val);
    System.out.println(val2);
}
```



```java
void main()

{
    //takto je to pretypovanie ok
    long num1 = Integer.MAX_VALUE + 150L;
    long num2 =  (long) Integer.MAX_VALUE + 150;
    System.out.println(num1);
    System.out.println(num2);
    }

```


##CHART


https://github.com/janbodnar/Java-Skolenie/blob/main/libs/charts.md
novy MAVEN projekt + stahnut Jfreechart kniznicu z maven repository
https://mvnrepository.com/artifact/org.jfree/jfreechart/1.5.5

a dat do pom.xml dependencies:
![image](https://github.com/user-attachments/assets/c929ca4d-9b2e-4b4c-a7e1-443540632291)


![image](https://github.com/user-attachments/assets/b413d5ad-3121-4ceb-9585-82f98bb82b7c)


```java
package org.example;

import org.jfree.chart.ChartFactory;
import org.jfree.chart.ChartUtils;
import org.jfree.chart.JFreeChart;
import org.jfree.data.statistics.HistogramDataset;

import java.io.File;
import java.io.IOException;

public class HistogramEx {

    public static void main(String[] args) throws IOException {

        double[] vals = {

                0.71477137, 0.55749811, 0.50809619, 0.47027228, 0.25281568,
                0.66633175, 0.50676332, 0.6007552, 0.56892904, 0.49553407,
                0.61093935, 0.65057417, 0.40095626, 0.45969447, 0.51087888,
                0.52894806, 0.49397198, 0.4267163, 0.54091298, 0.34545257,
                0.58548892, 0.3137885, 0.63521146, 0.57541744, 0.59862265,
                0.66261386, 0.56744017, 0.42548488, 0.40841345, 0.47393027,
                0.60882106, 0.45961208, 0.43371424, 0.40876484, 0.64367337,
                0.54092033, 0.34240811, 0.44048106, 0.48874236, 0.68300902,
                0.33563968, 0.58328107, 0.58054283, 0.64710522, 0.37801285,
                0.36748982, 0.44386445, 0.47245989, 0.297599, 0.50295541,
                0.39785732, 0.51370486, 0.46650358, 0.5623638, 0.4446957,
                0.52949791, 0.54611411, 0.41020067, 0.61644868, 0.47493691,
                0.50611458, 0.42518211, 0.45467712, 0.52438467, 0.724529,
                0.59749142, 0.45940223, 0.53099928, 0.65159718, 0.38038268,
                0.51639554, 0.41847437, 0.46022878, 0.57326103, 0.44913632,
                0.61043611, 0.42694949, 0.43997814, 0.58787928, 0.36252603,
                0.50937634, 0.47444256, 0.57992527, 0.29381335, 0.50357977,
                0.42469464, 0.53049697, 0.7163579, 0.39741694, 0.41980533,
                0.68091159, 0.69330702, 0.50518926, 0.55884098, 0.48618324,
                0.48469854, 0.55342267, 0.67159111, 0.62352006, 0.34773486};


        var dataset = new HistogramDataset();
        dataset.addSeries("key", vals, 50);

        JFreeChart histogram = ChartFactory.createHistogram("Normal distribution",
                "y values", "x values", dataset);

        ChartUtils.saveChartAsPNG(new File("histogram.png"), histogram, 450, 400);
    }
}
```

![image](https://github.com/user-attachments/assets/8777df7d-dc14-45ea-bc47-0f7191cc2d22)



##LINE chart


```java
package com.zetcode;

import org.jfree.chart.ChartFactory;
import org.jfree.chart.ChartPanel;
import org.jfree.chart.JFreeChart;
import org.jfree.chart.block.BlockBorder;
import org.jfree.chart.plot.PlotOrientation;
import org.jfree.chart.plot.XYPlot;
import org.jfree.chart.renderer.xy.XYLineAndShapeRenderer;
import org.jfree.chart.title.TextTitle;
import org.jfree.data.xy.XYDataset;
import org.jfree.data.xy.XYSeries;
import org.jfree.data.xy.XYSeriesCollection;

import javax.swing.BorderFactory;
import javax.swing.JFrame;
import java.awt.BasicStroke;
import java.awt.Color;
import java.awt.EventQueue;
import java.awt.Font;

public class LineChartEx extends JFrame {

    public LineChartEx() {

        initUI();
    }

    private void initUI() {

        XYDataset dataset = createDataset();
        JFreeChart chart = createChart(dataset);

        ChartPanel chartPanel = new ChartPanel(chart);
        chartPanel.setBorder(BorderFactory.createEmptyBorder(15, 15, 15, 15));
        chartPanel.setBackground(Color.white);
        add(chartPanel);

        pack();
        setTitle("Line chart");
        setLocationRelativeTo(null);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }

    private XYDataset createDataset() {

        var series = new XYSeries("2016");
        series.add(18, 567);
        series.add(20, 612);
        series.add(25, 800);
        series.add(30, 980);
        series.add(40, 1410);
        series.add(50, 2350);

        var dataset = new XYSeriesCollection();
        dataset.addSeries(series);

        return dataset;
    }

    private JFreeChart createChart(XYDataset dataset) {

        JFreeChart chart = ChartFactory.createXYLineChart(
                "Average salary per age",
                "Age",
                "Salary (€)",
                dataset,
                PlotOrientation.VERTICAL,
                true,
                true,
                false
        );

        XYPlot plot = chart.getXYPlot();

        var renderer = new XYLineAndShapeRenderer();
        renderer.setSeriesPaint(0, Color.RED);
        renderer.setSeriesStroke(0, new BasicStroke(2.0f));

        plot.setRenderer(renderer);
        plot.setBackgroundPaint(Color.white);

        plot.setRangeGridlinesVisible(true);
        plot.setRangeGridlinePaint(Color.BLACK);

        plot.setDomainGridlinesVisible(true);
        plot.setDomainGridlinePaint(Color.BLACK);

        chart.getLegend().setFrame(BlockBorder.NONE);

        chart.setTitle(new TextTitle("Average Salary per Age",
                        new Font("Serif", java.awt.Font.BOLD, 18)
                )
        );

        return chart;
    }

    public static void main(String[] args) {

        EventQueue.invokeLater(() -> {

            var ex = new LineChartEx();
            ex.setVisible(true);
        });
    }
}
```
![image](https://github.com/user-attachments/assets/7cb8e106-856b-45d8-8189-530d5fb4eaef)


##BAR Chart


```java
package org.example;

import org.jfree.chart.ChartFactory;
import org.jfree.chart.ChartPanel;
import org.jfree.chart.JFreeChart;
import org.jfree.chart.plot.PlotOrientation;
import org.jfree.data.category.CategoryDataset;
import org.jfree.data.category.DefaultCategoryDataset;

import javax.swing.BorderFactory;
import javax.swing.JFrame;
import java.awt.Color;
import java.awt.EventQueue;

public class BarChartEx extends JFrame {

    public BarChartEx() {

        initUI();
    }

    private void initUI() {

        CategoryDataset dataset = createDataset();

        JFreeChart chart = createChart(dataset);
        ChartPanel chartPanel = new ChartPanel(chart);
        chartPanel.setBorder(BorderFactory.createEmptyBorder(15, 15, 15, 15));
        chartPanel.setBackground(Color.white);
        add(chartPanel);

        pack();
        setTitle("Bar chart");
        setLocationRelativeTo(null);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }

    private CategoryDataset createDataset() {

        var dataset = new DefaultCategoryDataset();
        dataset.setValue(46, "Gold medals", "USA");
        dataset.setValue(38, "Gold medals", "China");
        dataset.setValue(29, "Gold medals", "UK");
        dataset.setValue(22, "Gold medals", "Russia");
        dataset.setValue(13, "Gold medals", "South Korea");
        dataset.setValue(11, "Gold medals", "Germany");

        return dataset;
    }

    private JFreeChart createChart(CategoryDataset dataset) {

        JFreeChart barChart = ChartFactory.createBarChart(
                "Olympic gold medals in London",
                "",
                "Gold medals",
                dataset,
                PlotOrientation.VERTICAL,
                false, true, false);

        return barChart;
    }

    public static void main(String[] args) {

        EventQueue.invokeLater(() -> {

            var ex = new BarChartEx();
            ex.setVisible(true);
        });
    }
}
```

![image](https://github.com/user-attachments/assets/cbb55e54-bdce-4327-82ff-da1ee82b6b0f)


#Filtrovanie, sortovanie:


```java
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

void main() throws IOException {
    String fileName = "user.csv";
    Path filePath = Path.of(fileName);

    List<String> lines = Files.readAllLines(filePath);
    List<User> users = new ArrayList<>();

    for (String line: lines){
        String[] fields = line.split(",");
        User user = new User(fields[0],fields[1],fields[2]);
        users.add(user);
    }
    //users.forEach(System.out::println);
    List<User> filtered = users.stream().filter(user -> user.occupation().equals("driver")).toList();
    System.out.println(filtered);

//    List<User> sorted = users.stream().sorted(Comparator.comparing(User::lastName)).toList();
//    sorted.forEach(System.out::println);

}
record User(String firstName, String lastName, String occupation){}
```


##alternativne na pracu s csv mame opencsv kniznicu:


https://github.com/janbodnar/Java-Skolenie/blob/main/libs/opencsv.md (nacitat z maven repozitara + pomxml + reload  )


```java
import com.opencsv.CSVReader;
import com.opencsv.exceptions.CsvValidationException;

import java.io.FileReader;
import java.io.IOException;
import java.nio.charset.StandardCharsets;

void main() throws IOException, CsvValidationException {

    var fileName = "src/main/resources/user.csv";

    try (var fr = new FileReader(fileName, StandardCharsets.UTF_8);
         var reader = new CSVReader(fr)) {

        String[] nextLine;

        while ((nextLine = reader.readNext()) != null) {

            for (var e : nextLine) {
                System.out.format("%s ", e);
            }
        }
    }
}
```

## to iste ako v predchadzajucom sme robili, ale teraz pomocou kniznice CSVReader


```java
import com.opencsv.CSVReader;
import com.opencsv.exceptions.CsvValidationException;

import java.io.FileReader;
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

void main() throws IOException, CsvValidationException {

    var fileName = "src/main/resources/user.csv";
    List<User> users = new ArrayList<>();
    try (var fr = new FileReader(fileName, StandardCharsets.UTF_8);
         var reader = new CSVReader(fr)) {

        String[] nextLine;

        while ((nextLine = reader.readNext()) != null) {
            User user = new User(nextLine[0],nextLine[1],nextLine[2]);
            users.add(user);
//            for (var e : nextLine) {
//                System.out.format("%s %n ", e);
//            }
        }
        List<User> filtered = users.stream().filter(user -> user.occupation().equals("driver")).toList();
        System.out.println(filtered);

        List<User> sorted = users.stream().sorted(Comparator.comparing(User::lastName).reversed()).toList();
        sorted.forEach(System.out::println);
    }
}
record  User(String firstname, String lastName, String occupation){}
```


## Praca s WEB


## nacitanie obsahu stranky - content


```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

void main() throws IOException, InterruptedException {

    URI uri = URI.create("https://webcode.me/");
    HttpRequest request = HttpRequest.newBuilder(uri).build();

    try (HttpClient client = HttpClient.newHttpClient()){
        // vrati body stranky
        String content = client.send(request, HttpResponse.BodyHandlers.ofString()).body();
        System.out.println(content);
        // discarding()  - nepotrebujem obsah, staci mi statusCode
        int status = client.send(request, HttpResponse.BodyHandlers.discarding()).statusCode();
        System.out.println(status);
    }
}
```


```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.util.ArrayList;
import java.util.List;

void main() throws IOException, InterruptedException {

    URI uri1 = URI.create("https://webcode.me");
    URI uri = URI.create("https://webcode.me/users.csv");
    HttpRequest request1 = HttpRequest.newBuilder(uri1).build();
    HttpRequest request = HttpRequest.newBuilder(uri).build();
    List<User> users = new ArrayList<>();
    try (HttpClient client = HttpClient.newHttpClient()){
        // vrati body stranky
        String content1 = client.send(request1, HttpResponse.BodyHandlers.ofString()).body();
        String content = client.send(request, HttpResponse.BodyHandlers.ofString()).body();
        System.out.println(content1);
        System.out.println(content);
        // discarding()  - nepotrebujem obsah, staci mi statusCode
        int status = client.send(request1, HttpResponse.BodyHandlers.discarding()).statusCode();
        System.out.println(status);

        //poseka mi to obsah csv na riadky; nechcem 1. riadok (hlavicka); nechcme posledny riadok, lebo ten je prazdny
        List<String> lines = content.lines().skip(1).limit(100).toList();
        System.out.println(lines);

        lines.forEach(line ->{
            String[] fields = line.split(",",4);
            User user = new User(Integer.parseInt(fields[0]),fields[1],fields[2], fields[3]);
            users.add(user);
        });
        //vypisem prvych 10
        users.stream().limit(10).forEach(System.out::println);
        // vypisem prvych 10 bez id-cok
        users.stream().limit(10).forEach(user -> System.out.printf("%s %s %s %n", user.firstname(), user.lastName(), user.occupation()));
    }
}
record  User(int id, String firstname, String lastName, String occupation){}
```

##Staticke metody

https://github.com/janbodnar/Java-Skolenie/blob/main/oop/static.md

## zakomentovane je keby bola Basic tiada statiska, odkomentovane je, ked je clenska (volam ju ako novy objekt v Main triede)


```java
package com.zetcode;

class Basic {

//    static int id = 2321;
    int id = 2321;
    public void showInfo() {

        System.out.println("This is Basic class");
        System.out.format("The Id is: %d%n", id);
    }
}

public class Main {

    public static void main(String[] args) {
        Basic info = new Basic();
        info.showInfo();
//        Basic.showInfo();
    }
}
```

## staticka premenna count v Beeing a v ostatnych tiredach Extendovanch dedena


```java
package com.zetcode;

import java.util.ArrayList;
import java.util.List;

class Being {
    public static int count = 0; // Initialize count
}

class Cat extends Being {
    public Cat() {
        count++;
    }
}

class Dog extends Being {
    public Dog() {
        count++;
    }
}

class Donkey extends Being {
    public Donkey() {
        count++;
    }
}

public class Main { // Added class declaration
    public static void main(String[] args) { // Corrected main method signature
        List<Being> beings = new ArrayList<>();

        beings.add(new Cat());
        beings.add(new Cat());
        beings.add(new Cat());
        beings.add(new Dog());
        beings.add(new Donkey());

        int nOfBeings = Being.count;

        System.out.format("There are %d beings %n", nOfBeings);
    }
}
```


## PostGreQQL

https://www.enterprisedb.com/postgresql-tutorial-resources-training-2?uuid=69f95902-b451-4735-b7e4-1b62209d4dfd&campaignId=postgres_rc_17

stiahnut PotgreDB a nainstalovat -> spustit pgAdmin -> vytvorit DB testdb
MAEVEN + do pom.xml pridat dependences:
https://mvnrepository.com/artifact/org.postgresql/postgresql/42.7.4


```java

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.logging.Level;
import java.util.logging.Logger;

void main() {

    String query = "SELECT VERSION()";
    String username = "postgres";
    String password = "postgre";

    try (Connection con = DriverManager.getConnection("jdbc:postgresql://localhost:5432/testdb", username, password);
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

##naplnenie DB tabulky:
DROP TABLE IF EXISTS countries;
CREATE TABLE countries(id serial PRIMARY KEY, name VARCHAR(255), population INTEGER);
INSERT INTO countries(name, population) VALUES('China', 1382050000);
INSERT INTO countries(name, population) VALUES('India', 1313210000);
INSERT INTO countries(name, population) VALUES('USA', 324666000);
INSERT INTO countries(name, population) VALUES('Indonesia', 260581000);
INSERT INTO countries(name, population) VALUES('Brazil', 207221000);
INSERT INTO countries(name, population) VALUES('Pakistan', 196626000);
INSERT INTO countries(name, population) VALUES('Nigeria', 186988000);
INSERT INTO countries(name, population) VALUES('Bangladesh', 162099000);
INSERT INTO countries(name, population) VALUES('Russia', 146838000);
INSERT INTO countries(name, population) VALUES('Japan', 126830000);
INSERT INTO countries(name, population) VALUES('Mexico', 122273000);
INSERT INTO countries(name, population) VALUES('Philippines', 103738000);
INSERT INTO countries(name, population) VALUES('Ethiopia', 101853000);
INSERT INTO countries(name, population) VALUES('Vietnam', 92700000);
INSERT INTO countries(name, population) VALUES('Egypt', 92641000);
INSERT INTO countries(name, population) VALUES('Germany', 82800000);
INSERT INTO countries(name, population) VALUES('the Congo', 82243000);
INSERT INTO countries(name, population) VALUES('Iran', 82800000);
INSERT INTO countries(name, population) VALUES('Turkey', 79814000);
INSERT INTO countries(name, population) VALUES('Thailand', 68147000);
INSERT INTO countries(name, population) VALUES('France', 66984000);
INSERT INTO countries(name, population) VALUES('United Kingdom', 60589000);
INSERT INTO countries(name, population) VALUES('South Africa', 55908000);
INSERT INTO countries(name, population) VALUES('Myanmar', 51446000);
INSERT INTO countries(name, population) VALUES('South Korea', 68147000);
INSERT INTO countries(name, population) VALUES('Colombia', 49129000);
INSERT INTO countries(name, population) VALUES('Kenya', 47251000);
INSERT INTO countries(name, population) VALUES('Spain', 46812000);
INSERT INTO countries(name, population) VALUES('Argentina', 43850000);
INSERT INTO countries(name, population) VALUES('Ukraine', 42603000);
INSERT INTO countries(name, population) VALUES('Sudan', 41176000);
INSERT INTO countries(name, population) VALUES('Algeria', 40400000);
INSERT INTO countries(name, population) VALUES('Poland', 38439000);


## java code select z DB:


```java

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.logging.Level;
import java.util.logging.Logger;

void main() {
        //String query = "SELECT VERSION()";
        String username = "postgres";
        String password = "postgre";
        String query = "SELECT * FROM countries";

        try (Connection con = DriverManager.getConnection("jdbc:postgresql://localhost:5432/testdb", username, password);
        PreparedStatement pst = con.prepareStatement(query);
        ResultSet rs = pst.executeQuery()) {

        while (rs.next()) {

        System.out.printf("%d %s %d%n", rs.getInt(1),
        rs.getString(2), rs.getInt(3));
        }

        } catch (SQLException ex) {

        Logger lgr = Logger.getLogger(getClass().getName());
        lgr.log(Level.SEVERE, ex.getMessage(), ex);
        }
        }
```
