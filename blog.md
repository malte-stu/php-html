# Praktikumsaufgabe: Persönliche Miniblog-Seite mit HTML und PHP

## Überblick
In dieser Aufgabe erstellst du eine einfache persönliche Webseite mit einem Kommentarbereich. Besucher können einen Namen eingeben und einen Kommentar hinterlassen. Diese Kommentare werden gespeichert und auf der Seite angezeigt.

## Was du lernen wirst
- Grundlegendes HTML zum Erstellen einer Webseite
- Einfaches CSS zur Gestaltung
- Einfache PHP-Programmierung zum Speichern und Anzeigen von Daten
- Zusammenspiel von HTML und PHP

## Voraussetzungen
- XAMPP installiert (für den lokalen Webserver mit PHP)
- Ein Texteditor (wie Notepad++ oder Visual Studio Code)
- Grundlegende HTML-Kenntnisse
- Zugriff auf W3Schools als Nachschlagewerk

## Zeitplan (1,5 Stunden)
- **30 Minuten**: HTML-Grundgerüst und Styling erstellen
- **30 Minuten**: Kommentarformular hinzufügen
- **30 Minuten**: PHP-Code für Kommentarspeicherung und -anzeige schreiben

## Schritt-für-Schritt-Anleitung

### Teil 1: HTML-Grundgerüst (30 Minuten)

