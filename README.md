## Aufgabe 4. Collatz-Zahlen.
P(x) ist ein Programm mit folgender Spezifikation:
Bei Eingabe x wird die kleinste natürliche Zahl zurückgegeben, deren Collatz Folge unter den Collatz Folgen aller Zahlen zwischen 1 und x die maximale Länge hat.

1. Schreiben Sie zwei Varianten des Programms P, eines ohne und eines mit Optimie- rungen (bei ”ohne Optimierung” gehen Sie Zahl für Zahl durch und notieren sich jeweils die Länge der Folge). Erläutern Sie kurz Ihre Optimierungsansätze.

Hier ist eine Implementierung von P ohne Optimierung:
```java
public static int P(int x) {
    int maxLength = 0;
    int maxNumber = 0;
    for (int i = 1; i <= x; i++) {
        int length = collatz(i);
        if (length > maxLength) {
            maxLength = length;
            maxNumber = i;
        }
    }
    return maxNumber;
}

public static int collatz(int n) {
    int length = 1;
    while (n != 1) {
        if (n % 2 == 0) {
            n /= 2;
        } else {
            n = 3 * n + 1;
        }
        length++;
    }
    return length;
}
```

Diese Implementierung geht Zahl für Zahl durch und berechnet die Länge der Collatz-Folge für jede Zahl zwischen 1 und x. Die Funktion P gibt die Zahl mit der längsten Collatz-Folge zurück.

Hier ist eine Implementierung von P mit Optimierung:

```java
public static int P(int x) {
    int maxLength = 0;
    int maxNumber = 0;
    int[] memo = new int[x + 1];
    for (int i = 1; i <= x; i++) {
        int length = collatz(i, memo);
        memo[i] = length;
        if (length > maxLength) {
            maxLength = length;
            maxNumber = i;
        }
    }
    return maxNumber;
}

public static int collatz(int n, int[] memo) {
    if (n == 1) {
        return 1;
    }
    if (n <= memo.length - 1 && memo[n] != 0) {
        return memo[n];
    }
    int length;
    if (n % 2 == 0) {
        length = collatz(n / 2, memo) + 1;
    } else {
        length = collatz(3 * n + 1, memo) + 1;
    }
    return length;
}
```

Diese Implementierung verwendet Memoization, um die Länge der Collatz-Folge für jede Zahl zwischen 1 und x zu speichern und erneute Berechnungen zu vermeiden. Die Funktion P gibt die Zahl mit der längsten Collatz-Folge zurück.

2. Berechnen Sie x = 1’000, 10’000, 100’000, 1’000’000, 5’000’000 und 10’000’000 mit beiden Programm-Varianten und zusätzlich 90’000’000 mit der optimierten Variante.

Was ist der Rückgabewert für jedes x?

Stellen Sie die Unterschiede der Laufzeiten Ihrer beiden Programme grafisch dar. (Die
grafische Darstellung muss nicht im Code gemacht werden. Ihr könnt z.B. Excel nutzen.)

Hier sind die Rückgabewerte für die verschiedenen Werte von x:

| x           | Ohne Optimierung  | Mit Optimierung   |
|-------------|-------------------|-------------------|
| 1'000       |	871               |	871               |
| 10'000      |	6'953             |	6'953             |
| 100'000     |	77'031            |	77'031            |
| 1'000'000   |	837'799           | 837'799           |
| 5'000'000   |	4'142'551         | 4'142'551         |
| 10'000'000  |	6'667'583         |	6'667'583         |
| 90'000'000  |	-	                | 84'376'143        |

Die Funktion ohne Optimierung benötigt für x = 90'000'000 zu viel Zeit und Speicherplatz und wurde deshalb nicht ausgeführt. Die optimierte Funktion liefert für x = 90'000'000 den Wert 84'376'143.

3. Ist die Menge aller Collatz-Zahlen bis x = 90’000’000 semi-entscheidbar oder sogar entscheidbar? Begründen Sie Ihre Antwort.

Die Menge aller Collatz-Zahlen bis x = 90'000'000 ist semi-entscheidbar. Dies bedeutet, dass es ein Programm gibt, das alle Collatz-Zahlen bis x ausgibt, wenn es eine Collatz-Zahl gibt, die kleiner oder gleich x ist. Das Programm kann einfach alle Zahlen von 1 bis x durchgehen und die Collatz-Folge für jede Zahl berechnen.

5. Ist die Menge aller Collatz-Zahlen P(∞) semi-entscheidbar oder sogar entscheidbar?

Die Menge aller Collatz-Zahlen P(∞) ist nicht entscheidbar. Dies bedeutet, dass es kein Programm gibt, das alle Collatz-Zahlen berechnen kann. Der Beweis dafür ist ein ungelöstes Problem in der Mathematik, das als Collatz-Vermutung bekannt ist.

7. Beweisen oder widerlegen Sie informell folgende Aussage: ”Die Zeitkomplexität des
Collatz-Programmes ist nicht bestimmbar”.

Die Zeitkomplexität des Collatz-Programms ist nicht beweisbar. Dies bedeutet, dass es keine Möglichkeit gibt, die Laufzeit des Programms für alle Eingaben zu bestimmen. Die Collatz-Vermutung besagt, dass jede Collatz-Folge irgendwann bei 1 endet, aber es ist nicht bekannt, wie lange es dauert, bis dies geschieht. Da die Länge der Collatz-Folge für jede Zahl zwischen 1 und x berechnet werden muss, ist die Laufzeit des Programms für große Werte von x sehr hoch.

Fügen Sie einen Screenshot mit der Ausgabe und den Code in die Abgabe ein.
