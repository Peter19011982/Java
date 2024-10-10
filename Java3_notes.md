[003100091342.txt](https://github.com/user-attachments/files/17334293/003100091342.txt)JAVA
## najlepsi AI chat na java  
https://www.perplexity.ai/

## ako to vyriesit?



```java
package sk.peter.java1;

import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Scanner;
import java.util.stream.Stream;

public class Octal {
    public static void main(String[] args) throws IOException {
        String filename = "003100091342.txt";
        Path myPath = Paths.get("003100091342.txt");

        String content = Files.readString(myPath, StandardCharsets.UTF_8);
       // System.out.println(content);

//       byte[] c = content.getBytes(StandardCharsets.ISO_8859_1);
       byte[] c = "<CustomerRelation>Odberate\\304\\276/majite\304\276</CustomerRelation>".getBytes(StandardCharsets.ISO_8859_1);
       System.out.println(new String(c, StandardCharsets.UTF_8));
            //System.out.println(c);

    }
}
```




## Opakovanie
funkcionalne Streamy - 

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

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.List;
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) throws IOException {

            String filename = "words.txt";
            // mozem dat aj absolutnu cestu C:\Users\student\IdeaProjects\Java_Proj\words.txt
            // alebo relativnu cestu ak by som mal words.txt napr v src: src/words.txt
            Path filePath = Path.of(filename);
            try (Stream<String> lines = Files.lines(filePath)){

                //List<String> words = lines.filter(word -> word.length()== 3).toList();
                List<String> words = lines.filter(word -> word.startsWith("w")).toList();
                System.out.println(words);
                //words.forEach(System.out::println);
        }
    }
}
```


## Datove streamy

https://github.com/janbodnar/Java-Skolenie/blob/main/io/basics.md

## Create File and Size

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

void main() throws IOException {

    Path myPath = Paths.get("src/resources/words.txt");

    if (Files.exists(myPath)) {

        System.out.println("File already exists");
        long fileSize = Files.size(myPath);
        System.out.println("velkost suboru je: "+fileSize );
    } else {

        Files.createFile(myPath);
        System.out.println("File created");
    }
}
```

## DELETE

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

void main() throws IOException {

    Path myPath = Paths.get("src/resources/myfile.txt");
    boolean fileDeleted = Files.deleteIfExists(myPath);

    if (fileDeleted) {

        System.out.println("File deleted");
    } else {

        System.out.println("File does not exist");
    }
}
```

## Nacitanie a rozsekanie textu do listu slov


```java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.List;
import java.util.regex.Pattern;

void main() throws IOException {

    Path myPath = Paths.get("src/resources/thermopylae.txt");

    List<String> lines = Files.readAllLines(myPath, StandardCharsets.UTF_8);
    lines.forEach(System.out::println);

    // suitable for small files
    String content = Files.readString(myPath, StandardCharsets.UTF_8);
    System.out.println(content);
//+_ znamena, ze to moze urobit na viacerych miestach
    Pattern pattern = Pattern.compile("[\\s,.]+");
    
    //rozseka text na List slov nazaklade znakov hore "[\\s,.]+" biele mieeto, ciarka a bodka viackrat
    List<String> words =pattern.splitAsStream(content).toList();
    System.out.println(words);


}
```

## vytvorenie suborov

```java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.StandardOpenOption;
import java.util.ArrayList;
import java.util.List;

void main() throws IOException {

    Path myPath = Paths.get("src/resources/words.txt");

    List<String> lines = new ArrayList<>();
    lines.add("blue sky");
    lines.add("sweet orange");
    lines.add("fast car");
    lines.add("old book");

    Files.write(myPath, lines, StandardCharsets.UTF_8,
            StandardOpenOption.CREATE, 
            StandardOpenOption.TRUNCATE_EXISTING,);

    System.out.println("Data written");
}
```

## kopirovanie file do file  filereader

```java
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.StandardCopyOption;

void main() throws IOException {

    var source = new File("src/resources/bugs.txt");
    var dest = new File("src/resources/bugs2.txt");

    Files.copy(source.toPath(), dest.toPath(),
            StandardCopyOption.REPLACE_EXISTING);
}
```

## Praca s vacsimi subormi

https://github.com/janbodnar/Java-Skolenie/blob/main/io/filereader.md

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.nio.charset.StandardCharsets;

void main() throws IOException {

    var fileName = "src/resources/thermopylae.txt";

    try (var br = new BufferedReader(new FileReader(fileName,
            StandardCharsets.UTF_8))) {

        String line;
        while ((line = br.readLine()) != null) {

            System.out.println(line);
        }
    }
}
```


