# Java
## Instalacia 

1. Download IntelliJ IDEA – The Leading Java and Kotlin IDE (jetbrains.com)  --> Community edition
https://www.jetbrains.com/idea/download/?fromIDE=%2F&section=windows

 ![image](https://github.com/user-attachments/assets/9d504739-0d7f-485e-933a-ed85bbd53fef)


## Skolenie


https://github.com/janbodnar/Java-Skolenie
https://github.com/janbodnar/Java-Skolenie/blob/main/definitions.md
https://github.com/janbodnar/Java-Skolenie/blob/main/basics.md


Test.md - vsetky priklady zo skolenia:
https://github.com/janbodnar/Java-Skolenie/blob/main/test.md

-	Zjednodusena syntax class Main pre edukacne ucely od java 21, 22:

```java
void main() {

    int age = 34;
    String name = "William";

    String output = String.format("%s is %d years old.", name, age);

    System.out.println(output);
}
```


[Java-Skolenie/lexis.md at main · janbodnar/Java-Skolenie · GitHub](https://github.com/janbodnar/Java-Skolenie/blob/main/lexis.md)
## Zdrojovy kod je tvoreny tokenmi
## reformatovat kod : Ctrl+ Alt + l
## Priklady:


```java
import java.util.List;

void say_hello() {
    System.out.println("bla bla");
}

void main() {
    String name = "John Doe";
    int age = 34;

    System.out.println(name);
    System.out.println(age);
    System.out.println("Hello java");
    say_hello();

    name = "John Deep";
    System.out.println(name);
    age = 25;
    System.out.println(age);
    String occupation = "gardener";
    System.out.println(name + " is " + age + " years old and he is " + occupation);


    List<String> words = List.of("sky", "blue", "nice", "pet", "nord", "blabla");
    for (String word : words) {

        System.out.println(word);
    }
    System.out.println("There are " + words.size() + " words");

    final int WIDTH = 100;
    final int HEIGHT = 150;
    //WIDTH = 120;
    System.out.println(WIDTH + " " + HEIGHT);

    //formatovanie stringu
    age = 34;
    name = "William";
    float weight = 78.5f; // bud double alebo float  var weight= 78.5f bude float; var weight= 78.5 bude double

    //String output = String.format("%s is %d years old and he is a %s", name, age, occupation);
    var output = String.format("%s is %d years old and he is a %s and he is %f", name, age, occupation, weight);
    System.out.println(output);

    //rovno formatuje string  System.out.printf
    System.out.printf("%s is %d years old and he is a %s and he is %f", name, age, occupation, weight);
}
```


## Flow control


https://github.com/janbodnar/Java-Skolenie/blob/main/flow_control.md


## „case“ - The switch statement


```java
import java.util.Scanner;

void main() {

    System.out.print("Enter a domain:");

    try (var sc = new Scanner(System.in)) {

        String domain = sc.nextLine();
        domain = domain.trim().toLowerCase(); // odstrani prazdne znaky trim() a zmeni na male pismena toLowerCase()

        switch (domain) {

            case "us":
                System.out.println("United States");
                break;

            case "de":
                System.out.println("Germany");
                break;

            case "sk":
                System.out.println("Slovakia");
                break;

            case "hu":
                System.out.println("Hungary");
                break;

            default:
                System.out.println("Unknown");
                break;
        }
    }
}
```


## modernejsia syntax „case“  - The switch expression


```java
import java.util.Scanner;

void main() {

    System.out.print("Enter a domain: ");

    try (var sc = new Scanner(System.in)) {

        String domain = sc.nextLine();
        domain = domain.trim().toLowerCase();

        switch (domain) {

            case "us" -> System.out.println("United States");
            case "de" -> System.out.println("Germany");
            case "sk" -> System.out.println("Slovakia");
            case "hu" -> System.out.println("Hungary");
            default -> System.out.println("Unknown");
        }
    }
}
```


```java
import java.util.Scanner;

void main() {

    System.out.print("Enter a domain: ");

    try (var sc = new Scanner(System.in)) {

        String domain = sc.nextLine();
        domain = domain.trim().toLowerCase();

        String res = switch (domain) {

            case "us" -> "United States";
            case "de" -> "Germany";
            case "sk" -> "Slovakia";
            case "hu" -> "Hungary";
            case "cz" -> "Czech";
            default -> "Unknown";
        };
        System.out.println("Domena je "+res);
    }
}
```


## WHILE - The while statement


void main() {

    int i = 0;
    int sum = 0;
    String message = "Hello there";

    while (i < 20) {
        System.out.println(message);
        i++;
    }
}

## FOR - The for statement


Premenne prostredia
String heslo = System.getenv("DB_PASSWORD")


```java
void main() {

    int i = 0;
    int sum = 0;
    String message = "Hello there";

    while (i < 20) {
        System.out.println(message);
        i++;
    }


    for (int j = 10; j > 0; j--) {

            System.out.println(j);
        }
    String heslo = System.getenv("DB_PASSWD");
    System.out.println(heslo);
}
```

## Polia + for each cyklus - Enhanced for statement


```java
void main() {
    String[] planets = {
                "Mercury", "Venus", "Earth",
                "Mars", "Jupiter", "Saturn", "Uranus", "Pluto"
        };

        for (String planet : planets) {

            System.out.println(planet);
        }
}
```


```java
void main() {
    String[] planets = {
            "Mercury", "Venus", "Earth",
            "Mars", "Jupiter", "Saturn", "Uranus", "Pluto"
    };
    int len = planets.length;
    System.out.println(len);
    System.out.println(planets[0]);
    System.out.println(planets[len - 1]);


    for (int i = 0; i < planets.length - 1; i++)
        System.out.println(planets[i]);

    for (int i = planets.length - 1; i >= 0; i--)
        System.out.println(planets[i]);
//        for (String planet : planets) {
//
//            System.out.println(planet);
//        }
    int sum = 0;
    int[] vals = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int dlzka = vals.length;
    for (int j = 0; j < vals.length; j++) {
        sum += vals[j];
    }
    System.out.println(sum);
}
```

## nova a stara syntax


```java
//nova syntax:
void main() {
    String[] planets = {
            "Mercury", "Venus", "Earth",
            "Mars", "Jupiter", "Saturn", "Uranus", "Pluto"
    };
    int len = planets.length;
    System.out.println(len);
    System.out.println(planets[0]);
    System.out.println(planets[len - 1]);


    for (int i = 0; i < planets.length - 1; i++)
        System.out.println(planets[i]);

    for (int i = planets.length - 1; i >= 0; i--)
        System.out.println(planets[i]);

    for (String planet : planets) {
        System.out.println(planet);
        }

    //stara syntax 
    int sum = 0;
    int[] vals = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int dlzka = vals.length;
    for (int j = 0; j < vals.length; j++) {
        sum += vals[j];
    }
    System.out.println("stara syntax: "+sum);

    //nova syntax
    int suma =0;
    for (int k : vals) {
        suma += k;
    }
    System.out.println("nova syntax: "+suma);
}
```


The break statement:
import java.util.Random;

void main() {

    var random = new Random();

    while (true) {

        int num = random.nextInt(30);
        System.out.print(num + " ");

        if (num == 22) {

            break;
        }
    }

    System.out.print('\n');
}

The continue statement
void main() {

    int num = 0;

    while (num < 100) {

        num++;

        if (num % 2 == 0) {
            continue;
        }

        System.out.print(num + " ");
    }

    System.out.print('\n');
}



Priklady
Print words in titlecase
void main() {

    String[] words = { "sky", "nord", "cup", "cloud", "war", "water" };

    for (String word: words) {

        System.out.println(Character.toUpperCase(word.charAt(0)) + word.substring(1).toLowerCase());
        
    }
}
Generate 10 random integers
import java.util.Random;

void main() {

    var random = new Random();

    for (var i = 0; i < 10; i++) {

        var r = random.nextInt(10);
        System.out.println(r);
    }
}
Calculate sum
void main() {

    int sum = 0;
    int[] vals = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

    for (int i = 0; i< vals.length; i++) {

        sum = sum + vals[i];
    }

    System.out.println(sum);
}
void main() {

    int[] vals = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int sum = 0;

    for (int val: vals) {
        sum = sum + val;
    }

    System.out.println(sum);

    System.out.println("end of program");
}
Formatovany vystup
void main() {

    int age = 34;
    String name = "William";
    String occupation = "gardener";
    float weight = 78.5f;

    String output = String.format("%s is %d years old and he is a %s, his weight is %f kg", name, age, occupation, weight);
    System.out.println(output);
    
    System.out.printf("%s is %d years old and he is a %s, his weight is %f kg", name, age, occupation, weight);
}
Premenne
void main() {

    String name = "John Doe";
    int age = 34;

    System.out.println(name);
    System.out.println(age);

    name = "Roger Roe";
    System.out.println(name);

    age = 40;
    System.out.println(age);
}
void main() {

    String name = "John Doe";
    int age = 34;
    String occupation = "gardener";

    System.out.println(name + " is " + age + " years old" + " and he is a " + occupation );
}







-	Vypise vsetky slova zacinajuce na w:
void main() {

    String[] words = {"sky", "war", "water", "cup", "cloud", "warm"};

    for (String word : words) {
        if (word.startsWith("w")) {
            System.out.println(word);
        }

    }
}



Java-Skolenie/operators.md at main · janbodnar/Java-Skolenie · GitHub

import java.util.Arrays;
/*
rozbije retazec cisel na pole stringov, prekonvertuje na integer a spocita:
 */
void main() {
    int sum=0;
    String data = "1,2,3,4,5,6,7,8,9,10";
    String[] parts= data.split(",");
    System.out.println(Arrays.toString(parts));
    for (String part : parts){
        sum += Integer.parseInt(part);
    }
    System.out.println(sum);
}

Java-Skolenie/arrays.md at main · janbodnar/Java-Skolenie · GitHub

import java.util.Arrays;

void main() {

    int[] a = new int[5];

    a[0] = 1;
    a[1] = 2;
    a[2] = 3;
    a[3] = 4;
    a[4] = 5;

    System.out.println(Arrays.toString(a));

    //alternativa
    int[] b = {1,2,3,4,5};
    System.out.println((Arrays.toString(b)));

    //alternativa
    var c = new int[] {1,2,3,4,5};
    System.out.println((Arrays.toString(b)));

    //pole jednotiek
    int[] d = new int[1000];

    // existuje cely rad Arrays funkcii
    Arrays.fill(d,1);
    System.out.println((Arrays.toString(d)));

}


Vytvorenie artefaktu : Hamburger - > Project structure -> Artefacts -> + 
C:\Users\student\IdeaProjects\FristArchive\out\artifacts\FristArchive_jar
 

Potom hamburger - > Build Airtifacts - > Build
 

 


Do consoly:
Najst cd .\artifacts\FristArchive_jar\
A spustit:
java -jar .\FristArchive.jar 1 2 3 4 5
 


Java-Skolenie/data_types.md at main · janbodnar/Java-Skolenie · GitHub

Java-Skolenie/data_types.md at main · janbodnar/Java-Skolenie · GitHub
Ak su premenne zadefinovane mimo funkciu, tak nadobudaju defaut hodnoty vid. nizsie
Ak su definovane vo funkcii, tak ich je potrebne nainializovat
byte b;
char c;
short s;
int i;
float f;
double d;
String str;
Object o;

void main() {

    System.out.println(b);
    System.out.println(c);
    System.out.println(s);
    System.out.println(i);
    System.out.println(f);
    System.out.println(d);
    System.out.println(str);
    System.out.println(o);
}


Objektove programovanie:
Java-Skolenie/oop/oop.md at main · janbodnar/Java-Skolenie · GitHub

package com.zetcode;

class Person {

    private String fName;
    private String lName;
    public String getFname() {
        return fName;
    }

    public void setFname(String fName) {
        this.fName = fName;
    }

    public String getLname() {
        return lName;
    }

    public void setLname(String lName) {
        this.lName = lName;
    }
    
}

public class Main {

    public static void main(String[] args) {

        Person p1 = new Person();
        p1.setFname("Jane");
        p1.setLname("Black");

        Person p2 = new Person();
        p2.setFname("Beky");
        p2.setLname("White");

        System.out.println(p1.getFname()+" " +p1.getLname());
        System.out.println(p2.getFname()+" " +p2.getLname());
    }
}



2 triedy
 


 

package com.zetcode;
import com.zetcode.model.Person;

public class Main {

    public static void main(String[] args) {

        Person p1 = new Person();
        p1.setFname("Jane");
        p1.setLname("Black");

        Person p2 = new Person();
        p2.setFname("Beky");
        p2.setLname("White");

        System.out.println(p1.getFname()+" " +p1.getLname());
        System.out.println(p2.getFname()+" " +p2.getLname());
        System.out.println(p1);
        System.out.println(p2);
    }
}


package com.zetcode.model;

public class Person {

    private String fName;
        private String lName;
        public String getFname() {
            return fName;
        }

        public void setFname(String fName) {
            this.fName = fName;
        }

        public String getLname() {
            return lName;
        }

        public void setLname(String lName) {
            this.lName = lName;
        }

    @Override
    public String toString() {
        return "Person{" +
                "fName='" + fName + '\'' +
                ", lName='" + lName + '\'' +
                '}';
    }
}



KONSTRUKTOR:

package com.zetcode;
import com.zetcode.model.Person;

public class Main {

    public static void main(String[] args) {

        Person p1 = new Person("Jane","Black");
//        p1.setFname("Jane");
//        p1.setLname("Black");

        Person p2 = new Person("Beky", "White");
//        p2.setFname("Beky");
//        p2.setLname("White");

        System.out.println(p1.getFname()+" " +p1.getLname());
        System.out.println(p2.getFname()+" " +p2.getLname());
        System.out.println(p1);
        System.out.println(p2);
    }
}


package com.zetcode.model;

public class Person {
    //konstruktor:
    public Person(String fName, String lName) {
        this.fName = fName;
        this.lName = lName;
    }

    private String fName;
        private String lName;
        public String getFname() {
            return fName;
        }

        public void setFname(String fName) {
            this.fName = fName;
        }

        public String getLname() {
            return lName;
        }

        public void setLname(String lName) {
            this.lName = lName;
        }

    @Override
    public String toString() {
        return "Person{" +
                "fName='" + fName + '\'' +
                ", lName='" + lName + '\'' +
                '}';
    }
}



package com.zetcode;

class Rectangle {
    private int width;
    private int height;

    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    public int getWidth() {
        return width;
    }

    public void setWidth(int width) {
        this.width = width;
    }

    public int getHeight() {
        return height;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    public int getArea(){
        return this.height* this.width;
    }
}


class Circle {
    public Circle(int radius) {
        this.radius = radius;
    }

    private int radius;

    public void setRadius(int radius) {

        this.radius = radius;
    }

    public double area() {

        return this.radius * this.radius * Math.PI;
    }
}

public class Main {

    public static void main(String[] args) {

        Circle c = new Circle(10);
        System.out.println(c.area());
        c.setRadius(5);
        System.out.println(c.area());

        Rectangle r = new Rectangle(2,4);
        System.out.println(r.getArea());

    }
}


rozbite na 2 triedy:
package com.zetcode;

public class Main {

    public static void main(String[] args) {

        Circle c = new Circle(10);
        System.out.println(c.area());
        c.setRadius(5);
        System.out.println(c.area());

        Rectangle r = new Rectangle(2,4);
        System.out.println(r.getArea());

    }
}


package com.zetcode;

public class Circle {
        public Circle(int radius) {
            this.radius = radius;
        }

        private int radius;

        public void setRadius(int radius) {

            this.radius = radius;
        }

        public double area() {

            return this.radius * this.radius * Math.PI;
        }
}

package com.zetcode;

public class Rectangle {

        private int width;
        private int height;

        public Rectangle(int width, int height) {
            this.width = width;
            this.height = height;
        }

        public int getWidth() {
            return width;
        }

        public void setWidth(int width) {
            this.width = width;
        }

        public int getHeight() {
            return height;
        }

        public void setHeight(int height) {
            this.height = height;
        }

        public int getArea(){
            return this.height* this.width;
        }
}


Poznamky vseobecne:
Copilot (microsoft.com)

