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
```


```java
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

# tu pride vypisanie do suboru

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
```


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
```


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


## Opakovanie patern


```java
import java.util.ArrayList;
import java.util.List;
import java.util.Optional;
import java.util.OptionalDouble;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

void main () {
    
    // calculate sum
    
    String data = """
            1;2;12,  4,5 ,6,  7;2;3
            1;2;6; 15;2;5;6;7;34
            """;

    Pattern pattern = Pattern.compile("[,;\\s]+");

    int suma = pattern.splitAsStream(data).mapToInt(Integer::valueOf).sum();
    System.out.println(suma);
    
    // calculate average
    String data2 = """
            | Jozef Novak 1230 |
            | John Doe 2340    |
            | Paul Smith 1234  |
            | Lucia Novak 1224 |
            """;

    Pattern pattern2 = Pattern.compile("\\d+");

    Matcher matcher = pattern2.matcher(data2);

    List<Integer> values = new ArrayList<>();

    while (matcher.find()) {
        int val = Integer.parseInt(matcher.group());
        values.add(val);
    }

    System.out.println(values);

    OptionalDouble avg = values.stream().mapToDouble(Double::valueOf).average();
    avg.ifPresent(System.out::println);


    // pick phrases that contain dog, falcon or night
    
    String data3 = """
            a new coin
            an old falcon
            a small house
            a stormy night
            a new costume
            a happy dog
            """;

//    Pattern pattern = Pattern.compile("dog|falcon|night");
//    List<String> found = data3.lines().filter(word -> pattern.matcher(word).find()).toList();
    List<String> found = data3.lines().filter(word -> word.matches(".* dog|.* falcon|night")).toList();
    System.out.println(found);
}
```

## Concurrency - specialitka, ktorou sa zaoberaju specialni programatori; dokopy, parelelen, multitasking programovanie
- vytvaranie vlakien Threads, ktore sa spustia z hlavneho programu ale bezia mimo hlavneho programu - mozu ist paralene ale nemusia, zavisi od HW a volnych CPU (vieme v java pozadovat paralelne fungovanie ale nevieme to velmi ovlyvnit)
- 

https://github.com/janbodnar/Java-Skolenie/blob/main/concurrency.md

```java
package com.zetcode;

class Task implements Runnable {

    private int delay;
    private String name;

    public Task(String name, int delay) {

        this.name = name;
        this.delay = delay;
    }

    @Override
    public void run() {

        try {

            System.out.println("starting task: " + name);

            Thread.sleep(delay);
            System.out.printf("finishing task %s%n", this.name);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

public class Main {

    public static void main(String[] args) {

        var task1 = new Task("Task/2000", 2000);
        var t1 = new Thread(task1);
        t1.start();

        var task2 = new Task("Task/1000", 1000);
        var t2 = new Thread(task2);
        t2.start();

        var task3 = new Task("Task/500", 500);
        var t3 = new Thread(task3);
        t3.start();

        System.out.println("tasks launched");
    }
}
```

- v tomto programe sa caka na ukoncneie taskov (Threadov) a az po ich ukonceni pokracuje dalej (join metoda)

```java
package com.zetcode;

class Worker extends Thread {

    private int delay;
    private String msg;

    public Worker(int delay, String msg) {

        this.delay = delay;
        this.msg = msg;
    }

    public void run() {

        try {
            Thread.sleep(delay);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(msg);
    }
}

public class JoinEx {

    public static void main(String[] args) {

        var w1 = new Worker(2000, "Hello there");
        var w2 = new Worker(1000, "New mail received");
        var w3 = new Worker(500, "Notes taken");

        // start three threads
        w1.start();
        w2.start();
        w3.start();

        // wait for threads to end
        try {

            // join is a blocker method which waits for a thread to complete.

            // the w1.join() causes the current (main) thread to pause execution
            // until w1's thread terminates.
            w1.join();
            w2.join();
            w3.join();

        } catch (InterruptedException e) {

            e.printStackTrace();
        }

        System.out.println("doing main tasks");
        System.out.println("finished tasks");
    }
}
```

- synchronizacne primitivum AtomicLong sa pouziva na zabezpecenie toho, aby sa najprv ukoncilo jedno vlakno a az potom riesilo dalsie, aby sa vlakna nebili a nedochadzalo k chybam

