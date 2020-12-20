# Praktikum 5
## Kontrollfragen
### 1.  Was ist der Unterschied zwischen einer Prozedur und einer Funktion? Wie dirdiese in C umgesetzt?
Funktion: Eine Funktion besitzt einen Rückgabewert.
```c
    /* Die Deklaration der Funktion "foo" 
     * mit int als Rueckgabedatenwert.
     * "bar" ist ein Parameter vom Tpy float.
     */
    int foo(float bar);
``` 

Prozedur: Es werden Anweisungen ausgeführt.
```c
    /* Die Deklaration der Funktion "foo" 
     * als Prozedur ohne Rueckgabedatenwert.
     * "bar" ist ein Parameter vom Tpy float.
     */
    void foo(float bar);
``` 
In C wird nicht zwischen Finktionen und Prozeduren unterschieden. beide werden mit der gleichen Syntax daklariert. Der Unterschied ist lediglich der Rückgabedatenwert `void`, was soviel wie "leer" bedeutet.

Quelle: https://stackoverflow.com/questions/721090/what-is-the-difference-between-a-function-and-a-procedure

### 2. Was sind die typtischen Gründe für die Verwendung von C-Funktionen?
Funktionen fassen Blöcke von inhaltlich zusammenhängenden Anweisungen zusammen. Durch die Verwendung von Funktionen lässt sich die Übersichtlichkeit und die Struktur des Quellcodes verbessern.
 
Eine Funktion belegt immer den gleichen Speicher, unabhängig davon, wie oft diese aufgerufen wird. Das bedeuttd eine geringere Größe der Binärdatei.

### 3. Was ist der Unterschied zwischen einem MAKRO und einer Inline-Funktion? Warum sollte einer Inline-Funktion der Vorzug gewährt werden?

### 4. Was ist unter Parameterübergabe per Value zu verstehen? Wann wird sie verwendet?
Wenn eine Variable bei einer Funktion per Value (Wert) übergeben wird, dann wird die eigentliche Variable nicht verändert. Nur der wert in einer Variable und nicht "die Variable selbst" wird übergeben.
```c
    // Funktionsdeklaration 
    // Rueckgabedatentyp: int / Parameterdatentyp: int
    int foo(int bar){
        return (bar + 2);
    }
    // Variablendeklaration
    int foobar = 1; // globale Variable

    int main (void){
        // locale Variablendaklaration
        int barfoo = foo(foobar);  // barfoo == 3
        return 0; 
        /* 0 (kein Fehler) an aufreufendes 
         * Programm zurueck geben.
        */
    }

```

### 5. Was ist unter Parameterübergabe per Referenz zu verstehen? Wann wird sie verwendet?
Bei der Übergabe per Referenz wir die Adresse einer Variable übergeben und auf den physischen Speicher der Variable zu gegriffen.
Die Sprungweite ist immer die Größe des Datentypes auf den der Pointer zeigt (z.B. double: 8 Byte, char: 1 Byte, float: 4 Byte, int: Abhängig vom Prozessor)

```c
    // Funktionsdeklaration
    // Rueckgabedatentyp: int 
    // Parameterdatentyp: Pointer auf int
    int foo(int * bar){
        return *(bar + 2); 
        /* Rueckgabe des Wertes auf dem 
         * Speicher der Adresse von bar + 2    */
    }
    // Variablendeklaration
    int foobar = 1; // globale Variable (Bsp.-Adresse: 0x555555)

    int main (void){
        // locale Variablendaklaration
        int barfoo = foo(&foobar);  
        /* barfoo == ?
         * Bsp: 0x555555 + 2 == 0x555557
         * Durch den * wird der Wert von 
         * der Adresse 0x555557 zurueck gegeben  */
        return 0; 
        /* 0 (kein Fehler) an aufreufendes 
         * Programm zurueck geben.  */
    }
```

### 6. Worin besteht die Besonderheit von Feldern als Übergabeparametern?
Felder sind einfach gesagt Pointer auf mehere Variablen vom gleichen Typ. Felder lassen sich bei einer Übergabe per Referenz wie Pointer behandeln.

```c
    // Funktionsdeklaration
    // Rueckgabedatentyp: int 
    // Parameterdatentyp: Pointer auf int
    int foo(int * bar){
        return *(bar + 2); 
        /* Rueckgabe des Wertes auf dem 
         * Speicher der Adresse von bar + 2 
        */
    }
    // Variablendeklaration
    // globale Variable (Bsp.-Adresse: 0x555555)
    int foobar[5] = {7,1,2543,77,-2}; 

    int main (void){
        // locale Variablendaklaration
        int barfoo = foo(&foobar);  
        /* barfoo == 2543
         * Bsp: 0x555555 + 2 == 0x555557
         * Durch den * wird der Wert von der 
         * Adresse 0x555557 (3. Element) zurueck gegeben   */
        return 0; 
        /* 0 (kein Fehler) an aufreufendes 
         * Programm zurueck geben   */
    }
```

### 7. Was sind lokale Variablen und wodurch unterscheiden sie sich von globalen Variablen? 
Lokale Variablen sind nur innhalb der Instanz (Funktion, Library, etc.) verwendbar. Bei der Deklaration wird die eine lokale Variable im RAM und eine globale Variable auf der Festplatte (unter Windows, Linux läuft etwas anders, aber das ist hier erst mal egal) gespeichert.

Ein weiterer Unterschied ist der Wert bei der Deklaration. Lokale werden mit einen nicht definierten Wert und eine Globale wird mit 0 initialisiert.

```c
    // Variablendeklaration
    // globale Variable
    int foobar; // foobar == 0

    int main (void){
        // locale Variablendaklaration
        int barfoo; // barfoo == ? 
        return 0; 
        /* 0 (kein Fehler) an aufreufendes 
         * Programm zurueck geben   */
    } 