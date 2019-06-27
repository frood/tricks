---
title: "Medienpool: Erweiterter Schutz vor dem Löschen von Daten"
authors: [dpf-dd skerbis]
prio:
---

# Medienpool: Erweiterter Schutz vor dem Löschen von Daten

REDAXO prüft nicht ob Medien oder Artikel in anderen Tabellen als den Artikeln und Metas verlinkt sind. 

## Beispiel

Es existiert z.B. ein yForm-Formular, mit dessen Hilfe ein Frontend-User Bilder hochlädt und zum Medienpool hinzufügt.
Da der Dateiname des hochgeladenen Bildes in der yForm-Tabelle gespeichert wird, kann der Medienpool das entsprechende Bild von Haus aus **NICHT** vor dem Löschen schützen. Das Bild kann somit im Medienpool gelöscht werden, obwohl es sich noch in Benutzung befindet (In diesem Fall in der yForm-Datenausgabe / Table Manager).
Durch das Einbinden der hier geizeigten Klasse, wird diese Funktion nachgeliefert unhd vor dem Löschen eines Mediums die Tabelle nach dem Medium durchsucht. 

## AddOn Yakme

Das AddOn Yakme](https://github.com/yakamara/yakme) eine fertige Lösung für diesen Fall. 

## Alternativer Weg 

Falls man Yakme nicht nutzen möchte, kann man sich die entsprechende Class YForm aus Yakme kopieren, umbenennen und z.B. im Projekt-AddOn verwenden. 

https://github.com/yakamara/yakme/blob/master/lib/Yakme/Extension/YForm.php

- Zur Verwendung im eigenen Projekt kopiert man die Class als neue Datei z.B. in den lib-Ordner des Project-AddOns
- Entfernt oder ändert den Namespace
- Ändert den Class-Namen z.B. auf: MediaInUseCheck

Also aus: 

```php 
namespace Yakme\Extension;
class YForm
```

wird z.B. 

```
class MediaInUseCheck


### Installation

Folgende zwei Zeilen der `boot.php` im `project`-Addon hinzufügen
```php
rex_extension::register('MEDIA_IS_IN_USE', 'MediaInUseCheck::isMediaInUse');
\rex_extension::register('PACKAGES_INCLUDED', 'MediaInUseCheck::isArticleInUse');
```

Es sind dann keine weiteren Schritte erforderlich. 