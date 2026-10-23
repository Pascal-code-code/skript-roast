---
name: skript-roast
description: Prüft ein Reel-Skript aus fünf Rollen (Zuschauer, Skeptiker, Konkurrent, Lektor, Stratege), vergibt Noten und schreibt das Skript neu, wenn es durchfällt (Schnitt unter 6 oder eine Rolle unter 5). Nutzen bei "roast das Skript", "prüf das Skript", "zerleg das Skript", "Skript-Rat", "/skript-roast" oder direkt nachdem ein Reel-Skript geschrieben wurde.
argument-hint: "[Pfad zum Skript oder Skript-Text]"
---

# Skript-Roast: fünf Rollen, ein Urteil

Ein Skript, das Claude gerade geschrieben hat, findet Claude meistens gut. Dieser Skill dreht das um: Fünf Rollen greifen das Skript an, jede auf genau einer Ebene. Fällt es durch, schreibt Claude es neu, bevor du es siehst.

Der Skill funktioniert mit jedem Skript, egal ob Claude es geschrieben hat oder du. Liegt im Projekt eine Datei zu deiner Stimme (zum Beispiel `mein-content/stimme.md` aus den Claude Content-Skills), liest der Lektor sie mit.

## Schritt 1: Die Vorlage bauen

Sammle in einem Block, der wortgleich an alle Rollen geht:

1. **Das Skript**, komplett, mit Satznummern. Jeder gesprochene Satz bekommt eine Nummer (`S1`, `S2` …), Gesten in `[ ]` bleiben dran. Was ab Bild 1 zu sehen ist (Visuell Hook), heißt `V`.
2. **Kernaussage** in einem Satz (was der Zuschauer danach glauben oder tun soll).
3. **Ziel-Länge** und **Wortzahl**.
4. **CTA** und Lead-Magnet, falls vorhanden, sonst „keiner“.
5. **Kanal-Thema** in einem Satz (worüber der Creator postet und wen er erreichen will).
6. **Was echt ist:** welche Zahlen, Beispiele und Erlebnisse nachweislich vom Creator stammen (Gespräch, Datei). Alles andere gilt als erfunden.
7. Falls das Reel ein Nachbau eines fremden Reels ist: „Inspo-Nachbau“ und was das Vorbild macht.

Fehlt etwas davon, nimm es aus dem Gespräch oder der Skript-Datei. Frag nur nach, wenn die Kernaussage unklar ist.

## Schritt 2: Den Rat starten (7 Agents parallel)

Starte **alle Rollen in einer einzigen Nachricht**: je ein `Agent`-Aufruf, `subagent_type: general-purpose`, `model: "sonnet"`. Der Zuschauer läuft dreimal (siehe unten), die anderen vier je einmal. Jeder Prompt = Rollenauftrag + Rückgabeformat + Vorlage.

**Rückgabeformat (für alle gleich, in den Prompt kopieren):**
> Gib zurück, unter 250 Wörtern, ohne Gedankenstriche:
> HALTUNG: ein Satz.
> PUNKTE: 3 bis 5 Punkte, jeder mit Satznummer (S1, S4 …) und dem genauen Problem.
> URTEIL: der eine Satz für den Creator, kurz wie eine Randnotiz (z. B. „Steige nach Satz 1 aus.“, „Satz 4 ist zu lang.“).
> ÄNDERUNG: was konkret anders muss, mit Satznummer. Keine neuen Fakten erfinden.
> NOTE: eine Zahl von 1 bis 10 nur auf deiner Ebene (1 = so nicht drehen, 10 = sofort drehen).
> Bleib in deiner Rolle, schwäch nichts ab, lob nicht aus Höflichkeit.

**1. Der Zuschauer**
> Du bist der Zuschauer im Skript-Rat. Du scrollst abends durch Instagram, der Daumen liegt schon auf dem Bildschirm, und du kennst den Creator nicht. Lies das Skript Satz für Satz, als würdest du es hören, und sag in der Ich-Form, nach welchem Satz du weiterwischst und warum. Prüfe: Weißt du nach 2 Sekunden, worum es geht? Hast du eine Frage im Kopf, deren Antwort noch fehlt? Kommt die Antwort zu früh (Satz 1 oder 2)? Gibt es nach etwa 8 bis 10 Sekunden einen neuen Grund zu bleiben? Überrascht dich etwas (A erwartet, B gesagt)? Deine einzige Frage ist: Bleibe ich bis zum Ende?

