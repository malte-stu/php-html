# Praktikumsaufgabe: Interaktives Raumschiff-Spiel mit HTML und PHP

## Was wir heute programmieren

Wir werden ein spannendes Weltraum-Abenteuerspiel programmieren! In diesem Spiel steuerst du ein Raumschiff durch das Universum, besuchst verschiedene Planeten, sammelst wertvolle Kristalle und musst deinen Treibstoffvorrat im Auge behalten. Am Ende werden die besten Spieler in einer Highscore-Liste verewigt.

Das Spiel funktioniert so:
- Du gibst deinen Namen ein und startest als Pilot eines Raumschiffs
- Du kannst verschiedene Planeten besuchen
- Jeder Besuch verbraucht Treibstoff
- Auf jedem Planeten kannst du verschiedene Aktionen durchführen
- Du kannst Kristalle sammeln und nach Treibstoff suchen
- Wenn dein Treibstoff aufgebraucht ist, endet das Spiel
- Dein Highscore wird gespeichert, basierend auf der Anzahl der gesammelten Kristalle

## Was du lernen wirst

- **HTML**: Wie man die Oberfläche einer Webseite gestaltet
- **CSS**: Wie man die Webseite schön und ansprechend macht
- **PHP**: Wie man die Logik eines Spiels programmiert
- **Sessions**: Wie man Daten zwischen verschiedenen Seitenaufrufen speichert
- **Dateiverarbeitung**: Wie man Highscores in einer Datei speichert und wieder ausliest

## Was du brauchst

- **XAMPP**: Ein Programm, das einen lokalen Webserver auf deinem Computer erstellt
- **Texteditor**: Ein Programm zum Schreiben von Code (z.B. Notepad++ oder Visual Studio Code)
- **Grundlegende HTML-Kenntnisse**: Du solltest wissen, was Tags und Attribute sind
- **Interesse an Weltraum-Abenteuern!**

## Vorbereitung

1. Stelle sicher, dass XAMPP installiert ist.
2. Starte XAMPP und aktiviere den Apache-Server (klicke auf den "Start"-Button neben "Apache").
3. Erstelle einen neuen Ordner namens `raumschiff_spiel` im XAMPP `htdocs`-Verzeichnis:
   - Gehe zu dem Ort, wo XAMPP installiert ist (normalerweise `C:\xampp`)
   - Öffne den Ordner `htdocs`
   - Erstelle dort einen neuen Ordner namens `raumschiff_spiel`
4. Erstelle in diesem Ordner folgende Dateien:
   - `index.php` (Hauptspielseite)
   - `spielstand.txt` (leere Datei für die Highscores)
   - `planeten.php` (für die Logik der Planeten)
5. Öffne deinen Texteditor und lass uns loslegen!

## Schritt-für-Schritt-Anleitung

### Teil 1: Die Grundstruktur unseres Spiels erstellen (30 Minuten)

#### 1.1 Die Hauptdatei `index.php` erstellen

Öffne die Datei `index.php` in deinem Texteditor und füge den folgenden grundlegenden Code ein:

```php
<?php
// Dieser PHP-Code wird ausgeführt, bevor die HTML-Seite angezeigt wird
// Die Session ermöglicht es uns, Daten zwischen verschiedenen Seitenaufrufen zu speichern
session_start();

// Hier kommt später mehr PHP-Code hin
?>

<!DOCTYPE html>
<html>
<head>
    <title>Raumschiff Abenteuer</title>
    <meta charset="UTF-8">
    <style>
        /* Hier kommt das CSS hin, das bestimmt, wie unsere Seite aussieht */
        body {
            font-family: 'Arial', sans-serif;
            background-color: #0a0a2a; /* Dunkles Weltraum-Blau */
            background-image: url('https://www.transparenttextures.com/patterns/star-field.png');
            color: #fff;
            margin: 0;
            padding: 20px;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: rgba(20, 20, 50, 0.8);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0, 200, 255, 0.5);
        }
        
        h1 {
            text-align: center;
            color: #0cf;
            text-shadow: 0 0 5px #0cf;
        }
        
        h2 {
            color: #0cf;
            border-bottom: 1px solid #0cf;
            padding-bottom: 5px;
        }
        
        /* Füge hier später weitere CSS-Regeln hinzu */
    </style>
</head>
<body>
    <div class="container">
        <h1>Raumschiff Abenteuer</h1>
        
        <!-- Hier kommt später der Inhalt unseres Spiels hin -->
        
    </div>
</body>
</html>
```

> **Was passiert hier?**
> - Wir starten eine PHP-Session, um Spielinformationen zu speichern
> - Wir erstellen eine HTML-Struktur mit einem Titel und einem Container
> - Wir fügen etwas CSS hinzu, damit unser Spiel wie ein Weltraumabenteuer aussieht

#### 1.2 Spielvariablen initialisieren

Jetzt müssen wir die Grundvariablen für unser Spiel festlegen. Füge diesen Code unter `session_start();` ein:

```php
// Falls das Spiel neu gestartet wird
if (isset($_GET['neues_spiel'])) {
    // Alle Spielvariablen zurücksetzen
    $_SESSION = array();
    $_SESSION['ereignis'] = "Neues Spiel gestartet. Gib deinen Namen ein, um zu beginnen!";
}

// Wenn ein Spielername eingegeben wurde, starte das Spiel
if (isset($_POST['spieler_name']) && !empty($_POST['spieler_name'])) {
    // Speichere den Spielernamen und setze die Startwerte
    $_SESSION['spieler_name'] = htmlspecialchars($_POST['spieler_name']);
    $_SESSION['treibstoff'] = 100; // Wir starten mit 100 Einheiten Treibstoff
    $_SESSION['kristalle'] = 0;    // Noch keine Kristalle gesammelt
    $_SESSION['besuchte_planeten'] = 0;
    $_SESSION['ereignis'] = "Willkommen an Bord, " . $_SESSION['spieler_name'] . "! Wähle einen Planeten, um dein Abenteuer zu beginnen.";
}

// Hier kommt später die Planeten- und Aktionslogik hin
```

> **Was bedeutet das?**
> - `$_GET['neues_spiel']` wird gesetzt, wenn der Spieler auf "Neues Spiel" klickt
> - `$_POST['spieler_name']` enthält den Namen, den der Spieler eingegeben hat
> - Mit `$_SESSION` speichern wir Informationen, die während des gesamten Spiels erhalten bleiben
> - `htmlspecialchars()` sorgt dafür, dass keine gefährlichen HTML-Zeichen eingegeben werden können

#### 1.3 Das Spielerformular erstellen

Jetzt fügen wir ein Formular hinzu, mit dem der Spieler seinen Namen eingeben kann. Füge diesen Code dort ein, wo es im HTML-Teil steht: `<!-- Hier kommt später der Inhalt unseres Spiels hin -->`:

```html
<!-- Anzeige des aktuellen Ereignisses -->
<div class="ereignis">
    <?php 
    if (isset($_SESSION['ereignis'])) {
        echo "<p>" . $_SESSION['ereignis'] . "</p>";
    }
    ?>
</div>

<?php if (!isset($_SESSION['spieler_name'])): ?>
    <!-- Spielstart-Formular, wird nur angezeigt, wenn noch kein Spielername gesetzt ist -->
    <div class="spielstart">
        <h2>Neues Spiel starten</h2>
        <p>Gib deinen Namen ein, um das Abenteuer zu beginnen:</p>
        
        <form method="post">
            <input type="text" name="spieler_name" placeholder="Dein Name" required>
            <button type="submit">Abenteuer starten</button>
        </form>
    </div>
<?php else: ?>
    <!-- Spielinhalt, wird angezeigt, wenn ein Spielername gesetzt ist -->
    <div class="spielinhalt">
        <!-- Hier kommt später der eigentliche Spielinhalt hin -->
    </div>
    
    <!-- Link zum Neustarten des Spiels -->
    <div class="neues-spiel">
        <a href="index.php?neues_spiel=1">Neues Spiel starten</a>
    </div>
<?php endif; ?>
```

> **Was passiert hier?**
> - Wir zeigen Ereignisse an, die im Spiel passieren
> - Wenn noch kein Spielername gesetzt ist, zeigen wir ein Formular zur Namenseingabe an
> - Wenn bereits ein Spielername gesetzt ist, zeigen wir den Spielinhalt an
> - Wir bieten einen Link zum Neustarten des Spiels an

#### 1.4 Füge CSS für das Formular hinzu

Füge diese CSS-Regeln zu deinem vorhandenen CSS-Code hinzu:

```css
.ereignis {
    background-color: rgba(0, 0, 0, 0.5);
    padding: 10px;
    margin-bottom: 20px;
    border-left: 3px solid #0cf;
}

input[type="text"], button {
    padding: 8px;
    margin: 5px 0;
}

button, a {
    background-color: #0a84ff;
    color: white;
    border: none;
    padding: 8px 15px;
    border-radius: 4px;
    cursor: pointer;
    text-decoration: none;
    display: inline-block;
}

button:hover, a:hover {
    background-color: #0068d6;
}

.neues-spiel {
    margin-top: 20px;
    text-align: center;
}
```

> **Was bewirkt das CSS?**
> - Die Ereignisse werden in einem speziellen Bereich mit blauem Rand angezeigt
> - Die Eingabefelder und Buttons bekommen ein ansprechendes Aussehen
> - Der "Neues Spiel"-Link wird zentriert am unteren Rand angezeigt

#### 1.5 Teste deine Fortschritte

1. Speichere die Datei `index.php`
2. Öffne einen Browser und gehe zu `http://localhost/raumschiff_spiel/`
3. Du solltest jetzt ein Formular sehen, in dem du deinen Namen eingeben kannst
4. Gib einen Namen ein und klicke auf "Abenteuer starten"
5. Die Seite sollte sich ändern und eine Willkommensnachricht anzeigen

### Teil 2: Die Spielmechanik programmieren (30 Minuten)

#### 2.1 Spielerinfo-Bereich erstellen