## zapisanie do suboru filewriter


https://github.com/janbodnar/Java-Skolenie/blob/main/io/filewriter.md

```java
import java.io.FileWriter;
import java.io.IOException;

void main(String[] args) throws IOException {

    var fileName = "src/resources/myfile.txt";

    try (var fr = new FileWriter(fileName, StandardCharsets.UTF_8)) {

        fr.write("Today is a sunny day");
    }
}
```

```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.URI;
import java.nio.charset.StandardCharsets;

void main() throws IOException {

    String text = readText();

    var fileName = "src/resources/webcode_home_page.txt";

    try (var fr = new FileWriter(fileName, StandardCharsets.UTF_8);
         var bufWriter = new BufferedWriter(fr)) {

        bufWriter.write(text);
    }
}

String readText() throws IOException {

    StringBuilder sb;

    var url = URI.create("https://webcode.me").toURL();

    try (var br = new BufferedReader(new InputStreamReader(url.openStream(),
            StandardCharsets.UTF_8))) {

        String line;
        sb = new StringBuilder();

        while ((line = br.readLine()) != null) {

            sb.append(line);
            sb.append(System.lineSeparator());
        }
    }

    return sb.toString();
}
```

## funkcionalne streamy - viac operacii nad polami

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.util.Arrays;

void main() throws IOException {
    int[] vals = {-2,-6,1,2,3,4,5,7,8,6,45};
    //ak chcem nad polom riesit viac operaci, tak si to prevediem do pola
    Arrays.stream(vals).count();
    System.out.println();

    long suma = Arrays.stream(vals).sum();
    System.out.println(suma);
    long min = Arrays.stream(vals).min().getAsInt();
    System.out.println(min);
}
```
alebo aj takto viem cez List

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.util.Arrays;
import java.util.List;

void main() throws IOException {
    List<Integer> vals = List.of(1,2,3,4,5,6,8);
    int min = vals.stream().min(Integer::compareTo).get();
    System.out.println(min);

//    int[] vals = {-2,-6,1,2,3,4,5,7,8,6,45};
//    //ak chem na polom ruiesit viac operaci, tak si to prevediem do pola
//    Arrays.stream(vals).count();
//    System.out.println();
//
//    long suma = Arrays.stream(vals).sum();
//    System.out.println(suma);
//    long min = Arrays.stream(vals).min().getAsInt();
//    System.out.println(min);

}
```


https://github.com/janbodnar/Java-Skolenie/blob/main/streams/basics.md
## filter, limit, map sa casto pouziva


```java
import java.util.Comparator;
import java.util.stream.Stream;

void main() {

    Stream<String> colours = Stream.of("red", "green", "blue","grey","white");
    String col = colours.skip(2).findFirst().get();
    System.out.println(col);

    Stream<Integer> nums = Stream.of(3, 4, 5, 6, 7);
    int maxVal = nums.max(Comparator.naturalOrder()).get();
    System.out.println(maxVal);
}
```

```java
import java.util.Random;
import java.util.stream.Stream;

void main() {

    Stream<Integer> s1 = Stream.iterate(5, n -> n * 2).limit(10);
    s1.forEach(System.out::println);
// generovanie streamu a retazenim vykonavam operacie
    Stream.generate(new Random()::nextDouble)
            .map(e -> (e * 10))
            .limit(5)
            .forEach(System.out::println);
}
```

```java
import java.util.Arrays;
import java.util.Random;
import java.util.stream.Stream;

void main() {

    Stream<Integer> s1 = Stream.iterate(5, n -> n * 2).limit(10);
    s1.forEach(System.out::println);
// generovanie streamu a retazenim vykonavam operacie
    Stream.generate(new Random()::nextDouble)
            .map(e -> (e * 10))
            .limit(5)
            .forEach(System.out::println);

    int[] vals ={1,2,3,4,5,6,7};
    //filter positive values, multiply by 2, create list or array
    int[] vals2 = Arrays.stream(vals).filter(e -> e>0).map(e-> e * 2).toArray();

    for (int val: vals2) {
        System.out.println(val);
    }
}
```

