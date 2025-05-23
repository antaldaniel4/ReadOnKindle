A `List`, `Set` és `Map` a Java három leggyakrabban használt **kollekció típusa**, és mindegyik más-más célra készült. Nézzük meg **részletesen**, **példákkal és hasonlattal** is\!

---

## **📋 1\. `List` – Sorrendben tárolt elemek, duplikátumok engedélyezettek**

### **✅ Tulajdonságok:**

* **Megőrzi a hozzáadás sorrendjét**.

* **Lehetnek benne ismétlődő elemek**.

* Index alapján elérhetőek az elemek (pl. `list.get(0)`).

### **🧠 Használat:**

* Bevásárlólista, keresési előzmények, naplófájl.

### **📌 Példa:**
```java
import java.util.ArrayList;  
import java.util.List;

public class ArrayListPelda {  
    public static void main(String\[\] args) {  
        List\<String\> nevek \= new ArrayList\<\>();  
        nevek.add("Anna");  
        nevek.add("Béla");

        for (String nev : nevek) {  
            System.out.println(nev);  
        }  
    }  
}
```
---

## **🌳 2\. `Set` – Nincs sorrend, nincs ismétlődés**

### **✅ Tulajdonságok:**

* **Nem engedi meg a duplikált elemeket**.

* **Nincs garantált sorrend** (kivéve pl. `LinkedHashSet` vagy `TreeSet`).

* Gyors keresés `contains()` segítségével.

### **🧠 Használat:**

* Felhasználónevek, e-mail címek, címkék (tag-ek) tárolására.

### **📌 Példa:**
```java
import java.util.HashSet;  
import java.util.Set;

public class HasSetPelda {  
    public static void main(String\[\] args) {  
        Set\<String\> gyumolcsok \= new HashSet\<\>();  
        gyumolcsok.add("alma");  
        gyumolcsok.add("körte");  
        gyumolcsok.add("szilva");  
        gyumolcsok.add("alma"); // duplikált elem

        for (String gyumolcs : gyumolcsok) {  
            System.out.println(gyumolcs);  
        }  
    }  
}
```
---

## **🗺️ 3\. `Map` – Kulcs-érték párok (mint egy szótár)**

### **✅ Tulajdonságok:**

* Minden kulcshoz **egy érték** tartozik.

* A kulcsok **egyediek**.

* Gyors elérés kulcs alapján (`map.get("kulcs")`).

### **🧠 Használat:**

* Felhasználónév–jelszó párok, termék–ár lista, név–telefonszám tárolása.

### **📌 Példa:**
```java
import java.util.HashMap;  
import java.util.Map;

public class HasMapPelda {  
    public static void main(String\[\] args) {  
        Map\<String, Integer\> jegyek \= new HashMap\<\>();  
        jegyek.put("Anna", 5);  
        jegyek.put("Béla", 4);

        System.out.println("Anna jegye: " \+ jegyek.get("Anna"));  
    }  
}
```
---

## **🧾 Összefoglaló táblázat**

| Jellemző | `List` | `Set` | `Map` |
| ----- | ----- | ----- | ----- |
| Tárolási forma | Elemlista | Egyedi elemek | Kulcs–érték párok |
| Ismétlődő elemek? | ✅ igen | ❌ nem | 🔑 kulcs: ❌, érték: ✅ |
| Sorrend számít? | ✅ igen | ❌ nem (de lehet) | ❌ kulcs szerint sem (kivéve `TreeMap`) |
| Példa | Bevásárlólista | Egyedi nevek listája | Felhasználó → jelszó |
| Index alapú elérés | ✅ igen | ❌ nem | ❌ (csak kulcs alapján) |

---

## **🎯 Mikor melyiket használd?**

| Cél | Használj |
| ----- | ----- |
| Sorrend számít, lehet ismétlés | `List` |
| Sorrend nem számít, nincs ismétlés | `Set` |
| Kulcs alapján keresel értéket | `Map` |

---

## **4\. Interface szerepe**

### **Példa: `Animal` interfész és két megvalósítása**
```java
interface Animal {  
    void makeSound();  
}

class Dog implements Animal {  
    public void makeSound() {  
        System.out.println("Vau vau\!");  
    }  
}

class Cat implements Animal {  
    public void makeSound() {  
        System.out.println("Miau\!");  
    }  
}

public class InterfacePelda {  
    public static void main(String\[\] args) {  
        Animal a1 \= new Dog();  
        Animal a2 \= new Cat();

        a1.makeSound();  
        a2.makeSound();  
    }  
}
```
### **Magyarázat:**

* Az `interface` definiálja, **mit tud egy osztály**, de nem **hogyan**.

* A `Dog` és `Cat` osztályok saját módon valósítják meg a `makeSound()` metódust.

* Ez lehetővé teszi a **polimorfizmust**.

---

## **5\. `Object.equals()` és keresés adattagokra**
```java
class Ember {  
    String nev;  
    int kor;

    Ember(String nev, int kor) {  
        this.nev \= nev;  
        this.kor \= kor;  
    }

    @Override  
    public boolean equals(Object obj) {  
        if (this \== obj) return true;  
        if (\!(obj instanceof Ember)) return false;

        Ember masik \= (Ember) obj;  
        return this.nev.equals(masik.nev) && this.kor \== masik.kor;  
    }

    @Override  
    public String toString() {  
        return nev \+ " (" \+ kor \+ ")";  
    }  
}
```
```java
import java.util.ArrayList;  
import java.util.List;

public class EmberKereses {  
    public static void main(String\[\] args) {  
        List\<Ember\> lista \= new ArrayList\<\>();  
        lista.add(new Ember("Anna", 20));  
        lista.add(new Ember("Béla", 25));

        Ember keresett \= new Ember("Anna", 20);  
        System.out.println("Tartalmazza?: " \+ lista.contains(keresett));  
    }  
}
```

### **Magyarázat:**

* `equals()` metódust **felül kell írni**, ha objektumokat akarunk összehasonlítani.

* `contains()` a `List`\-ben `equals()`\-t használ.

---

## **6\. Fájl írás/olvasás**

### **Fájlba írás**
```java
import java.io.FileWriter;  
import java.io.IOException;

public class FileIras {  
    public static void main(String\[\] args) {  
        try (FileWriter writer \= new FileWriter("pelda.txt")) {  
            writer.write("Helló fájl\!\\nEz egy új sor.");  
        } catch (IOException e) {  
            e.printStackTrace();  
        }  
    }  
}
```
### **Fájl olvasás**
```java
import java.io.BufferedReader;  
import java.io.FileReader;  
import java.io.IOException;

public class FileOlvasas {  
    public static void main(String\[\] args) {  
        try (BufferedReader reader \= new BufferedReader(new FileReader("pelda.txt"))) {  
            String sor;  
            while ((sor \= reader.readLine()) \!= null) {  
                System.out.println(sor);  
            }  
        } catch (IOException e) {  
            e.printStackTrace();  
        }  
    }  
}
```
### **Magyarázat:**

* A fájlkezelés try-with-resources használatával **automatikus zárást** biztosít.

* `FileWriter`: szöveg írására.

* `BufferedReader`: soronkénti olvasásra.

---
