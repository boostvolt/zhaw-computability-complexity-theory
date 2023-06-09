## Aufgabe 1. LOOP-Programme
Erstellen Sie LOOP-Programme (ohne die Verwendung von Makros), welche folgende Funktionen berechnen:

a) f(x,y)=max(y,y)

```
x0 = x2 + 0
```

b) g(x,y,z)=10z+|x−3y|

```
Loop 10 Do
  Loop x3 Do
    x0 = x0 + 1
  End
End;

Loop x2 Do
  x4 = x4 + 3
End;
x5 = x1 + 0;
Loop x4 Do
  x5 = x5 - 1
End;
Loop x1 Do
  x4 = x4 -1
End;
Loop x4 Do
  x5 = x5 + 1
End;
x6 = x5 + 0;

Loop x6 Do
  x0 = x0 + 1
End
```

c) h(x,y)=xy

```
x0 = x0 + 1;
Loop x2 Do
  x4 = x0 + 0;
  x0 = x5 + 0;
  Loop x1 Do
    Loop x4 Do
      x0 = x0 + 1
    End
  End
End
```

## Aufgabe 2. While-Programme
Geben Sie While-Programme (ohne Loop) an, die folgende Funktionen abbilden (ohne Verwen- dung von Makros)

a) h(x) = Pi xi, x = [x,y,z]

```
x0 = x1 + 0;
While x2 > 0 Do
  x0 = x0 + 1;
  x2 = x2 - 1
End;
While x3 > 0 Do
  x0 = x0 + 1;
  x3 = x3 - 1
End
```

b) g(n) =↑ (ein While-Programm, welches nie terminiert: Interrupt due to timeout)

```
x1 = x1 + 1;
While x1 > 0 Do
  x1 = x1 + 1
End
```

c) f(x)= (f(x−1)+x falls x > 1 / 1 sonst

```
x0 = x0 + 1;
x2 = x1 - 1;
While x2 > 0 Do
  x3 = x1 + 0;
  While x3 > 0 Do
    x0 = x0 + 1;
    x3 = x3 - 1
  End;
  x1 = x1 - 1;
  x2 = x2 - 1
End
```

## Aufgabe 3. Entscheidbarkeit. 
Beantworten Sie folgende Aufgaben:

a) ZeigenSiefürbeliebigeSprachenA,B:A≼B⇒A≼B

Angenommen, A ⪯ B gilt, d.h. es gibt eine berechenbare Funktion, die A auf B abbildet. Um zu zeigen, dass ¬A ⪯ ¬B gilt, können wir eine einfache Konstruktion verwenden: 

- Sei f eine berechenbare Funktion, die A auf B abbildet (basierend auf der Annahme A ⪯ B).
- Nun können wir eine Funktion g definieren, die das Komplement der Ausgaben von f nimmt. Das bedeutet, wenn f(x) = y, dann ist g(x) = ¬y.
- Es ist offensichtlich, dass g eine berechenbare Funktion ist, da sie einfach die Ausgabe von f negiert.
- Darüber hinaus bildet g ¬A auf ¬B ab, da wenn x in A liegt, dann liegt f(x) in B (basierend auf A ⪯ B), und folglich ist ¬f(x) = ¬(f(x)) = g(x) in ¬B.
- Daher haben wir gezeigt, dass ¬A ⪯ ¬B gilt, basierend auf der Annahme A ⪯ B.
- Es ist wichtig, die Voraussetzung A ⪯ B in der Argumentation zu berücksichtigen.

b) Es sei nun A eine Sprache mit H ≼ A, wobei H das Halteproblem ist.
Verwenden Sie die in (a) gezeigte Tatsache zum Beweisen, dass A nicht semi-entscheidbar ist.

Angenommen, A wäre semi-entscheidbar. Da H ⪯ A gilt, können wir eine berechenbare Funktion f konstruieren, die das Halteproblem H auf A abbildet. Das bedeutet, für jede Eingabe x erzeugt f(x) eine Turing-Maschine, die M simuliert und genau dann akzeptiert, wenn die ursprüngliche Turing-Maschine auf der Eingabe x hält.

