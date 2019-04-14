_Übungsaufgabe zur Veranstaltung [objektrorientiertes Programmieren](https://hsro-wif-oop.github.io) im [Bachelorstudiengang Wirtschaftsinformatik](https://www.th-rosenheim.de/technik/informatik-mathematik/wirtschaftsinformatik-bachelor/) an der [Hochschule Rosenheim](http://www.th-rosenheim.de)._


# Iteratoren

In dieser Übung implementieren wir Iteratoren für die Datenstrukturen _Stack_ und _Set_ aus den letzten beiden Übungen.



## Aufgabe 1: Iterator für Set

Gegeben ist eine generische Implementierung für das Set, in Anlehnung an die Musterlösung der [Übung 3](https://github.com/hsro-wif-oop/oop-uebung03).

- Implementieren Sie die durch das Interface `Iterable` vorgeschriebene Methode `iterator`.
- Implementieren Sie dazu einen Iterator, welcher alle Elemente besucht.
- Stellen Sie sicher, dass der Testcase `TestSet.testStringSet` korrekt durchläuft.

### Hinweise

- Die Verwendung einer Agenda ist zwingend notwendig!
- Was ändert sich an der Besuchsreihenfolge, wenn Sie für die Agenda statt einer Liste einen Stack verwenden?


## Aufgabe 2: Reverse-Iterator für `Stack<T>`

Gegeben ist eine generische Implementierung eines Stapels (_stack_), in Anlehnung an die Musterlösung der [Übung 3](https://github.com/hsro-wif-oop/oop-uebung03).
Ein Stack ist eine Datenstruktur, dessen Reihenfolge bei der Entnahme (`pop`) umgekehrt zur Reihenfolge des hinzufügens (`push`) ist.
Das heisst, das zuletzt mit `push` hinzugefügte Element das wird als nächstes mit `pop` entnommen (_last in, first out_).

- Implementieren Sie (nur) die durch das Interface `Iterable` vorgeschriebene Methode `iterator`.
- Implementieren Sie dazu einen _Reverse-Iterator_, der die Elemente in umgekehrter Reihenfolge besucht.
	Für einen Stack bedeutet das: in der Reihenfolge, in der die Elemente hinzugefügt wurden, also _first in, first out_.
- Stellen Sie sicher, dass der Testcase `StackTest.testStack` korrekt durchläuft.

Ein Beispiel: Werden in einen `Stack<Integer>` die Werte 1, 4, 5, 2 gepusht, so ist die Reihenfolge bei `pop` 2, 5, 4, 1.

```java
Stack<Integer> stack = new StackImpl<>();

stack.push(1);
stack.push(4);
stack.push(5);
stack.push(2);

stack.pop();  // 2
stack.pop();  // 5
stack.pop();  // 4
stack.pop();  // 1
```

Iteriert man hingegen darüber, so soll die Einfügereihenfolge eingehalten werden:

```java
Stack<Integer> stack = new StackImpl<>();

stack.push(1);
stack.push(4);
stack.push(5);
stack.push(2);

for (int i : stack)
	System.out.println(i);

// 1
// 4
// 5
// 2
```


### Hinweise

- Auch die Iteration einer sequenziellen Datenstruktur kann mit einer Agenda realisiert werden; wie verhält sich diese über die Lebensdauer (der Iteration)?
- Welche Datenstruktur eignet sich, um die Reihenfolge zu invertieren?


## Bonusaufgabe: Blattiterator

- Implementieren Sie die Methode `SetImpl<T>.leafIterator`.
- Implementieren Sie diesen Iterator so, dass nur **Blätter** zurückgegeben werden, also Elemente **ohne Nachfolger**.
- Stellen Sie sicher, dass der Testcase `SetTest.testLeafIterator` korrekt durchläuft.

### Hinweise

Diese Aufgabe ist aussergewöhnlich trickreich!
Die Hauptschwierigkeit besteht darin, dass auch die `hasNext` Methode verlässlich funktioniert.
Eine Herangehensweise ist, neben der Agenda für die Traversierung der Baumstruktur auch eine Referenz auf das nächste Blatt zu unterhalten.
Wird nun das nächste Element angefordert, so kann man dieses schnell zurückgeben, muss aber anschließend gleich versuchen, das nächste zu finden.
