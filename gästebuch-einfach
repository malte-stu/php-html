# Praktikumsaufgabe: Persönliche Webseite mit Steckbrief und Gästebuch

## Überblick
In dieser Aufgabe erstellst du eine persönliche Webseite mit deinem Steckbrief und einem Gästebuch. Du wirst selbst HTML, CSS und einfaches PHP programmieren.

## Was du lernen wirst
- HTML zum Aufbau einer Webseite
- CSS zur Gestaltung
- Einfache PHP-Programmierung für ein Gästebuch

## Voraussetzungen
- XAMPP installiert (für den lokalen Webserver)
- Ein Texteditor (wie Notepad++ oder Visual Studio Code)
- Grundlegende HTML-Kenntnisse

## Zeitplan (1,5 Stunden)
- **45 Minuten**: HTML-Seite mit Steckbrief erstellen
- **45 Minuten**: Gästebuch mit PHP programmieren

## Schritt-für-Schritt-Anleitung

### Teil 1: HTML-Seite mit Steckbrief (45 Minuten)

#### 1. Vorbereitung
- Erstelle einen neuen Ordner namens `meine_webseite` im XAMPP `htdocs`-Verzeichnis
- Erstelle in diesem Ordner eine neue Datei namens `index.html`

#### 2. HTML-Grundgerüst
Hier ist ein Grundgerüst für deine HTML-Datei. Fülle die fehlenden Teile aus:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Meine Webseite</title>
    <meta charset="UTF-8">
    <style>
        /* Hier kommt dein CSS hin */
    </style>
</head>
<body>
    <!-- Hier kommt dein Inhalt hin -->
</body>
</html>
```

#### 3. Aufgaben für den Inhalt
Ergänze das HTML-Grundgerüst mit folgenden Elementen:

a) Erstelle eine Überschrift mit deinem Namen
b) Erstelle einen Steckbrief mit folgenden Informationen in einer Tabelle:
   - Name
   - Alter
   - Schule
   - Klasse
   - Lieblingsfächer
   - Hobbys
c) Schreibe einen kurzen Text über dich
d) Füge am Ende einen Abschnitt für das Gästebuch ein mit einem Link zur noch zu erstellenden `gaestebuch.php`

#### 4. CSS-Gestaltung
Füge im `<style>`-Bereich CSS-Code ein, um deine Seite zu gestalten:

a) Ändere die Schriftart für die gesamte Seite
b) Setze eine Hintergrundfarbe
c) Gestalte deine Überschrift mit einer anderen Farbe
d) Gestalte deine Tabelle mit Rahmen und Abständen

#### 5. Hilfestellung für HTML und CSS
Hier einige Beispiele, die du verwenden kannst:

HTML-Tabelle:
```html
<table>
    <tr>
        <td>Name:</td>
        <td>Dein Name</td>
    </tr>
    <!-- Weitere Zeilen für die anderen Informationen -->
</table>
```

CSS für die Gestaltung:
```css
body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
    margin: 0;
    padding: 20px;
}

h1 {
    color: #4287f5;
    text-align: center;
}

table {
    width: 80%;
    margin: 0 auto;
    border-collapse: collapse;
}

td {
    padding: 8px;
    border-bottom: 1px solid #ddd;
}
```

### Teil 2: Gästebuch mit PHP (45 Minuten)

#### 1. Vorbereitung
- Erstelle eine neue Datei namens `gaestebuch.php` im selben Ordner
- Erstelle eine leere Textdatei namens `nachrichten.txt` im selben Ordner

#### 2. PHP-Grundgerüst
Hier ist ein Grundgerüst für deine PHP-Datei:

```php
<?php
// Hier kommt dein PHP-Code hin
?>

<!DOCTYPE html>
<html>
<head>
    <title>Mein Gästebuch</title>
    <meta charset="UTF-8">
    <style>
        /* Hier kommt dein CSS hin (kann der gleiche sein wie in index.html) */
    </style>
</head>
<body>
    <h1>Mein Gästebuch</h1>
    
    <!-- Hier kommt dein Formular hin -->
    
    <!-- Hier kommen die Gästebucheinträge hin -->
    
    <a href="index.html">Zurück zum Steckbrief</a>
</body>
</html>
```

#### 3. Aufgaben für PHP
Ergänze das PHP-Grundgerüst mit folgenden Elementen:

a) Erstelle ein Formular mit:
   - Einem Feld für den Namen
   - Einem Textfeld für die Nachricht
   - Einem Button zum Absenden

b) Schreibe PHP-Code, der:
   - Prüft, ob das Formular abgesendet wurde
   - Die eingegebenen Daten aus dem Formular liest
   - Die Daten in die Datei `nachrichten.txt` schreibt

c) Schreibe PHP-Code, der:
   - Die Datei `nachrichten.txt` liest
   - Alle Einträge auf der Seite anzeigt

#### 4. Hilfestellung für PHP
Hier einige Codebeispiele, die du verwenden kannst:

HTML-Formular:
```html
<form method="post">
    <p>
        <label for="name">Dein Name:</label><br>
        <input type="text" id="name" name="name" required>
    </p>
    <p>
        <label for="nachricht">Deine Nachricht:</label><br>
        <textarea id="nachricht" name="nachricht" rows="4" required></textarea>
    </p>
    <p>
        <button type="submit">Eintrag speichern</button>
    </p>