```java
package com.zetcode;

import java.util.concurrent.atomic.AtomicLong;

class Counter {

    private final AtomicLong counter = new AtomicLong(0);

    public void inc() {

        counter.getAndIncrement();
    }

    public long get() {

        return counter.get();
    }
}

public class AtomicLongEx {

    public static void main(String[] args) throws InterruptedException {

        final Counter counter = new Counter();

        // 500 threads
        for (int i = 0; i < 500; i++) {

            var thread = new Thread(() -> counter.inc());

            thread.start();
        }

        // sleep three seconds
        Thread.sleep(3000);

        System.out.println("Value: " + counter.get());
    }
}
```

- dlhotrvajuca uloha je posunuta na pozadie a bezi na pozadi, tam sa zaruci, ze hlavne okno dokaze v pohode prekreslovat 

```java
package com.zetcode;

import javax.swing.GroupLayout;
import javax.swing.JButton;
import javax.swing.JComponent;
import javax.swing.JFrame;
import javax.swing.SwingWorker;
import java.awt.EventQueue;

class MyWorker extends SwingWorker<Void, Void> {

    @Override
    protected Void doInBackground() throws Exception {
        // Simulate a time-consuming task
        Thread.sleep(3000);
        return null;
    }

    @Override
    protected void done() {
        System.out.println("task done");
    }
}

public class ButtonTaskEx extends JFrame {

    public ButtonTaskEx() {

        initUI();
    }

    private void initUI() {

        var taskButton = new JButton("Task");

//        taskButton.addActionListener((event) -> {
//            var worker = new MyWorker();
//            worker.execute();
//        });


        taskButton.addActionListener((event) -> {
            try {
                Thread.sleep(3000);
                System.out.println("task done");
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
        });

        createLayout(taskButton);

        setTitle("Task button");
        setSize(500, 450);
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

            var ex = new ButtonTaskEx();
            ex.setVisible(true);
        });
    }
}
```

uloha prehladavania disku a hladania obrazkov je v dlhotrvajucom vlakne a info o najdeni sa posiela hlavnemu programu a zoznam sa prekresluje na obrazovku


```java

import javax.swing.AbstractAction;
import javax.swing.GroupLayout;
import javax.swing.JButton;
import javax.swing.JComponent;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JScrollPane;
import javax.swing.JTextArea;
import javax.swing.SwingWorker;
import java.awt.Container;
import java.awt.EventQueue;
import java.awt.event.ActionEvent;
import java.io.IOException;
import java.nio.file.FileSystems;
import java.nio.file.FileVisitResult;
import java.nio.file.FileVisitor;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.PathMatcher;
import java.nio.file.Paths;
import java.nio.file.attribute.BasicFileAttributes;
import java.util.List;

import static javax.swing.GroupLayout.Alignment.BASELINE;
import static javax.swing.GroupLayout.Alignment.CENTER;

/*
 * This program initiates a background search for
 * various image files in a user's home directory.
 */

public class Main extends JFrame {

    private JTextArea area;
    private JLabel lbl;
    private JButton btn;

    public Main() {

        initUI();
    }

    private void initUI() {

        area = new JTextArea(20, 40);
        area.setEditable(false);
        var scrollPane = new JScrollPane(area);

        btn = new JButton("Start");
        btn.addActionListener(new StartSearchAction());

        lbl = new JLabel("Files found: ");

        createLayout(scrollPane, btn, lbl);

        setTitle("Searching for files");
        setLocationRelativeTo(null);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }

    private void createLayout(JComponent... arg) {

        Container pane = getContentPane();
        GroupLayout gl = new GroupLayout(pane);
        pane.setLayout(gl);

        gl.setAutoCreateContainerGaps(true);
        gl.setAutoCreateGaps(true);

        gl.setHorizontalGroup(gl.createParallelGroup(CENTER)
                .addComponent(arg[0])
                .addGroup(gl.createSequentialGroup()
                        .addComponent(arg[1])
                        .addComponent(arg[2]))
        );

        gl.setVerticalGroup(gl.createSequentialGroup()
                .addComponent(arg[0])
                .addGroup(gl.createParallelGroup(BASELINE)
                        .addComponent(arg[1])
                        .addComponent(arg[2]))
        );

        pack();
    }

    private class StartSearchAction extends AbstractAction {

        @Override
        public void actionPerformed(ActionEvent e) {

            doStartSearch();
        }

        private void doStartSearch() {

            btn.setEnabled(false);

            var tw = new FileTreeWalker();
            tw.execute();
        }
    }

    public static void main(String[] args) {

        EventQueue.invokeLater(() -> {
            var ex = new Main();
            ex.setVisible(true);
        });
    }

    private class FileTreeWalker extends SwingWorker<Void, Path>
            implements FileVisitor<Path> {

        private final PathMatcher matcher;
        private int count = 0;

        public FileTreeWalker() {

            var str = "glob:**.{png,PNG,gif,GIF,jpg,jpeg,JPG,JPEG}";
            matcher = FileSystems.getDefault().getPathMatcher(str);
        }

        @Override
        protected Void doInBackground() throws IOException {

            Path path = Paths.get(System.getProperty("user.home"));
            Files.walkFileTree(path, this);
            return null;
        }

        @Override
        protected void process(List<Path> chunks) {

            for (Path path : chunks) {

                area.append(path.toString() + "\n");
                count++;

                lbl.setText(String.format("Files found: %d", count));
            }
        }

        @Override
        protected void done() {

            btn.setEnabled(true);
        }

        @Override
        public FileVisitResult preVisitDirectory(Path dir, BasicFileAttributes attrs){

            return FileVisitResult.CONTINUE;
        }

        @Override
        public FileVisitResult visitFile(Path file, BasicFileAttributes attrs)  {

            if (matcher.matches(file)) {

                publish(file);
            }

            return FileVisitResult.CONTINUE;
        }

        @Override
        public FileVisitResult visitFileFailed(Path file, IOException exc) {

            return FileVisitResult.CONTINUE;
        }

        @Override
        public FileVisitResult postVisitDirectory(Path dir, IOException exc) {

            return FileVisitResult.CONTINUE;
        }
    }
}
```