**2. Der Skeptiker**
> Du bist der Skeptiker im Skript-Rat. Du glaubst keinem Creator ein Wort. Geh jede Behauptung durch und frag „Woher weißt du das?“. Markiere jede Zahl, jedes Beispiel und jedes Erlebnis, das laut Vorlage nicht nachweislich vom Creator stammt. Markiere jeden Satz, der etwas verspricht, ohne es zu zeigen. Deine einzige Frage ist: Würde ich das glauben, und was fehlt als Beweis? Drei Grenzen: Ein Beleg im Bild (Screenshot, Notiz, Split-Screen) zählt als Beweis. Du-Beispiele, die erkennbar zur Veranschaulichung dienen („Du erzählst von einer Reise?“), sind keine Behauptung. Eine Wirkung, die man in 30 Sekunden grundsätzlich nicht beweisen kann (z. B. „genau diese Zeile war der Grund“), kostet höchstens einen Punkt, wenn der Satz sie nicht als Tatsache verkauft.

**3. Der Konkurrent**
> Du bist der Konkurrent im Skript-Rat: ein anderer Creator, der über dasselbe Thema postet (siehe Kanal-Thema in der Vorlage). Mach den Tausch-Test an jedem Satz: Könntest du ihn unverändert in dein eigenes Reel übernehmen? Nenn diese Sätze. Sag dann, was in diesem Skript nur dieser Creator sagen kann (eigene Zahl, eigenes Werkzeug, eigene Erfahrung) und ob davon genug drin ist. Deine einzige Frage ist: Macht das nicht jeder? Ausnahme Inspo-Nachbau (steht dann in der Vorlage): Nähe zum Vorbild in Aufbau, Hook und CTA ist gewollt und kostet keinen Punkt. Du prüfst dann nur, ob in jedem Teil die eigenen Inhalte des Creators stecken (Befehle, Werkzeuge, Zahlen, Erlebnisse) statt der übersetzten des Vorbilds.

**4. Der Lektor**
> Du bist der Lektor im Skript-Rat. Der Creator spricht dieses Skript in die Kamera, also liest du es laut. Falls im Projekt eine Datei zur Stimme des Creators liegt (z. B. `mein-content/stimme.md`), lies sie vorher. Prüfe:
> - Satzstücke und Ein-Wort-Sätze („Kein CapCut. Kein Premiere.“ als Dauerfigur). Gedanken sollen mit „und“, „und dann“, „aber“, „wenn … dann“, „statt“ durchlaufen.
> - Nebensatz-Stapel: ein Satz folgt einer Handlung oder einem Gedanken, er stapelt keine Argumente.
> - Sätze, bei denen man mittendrin Luft holen muss (zu kurz geschnitten) oder sich verhaspelt (zu lang).
> - Jedes „das/es/drin/da“ ohne hörbaren Bezug.
> - Indirekte Rede, die wie ein Befehl an den Zuschauer klingt. Zitate müssen als Zitat hörbar sein („und sagt: Hier bin ich weg“).
> - Schriftdeutsch statt gesprochener Kurzformen („hab“, „mach“, „geb ich ab“).
> - Gedankenstriche, KI-Floskeln („zudem“, „des Weiteren“, „nahtlos“, „revolutionär“, „bahnbrechend“, „eintauchen in“, „Fazit:“), „nicht nur X, sondern auch Y“ als Dauerfigur, Sie-Anrede, Passiv wo Aktiv geht, Absolutheit („garantiert“, „die beste Lösung“), Hedging wie „quasi“.
> - Wortzahl gegen Ziel-Länge (15 s ≈ 50 Wörter, 25 s ≈ 80 bis 85, 35 s ≈ 115, CTA kostet etwa 4 s).
> Ausnahme: In Story-Szenen mit Befehlen und Reaktionen („Claude, gib mir mal einen Ball.“ „Der war neu.“) sind kurze Sätze richtig. Deine einzige Frage ist: Spricht sich das sauber in einem Take?

