---
footer-left: 'Schuljahr 2020/21'
header-left: 'HTL Villach'
header-right: 'POS2'
---
# Textverschlüsselung

## Grundfunktionalität

Entwickle ein objektorientiertes Programm, welches zeilenweise Text "verschlüsselt" kann.
Der verschlüsselte Text soll zeilenweise in eine Textdatei geschrieben werden.

Halte dich bei der Implementierung an folgendes Klassendiagramm:

```{ .plantuml width=100% }
class TextEncrypter {
 + TextEncrypter(String outputFile, CipherAlgorithm alg);
 + void encryptLine(String line, boolean isLastLine);
}

abstract class CipherAlgorithm {
   {abstract} + String encrypt(String plainText);
}

class PlainCipher {
}

class CaesarCipher {
+ CaesarCipher(int key);
}

TextEncrypter -right-> "1" CipherAlgorithm

CipherAlgorithm <|-down- PlainCipher
CipherAlgorithm <|-down- CaesarCipher

```

Die Klasse `TextEncrypter` soll im Konstruktor den Namen der Ausgabedatei erhalten
und eine Referenz auf eine Implementierung des Verschlüsselungsalgorithmus 
(`CipherAlgorithm`). Im Anschluss daran kann die Methode `encryptLine` beliebig oft aufgerufen werden,
die jeweils eine zu verschlüsselnde Textzeile erhält und eine Information darüber, ob es
sich um die letzte zu verschlüsselnde Zeile handelt. In der Ausgabedatei soll eine
fortlaufende Nummer der Zeile und der verschlüsselte Text enthalten sein.

Es sollen zwei "Verschlüsselungsalgorithmen" implementiert werden:

* Der Algorithmus `PlainCipher` dient nur zu Testzwecken und gibt die Zeichenkette
unverschlüsselt wieder zurück.
* Der Algorithmus `CaesarCipher` soll die bereits bekannte Cäsar-Chiffre auf die Zeile anwenden.
  Dabei sollen alle Buchstaben (a-z, A-Z) abhängig vom Schlüsselwert _key_ 
  verschoben werden. D.h. bei einem Schlüsselwert von 2 wird aus einem A ein C, einem y ein a, etc.
  Der Schlüsselwert soll im Bereich von 1 bis 25 liegen und wird beim Konstruktor mitübergeben.
  
Beispiel - Anwendung

```java
CipherAlgorithm alg = new CaesarCipher(2);
TextEncrypter enc = new TextEncrypter("encrypted.txt", alg);

enc.encryptLine("PLF", false);
enc.encryptLine("Programmieren", true);
```

Resultat - `encrypted.txt`:

```text
1: RNH
2: Rtqitcookgtgp
```

## Einlesen aus einer Textdatei

Erweitere die Klasse `TextEncrypter` um eine Methode `encryptFile(String inputFile, boolean isLastFile)`.
Die Methode soll die angegebene Textdatei öffnen und deren Inhalt zeilenweise
verschlüsselt in die Ausgabedatei schreiben. Es soll möglich sein, die Methode hintereinander
mit mehreren Eingabedateien aufzurufen. Bei der Verarbeitung der letzten Datei muss der Parameter
`isLastFile` entsprechend auf `true` gesetzt werden.

## Statistiken

Erweitere die Klasse `CipherAlgorithm` um zwei Methoden `int totalCharacters()` bzw. `int totalLines()`.
Die Methoden sollen jeweils die Anzahl der vom Algorithmus verarbeiteten Zeichen bzw. Zeilen zurückliefern.
