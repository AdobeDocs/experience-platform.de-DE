---
title: Metrik für das gesamte Datenvolumen
description: Erfahren Sie mehr über die neue Metrik „Gesamtdatenvolumen“ und darüber, wie sie die frühere Metrik „Durchschnittlicher Profilreichtum“ ersetzt.
exl-id: 4b21d25c-b82b-4d1a-83ce-b510f02fd160
source-git-commit: 62f5ecf82df46284365e64d633c8242ac45567bc
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 1%

---

# Metrik für das gesamte Datenvolumen

Das Gesamtdatenvolumen ersetzt die frühere Metrik Durchschnittlicher Profilreichhaltigkeitsgrad als einfachere und besser erklärbare Methode zur Verfolgung der Nutzung anhand Ihrer Profilspeicher-Berechtigung.

**Gesamtdatenvolumen = adressierbare Zielgruppe × durchschnittliche Profilreichhaltigkeit**

Diese Metrik spiegelt die Gesamtmenge der im **Profilspeicher“ gespeicherten Daten wider** die in Echtzeit-Kundenprofil-Interaktions-Workflows verwendet werden können. Es **keine** im **Data Lake** gespeicherten Daten enthalten. Diese Änderung bietet eine fokussiertere und transparentere Ansicht von Daten, die für die profilbasierte Personalisierung und Interaktion relevant sind.

## Häufig gestellte Fragen {#faq}

Im folgenden Abschnitt finden Sie häufig gestellte Fragen zu diesem Update.

### Warum wurde diese Änderung vorgenommen?

Diese Änderung wurde vorgenommen, um die Einhaltung der Lizenzberechtigungsmetriken zu vereinfachen. Wir haben oft von Kunden gehört, dass sie die durchschnittliche Reichweite von Profilen schwer verstehen und verwalten können. Mit dieser Änderung hoffen wir, dass Sie Ihre lizenzierte Verwendung des Echtzeit-Kundenprofils besser verstehen und verwalten können.

### Ändert sich durch diese Metrikänderung meine Berechtigung für den Profilspeicher?

Nein. Die Berechtigung für den Profilspeicher bleibt gleich wie zuvor, da das Gesamtdatenvolumen der adressierbaren Zielgruppe entspricht, multipliziert mit der berechtigten durchschnittlichen Profilreichhaltigkeit.

### Hat diese Änderung Auswirkungen auf die von mir erworbenen Berechtigungspakete?

Nein. Sie erhalten weiterhin die Vorteile der Berechtigungspakete, die Sie zuvor gekauft haben.

### Warum sehe ich für mein Gesamtdatenvolumen einen anderen Wert als für meine Berechtigung für den Profilspeicher?

Das Gesamtdatenvolumen stellt die **gesamte** Datenmenge dar, die für Profil zur Verwendung in Interaktions-Workflows verfügbar ist. Die Messung wurde aktualisiert, um deterministischer und erklärbarer zu sein. Die meisten Benutzer sollten **nicht** eine wesentliche Änderung zwischen ihrem gesamten Datenvolumen und ihrem gesamten Profilspeicher sehen. Wenn Sie Bedenken haben, erstellen Sie bitte ein Ticket bei Ihrem Kundendienstmitarbeiter.

### Wie wird das Gesamtdatenvolumen berechnet? Enthält es Data Lake-Speicher?

Das Gesamtdatenvolumen wird anhand der folgenden Formel berechnet:

**Gesamtdatenvolumen = adressierbare Zielgruppe × durchschnittliche Profilreichhaltigkeit**

Diese Metrik spiegelt die Gesamtmenge der im Profilspeicher gespeicherten Daten wider, die für das Echtzeit-Kundenprofil zur Verwendung in Interaktions-Workflows verfügbar ist. Es **keine** im Data Lake gespeicherten Daten enthalten.

Zuvor verwendeten einige ältere Angebote die Metrik „Gesamtspeicher“, die sowohl die Nutzung des Profilspeichers als auch des Data Lake kombinierte. Das gesamte Datenvolumen ist jedoch auf den Profilspeicher beschränkt und bietet eine fokussiertere Ansicht der Daten, die für die profilbasierte Interaktion relevant sind.

### Muss ich meine Änderungen neu erstellen, um meine durchschnittliche Reichweite des Profils weiterhin zu verwalten?

Nein. Alle Aktionen wie Filtern, Deaktivieren von Profilen für Datensätze sowie das Einrichten von Gültigkeitsdauern von Erlebnisereignissen und Ablauf von Daten pseudonymer Profile spielen weiterhin eine Rolle bei der Verwaltung des gesamten Datenvolumens.

### Warum hat die Größe der in die Sandbox aufgenommenen Datei eine andere als das gesamte Datenvolumen?

Das Profil optimiert Daten für eine schnelle Verarbeitung, um die Personalisierungs- und Interaktions-Workflows auszuführen, für die das System entwickelt wurde. Die Dateigröße auf der Client-Seite kann sich vom gesamten Datenvolumen unterscheiden, da Faktoren wie die Art der Kodierung, Komprimierung und das Format eine Rolle spielen.

### Gilt diese Änderung für SKUs, die sowohl für Profil als auch für Data Lake ein gemeinsames Limit haben?

Kunden, die SKUs verwenden, bei denen für Profil und Data Lake das Kriterium „Durchschnittlicher Profilreichhaltigkeit“ verwendet wurde, sehen weiterhin die Metrik „Total Consumed Storage“ und **nicht** die Metrik „Durchschnittlicher Profilreichhaltigkeit“.
