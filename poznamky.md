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



pouzite try catch blokov

'''java
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
'''

https://github.com/janbodnar/Java-Skolenie/blob/main/db/sqlite.md
https://github.com/janbodnar/Java-Skolenie/blob/main/db/sql.md

BROWSER SQLite DB
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