Wenn A semi-entscheidbar ist, können wir eine Turing-Maschine N konstruieren, die das Halteproblem H entscheidet, indem wir f verwenden, um eine Turing-Maschine zu erzeugen, die A simuliert.

Dies steht jedoch im Widerspruch zur Unentscheidbarkeit von H.

Daher kann A nicht semi-entscheidbar sein, wenn H ⪯ A gilt.

## Aufgabe 4. Collatz-Zahlen
P(x) ist ein Programm mit folgender Spezifikation:
Bei Eingabe x wird die kleinste natürliche Zahl zurückgegeben, deren Collatz Folge unter den Collatz Folgen aller Zahlen zwischen 1 und x die maximale Länge hat.

a) Schreiben Sie zwei Varianten des Programms P, eines ohne und eines mit Optimie- rungen (bei ”ohne Optimierung” gehen Sie Zahl für Zahl durch und notieren sich jeweils die Länge der Folge). Erläutern Sie kurz Ihre Optimierungsansätze.

Hier ist eine Implementierung von P ohne Optimierung:
```java
public static int P(int x) {
    int maxLength = 0;
    int maxNumber = 0;
    for (int i = 1; i <= x; i++) {
        int length = collatz(i, limit);
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
import java.util.Arrays;

import static java.lang.System.currentTimeMillis;

class P {
  public static void main(String[] args) {
    solve(1_000);
    solve(10_000);
    solve(100_000);
    solve(1_000_000);
    solve(5_000_000);
    solve(10_000_000);
    solve(90_000_000);
  }

  private static void solve(int x) {
    long before = currentTimeMillis();
    System.out.println(x + ": Result: " + calc(x));
    long after = currentTimeMillis();
    System.out.println(x + " took " + (after - before) + " ms");
  }

  public static int calc(int x) {
    int maxLength = 0;
    int maxNumber = 0;
    long[] memo = new long[x + 1];
    Arrays.fill(memo, -1);
    memo[1] = 1;
    for (int i = 1; i <= x; i++) {
      long length = collatz(i, memo);
      memo[i] = length;
      if (length > maxLength) {
        maxLength = (int) length;
        maxNumber = i;
      }
    }
    return maxNumber;
  }

  public static long collatz(long n, long[] memo) {
    if (n <= memo.length - 1 && memo[(int) n] != -1) {
      return memo[(int) n];
    }
    long length;
    if (n % 2 == 0) {
      length = collatz(n / 2, memo) + 1;
    } else {
      length = collatz(3 * n + 1, memo) + 1;
    }
    if (n <= memo.length - 1) {
      memo[(int) n] = length;
    }
    return length;
  }

}
```

Diese Implementierung verwendet Memorization, um die Länge der Collatz-Folge für jede Zahl zwischen 1 und x zu speichern und erneute Berechnungen zu vermeiden. Die Funktion P gibt die Zahl mit der längsten Collatz-Folge zurück.

b) Berechnen Sie x = 1’000, 10’000, 100’000, 1’000’000, 5’000’000 und 10’000’000 mit beiden Programm-Varianten und zusätzlich 90’000’000 mit der optimierten Variante.
Was ist der Rückgabewert für jedes x?
Stellen Sie die Unterschiede der Laufzeiten Ihrer beiden Programme grafisch dar. (Die
grafische Darstellung muss nicht im Code gemacht werden. Ihr könnt z.B. Excel nutzen.)

Hier sind die Rückgabewerte für die verschiedenen Werte von x:

| x           | Ohne Optimierung  | Mit Optimierung   |
|-------------|-------------------|-------------------|
| 1'000       |	871               |	871               |
| 10'000      |	6'171             |	6'171             |
| 100'000     |	77'031            |	77'031            |
| 1'000'000   |	837'799           | 837'799           |
| 5'000'000   |	3'732'423         | 3'732'423         |
| 10'000'000  |	8'400'511         |	8'400'511         |
| 90'000'000  |	-	                | 63'728'127        |

