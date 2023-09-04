# Maven

Az Apache Maven egy erőteljes és széles körben használt szoftverprojekt-kezelő és 
build-tool (eszköz), 
amit főként Java projektekhez használnak, de más nyelvekhez is alkalmazható. 
A Maven egyszerűsíti a build folyamatot, kezeli a függőségeket, 
és automatizál számos gyakori feladatot, így alapvető eszköz a fejlesztők számára. 

---

## 1. Bevezetés

### 1.1 Miért érdemes a Mavent használni?

- **Függőségkezelés:** A Maven egyszerűsíti a projekt függőségeinek kezelését, 
- lehetővé téve a könyvtárak deklarációját és letöltését.

- **Konzisztencia:** A Maven egy egységes projektstruktúrát, elnevezési konvenciókat 
- és build folyamatot biztosít, ezzel biztosítva a projektek konzisztenciáját.

- **Build Automatizálás:** A Maven automatizálja a fordítás, tesztelés és csomagolás stb. 
- feladatokat.

- **Bővíthetőség:** A Maven erősen bővíthető bővítmények segítségével, 
- lehetővé téve az eszköz testreszabását a projekt saját igényeinek megfelelően.

### 1.2 Telepítés


1. **Maven Letöltése:** Látogass el az [Apache Maven hivatalos weboldalára](https://maven.apache.org/download.cgi) 
2. és töltsd le a legfrissebb Maven verziót.

2. **Maven Telepítése:** Kövesd a telepítési utasításokat (az operációs rendszered függvényében).

3. **Telepítés Ellenőrzése:** Nyisd meg a terminált vagy parancssort, és futtasd 
a `mvn -version` parancsot, hogy leellenőrizzük a Maven sikeres telepítését. 

---

## 2. Maven Alapok

### 2.1 Projekt struktúra

A Maven egy meghatározott könyvtárstruktúrát vár el a projektjétől:

- `src/` könyvtár: Tartalmazza a forráskódot
- `target/` könyvtár: A Maven itt helyezi el a fordított osztályokat és a generált fájlokat
- `pom.xml`: A Projekt Object Model (POM) fájl, ami definiálja a projekt konfigurációját

### 2.2 POM (Project Object Model)

A `pom.xml` fájl a Maven projekt központja. 
Tartalmazza a projekt metaadatait, függőségeit és build utasításokat.
Itt van egy alapvető `pom.xml` struktúra:

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>hu.progmatic</groupId>
    <artifactId>my-first-maven-project</artifactId>
    <version>1.0.0</version>
    
    <!-- Függőségek és Bővítmények ide -->
</project>
```
* `groupId`: Az cég/csapat egyedi azonosítója, aki létrehozza a projektet
* `artifactId`: A projekt neve
* `version`: A projekt verziószáma

### 2.3 Életciklus
A Maven előre definiált build életciklust használ, amelynek leggyakoribb "fázis"-ai:

* `clean`: Törli a target könyvtárat
* `compile`: Fordítja a forráskódot
* `test`: Futtatja a teszteket
* `package`: Csomagolja a fordított kódot egy alkalmazásba
* `install`: Telepíti az alkalmazást lokálisan
* `deploy`: Feltölti az alkalmazást egy távoli szerverre

Ezeket a fázisokat Maven parancsokkal lehet futtatni, például `mvn clean`, `mvn compile`, stb.

### 2.4 Célok és bővítmények
A Maven bővítmények felelősek a célok végrehajtásáért, amik a fázisokon belüli konkrét feladatok. Például a compiler bővítmény biztosítja a compile célt a forráskód fordításához. A bővítményeket a pom.xml fájlban lehet testre szabni.

## 3. Függőségek Kezelése
### 3.1 Függőségkezelés
A Maven egyszerűsíti az külső könyvtárak (library-k, avagy függőségek) kezelését. 
A függőségeket a `pom.xml` fájlban kell meghatározni, és a Maven letölti és kezeli őket. 
Például:

```xml
<dependencies>
    <dependency>
        <groupId>csoport-azonosito</groupId>
        <artifactId>artifact-azonosito</artifactId>
        <version>1.0.0</version>
    </dependency>
</dependencies>
```
### 3.2 Függőségek hatóköre
A függőség hatókör meghatározza, hogy mikor érhető el egy függőség a build folyamat során.
A közönséges hatókörök a következők:

* `compile`: Elérhető a fordítás és futási idő alatt
* `test`: Csak a tesztelés során érhető el
* `provided`: A futási környezet által biztosított (például servlet konténerek)
* 
### 3.3 Függőségfeloldás
A Maven rekurzívan feloldja a függőségeket, hogy biztosítsa a projektnek az összes szükséges
függőséget és azok tranzitív (implikált) függőségeit, avagy: a függőségek által hivatkozott függőségeket.

## 4. Projektek buildelése
### 4.1 Tisztítás és fordítás
* `mvn clean`: Törli a *target* könyvtárat
* `mvn compile`: Fordítja a forráskódot a src könyvtárban
### 4.2 Csomagolás
* `mvn package`: Fordítja, teszteli és csomagolja a projektet egy futtatható formátumba (pl. JAR, WAR)
### 4.3 Tesztek futtatása
* `mvn test`: Futtatja a unit teszteket a src/test könyvtárban

# Feladat

## Library Maven projekt létrehozása IntelliJ-ben

**pom.xml**

```xml

<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>hu.progmatic</groupId>
    <artifactId>library-module</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>
</project>
```

### Példakód különböző láthatóságokkal

*hu.progmatic.LibraryClass*

```java
package hu.progmatic;

public class LibraryClass {

    private void youCannotSeeMe() {
        System.out.println("This is a secret!");
    }

    public void doSomethingFun() {
        System.out.println("LibraryClass is doing something!");
    }
}
```

---

*hu.progmatic.AbstractLibraryClass*

```java
package hu.progmatic;

public abstract class AbstractLibraryClass {

    protected void shieldMeFromPublicEyes() {
        System.out.println("This is only for the select few!");
    }

    public abstract void doSomethingAbstractFun();
}
```

## Maven lib telepitése lokális környezetben

1. `mvn clean install`
2. Main maven porojekt létrehozása
3. `library-module` hivatkozása a pom.xml-be:

```xml

<project>
    <!-- ... -->

    <groupId>hu.progmatic.main</groupId>
    <artifactId>main</artifactId>

    <!-- ... -->
    <dependencies>
        <dependency>
            <groupId>hu.progmatic</groupId>
            <artifactId>library-module</artifactId>
            <version>1.0</version>
        </dependency>
    </dependencies>

</project>
```

### Példakód a module kipróbálására

```java
package hu.progmatic.main;

import hu.progmatic.LibraryClass;
import hu.progmatic.LocalChildLibrary;

public class Main {
    public static void main(String[] args) {

        LibraryClass progmaticLibraryClass = new LibraryClass();

        progmaticLibraryClass.doSomethingFun(); // Should println something
        progmaticLibraryClass.youCannotSeeMe(); // Compilation error, for private method

        LocalChildLibrary localChildLibrary = new LocalChildLibrary();
        localChildLibrary.shieldMeFromPublicEyes(); // Compilation error if we access from different package
        localChildLibrary.doSomethingAbstractFun();
    }
}
```

### Öröklödés külső függőségből

```java
package hu.progmatic.main;

public class LocalChildLibrary extends AbstractLibraryClass {

    @Override
    public void doSomethingAbstractFun() {
        // We have to implement this

        super.shieldMeFromPublicEyes(); // We can only see this from inside
    }
}
```

4. `mvn dependency:tree`: Megmutatja, hogy milyen függőségek kerültek telepitésre a projekten belül, rekurzivan

## Más Maven függőségek használata

### Json

```xml

<dependency>
    <groupId>org.json</groupId>
    <artifactId>json</artifactId>
    <version>20230227</version>
</dependency>
```