</form>
```

PHP-Code zum Speichern der Nachrichten:
```php
<?php
// Name der Datei, in der die Nachrichten gespeichert werden
$datei = "nachrichten.txt";

// Prüfen, ob das Formular abgesendet wurde
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Daten aus dem Formular holen
    $name = $_POST["name"];
    $nachricht = $_POST["nachricht"];
    
    // Datum hinzufügen
    $datum = date("d.m.Y");
    
    // Neuen Eintrag erstellen
    $eintrag = "Name: " . $name . "\n";
    $eintrag .= "Nachricht: " . $nachricht . "\n";
    $eintrag .= "Datum: " . $datum . "\n\n";
    
    // Eintrag in die Datei schreiben
    file_put_contents($datei, $eintrag, FILE_APPEND);
}
?>
```

PHP-Code zum Anzeigen der Nachrichten:
```php
<?php
// Name der Datei mit den Nachrichten
$datei = "nachrichten.txt";

// Prüfen, ob die Datei existiert
if (file_exists($datei)) {
    // Inhalt der Datei lesen
    $inhalt = file_get_contents($datei);
    
    // Prüfen, ob es Einträge gibt
    if (!empty($inhalt)) {
        // Einträge trennen (leere Zeile als Trennzeichen)
        $eintraege = explode("\n\n", $inhalt);
        
        // Einträge in umgekehrter Reihenfolge anzeigen (neueste zuerst)
        $eintraege = array_reverse($eintraege);
        
        // Jeden Eintrag anzeigen
        foreach ($eintraege as $eintrag) {
            if (!empty($eintrag)) {
                echo '<div style="background-color: #f9f9f9; padding: 10px; margin-bottom: 10px;">';
                echo nl2br($eintrag); // Zeilenumbrüche in HTML umwandeln
                echo '</div>';
            }
        }
    } else {
        echo '<p>Noch keine Einträge vorhanden.</p>';
    }
} else {
    echo '<p>Noch keine Einträge vorhanden.</p>';
}
?>
```

## Zusatzaufgaben (falls du schneller fertig bist)

1. **Zeitanzeige verbessern**:
   - Füge die Uhrzeit zum Datum hinzu
   - Verwende dafür die PHP-Funktion `date("d.m.Y H:i")`

2. **Eingabevalidierung**:
   - Prüfe, ob der Name mindestens 3 Zeichen hat
   - Prüfe, ob die Nachricht mindestens 10 Zeichen hat

3. **Daten sichern**:
   - Füge Code hinzu, der verhindert, dass HTML-Tags in den Nachrichten ausgeführt werden (Sicherheit)
   - Verwende dafür die PHP-Funktion `htmlspecialchars()`

4. **Seite verschönern**:
   - Füge weitere CSS-Eigenschaften hinzu, um die Seite noch ansprechender zu gestalten
   - Experimentiere mit verschiedenen Farben, Schriftarten und Hintergründen

## Hilfestellungen

- Bei HTML-Fragen: [W3Schools HTML](https://www.w3schools.com/html/)
- Bei CSS-Fragen: [W3Schools CSS](https://www.w3schools.com/css/)
- Bei PHP-Fragen: [W3Schools PHP](https://www.w3schools.com/php/)

## Wichtige Hinweise

- Denke daran, deine Dateien regelmäßig zu speichern
- Achte darauf, dass XAMPP läuft und der Apache-Server gestartet ist
- Überprüfe deine Website im Browser unter `http://localhost/meine_webseite/`
- Wenn etwas nicht funktioniert, prüfe die Fehlermeldungen und deinen Code sorgfältig

## Fertige Grundgerüste zum Kopieren

### index.html - Grundgerüst
```html
<!DOCTYPE html>
<html>
<head>
    <title>Meine Webseite</title>
    <meta charset="UTF-8">
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f0f0f0;
        }
        h1 {
            color: #4287f5;
            text-align: center;
        }
        /* Hier mehr CSS einfügen */
    </style>
</head>
<body>
    <h1>Mein Steckbrief</h1>
    
    <!-- Hier deine Tabelle mit persönlichen Informationen einfügen -->
    
    <h2>Über mich</h2>
    <!-- Hier deinen Text über dich einfügen -->
    
    <h2>Gästebuch</h2>
    <p>Hinterlasse einen Eintrag in meinem <a href="gaestebuch.php">Gästebuch</a>!</p>
</body>
</html>
```

### gaestebuch.php - Grundgerüst
```php
<?php
// Name der Datei, in der die Nachrichten gespeichert werden
$datei = "nachrichten.txt";

// Hier Code zum Speichern der Nachrichten einfügen
// (Wenn das Formular abgeschickt wurde)

?>

<!DOCTYPE html>
<html>
<head>
    <title>Mein Gästebuch</title>
    <meta charset="UTF-8">
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f0f0f0;
        }
        h1 {
            color: #4287f5;
            text-align: center;
        }
        /* Hier mehr CSS einfügen */
    </style>
</head>
<body>
    <h1>Mein Gästebuch</h1>
    
    <!-- Hier dein Formular einfügen -->
    
    <h2>Bisherige Einträge</h2>
    
    <?php
    // Hier Code zum Anzeigen der Nachrichten einfügen
    ?>
    
    <p><a href="index.html">Zurück zum Steckbrief</a></p>
</body>
</html>
```