1. Erstelle einen neuen Ordner namens `miniblog` im XAMPP `htdocs`-Verzeichnis
2. Erstelle eine neue Datei namens `index.html` in diesem Ordner
3. Kopiere das folgende HTML-Grundgerüst in die Datei:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Mein Miniblog</title>
    <meta charset="UTF-8">
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        header {
            background-color: #4CAF50;
            color: white;
            padding: 10px;
            text-align: center;
            border-radius: 5px;
        }
        .content {
            background-color: white;
            padding: 20px;
            margin-top: 20px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        footer {
            text-align: center;
            margin-top: 20px;
            font-size: 0.8em;
            color: #666;
        }
    </style>
</head>
<body>
    <header>
        <h1>Mein persönlicher Miniblog</h1>
    </header>
    
    <div class="content">
        <h2>Über mich</h2>
        <p>Hallo! Mein Name ist [Dein Name]. Ich bin Schüler/in der 9. Klasse am [Name deines Gymnasiums].</p>
        <p>Das sind meine Hobbys:</p>
        <ul>
            <li>Hobby 1</li>
            <li>Hobby 2</li>
            <li>Hobby 3</li>
        </ul>
        
        <!-- Hier wird später das Kommentarformular eingefügt -->
    </div>
    
    <footer>
        &copy; 2025 Mein Miniblog - Erstellt während meines Praktikums
    </footer>
</body>
</html>
```

4. Passe den Text an, indem du deinen Namen, deine Schule und deine Hobbys einträgst
5. Speichere die Datei
6. Starte XAMPP und aktiviere den Apache-Server
7. Öffne einen Browser und gehe zu `http://localhost/miniblog/` um zu sehen, wie deine Seite aussieht

### Teil 2: Kommentarformular (30 Minuten)

1. Wandle deine HTML-Datei in eine PHP-Datei um, indem du sie als `index.php` speicherst (du kannst die alte `index.html` löschen)
2. Füge das folgende Formular in die `index.php` ein, wo der Kommentar `<!-- Hier wird später das Kommentarformular eingefügt -->` steht:

```html
<h2>Kommentare</h2>
<form action="index.php" method="post">
    <div>
        <label for="name">Dein Name:</label><br>
        <input type="text" id="name" name="name" required>
    </div>
    <div style="margin-top: 10px;">
        <label for="comment">Dein Kommentar:</label><br>
        <textarea id="comment" name="comment" rows="4" cols="50" required></textarea>
    </div>
    <div style="margin-top: 10px;">
        <button type="submit">Kommentar abschicken</button>
    </div>
</form>

<div class="comments">
    <h3>Bisherige Kommentare:</h3>
    <!-- Hier werden später die Kommentare angezeigt -->
</div>
```

3. Speichere die Datei

### Teil 3: PHP-Kommentarverarbeitung (30 Minuten)

1. Erstelle eine neue Datei namens `comments.txt` im selben Ordner. Diese Datei wird die Kommentare speichern.
2. Füge am Anfang deiner `index.php` (direkt nach `<?php`) den folgenden PHP-Code ein:

```php
<?php
// Kommentare speichern, wenn das Formular abgeschickt wurde
if ($_SERVER["REQUEST_METHOD"] == "POST" && isset($_POST['name']) && isset($_POST['comment'])) {
    $name = htmlspecialchars($_POST['name']);
    $comment = htmlspecialchars($_POST['comment']);
    $date = date("d.m.Y H:i");
    
    // Format: [Datum] Name: Kommentar
    $newComment = "[$date] $name: $comment\n";
    
    // Kommentar in die Datei schreiben
    file_put_contents("comments.txt", $newComment, FILE_APPEND);
}
?>
```

3. Jetzt füge den Code ein, der die Kommentare anzeigt. Ersetze den Kommentar `<!-- Hier werden später die Kommentare angezeigt -->` durch:

```php
<?php
// Kommentare aus der Datei lesen und anzeigen
if (file_exists("comments.txt")) {
    $comments = file("comments.txt");
    
    // Kommentare vom neuesten zum ältesten sortieren
    $comments = array_reverse($comments);
    
    foreach ($comments as $comment) {
        echo "<div style='margin-bottom: 10px; padding: 10px; background-color: #f1f1f1; border-radius: 5px;'>";
        echo $comment;
        echo "</div>";
    }
} else {
    echo "<p>Noch keine Kommentare vorhanden.</p>";
}
?>
```

4. Stelle sicher, dass die erste Zeile deiner Datei `<?php` ist und dass du vor dem HTML-Code einen schließenden PHP-Tag (`?>`) hast
5. Speichere die Datei
6. Aktualisiere die Seite in deinem Browser und teste das Kommentarformular

## Wichtige Hinweise

- Achte darauf, dass XAMPP läuft, wenn du die Seite testen möchtest
- Die Kommentare werden in einer einfachen Textdatei gespeichert
- Stell sicher, dass die Datei `comments.txt` für den Webserver beschreibbar ist
- Bei Problemen kannst du auf W3Schools nachschlagen:
  - [HTML-Formulare](https://www.w3schools.com/html/html_forms.asp)
  - [PHP-Einführung](https://www.w3schools.com/php/default.asp)
  - [PHP-Dateizugriff](https://www.w3schools.com/php/php_file.asp)

## Erweiterungsmöglichkeiten (falls du früher fertig bist)

- Füge eine Möglichkeit hinzu, den Hintergrund der Seite zu ändern
- Erstelle eine separate Seite für deine Hobbys mit Links zwischen den Seiten
- Füge ein Datum/Uhrzeit-Feld zu den Kommentaren hinzu (Tipp: PHP-Funktion `date()`)
- Gestalte die Kommentare optisch ansprechender mit CSS

## Vollständiger Code für index.php

Hier ist der vollständige Code für deine `index.php`, den du als Referenz verwenden kannst:

```php
<?php
// Kommentare speichern, wenn das Formular abgeschickt wurde
if ($_SERVER["REQUEST_METHOD"] == "POST" && isset($_POST['name']) && isset($_POST['comment'])) {
    $name = htmlspecialchars($_POST['name']);
    $comment = htmlspecialchars($_POST['comment']);
    $date = date("d.m.Y H:i");
    
    // Format: [Datum] Name: Kommentar
    $newComment = "[$date] $name: $comment\n";
    
    // Kommentar in die Datei schreiben
    file_put_contents("comments.txt", $newComment, FILE_APPEND);
}
?>
<!DOCTYPE html>
<html>
<head>
    <title>Mein Miniblog</title>
    <meta charset="UTF-8">
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        header {
            background-color: #4CAF50;
            color: white;
            padding: 10px;
            text-align: center;
            border-radius: 5px;
        }
        .content {
            background-color: white;
            padding: 20px;
            margin-top: 20px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        footer {
            text-align: center;
            margin-top: 20px;
            font-size: 0.8em;
            color: #666;
        }
        textarea, input[type="text"] {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <header>
        <h1>Mein persönlicher Miniblog</h1>
    </header>
    
    <div class="content">
        <h2>Über mich</h2>
        <p>Hallo! Mein Name ist [Dein Name]. Ich bin Schüler/in der 9. Klasse am [Name deines Gymnasiums].</p>
        <p>Das sind meine Hobbys:</p>
        <ul>
            <li>Hobby 1</li>
            <li>Hobby 2</li>
            <li>Hobby 3</li>
        </ul>
        
        <h2>Kommentare</h2>
        <form action="index.php" method="post">
            <div>
                <label for="name">Dein Name:</label><br>
                <input type="text" id="name" name="name" required>
            </div>
            <div style="margin-top: 10px;">
                <label for="comment">Dein Kommentar:</label><br>
                <textarea id="comment" name="comment" rows="4" cols="50" required></textarea>
            </div>
            <div style="margin-top: 10px;">
                <button type="submit">Kommentar abschicken</button>
            </div>
        </form>

        <div class="comments">
            <h3>Bisherige Kommentare:</h3>
            <?php
            // Kommentare aus der Datei lesen und anzeigen
            if (file_exists("comments.txt")) {
                $comments = file("comments.txt");
                
                // Kommentare vom neuesten zum ältesten sortieren
                $comments = array_reverse($comments);
                
                foreach ($comments as $comment) {
                    echo "<div style='margin-bottom: 10px; padding: 10px; background-color: #f1f1f1; border-radius: 5px;'>";
                    echo $comment;
                    echo "</div>";
                }
            } else {
                echo "<p>Noch keine Kommentare vorhanden.</p>";
            }
            ?>
        </div>
    </div>
    
    <footer>
        &copy; 2025 Mein Miniblog - Erstellt während meines Praktikums
    </footer>
</body>
</html>
```