- Paralelne tasky - vynutenie (ale pc sa rozhodne ci pojde to naozaj paralelne)
- Palindróm je všeobecne akákoľvek postupnosť symbolov, typicky slovo, veta, verš či číslo (ale napríklad i postupnosť nôt, DNA sekvencia a podobne), ktorá má tú vlastnosť, že ju možno čítať v ľubovoľnom smere (sprava doľava alebo zľava doprava).


```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;


void main() {
    // List of words to check
    List<String> words = Arrays.asList("level", "world", "radar", "java",
            "civic", "hello", "deified", "noon");

    // Find palindromes using parallel stream
    List<String> palindromes = findPalindromes(words);

    // Print the results
    System.out.println("Palindromes: " + palindromes);
}

List<String> findPalindromes(List<String> words) {
    return words.parallelStream() // Use parallel stream for concurrent processing
            .filter(this::isPalindrome) // Filter palindromes
            .collect(Collectors.toList()); // Collect results into a list
}

boolean isPalindrome(String word) {
    String reversed = new StringBuilder(word).reverse().toString(); // Reverse the word
    return word.equals(reversed); // Check if the original word is equal to its reverse
}
```

# Sekvencna kontrola dostupnosti stranok

```java
package com.zetcode;

import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.time.Duration;
import java.util.List;
import java.util.stream.Stream;

public class Main {

    public static void main(String[] args) {
        List<URI> uris = Stream.of(
                "https://www.google.com/",
                "https://clojure.org",
                "https://www.rust-lang.org",
                "https://golang.org",
                "https://www.python.org",
                "https://code.visualstudio.com",
                "https://ifconfig.me",
                "http://termbin.com",
                "https://www.github.com/"
        ).map(URI::create).toList();

        try (HttpClient httpClient = HttpClient.newBuilder()
                .connectTimeout(Duration.ofSeconds(10))
                .followRedirects(HttpClient.Redirect.ALWAYS)
                .build()) {

            for (URI uri : uris) {
                verifyUri(httpClient, uri);
            }
        }
    }

    private static void verifyUri(HttpClient httpClient, URI uri) {
        HttpRequest request = HttpRequest.newBuilder()
                .timeout(Duration.ofSeconds(5))
                .uri(uri)
                .build();

        try {
            HttpResponse<Void> response = httpClient.send(request, HttpResponse.BodyHandlers.discarding());
            if (response.statusCode() == 200) {
                System.out.printf("[SUCCESS] Verified %s%n", uri);
            } else {
                System.out.printf("[FAILURE] Failed to verify %s%n", uri);
            }
        } catch (Exception e) {
            System.out.printf("[FAILURE] Exception while verifying %s: %s%n", uri, e.getMessage());
        }
    }
}
```

# to iste ako hore ale asynchronne (requesty sa poslu naraz a potom sa caka na odpoved) rychlejsie 