Jetzt fügen wir einen Bereich hinzu, der Informationen über den Spieler anzeigt. Ersetze im HTML-Teil `<!-- Hier kommt später der eigentliche Spielinhalt hin -->` durch:

```html
<!-- Spielerinfo-Bereich -->
<div class="spieler-info">
    <h2>Pilot: <?php echo $_SESSION['spieler_name']; ?></h2>
    <div class="ressourcen">
        <p>Treibstoff: <span class="wert"><?php echo $_SESSION['treibstoff']; ?></span> Einheiten</p>
        <p>Kristalle: <span class="wert"><?php echo $_SESSION['kristalle']; ?></span> Stück</p>
        <p>Besuchte Planeten: <span class="wert"><?php echo $_SESSION['besuchte_planeten']; ?></span></p>
    </div>
</div>

<!-- Planeten-Auswahl -->
<div class="planeten">
    <h2>Verfügbare Planeten</h2>
    <div class="planeten-liste">
        <form method="get">
            <button type="submit" name="planet" value="alpha">Planet Alpha (Eisplanet)</button>
            <button type="submit" name="planet" value="beta">Planet Beta (Wüstenplanet)</button>
            <button type="submit" name="planet" value="gamma">Planet Gamma (Dschungelplanet)</button>
        </form>
    </div>
</div>

<!-- Aktionsbereich (wird nur angezeigt, wenn ein Planet ausgewählt ist) -->
<div class="aktionen">
    <?php if (isset($_SESSION['aktueller_planet'])): ?>
        <h2>Aktionen auf Planet <?php echo $_SESSION['aktueller_planet']; ?></h2>
        <!-- Hier kommen später die Aktionsbuttons hin -->
    <?php endif; ?>
</div>
```

> **Was bedeutet das?**
> - Wir zeigen den Namen des Spielers und seine aktuellen Ressourcen an
> - Wir erstellen Buttons für die drei Planeten, die der Spieler besuchen kann
> - Wir bereiten einen Bereich für Aktionen vor, der nur angezeigt wird, wenn ein Planet ausgewählt ist

#### 2.2 CSS für die Spielbereiche hinzufügen

Füge diese CSS-Regeln zu deinem vorhandenen CSS-Code hinzu:

```css
.spieler-info {
    margin-bottom: 20px;
}

.ressourcen {
    display: flex;
    justify-content: space-between;
    background-color: rgba(0, 0, 0, 0.3);
    padding: 10px;
    border-radius: 5px;
}

.wert {
    font-weight: bold;
    color: #0cf;
}

.planeten-liste button {
    margin: 5px;
    width: 220px;
    background-color: #446;
    transition: background-color 0.3s;
}

.planeten-liste button:hover {
    background-color: #668;
}

.aktionen {
    margin-top: 20px;
}
```

> **Was bewirkt das CSS?**
> - Die Ressourcen werden nebeneinander in einer Reihe angezeigt
> - Die Werte werden blau und fett hervorgehoben
> - Die Planetenbuttons bekommen ein besonderes Aussehen

#### 2.3 Implementiere die Planeten-Logik

Jetzt müssen wir programmieren, was passiert, wenn ein Planet angeklickt wird. Füge diesen Code in deinen PHP-Bereich ein, wo es steht: `// Hier kommt später die Planeten- und Aktionslogik hin`:

```php
// Lade die Funktionen für die Planeten
include('planeten.php');

// Prüfe, ob ein Planet angeklickt wurde
if (isset($_GET['planet'])) {
    $planet = $_GET['planet'];
    
    // Treibstoffverbrauch für den Flug (zufällig zwischen 5 und 15)
    $verbrauch = rand(5, 15);
    
    // Prüfe, ob genug Treibstoff vorhanden ist
    if ($_SESSION['treibstoff'] >= $verbrauch) {
        // Treibstoff abziehen und Zähler erhöhen
        $_SESSION['treibstoff'] -= $verbrauch;
        $_SESSION['besuchte_planeten']++;
        $_SESSION['aktueller_planet'] = $planet;
        
        // Hole die Informationen für diesen Planeten
        $planet_info = planet_info($planet);
        
        // Zufallsereignis erstellen
        $zufallszahl = rand(1, 10);
        if ($zufallszahl <= 3) {
            // 30% Wahrscheinlichkeit für ein besonderes Ereignis
            $ereignisse = [
                "Du entdeckst eine verlassene Raumstation!",
                "Ein Meteoritenschauer geht über dem Planeten nieder!",
                "Du siehst seltsame Lichter am Horizont..."
            ];
            $_SESSION['ereignis'] = "Planet " . ucfirst($planet) . " erreicht! " . $ereignisse[array_rand($ereignisse)];
        } else {
            // Standardnachricht
            $_SESSION['ereignis'] = "Du hast Planet " . ucfirst($planet) . " erreicht. " . $planet_info['beschreibung'];
        }
    } else {
        $_SESSION['ereignis'] = "Nicht genug Treibstoff für den Flug zum Planeten! Du benötigst mindestens " . $verbrauch . " Einheiten.";
    }
}

// Prüfe, ob eine Aktion auf einem Planeten durchgeführt wurde
if (isset($_GET['aktion']) && isset($_SESSION['aktueller_planet'])) {
    $aktion = $_GET['aktion'];
    $planet = $_SESSION['aktueller_planet'];
    
    // Führe die Aktion aus
    $ergebnis = planet_aktion($planet, $aktion);
    
    // Aktualisiere die Ereignisanzeige
    $_SESSION['ereignis'] = $ergebnis;
}

// Prüfe, ob das Spiel zu Ende ist (kein Treibstoff mehr)
if (isset($_SESSION['spieler_name']) && $_SESSION['treibstoff'] <= 0) {
    // Spiel ist zu Ende
    $name = $_SESSION['spieler_name'];
    $kristalle = $_SESSION['kristalle'];
    $planeten = $_SESSION['besuchte_planeten'];
    
    // Speichere den Highscore
    highscore_speichern($name, $kristalle, $planeten);
    
    $_SESSION['ereignis'] = "SPIELENDE: Dein Treibstoff ist aufgebraucht! Du hast " . $kristalle . " Kristalle gesammelt und " . $planeten . " Planeten besucht.";
}
```