**5. Der Stratege**
> Du bist der Stratege im Skript-Rat. Lies das Kanal-Thema in der Vorlage: Jedes Reel soll genau die Leute anziehen, die der Creator erreichen will. Prüfe: Passt das Thema zum Kern des Kanals? Ist jeder Wert etwas, das der Zuschauer selbst nachmachen kann? Weiß der Zuschauer am Ende genau, was er als Nächstes tun soll? Passt der Lead-Magnet genau zum Video, oder fehlt er? Deine einzige Frage ist: Bringt dieses Reel den Creator einen Schritt weiter, und gibt es einen klaren nächsten Schritt für den Zuschauer?

### Der Zuschauer läuft dreimal

Weil seine Note doppelt zählt, startet der Zuschauer in Runde 1 als **drei parallele Agents** mit identischem Prompt. Gewertet wird der **Median** der drei Noten. In den Rat-Block kommen nur Punkte, die **mindestens zwei von drei** nennen. Steigen alle drei beim selben Satz aus, ist das ein sicherer Befund. Kosten: 7 statt 5 Agents pro Runde.

### Ab Runde 2: dieselben Agents weiterführen, nicht neu starten

Neue Agents kennen ihre eigene frühere Kritik nicht und fordern dann jede Runde nur die Hälfte, die gerade fehlt (im Test forderte der Zuschauer erst „Überraschung in die Hook“, dann „Hook ist nur deine Geschichte“, dann wieder „Überraschung nach vorn“). Deshalb in Runde 2 und 3 jede Rolle per `SendMessage` an ihre Agent-ID aus Runde 1 weiterführen, mit dem neuen Skript, der Liste, was sich geändert hat, und diesem Zusatz:

> Hier ist die neue Fassung. Prüf zuerst, ob deine Forderung aus der letzten Runde umgesetzt ist und ob sie wirkt. Wenn du jetzt etwas forderst, das deiner früheren Forderung widerspricht, sag das ausdrücklich und erklär, was beides zusammen verlangt (z. B. „Überraschung UND Nutzen in einem Satz“). Gleiches Rückgabeformat.

Steht `SendMessage` nicht zur Verfügung, starte neue Agents und gib jedem seine eigene Antwort aus der Vorrunde mit in den Prompt.

## Schritt 3: Das Urteil (du selbst)

Wenn alle zurück sind, bist du der Richter. Rechne:

- **Schnitt** = gewichteter Mittelwert, **der Zuschauer zählt doppelt** (Summe mit Zuschauer × 2, geteilt durch 6), eine Nachkommastelle. Grund: Seine Note sagte im Test die Skip-Rate am genauesten voraus, und die Skip-Rate entscheidet über die Reichweite.
- **Durchgefallen**, wenn der Schnitt **unter 6** liegt **oder** eine einzelne Rolle **unter 5**.
- Sonst **bestanden**.

Widersprechen sich Rollen (der Lektor will kürzen, der Skeptiker will einen Beweis mehr), entscheide und schreib in einem Satz, wie.

Ausgabe, genau so:

```
SKRIPT-RAT · Runde [n]

Zuschauer    [X]/10  [Urteil-Satz]
Skeptiker    [X]/10  [Urteil-Satz]
Konkurrent   [X]/10  [Urteil-Satz]
Lektor       [X]/10  [Urteil-Satz]
Stratege     [X]/10  [Urteil-Satz]

Schnitt [X,X] · niedrigste [Rolle X] · BESTANDEN / ÜBERARBEITEN
```

## Schritt 4: Überarbeiten (nur wenn durchgefallen)

Schreib das Skript neu:

- **Format bleibt gleich.** Hatte das Skript ein Format, behalte es. Sonst dieses Drehzettel-Format, ohne Tabellen:

  ```
  Visuell Hook: [was ab Bild 1 zu sehen ist]

  SKRIPT [Setting: wo du sitzt, Einstellung]

  Gesprochener Satz eins. [Geste oder Blick]

  Gesprochener Satz zwei. [Geste]

  CTA

  _____________________________________________________________________
  ```
  Jeder Satz ein eigener Absatz, höchstens ein bis zwei Gesten pro Satz. Was der Schnitt braucht (Effekte, Einblendungen), kommt unter die Trennlinie.