```java
package com.zetcode;

import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.time.Duration;
import java.util.List;
import java.util.concurrent.CompletableFuture;
import java.util.stream.Stream;

public class Main {

    public static void main(String[] args) {

        List<URI> uris = Stream.of(
                "https://www.google.com/",
                "https://clojure.org",
                "https://www.rust-lang.org",
                "https://golang.org",
                "https://www.python.org",
                "https://code.visualstudio.com",
                "https://ifconfig.me",
                "http://termbin.com",
                "https://www.github.com/"
        ).map(URI::create).toList();

        try (HttpClient httpClient = HttpClient.newBuilder()
                .connectTimeout(Duration.ofSeconds(10))
                .followRedirects(HttpClient.Redirect.ALWAYS)
                .build()) {

            var futures = uris.stream()
                    .map(uri -> verifyUri(httpClient, uri))
                    .toArray(CompletableFuture[]::new);

            CompletableFuture.allOf(futures).join();
        }
    }

    private static CompletableFuture<Void> verifyUri(HttpClient httpClient,
                                                     URI uri) {
        HttpRequest request = HttpRequest.newBuilder()
                .timeout(Duration.ofSeconds(5))
                .uri(uri)
                .build();

        return httpClient.sendAsync(request, HttpResponse.BodyHandlers.discarding())
                .thenApply(HttpResponse::statusCode)
                .thenApply(statusCode -> statusCode == 200)
                .exceptionally(ex -> false)
                .thenAccept(valid -> {
                    if (valid) {
                        System.out.printf("[SUCCESS] Verified %s%n", uri);
                    } else {
                        System.out.printf("[FAILURE] Failed to verify%s%n", uri);
                    }
                });
    }
}
```

## JSoup  - struktura v html , vizual v  CSS
https://github.com/janbodnar/Java-Skolenie/blob/main/libs/jsoup.md
maven project
dependencies:
https://mvnrepository.com/artifact/org.jsoup/jsoup/1.18.1

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document title</title>
    <style>
        li {color:blue}
        p { font-family: Hevletica}
    </style>
</head>
<body>
<p>List of words</p>
<ul>
    <li>dark</li>
    <li>smart</li>
    <li>war</li>
    <li>cloud</li>
    <li>park</li>
    <li>cup</li>
    <li>worm</li>
    <li>water</li>
    <li>rock</li>
    <li>warm</li>
</ul>
<footer>footer for words</footer>
</body>
</html>
```

```java
package com.zetcode;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class JSoupFromStringEx {

    public static void main(String[] args) {

        String htmlString = """
                <html><head><title>My title</title></head>
                <body>Body content</body></html>""";

        Document doc = Jsoup.parse(htmlString);
        String title = doc.title();
        String body = doc.body().text();

        System.out.printf("Title: %s%n", title);
        System.out.printf("Body: %s", body);
    }
}

- stiahnutie stranky a dalsich veci zo stranky

```
package com.zetcode;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class Main {

    public static void main(String[] args) throws IOException {

        String url = "https://zoznam.sk";

        Document doc = Jsoup.connect(url).get();
        String title = doc.title();
        System.out.println(title);
        System.out.println(doc.body().text());

        String html = doc.html();
        Path path = Path.of("src/zoznam.html");
        Files.writeString(path,html);
    }
}
```

- ziskalnie najakych informacii zo stranok

```java
package com.zetcode;

import java.io.IOException;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class Main {

    public static void main(String[] args) throws IOException {

        String url = "https://zoznam.sk";
        Document document = Jsoup.connect(url).get();

        String description = document.select("meta[name=description]")
                .first().attr("content");
        System.out.println("Description : " + description);

        String keywords = document.select("meta[name=keywords]")
                .first().attr("content");
        System.out.println("Keywords : " + keywords);
    }
}
```

- najdenie vsetkych tagov v dokumente

```java
package com.zetcode;

import org.jsoup.Jsoup;

import java.io.File;
import java.io.IOException;

public class JSoupAll {

    public static void main(String[] args) throws IOException {

        var fileName = "src/main/resources/words.html";
        var myFile = new File(fileName);

        var doc = Jsoup.parse(myFile, "UTF-8");
        var all = doc.body().select("*");

        all.forEach(e -> System.out.println(e.tagName()));
    }
}
```

zmena hodnot tagov

```java
package com.zetcode;

import org.jsoup.Jsoup;

public class Main {

    public static void main(String[] args) {

        String htmlString = """
                <html><head><title>My title</title></head>
                <body></body></html>""";

        var doc = Jsoup.parse(htmlString);

        var e = doc.select("body").first();
        e.append("<p>hello there!</p>");
        e.prepend("<h1>Heading</h1>");

        System.out.println(doc);
    }
}
```