```java
import java.util.Arrays;
import java.util.Random;
import java.util.stream.IntStream;
import java.util.stream.Stream;

void main() {

    Stream<Integer> s1 = Stream.iterate(5, n -> n * 2).limit(10);
    s1.forEach(System.out::println);


    int[] vals ={1,2,3,4,4,5,6,6,7};
    //pole unikatnych hodnot
    int[] uvals = Arrays.stream(vals).distinct().toArray();

    for (int val: uvals) {
        System.out.println(val);
    }
    //sortovanie default od najmens po najvacsi
    IntStream nums = IntStream.of(1,2,3,4,4,5,6,6,7);
    nums.boxed().sorted().forEach(System.out::println);
}
```


```java
record Car(String name, int price) {}

void main() {

    List<Car> cars = List.of(new Car("Citroen", 23000),
            new Car("Porsche", 65000), new Car("Skoda", 18000),
            new Car("Volkswagen", 33000), new Car("Volvo", 47000));

    cars.stream().sorted(Comparator.comparing(Car::price))
            .forEach(System.out::println);
}


```java
import java.util.Comparator;
import java.util.List;

record Car(String name, int price) {}

void main() {

    List<Car> cars = List.of(new Car("Citroen", 23000),
            new Car("Porsche", 65000), new Car("Skoda", 18000),
            new Car("Volkswagen", 33000), new Car("Volvo", 47000));

//    cars.stream().sorted(Comparator.comparing(Car::price))
//            .forEach(System.out::println);

    List<Car> cheapCars = cars.stream().filter( car -> car.price<30000).toList();
    System.out.println(cheapCars);
}
```


## Regularne vyrazy

https://github.com/janbodnar/Java-Skolenie/blob/main/common/regex.md


```java
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    List<String> words = List.of("Seven", "even",
            "Maven", "Amen", "eleven");

    Pattern p = Pattern.compile(".+even");

    for (String word: words) {

        Matcher m = p.matcher(word);

        if (m.matches()) {

            System.out.printf("%s matches%n", word);
        } else {

            System.out.printf("%s does not match%n", word);
        }
    }
}
```

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    var text = "This island is beautiful";
// "\\bis\\b" toto zaruci, ze len slova: is
    Pattern p = Pattern.compile("\\bis\\b");
    Matcher matcher = p.matcher(text);

    while (matcher.find())
    {
        System.out.printf("%s at %d", matcher.group(), matcher.start());
    }
}

 
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    var content = """
Foxes are omnivorous mammals belonging to several genera
of the family Canidae. Foxes have a flattened skull, upright triangular ears,
a pointed, slightly 1985 upturned snout, and a long bushy tail. Foxes live on every
continent except Antarctica 1456. By far the most common and widespread species of
fox is the red fox.""";
//keby som chcel vsetky cisla , tak dam Pattern p = Pattern.compile("\\d+");
// vypise vsetky slova a spocita:
    Pattern p = Pattern.compile("\\w+");

    Matcher matcher = p.matcher(content);

    int count = 0;

    while (matcher.find()) {

        count++;
        System.out.println(matcher.group());
    }

    System.out.printf("There are %d words", count);
}
```

```java
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    List<String> sentences = List.of("I am looking for Jane.",
            "Jane was walking along the river.",
            "Kate and Jane are close friends.");
//ak chceme bud Jane|Beky|Robert tak p = Pattern.compile("Jane|Beky|Robert");
// vypise len ten riadok , kde je Jane na zaciatku vety
    Pattern p = Pattern.compile("^Jane");

    for (String word : sentences) {

        Matcher m = p.matcher(word);

        if (m.find()) {
            System.out.printf("%s matches%n", word);
        } else {
            System.out.printf("%s does not match%n", word);
        }
    }
}
```

```java
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    var sites = List.of("webcode.me", "zetcode.com", "freebsd.org",
            "netbsd.org");

    Pattern p = Pattern.compile("(\\w+)\\.(\\w+)");

    for (var site: sites) {

        Matcher matcher = p.matcher(site);

        while (matcher.find()) {
            //vsetko matchuje
            System.out.println(matcher.group(0));
            //prva grupa mechuje
            System.out.println(matcher.group(1));
            //druha grupa matchuje
            System.out.println(matcher.group(2));
        }

        System.out.println("*****************");
    }
}
```

## Regex, extrahovanie dat


