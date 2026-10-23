# Skript-Roast

Ein Skript, das Claude gerade geschrieben hat, findet Claude meistens gut. Dieser Skill dreht das um: Fünf Rollen zerlegen dein Reel-Skript, bevor du es drehst. Fällt es durch, schreibt Claude es neu und lässt den Rat noch mal drüberschauen.

## Die fünf Rollen

| Rolle | Seine Frage |
|---|---|
| Zuschauer | Bleibe ich bis zum Ende, oder wische ich nach Satz 2 weg? |
| Skeptiker | Würde ich das glauben, und wo fehlt der Beweis? |
| Konkurrent | Könnte ich diesen Satz unverändert in mein Reel packen? |
| Lektor | Spricht sich das sauber in einem Take? |
| Stratege | Bringt dich das Reel weiter, und weiß der Zuschauer, was er als Nächstes tun soll? |

Jede Rolle gibt eine Note von 1 bis 10. Der Zuschauer zählt doppelt, weil seine Note die Skip-Rate am besten vorhersagt. Liegt der Schnitt unter 6 oder eine Rolle unter 5, wird überarbeitet. Höchstens zwei Runden.

Am Ende bekommst du so einen Block:

```
SKRIPT-RAT · Runde 2

Zuschauer    7/10  Bleibe bis zum Ende, Satz 3 trägt.
Skeptiker    6/10  Die Zahl in Satz 5 will ich sehen.
Konkurrent   7/10  Satz 1 könnte jeder sagen, der Rest ist deins.
Lektor       8/10  Spricht sich in einem Take.
Stratege     6/10  CTA passt, Lead-Magnet fehlt noch.

Schnitt 6,8 · niedrigste Skeptiker 6 · BESTANDEN
```

## Hält das, was es verspricht?

Ich hab den Rat blind an vier meiner eigenen Reels laufen lassen, ohne ihm die Zahlen zu verraten. Das Reel mit 298k Views bekam 8,0, die drei schwachen zwischen 3,4 und 4,4. Die Reihenfolge des Rats war genau die Reihenfolge der Views. Die Details stehen unten im Skill.

## Installieren

1. Repo laden: oben den grünen Button "Code", dann "Download ZIP", entpacken. Oder im Terminal:
   ```
   git clone https://github.com/Pascal-code-code/skript-roast.git
   ```
2. Den Skill dahin kopieren, wo Claude Code ihn in jedem Projekt findet (Mac und Linux):
   ```
   mkdir -p ~/.claude/skills && cp -R skript-roast/.claude/skills/skript-roast ~/.claude/skills/
   ```
   Willst du ihn nur in einem Projekt: den Ordner `.claude/skills/skript-roast` in den `.claude/skills/` deines Projekts kopieren.
3. Claude Code neu starten.

## Benutzen

- `/skript-roast` und dein Skript direkt dahinter einfügen, oder den Pfad zur Datei angeben.
- Oder einfach schreiben "roast das Skript", nachdem Claude dir eins geschrieben hat.

Sag Claude kurz, worüber dein Kanal geht und welche Zahlen und Erlebnisse im Skript wirklich von dir sind. Der Skeptiker behandelt alles andere als erfunden.

Ein Durchgang startet sieben Agents parallel und dauert ein paar Minuten. Das geht auf dein Nutzungslimit, also lieber einmal am fertigen Skript laufen lassen als an jedem Zwischenstand.

Nutzt du schon meine [Claude Content-Skills](https://github.com/Pascal-code-code/claude-content-skills): Der Lektor liest dann automatisch deine `mein-content/stimme.md` mit.

## Voraussetzungen

- Claude Code, mit Pro- oder Max-Plan

## Fragen

Wenn etwas hakt, schreib mir in die Community, am besten mit einem Screenshot von der Stelle.

Claude ist eine Marke von Anthropic. Dieses Projekt steht in keiner Verbindung zu Anthropic.