vyhladanie liniek (externych/internych) na stranke


```java
package com.zetcode;

import java.io.IOException;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

public class Main {

    public static void main(String[] args) throws IOException {

        String url = "https://jsoup.org";

        Document document = Jsoup.connect(url).get();
        Elements links = document.select("a[href]");

        for (Element link : links) {

            System.out.println("link : " + link.attr("href"));
            System.out.println("text : " + link.text());
        }
    }
}
```


https://github.com/janbodnar/Java-Skolenie/blob/main/compile_run.md
Visual studio:


![image](https://github.com/user-attachments/assets/b519e0d9-8c5d-41b3-a47e-fc957694f5e8)

![image](https://github.com/user-attachments/assets/1c76989c-4f78-4a72-aff2-af040535fec4)

do prilkazoveho riadku (View - Terminal) vo visual studiu: 
![image](https://github.com/user-attachments/assets/80b8f8fb-67ee-470b-a55e-6b933533b7ad)
java --enable-preview --source 22  .\Main.java

1. Kompilacia do bytecode
javac -d bin .\com\example\Main.java

2. spustenie java class z bin adresara
C:\Users\student\Documents\javaprogram\bin> java com.example.Main

![image](https://github.com/user-attachments/assets/9ab87641-d28b-4f48-8e5e-fbfa8d396035)


## Datetime


https://github.com/janbodnar/Java-Skolenie/blob/main/common/datetime.md

```java
import java.time.Instant;
import java.time.ZoneId;
import java.time.temporal.ChronoUnit;

void main() {

    var timestamp = Instant.now();
    System.out.println("The current timestamp: " + timestamp);

    System.out.printf("Unix time: %d%n", timestamp.toEpochMilli());

    //Now minus five days
    var minusFive = timestamp.minus(5, ChronoUnit.DAYS);
    System.out.println("Now minus five days:" + minusFive);

    var atZone = timestamp.atZone(ZoneId.of("GMT"));
    System.out.printf("GMT: %s%n", atZone);

    var yesterday = Instant.now().minus(24, ChronoUnit.HOURS);
    System.out.println("Yesterday: " + yesterday);
}
```

```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.time.format.FormatStyle;
import java.util.Locale;

void main() {

//    Locale.setDefault(Locale.ENGLISH);
    Locale.setDefault(Locale.of("sk", "SK"));

    var now = LocalDate.now();

    var dtf1 = DateTimeFormatter.ofLocalizedDate(FormatStyle.SHORT);
    var dtf2 = DateTimeFormatter.ofLocalizedDate(FormatStyle.MEDIUM);
    var dtf3 = DateTimeFormatter.ofLocalizedDate(FormatStyle.LONG);
    var dtf4 = DateTimeFormatter.ofLocalizedDate(FormatStyle.FULL);

    System.out.println(dtf1.format(now));
    System.out.println(dtf2.format(now));
    System.out.println(dtf3.format(now));
    System.out.println(dtf4.format(now));
}
```

# operacia String datum/cas na format datum/cas


```java
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.time.temporal.TemporalAccessor;
import java.util.Locale;

void main() {

    Locale.setDefault(Locale.ENGLISH);

    String d = "2023-10-26";

    DateTimeFormatter dtf = DateTimeFormatter.ISO_DATE;
    TemporalAccessor ta = dtf.parse(d);
    LocalDate ld = LocalDate.from(ta);
    System.out.println(ld);

    String sd1 = "2018-01-04";
    LocalDate ld1 = LocalDate.parse(sd1);
    System.out.println("Date: " + ld1);

    String sdatetime = "2017-08-16T16:34:10";
    LocalDateTime ldt = LocalDateTime.parse(sdatetime);
    System.out.println("Datetime: " + ldt);

    DateTimeFormatter dtfmt = DateTimeFormatter.ofPattern("dd MMM yyyy");
    String anotherDate = "14 Aug 2017";
    LocalDate lds = LocalDate.parse(anotherDate, dtfmt);
    System.out.println(anotherDate + " parses to " + lds);
}
```

## Prakticke priklady
maven project
pgadmin install
https://mvnrepository.com/artifact/org.postgresql/postgresql/42.7.4
https://mvnrepository.com/artifact/org.jdbi/jdbi3-core/3.45.4