- **Nennen zwei Rollen oder zwei Runden denselben Grundfehler (z. B. „die Hook ist deine Geschichte, nicht mein Nutzen“), wird der betroffene Teil neu gebaut, nicht umformuliert.** Wörter tauschen und Sätze teilen behebt keinen Aufbau-Fehler. Springt der Schnitt nach einer Runde nur um ±0,3, braucht das Skript einen anderen Ansatz.
- **Kernaussage, echte Zahlen, Namen und CTA-Wort bleiben.** Nur die Schwächen beheben, die der Rat mit Satznummer genannt hat. Fang bei der Rolle mit der niedrigsten Note an.
- **Nichts erfinden.** Fordert der Skeptiker einen Beweis, den es nicht gibt, markiere die Stelle mit „bitte prüfen“ und frag den Creator in der Abgabe nach dem echten Erlebnis.
- Dann **zurück zu Schritt 2** mit dem neuen Skript.

**Höchstens 2 Überarbeitungsrunden** (also bis zu 3 Rat-Durchgänge). Fällt das Skript danach immer noch durch, gib die beste Fassung ab, nenn die offenen Punkte und frag, was der Creator dazu weiß. Meist fehlt dann ein echtes Erlebnis, das nur er liefern kann.

## Schritt 5: Abgabe

- Das Skript im Chat zeigen, darunter Wortzahl und geschätzte Länge.
- Darunter der Rat-Block der letzten Runde. Gab es Überarbeitungen, eine Zeile Verlauf: `Runde 1: 5,2 → Runde 2: 6,8`.
- Lag das Skript in einer Datei: neue Fassung dort speichern, Entwurfsnummer hochzählen, und unter die Trennlinie alle Rat-Blöcke mit den ÄNDERUNG-Punkten schreiben. So sieht man später, warum ein Satz so lautet.

## Eichung

Der Rat lief blind an vier veröffentlichten Reels mit bekannten Zahlen (Skripte ohne Zahlen, gemischte Reihenfolge). Noten Zuschauer/Skeptiker/Konkurrent/Lektor/Stratege:

- **Reel A** (298k Views auf TikTok, 46 % geschaut): 8/7/9/7/9 → Schnitt 8,0, bestanden
- **Reel B** (1.500 Views, 3× üblich, Skip 40 %): 6/4/4/4/4 → 4,4
- **Reel C** (~500 Views, Skip 69 %): 5/3/5/4/3 → 4,0
- **Reel D** (~500 Views, Skip 77 %): 3/2/3/3/6 → 3,4

Die Rangfolge des Rats stimmt genau mit den Views überein, die des Zuschauers sogar mit der Skip-Rate. Die Schwelle 6 trennt das starke Reel klar von den schwachen. Skeptiker und Stratege haben Reel B härter bestraft, als seine Zahlen es rechtfertigen. Deshalb zählt der Zuschauer doppelt, und der Skeptiker hat seine drei Grenzen bekommen.

Rauschen: Dasselbe Skript dreimal an denselben Zuschauer-Prompt ergab 6/6/6, jedes Mal Ausstieg beim selben Satz aus demselben Grund. Beim selben Text ist die Rolle also stabil. Widersprüche zwischen den Runden kamen vom fehlenden Gedächtnis, darum werden die Agents ab Runde 2 weitergeführt.

## Regeln

- Jede Rolle bewertet nur ihre Ebene. Der Lektor sagt nichts zur Hook, der Zuschauer nichts zur Grammatik.
- Keine Rolle schwächt ab. Ein Rat, der alles mit 8 bewertet, hat nichts geprüft. Liegen alle fünf Noten bei 8 oder höher, lies die PUNKTE kritisch nach: Steht dort ein echtes Problem, zählt es.
- Der Rat sieht die Vorlage, nicht das Gespräch. Alles, was er wissen muss, steht in Schritt 1.
- Das Feedback des Creators zu einem Skript schlägt jede Note.
- Kein Gedankenstrich, weder im Skript noch im Rat-Block.