> **Was passiert hier?**
> - Wir laden die Funktionen aus der Datei `planeten.php`
> - Wenn ein Planet angeklickt wird, verbrauchen wir Treibstoff und aktualisieren die Statistiken
> - Wir erstellen zufällige Ereignisse, um das Spiel interessanter zu machen
> - Wir verarbeiten Aktionen, die auf einem Planeten durchgeführt werden
> - Wir prüfen, ob das Spiel zu Ende ist (kein Treibstoff mehr)

#### 2.4 Die Planeten-Datei erstellen

Jetzt müssen wir die Datei `planeten.php` erstellen, die die Logik für die Planeten enthält. Öffne die Datei `planeten.php` in deinem Texteditor und füge diesen Code ein. Keine Sorge, ich erkläre dir gleich, was der Code macht:

```php
<?php
/**
 * Diese Datei enthält Funktionen für die verschiedenen Planeten im Spiel
 */

/**
 * Gibt Informationen zu einem bestimmten Planeten zurück
 * 
 * @param string $planet Der Name des Planeten
 * @return array Ein Array mit Informationen über den Planeten
 */
function planet_info($planet) {
    // Ein leeres Array für die Informationen vorbereiten
    $info = [];
    
    // Je nach Planet unterschiedliche Informationen zurückgeben
    switch ($planet) {
        case 'alpha':
            $info['name'] = "Alpha";
            $info['beschreibung'] = "Ein eisiger Planet mit glitzernden Kristallfeldern und gefrorenen Seen.";
            $info['aktionen'] = [
                'erkunden' => 'Den Planeten erkunden',
                'sammeln' => 'Kristalle sammeln',
                'tanken' => 'Nach Treibstoff suchen'
            ];
            break;
            
        case 'beta':
            $info['name'] = "Beta";
            $info['beschreibung'] = "Eine heiße Wüstenwelt mit endlosen Sanddünen und versteckten Oasen.";
            $info['aktionen'] = [
                'erkunden' => 'Die Wüste erkunden',
                'sammeln' => 'Nach Kristallen graben',
                'tanken' => 'Treibstoffquellen suchen'
            ];
            break;
            
        case 'gamma':
            $info['name'] = "Gamma";
            $info['beschreibung'] = "Ein üppiger Dschungelplanet mit exotischer Flora und Fauna.";
            $info['aktionen'] = [
                'erkunden' => 'Den Dschungel erkunden',
                'sammeln' => 'Kristalle aus Pflanzen extrahieren',
                'tanken' => 'Biologischen Treibstoff herstellen'
            ];
            break;
            
        default:
            $info['name'] = "Unbekannt";
            $info['beschreibung'] = "Ein mysteriöser Planet ohne bekannte Informationen.";
            $info['aktionen'] = [
                'erkunden' => 'Den Planeten erkunden'
            ];
            break;
    }
    
    return $info;
}

/**
 * Führt eine Aktion auf einem Planeten aus und gibt das Ergebnis zurück
 * 
 * @param string $planet Der Planet, auf dem die Aktion stattfindet
 * @param string $aktion Die auszuführende Aktion
 * @return string Eine Beschreibung des Ergebnisses
 */
function planet_aktion($planet, $aktion) {
    // Standardergebnis, falls etwas schiefgeht
    $ergebnis = "Diese Aktion ist nicht verfügbar.";
    
    // Je nach Planet und Aktion unterschiedliche Dinge tun
    switch ($aktion) {
        case 'erkunden':
            // Planet erkunden - kann verschiedene Ergebnisse haben
            $zufallszahl = rand(1, 10);
            
            if ($zufallszahl <= 3) {
                // 30% Chance für etwas Besonderes zu finden
                $ergebnis = "Bei deiner Erkundung findest du eine alte Karte, die auf eine Kristallhöhle hinweist!";
                // Chance, zusätzliche Kristalle zu finden
                if (rand(1, 3) == 1) {
                    $menge = rand(1, 3);
                    $_SESSION['kristalle'] += $menge;
                    $ergebnis .= " Du findest dabei " . $menge . " Kristalle!";
                }
            } elseif ($zufallszahl <= 7) {
                // 40% Chance für ein normales Ergebnis
                $ergebnisse = [
                    "Du erkundest die Umgebung, findest aber nichts Besonderes.",
                    "Die Landschaft ist beeindruckend, aber du entdeckst nichts Nützliches.",
                    "Du machst interessante Entdeckungen, die aber leider keinen praktischen Nutzen haben.",
                    "Die Erkundung ist anstrengend, aber nicht sehr ergiebig."
                ];
                $ergebnis = $ergebnisse[array_rand($ergebnisse)];
            } else {
                // 30% Chance für eine gefährliche Situation
                $ergebnis = "Deine Erkundung wird von einem plötzlichen Sturm unterbrochen! Du musst schnell zum Raumschiff zurückkehren.";
                // Chance, Treibstoff zu verlieren
                if (rand(1, 3) == 1) {
                    $verlust = rand(2, 5);
                    $_SESSION['treibstoff'] -= $verlust;
                    $ergebnis .= " Dabei verlierst du " . $verlust . " Einheiten Treibstoff!";
                }
            }
            break;
            
        case 'sammeln':
            // Kristalle sammeln - immer erfolgreich, aber mit unterschiedlicher Ausbeute
            $menge = rand(1, 5); // 1 bis 5 Kristalle
            $_SESSION['kristalle'] += $menge;
            
            // Je nach Planet andere Beschreibung
            switch ($planet) {
                case 'alpha':
                    $ergebnis = "Du sammelst " . $menge . " glitzernde Eiskristalle aus den gefrorenen Feldern.";
                    break;
                case 'beta':
                    $ergebnis = "Nach mühsamer Grabung in der Wüste findest du " . $menge . " funkelnde Kristalle.";
                    break;
                case 'gamma':
                    $ergebnis = "Du extrahierst " . $menge . " Kristalle aus den seltsamen Pflanzen des Dschungels.";
                    break;
                default:
                    $ergebnis = "Du sammelst " . $menge . " Kristalle.";
                    break;
            }
            break;
            
        case 'tanken':
            // Nach Treibstoff suchen - nicht immer erfolgreich
            $erfolg = rand(1, 10) <= 7; // 70% Erfolgswahrscheinlichkeit
            
            if ($erfolg) {
                $menge = rand(5, 15); // 5 bis 15 Einheiten Treibstoff
                $_SESSION['treibstoff'] += $menge;
                
                // Je nach Planet andere Beschreibung
                switch ($planet) {
                    case 'alpha':
                        $ergebnis = "Du schmilzt das Eis und extrahierst " . $menge . " Einheiten Treibstoff!";
                        break;
                    case 'beta':
                        $ergebnis = "Du findest eine unterirdische Treibstoffquelle und förderst " . $menge . " Einheiten!";
                        break;
                    case 'gamma':
                        $ergebnis = "Du stellst " . $menge . " Einheiten Bio-Treibstoff aus den Dschungelpflanzen her!";
                        break;
                    default:
                        $ergebnis = "Du findest " . $menge . " Einheiten Treibstoff!";
                        break;
                }
            } else {
                // Keine Treibstoffquelle gefunden
                $ergebnisse = [
                    "Du suchst intensiv, findest aber keine Treibstoffquelle.",
                    "Deine Suche nach Treibstoff bleibt leider erfolglos.",
                    "Die Suche nach Treibstoff gestaltet sich schwieriger als gedacht.",
                    "Trotz gründlicher Suche findest du keinen Treibstoff."
                ];
                $ergebnis = $ergebnisse[array_rand($ergebnisse)];
            }
            break;
    }
    
    return $ergebnis;
}

/**
 * Speichert einen Highscore in der Datei 'spielstand.txt'
 * 
 * @param string $name Der Name des Spielers
 * @param int $kristalle Die Anzahl der gesammelten Kristalle
 * @param int $planeten Die Anzahl der besuchten Planeten
 */
function highscore_speichern($name, $kristalle, $planeten) {
    // Das aktuelle Datum und die Uhrzeit
    $datum = date("d.m.Y H:i");
    
    // Der Eintrag für den Highscore (im Format "Name:Kristalle:Planeten:Datum")
    $eintrag = "$name:$kristalle:$planeten:$datum\n";
    
    // In die Datei schreiben (am Ende anhängen)
    file_put_contents("spielstand.txt", $eintrag, FILE_APPEND);
}

/**
 * Zeigt die Highscores aus der Datei 'spielstand.txt' an
 * 
 * @return string HTML-Code mit der Highscore-Tabelle
 */
function highscores_anzeigen() {
    // Prüfe, ob die Datei existiert
    if (file_exists("spielstand.txt")) {
        // Lese die Datei zeilenweise ein
        $eintraege = file("spielstand.txt", FILE_IGNORE_NEW_LINES);
        
        // Wenn Einträge vorhanden sind
        if (!empty($eintraege)) {
            // Array für die formatierten Einträge
            $formattedEntries = [];
            
            // Formatiere jeden Eintrag und füge ihn zum Array hinzu
            foreach ($eintraege as $eintrag) {
                // Teile den Eintrag am Doppelpunkt
                $teile = explode(":", $eintrag);
                
                // Prüfe, ob der Eintrag das richtige Format hat
                if (count($teile) >= 4) {
                    $name = $teile[0];
                    $kristalle = (int)$teile[1];
                    $planeten = (int)$teile[2];
                    $datum = $teile[3];
                    
                    // Füge den formatierten Eintrag zum Array hinzu
                    $formattedEntries[] = [
                        'name' => $name,
                        'kristalle' => $kristalle,
                        'planeten' => $planeten,
                        'datum' => $datum
                    ];
                }
            }
            
            // Sortiere die Einträge nach der Anzahl der Kristalle (absteigend)
            usort($formattedEntries, function($a, $b) {
                return $b['kristalle'] - $a['kristalle'];
            });
            
            // Baue die HTML-Tabelle
            $html = "<h2>Highscores</h2>";
            $html .= "<table class='highscore-tabelle'>";
            $html .= "<tr><th>Name</th><th>Kristalle</th><th>Planeten</th><th>Datum</th></tr>";
            
            // Zeige nur die Top 5 Highscores an (oder weniger, wenn nicht genug vorhanden)
            $count = 0;
            foreach ($formattedEntries as $entry) {
                $html .= "<tr>";
                $html .= "<td>" . $entry['name'] . "</td>";
                $html .= "<td>" . $entry['kristalle'] . "</td>";
                $html .= "<td>" . $entry['planeten'] . "</td>";
                $html .= "<td>" . $entry['datum'] . "</td>";
                $html .= "</tr>";
                
                $count++;
                if ($count >= 5) break; // Maximal 5 Einträge anzeigen
            }
            
            $html .= "</table>";
            
            return $html;
        } else {
            return "<p>Noch keine Highscores vorhanden.</p>";
        }
    } else {
        return "<p>Noch keine Highscores vorhanden.</p>";
    }
}
?>
```