```java
import java.util.ArrayList;
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    var sites = List.of("webcode.me", "zetcode.com", "freebsd.org", "netbsd.org");

    List<String> topLevels = new ArrayList<>();
    List<String> secondLevels = new ArrayList<>();

    Pattern p = Pattern.compile("(\\w+)\\.(\\w+)");

    for (var site: sites) {

        Matcher matcher = p.matcher(site);

        while (matcher.find()) {

            topLevels.add(matcher.group(1));
            secondLevels.add(matcher.group(2));
        }
    }

    System.out.println(topLevels);
    System.out.println(secondLevels);
}

## overenie spravnosti zadania e-mail adresy:


```java
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() {

    List<String> emails = List.of("luke@gmail.com",
            "andy@yahoocom", "34234sdfa#2345", "f344@gmail.com");

    String regex = "[a-zA-Z0-9._-]+@[a-zA-Z0-9-]+\\.[a-zA-Z.]{2,18}";

    Pattern p = Pattern.compile(regex);

    for (String email : emails) {

        Matcher m = p.matcher(email);

        if (m.matches()) {
            System.out.printf("%s matches%n", email);
        } else {
            System.out.printf("%s does not match%n", email);
        }
    }
}
```

## nacitanie suboru z web http requestom


```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main() throws IOException, InterruptedException {
    //ideme nacitat data zo suboru zweb stranky
    var uri= URI.create("https://www.mit.edu/~ecprice/wordlist.10000");
    try (HttpClient client = HttpClient.newHttpClient()){
        HttpRequest request= HttpRequest.newBuilder(uri).GET().build();
        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
        String body = response.body();
        Path path = Path.of("src/resources/words2");
        Files.writeString(path, body);
   }
}
```

## Regex words from web


```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
import java.util.stream.Stream;

void main() throws IOException, InterruptedException {

    var uri = URI.create("https://www.mit.edu/~ecprice/wordlist.10000");

    try (HttpClient client = HttpClient.newHttpClient()) {

        HttpRequest request = HttpRequest.newBuilder(uri).GET().build();
        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        Pattern pattern = Pattern.compile(".{10}");
        String body = response.body();

        List<String> lines = body.lines().toList();
        List<String> found = new ArrayList<>();

        for (String line : lines) {
            Matcher m = pattern.matcher(line);

            if (m.matches()) {
                found.add(line);
            }
        }

        System.out.println(found.size());

        Path path = Path.of("src/resources/words_10.txt");
        Files.write(path, found);

//        Path path = Path.of("src/resources/words.txt");
//        Files.writeString(path, body);

    }
}
```

## Exceptions 


https://github.com/janbodnar/Java-Skolenie/blob/main/exceptions.md

## Filters null

```java
import java.util.ArrayList;
import java.util.List;

void main() {

    List<String> words = new ArrayList<>() {{
        add("sky");
        add(null);
        add("blue");
        add(null);
        add("cloud");
        add(null);
        add("ocean");
    }};

    List<String> cleaned = words.stream().filter(word -> word != null).toList();

    cleaned.forEach(word -> {
        System.out.printf("The %s word has %d letters%n", word, word.length());
    });
}
```

- vynimka zadania nespravnej hodnoty - ocakava sa int cislo

```java
import java.util.InputMismatchException;
import java.util.Scanner;
import java.util.Locale;
import java.util.logging.Level;
import java.util.logging.Logger;

void main() {

    Locale.setDefault(Locale.ENGLISH);

    System.out.print("Enter an integer: ");

    try {

        try (Scanner sc = new Scanner(System.in)) {

            int x = sc.nextInt();
            System.out.println(x);
        }

    } catch (InputMismatchException e) {

        Logger.getLogger(getClass().getName()).log(Level.SEVERE,
                "wrong data entered");
    }
}
```


## v pripade Exceptions sa musia uzatvorit aj zdroje "finally" -nie je to prax, v praxi sa pouzivaju uz kniznice, ktore to vsetko osetri za nas


```java
package com.zetcode;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.logging.Level;
import java.util.logging.Logger;

public class MySqlVersionEx {

    public static void main(String[] args) {

        Connection con = null;
        Statement st = null;
        ResultSet rs = null;

        String url = "jdbc:mysql://localhost:3306/testdb?useSsl=false";
        String user = "testuser";
        String password = "test623";

        try {

            con = DriverManager.getConnection(url, user, password);
            st = con.createStatement();
            rs = st.executeQuery("SELECT VERSION()");

            if (rs.next()) {

                System.out.println(rs.getString(1));
            }

        } catch (SQLException ex) {

            Logger lgr = Logger.getLogger(MySqlVersionEx.class.getName());
            lgr.log(Level.SEVERE, ex.getMessage(), ex);

        } finally {

            if (rs != null) {
                try {
                    rs.close();
                } catch (SQLException ex) {
                    Logger lgr = Logger.getLogger(MySqlVersionEx.class.getName());
                    lgr.log(Level.SEVERE, ex.getMessage(), ex);
                }
            }

            if (st != null) {
                try {
                    st.close();
                } catch (SQLException ex) {
                    Logger lgr = Logger.getLogger(MySqlVersionEx.class.getName());
                    lgr.log(Level.SEVERE, ex.getMessage(), ex);
                }
            }

            if (con != null) {
                try {
                    con.close();
                } catch (SQLException ex) {
                    Logger lgr = Logger.getLogger(MySqlVersionEx.class.getName());
                    lgr.log(Level.SEVERE, ex.getMessage(), ex);
                }
            }
        }
    }
}
```

- e.printStackTrace() sa pouziva len pre vyvoj ucely, ked chcem vo vyvoji si vypisat chybu

```java
package com.zetcode;