![Laufzeiten](https://github.com/boostvolt/zhaw-computability-complexity-theory/assets/51777660/8a3c5cf8-9dc2-4817-9bd0-f691bbf6e8f0)

Die Funktion ohne Optimierung benötigt für x = 90'000'000 zu viel Zeit und Speicherplatz und wurde deshalb nicht ausgeführt. Die optimierte Funktion liefert für x = 90'000'000 den Wert 84'376'143.

c) Ist die Menge aller Collatz-Zahlen bis x = 90’000’000 semi-entscheidbar oder sogar entscheidbar? Begründen Sie Ihre Antwort.

Die Menge aller Collatz-Zahlen bis x = 90'000'000 ist semi-entscheidbar. Dies bedeutet, dass es ein Programm gibt, das alle Collatz-Zahlen bis x ausgibt, wenn es eine Collatz-Zahl gibt, die kleiner oder gleich x ist. Das Programm kann einfach alle Zahlen von 1 bis x durchgehen und die Collatz-Folge für jede Zahl berechnen.

d) Ist die Menge aller Collatz-Zahlen P(∞) semi-entscheidbar oder sogar entscheidbar?

Die Menge aller Collatz-Zahlen P(∞) ist nicht entscheidbar. Dies bedeutet, dass es kein Programm gibt, das alle Collatz-Zahlen berechnen kann. Der Beweis dafür ist ein ungelöstes Problem in der Mathematik, das als Collatz-Vermutung bekannt ist.

e) Beweisen oder widerlegen Sie informell folgende Aussage: ”Die Zeitkomplexität des
Collatz-Programmes ist nicht bestimmbar”.

Die Zeitkomplexität des Collatz-Programms ist nicht beweisbar. Dies bedeutet, dass es keine Möglichkeit gibt, die Laufzeit des Programms für alle Eingaben zu bestimmen. Die Collatz-Vermutung besagt, dass jede Collatz-Folge irgendwann bei 1 endet, aber es ist nicht bekannt, wie lange es dauert, bis dies geschieht. Da die Länge der Collatz-Folge für jede Zahl zwischen 1 und x berechnet werden muss, ist die Laufzeit des Programms für große Werte von x sehr hoch.

![Code](https://github.com/boostvolt/zhaw-computability-complexity-theory/assets/51777660/36aba075-85fa-40f3-8a51-f5cff86849be)

## Aufgabe 5. NP-vollständig
Ein cleverer Student der ZHAW findet in der Zukunft für ein bekanntes NP-vollständiges Problem P1 einen Lösungsalgorithmus, der nur polynomielle Zeit benötigt. Was würde das bedeuten?

NP-vollständige Probleme sind eine Untermenge von NP.

Wenn nun aber mit dem Lösungsverfahren vom Student der ZHAW ein NP-vollständiges Problem in polynomieller Zeit gelöst werden kann, würde dies bedeuten, dass jede Aufgabe in NP in polynomieller Zeit gelöst werden kann.

Das heißt, dass alle Probleme in NP effizient lösbar wären.

In diesem Fall wäre NP = P.

## Aufgabe 6. Polynomzeit-Verifizierer
Gegeben: Natürliche Zahlen a1, ..., an und b.

Ausgabe: Die Ausgabe ist JA, falls es eine Teilmenge S ⊆ { a1, ..., an } gibt, sodass Pa∈S = b gilt, und sonst NEIN.
Beschreiben Sie informell einen Polynomzeit-Verifizierer mit einem Zeugen für dieses Problem.

In diesem Fall wäre der Zeuge eine konkrete Menge von Zahlen und eine Zahl b.

Der Verifizierer muss nun nur noch die Menge der Zahlen addieren und überprüfen, ob die Summe mit der Zahl b übereinstimmt.