> **Was passiert in dieser Datei?**
> 
> Diese Datei enthält alle wichtigen Funktionen für das Spiel:
> 
> 1. **planet_info()**: Diese Funktion gibt Informationen über jeden Planeten zurück:
>    - Den Namen des Planeten
>    - Eine Beschreibung des Planeten
>    - Mögliche Aktionen, die auf dem Planeten durchgeführt werden können
> 
> 2. **planet_aktion()**: Diese Funktion verarbeitet, was passiert, wenn du eine Aktion auf einem Planeten ausführst:
>    - "Erkunden": Du kannst besondere Dinge finden, aber auch in gefährliche Situationen geraten
>    - "Sammeln": Du sammelst Kristalle, die Menge ist zufällig
>    - "Tanken": Du suchst nach Treibstoff, manchmal mit Erfolg, manchmal nicht
> 
> 3. **highscore_speichern()**: Diese Funktion speichert deinen Highscore am Ende des Spiels
> 
> 4. **highscores_anzeigen()**: Diese Funktion liest die Highscores und zeigt sie in einer Tabelle an

#### 2.5 Aktionsbuttons hinzufügen

Jetzt müssen wir die Aktionsbuttons anzeigen, wenn ein Planet ausgewählt ist. Ersetze den Kommentar `<!-- Hier kommen später die Aktionsbuttons hin -->` im HTML-Teil durch:

```php
<?php
// Hole die Informationen für den aktuellen Planeten
$planet = $_SESSION['aktueller_planet'];
$planet_info = planet_info($planet);

// Erstelle für jede Aktion einen Button
echo "<div class='aktionen-buttons'>";
foreach ($planet_info['aktionen'] as $aktion_key => $aktion_text) {
    echo "<a href='index.php?aktion=" . $aktion_key . "' class='aktion-button'>" . $aktion_text . "</a>";
}
echo "</div>";
?>
```

> **Was passiert hier?**
> - Wir holen die Informationen für den aktuellen Planeten mit der Funktion `planet_info()`
> - Wir erstellen für jede mögliche Aktion einen Button
> - Wenn der Button angeklickt wird, wird die Aktion ausgeführt

#### 2.6 CSS für die Aktionsbuttons hinzufügen

Füge diese CSS-Regeln zu deinem vorhandenen CSS-Code hinzu:

```css
.aktionen-buttons {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
}

.aktion-button {
    background-color: #2980b9;
    padding: 10px 15px;
    border-radius: 5px;
    color: white;
    text-decoration: none;
    transition: background-color 0.3s;
}

.aktion-button:hover {
    background-color: #3498db;
}

.highscore-tabelle {
    width: 100%;
    margin-top: 20px;
    border-collapse: collapse;
}

.highscore-tabelle th, .highscore-tabelle td {
    padding: 8px;
    text-align: left;
    border-bottom: 1px solid #555;
}

.highscore-tabelle th {
    background-color: rgba(0, 0, 0, 0.3);
    color: #0cf;
}
```