import java.io.FileReader;
import java.io.IOException;
import java.nio.charset.StandardCharsets;

public class IOExceptionEx {

    private static FileReader fr;

    public static void main(String[] args) {

        try {

            char[] buf = new char[1024];

            fr = new FileReader("src/resources/data.txt", StandardCharsets.UTF_8);

            while (fr.read(buf) != -1) {

                System.out.println(buf);
            }

        } catch (IOException e) {
            e.printStackTrace();
        } finally {

            if (fr != null) {
                try {
                    fr.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

## Pripad, ked vyvojar zada vynimku

```java
import java.util.InputMismatchException;
import java.util.Scanner;
import java.util.logging.Level;
import java.util.logging.Logger;

void main() {

    System.out.print("Enter your age: ");

    try {

        try (Scanner sc = new Scanner(System.in)) {

            short age = sc.nextShort();

            if (age <= 0 || age > 130) {

                throw new IllegalArgumentException("Incorrect age");
            }

            System.out.format("Your age is: %d %n", age);
        }

    } catch (IllegalArgumentException | InputMismatchException e) {

        Logger.getLogger(getClass().getName()).log(Level.SEVERE,
                e.getMessage(), e);
    }
}
```

## vlastne vynimky extendovanim triedy Exception


```java
package com.zetcode;

class BigValueException extends Exception {

  public BigValueException(String message) {

        super(message);
    }
}

public class Main {

    public static void main(String[] args) {

        int x = 340004;
        final int LIMIT = 333;

        try {

            if (x > LIMIT) {

                throw new BigValueException("Exceeded the maximum value");
            }

        } catch (BigValueException e) {

            System.out.println(e.getMessage());
        }
    }
}
```

## Serializacia (do json, xml...) a spat Deserializacia
https://github.com/janbodnar/Java-Skolenie/blob/main/libs/gson.md
New project maven
![image](https://github.com/user-attachments/assets/de4bb426-d39a-45a0-bbaf-ed95d11cc16f)

https://mvnrepository.com/artifact/com.google.code.gson/gson/2.11.0
![image](https://github.com/user-attachments/assets/fd7af3f7-0741-4bd3-9c54-2e300a1e5744)


```java

import com.google.gson.Gson;
import java.util.HashMap;
import java.util.Map;

void main() {

    Map<Integer, String> colours = new HashMap<>();
    colours.put(1, "blue");
    colours.put(2, "yellow");
    colours.put(3, "green");
//serializujem na json
    Gson gson = new Gson();

    String output = gson.toJson(colours);

    System.out.println(output);
}
```


```java

import com.google.gson.Gson;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

void main() {

    Map<Integer, String> colours = new HashMap<>();
    colours.put(1, "blue");
    colours.put(2, "yellow");
    colours.put(3, "green");
//serializujem na json
    Gson gson = new Gson();

    String output = gson.toJson(colours);

    System.out.println(output);

    // serializacia Listu
    List<String> words = List.of("sky","blue","earth");
    String output2 = gson.toJson(words);
    
    //serializacia takehoto objektoveho listu
    List<User> users = List.of(new User("John", "Doe", 1230),
            new User("Lucy", "Novak", 670),
            new User("Ben", "Walter", 2050),
            new User("Robin", "Brown", 2300),
            new User("Amy", "Doe", 1250),
            new User("Joe", "Draker", 1190),
            new User("Janet", "Doe", 980),
            new User("Albert", "Novak", 1930));

    String output3 = gson.toJson(users);
    System.out.println(output3);
}
record User(String firstName, String lastName, Integer sallary){}
```

## Deserializacia:


```java

import com.google.gson.Gson;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

void main() {

    String json_string = """
            {"firstName":"Tom", "lastName": "Broody"}""";
    Gson gson = new Gson();

    User user = gson.fromJson(json_string, User.class);
    System.out.println(user);
}

record User(String firstName, String lastName, Integer sallary){}
```java


```
import com.google.gson.FieldNamingPolicy;
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;

import java.io.PrintStream;
import java.nio.charset.StandardCharsets;

void main() {

    try (var prs = new PrintStream(System.out, true,
            StandardCharsets.UTF_8)) {

        Gson gson = new GsonBuilder()
                .setPrettyPrinting()
                .setFieldNamingPolicy(FieldNamingPolicy.UPPER_CAMEL_CASE)
                .create();

        User user = new User("Peter", "Flemming");
        gson.toJson(user, prs);
    }
}

record User(String firstName, String lastName) {
}
```

# tu pride vypisanie do suboru ??

'''
[
  {
    "firstName": "John",
    "lastName": "Doe",
    "occupation": "gardener"
  },
  {
    "firstName": "Roger",
    "lastName": "Roe",
    "occupation": "teacher"
  },
  {
    "firstName": "Paul",
    "lastName": "Novak",
    "occupation": "programmer"
  }
]
````


## nacitanie json zo stranky


import com.google.gson.Gson;
import com.google.gson.annotations.SerializedName;

import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;


void main() throws IOException, InterruptedException {

    String webPage = "http://time.jsontest.com";
    URI uri = URI.create(webPage);

    try (HttpClient client = HttpClient.newHttpClient()) {

        HttpRequest request = HttpRequest.newBuilder(uri).GET().build();
        String body = client.send(request, HttpResponse.BodyHandlers.ofString()).body();

        Gson gson = new Gson();
        TimeData td = gson.fromJson(body, TimeData.class);

        System.out.println(td);
    }
}

record TimeData(String time, @SerializedName("milliseconds_since_epoch") Long millisecondsSinceEpoch, String date) {
}


## zapis json do suboru:


```java
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
 
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.List;
 
void main() throws IOException {
 
    Gson gson = new GsonBuilder().setPrettyPrinting().create();
 
    List<User> users = List.of(new User("John", "Doe", "gardener"),
            new User("Roger", "Roe", "policeman"),
            new User("Paul", "Novak", "programmer")
    );
 
    String output3 = gson.toJson(users);
    System.out.println(output3);
 
    Path path = Path.of("src/main/resources/user.json");
 
    Files.writeString(path, output3);
}
 
record User(String firstName, String lastName, String job) {}
```


## nacitanie json "nepomenovane"


```java
import com.google.gson.Gson;
import com.google.gson.reflect.TypeToken;
 
import java.io.IOException;
import java.lang.reflect.Type;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.util.List;
 
 
void main() throws IOException, InterruptedException {
 
    String webPage = "https://webcode.me/users2.json";
    URI uri = URI.create(webPage);
 
    try (HttpClient client = HttpClient.newHttpClient()) {
 
        HttpRequest request = HttpRequest.newBuilder(uri).GET().build();
        String body = client.send(request, HttpResponse.BodyHandlers.ofString()).body();
 
        Gson gson = new Gson();
        Type userListType = new TypeToken<List<User>>(){}.getType();
        List<User> users = gson.fromJson(body, userListType);
        users.forEach(System.out::println);
    }
}
```


## nacitanie jsom "pomenovane":  treba jeden navyse objekt "record" oproti tomu,ked nacitava nepomenovany json


```java
import com.google.gson.Gson;
import com.google.gson.annotations.SerializedName;
import com.google.gson.reflect.TypeToken;

import java.io.IOException;
import java.lang.reflect.Type;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.util.List;


void main() throws IOException, InterruptedException {

    URI uri = URI.create("https://webcode.me/users.json");
    HttpRequest request = HttpRequest.newBuilder(uri).build();

    var gson = new Gson();
    List<User> users;
    UsersResponse response;

    try (HttpClient client = HttpClient.newHttpClient()) {

        String content = client.send(request,
                HttpResponse.BodyHandlers.ofString()).body();

        Type usersResponseType = new TypeToken<UsersResponse>() {}.getType();
        response = gson.fromJson(content, usersResponseType);

        for (var user : response.users()) {
            System.out.println(user);
        }
    }
}
//treba jeden navyse objekt oproti tomu,ked nacitava nepomenovany json 
record UsersResponse(List<User> users) {
}

record User(int id, @SerializedName("first_name") String firstName,
            @SerializedName("last_name") String lastName, String email) {
}