> **Was bewirkt das CSS?**
> - Die Aktionsbuttons werden nebeneinander angezeigt
> - Die Buttons haben ein besonderes Aussehen, das sich verändert, wenn man mit der Maus darüber fährt
> - Die Highscore-Tabelle bekommt ein ansprechendes Design

#### 2.7 Teste deine Fortschritte

1. Speichere alle Dateien
2. Öffne einen Browser und gehe zu `http://localhost/raumschiff_spiel/`
3. Gib deinen Namen ein und starte das Spiel
4. Klicke auf einen Planeten und probiere die verschiedenen Aktionen aus

### Teil 3: Highscores und Spielende implementieren (30 Minuten)

#### 3.1 Highscores anzeigen

Jetzt fügen wir den Code hinzu, um die Highscores anzuzeigen. Füge am Ende der `index.php`-Datei, direkt vor dem schließenden `</div>`-Tag der Container-Klasse, diesen Code ein:

```php
<!-- Highscores anzeigen -->
<div class="highscores">
    <?php 
    // Wenn das Spiel zu Ende ist oder noch kein Spiel gestartet wurde
    if (!isset($_SESSION['spieler_name']) || $_SESSION['treibstoff'] <= 0) {
        echo highscores_anzeigen();
    }
    ?>
</div>
```

> **Was passiert hier?**
> - Wir zeigen die Highscores an, wenn das Spiel zu Ende ist oder noch nicht begonnen hat
> - Wir verwenden die Funktion `highscores_anzeigen()` aus der Datei `planeten.php`

#### 3.2 Spiel-Ende-Logik verbessern

Jetzt verbessern wir die Logik für das Spielende. Ersetze den Code für die Spielende-Prüfung durch:

```php
// Prüfe, ob das Spiel zu Ende ist (kein Treibstoff mehr)
if (isset($_SESSION['spieler_name']) && $_SESSION['treibstoff'] <= 0) {
    // Spiel ist zu Ende
    $name = $_SESSION['spieler_name'];
    $kristalle = $_SESSION['kristalle'];
    $planeten = $_SESSION['besuchte_planeten'];
    
    // Speichere den Highscore (nur wenn das Spiel richtig zu Ende ist)
    if (!isset($_SESSION['spiel_beendet'])) {
        highscore_speichern($name, $kristalle, $planeten);
        $_SESSION['spiel_beendet'] = true;
    }
    
    $_SESSION['ereignis'] = "SPIELENDE: Dein Treibstoff ist aufgebraucht! Du hast " . $kristalle . " Kristalle gesammelt und " . $planeten . " Planeten besucht.";
    
    // Entferne den aktuellen Planeten, damit keine Aktionen mehr möglich sind
    unset($_SESSION['aktueller_planet']);
}
```

> **Was passiert hier?**
> - Wir prüfen, ob der Treibstoff aufgebraucht ist
> - Wenn ja, speichern wir den Highscore (aber nur einmal)
> - Wir zeigen eine Meldung über das Spielende an
> - Wir entfernen den aktuellen Planeten, damit keine Aktionen mehr möglich sind

#### 3.3 Zusätzliches CSS für das Spielende

Füge diese CSS-Regeln zu deinem vorhandenen CSS-Code hinzu:

```css
.spielende {
    background-color: rgba(200, 0, 0, 0.2);
    border: 1px solid red;
    padding: 15px;
    margin: 20px 0;
    border-radius: 5px;
    text-align: center;
}

.spielende h2 {
    color: red;
    margin-top: 0;
}
```

> **Was bewirkt das CSS?**
> - Die Spielende-Meldung wird in einem auffälligen roten Bereich angezeigt

#### 3.4 Spielanleitung hinzufügen

Zum Schluss fügen wir eine Spielanleitung hinzu, damit jeder weiß, wie das Spiel funktioniert. Füge diesen Code direkt nach dem Spielstart-Formular ein (nach dem schließenden `</div>`-Tag der `spielstart`-Klasse):

```html
<!-- Spielanleitung, wird nur angezeigt, wenn noch kein Spielername gesetzt ist -->
<div class="anleitung">
    <h2>Spielanleitung</h2>
    <p>Willkommen beim Raumschiff-Abenteuer! In diesem Spiel steuerst du ein Raumschiff durch das Universum.</p>
    
    <h3>So spielst du:</h3>
    <ol>
        <li>Gib deinen Namen ein und starte das Spiel</li>
        <li>Wähle einen Planeten, den du besuchen möchtest</li>
        <li>Führe Aktionen auf dem Planeten durch:
            <ul>
                <li><strong>Erkunden:</strong> Entdecke den Planeten (kann zu verschiedenen Ereignissen führen)</li>
                <li><strong>Sammeln:</strong> Sammle wertvolle Kristalle</li>
                <li><strong>Tanken:</strong> Suche nach Treibstoff für dein Raumschiff</li>
            </ul>
        </li>
        <li>Jeder Flug zu einem Planeten verbraucht Treibstoff</li>
        <li>Das Spiel endet, wenn dein Treibstoff aufgebraucht ist</li>
        <li>Dein Ziel ist es, so viele Kristalle wie möglich zu sammeln!</li>
    </ol>
</div>
```

> **Was passiert hier?**
> - Wir fügen eine ausführliche Anleitung hinzu, damit jeder weiß, wie das Spiel funktioniert
> - Die Anleitung wird nur angezeigt, wenn noch kein Spiel gestartet wurde

#### 3.5 CSS für die Spielanleitung

Füge diese CSS-Regeln zu deinem vorhandenen CSS-Code hinzu:

```css
.anleitung {
    background-color: rgba(0, 0, 0, 0.3);
    padding: 15px;
    margin: 20px 0;
    border-radius: 5px;
}

.anleitung h2 {
    margin-top: 0;
}

.anleitung ul, .anleitung ol {
    padding-left: 20px;
}

.anleitung li {
    margin-bottom: 5px;
}
```

> **Was bewirkt das CSS?**
> - Die Spielanleitung bekommt ein ansprechendes Design
> - Die Listen werden mit etwas Abstand und Zwischenraum formatiert

### Abschluss und Erweiterungsmöglichkeiten

Herzlichen Glückwunsch! Du hast jetzt ein funktionierendes Raumschiff-Spiel programmiert! Hier sind noch einige Ideen, wie du das Spiel erweitern könntest, wenn du noch Zeit hast:

#### Einfache Erweiterungen:

1. **Mehr Planeten hinzufügen:**
   - Füge weitere Planeten mit einzigartigen Beschreibungen und Aktionen hinzu
   - Beispiel: Ein Wasserplanet, ein Feuerplanet, ein Gasriese

2. **Raumschiff-Upgrades:**
   - Füge eine Möglichkeit hinzu, das Raumschiff zu verbessern
   - Beispiel: "Treibstofftanks vergrößern" oder "Kristalldetektoren installieren"

3. **Zufallsereignisse verbessern:**
   - Füge mehr und interessantere Zufallsereignisse hinzu
   - Beispiel: Begegnungen mit Aliens, Meteoritenschauer, Weltraumanomalien

#### Mittelschwere Erweiterungen:

1. **Grafische Elemente:**
   - Füge einfache Bilder oder Icons für die Planeten hinzu
   - Verwende ASCII-Kunst oder Unicode-Symbole für verschiedene Elemente

2. **Handelsystem:**
   - Füge die Möglichkeit hinzu, Kristalle gegen Treibstoff zu tauschen
   - Die Preise könnten je nach Planet unterschiedlich sein

3. **Spielspeicherung:**
   - Ermögliche es, ein Spiel zu speichern und später fortzusetzen
   - Verwende dazu die Datei `spielstand.txt` oder eine neue Datei

#### Schwierigere Erweiterungen:

1. **Missionen:**
   - Füge Missionen hinzu, die der Spieler erfüllen kann
   - Beispiel: "Sammle 10 Kristalle auf Planet Alpha" oder "Besuche alle Planeten"

2. **Inventarsystem:**
   - Füge ein Inventar hinzu, in dem der Spieler Gegenstände sammeln kann
   - Diese Gegenstände könnten besondere Fähigkeiten oder Vorteile bieten

3. **Mehrere Spieler:**
   - Ermögliche es, dass mehrere Spieler nacheinander spielen können
   - Zeige eine Rangliste der besten Spieler an

## Fehlerbehebung

Falls etwas nicht funktioniert, hier einige häufige Probleme und ihre Lösungen:

1. **Die Seite zeigt nur weißen Bildschirm:**
   - Prüfe, ob in deinem PHP-Code Syntaxfehler sind
   - Schaue im XAMPP-Fehlerlog nach (in der Datei `C:\xampp\php\logs\php_error_log`)

2. **Die Planeten-Aktionen funktionieren nicht:**
   - Prüfe, ob du die Datei `planeten.php` korrekt erstellt hast
   - Stelle sicher, dass der `include('planeten.php')`-Befehl in `index.php` vorhanden ist

3. **Die Highscores werden nicht angezeigt:**
   - Prüfe, ob die Datei `spielstand.txt` existiert und beschreibbar ist
   - Stelle sicher, dass die Funktionen `highscore_speichern()` und `highscores_anzeigen()` korrekt sind

4. **Das Spiel startet nicht richtig:**
   - Prüfe, ob die Session korrekt gestartet wird (`session_start()` am Anfang der `index.php`)
   - Stelle sicher, dass die Variablen in `$_SESSION` korrekt initialisiert werden

## Abschlusswort

Du hast jetzt ein eigenes Weltraum-Abenteuerspiel programmiert! Du hast dabei viele wichtige Konzepte der Webprogrammierung gelernt:

- HTML und CSS zur Gestaltung von Webseiten
- PHP zur Programmierung von Spiellogik
- Sessions zur Speicherung von Spielerdaten
- Dateiverarbeitung zur Speicherung von Highscores
- Zufallselemente zur Gestaltung eines interessanten Spiels

Diese Kenntnisse sind eine großartige Grundlage für weitere Programmierprojekte. Vielleicht hast du ja Lust, das Spiel weiter zu verbessern oder ein ganz neues Spiel zu programmieren!
