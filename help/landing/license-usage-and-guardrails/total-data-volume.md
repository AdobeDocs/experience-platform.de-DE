---
title: Metrik "Datenvolumen insgesamt"
description: Erfahren Sie mehr über die neue Metrik "Datenvolumen insgesamt"und wie sie die Metrik für den vorherigen durchschnittlichen Profilumfang ersetzt.
hide: true
hidefromtoc: true
source-git-commit: 9aba85d4e5a481b0eff53e1d87311c395934f585
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---


# Metrik &quot;Datenvolumen insgesamt&quot;

Ab dem 24. September 2024 ersetzt die Metrik Datenvolumen insgesamt die vorherige Metrik der durchschnittlichen Profilreichweite.

Das Datenvolumen insgesamt stellt die Gesamtdatenmenge dar, die für das Echtzeit-Kundenprofil von Adobe Experience Platform zur Verwendung in Interaktionsarbeitsabläufen verfügbar ist. Dieser Wert entspricht der Metrik Addressable Audience , multipliziert mit der durchschnittlichen Profilreichweite.

## Häufig gestellte Fragen {#faq}

Im folgenden Abschnitt finden Sie häufig gestellte Fragen zu diesem Update.

### Warum wurde diese Änderung vorgenommen?

Diese Änderung wurde vorgenommen, um die Einhaltung der Lizenzberechtigungsmetriken zu vereinfachen. Wir haben oft von Kunden gehört, dass es für sie schwierig ist, die Reichweite des durchschnittlichen Profils zu verstehen und zu bewältigen. Mit dieser Änderung hoffen wir, dass Sie Ihre lizenzierte Nutzung des Echtzeit-Kundenprofils besser verstehen und verwalten können.

### Ändert diese Änderung der Metrik meine Berechtigung für den Profilspeicher?

Nein. Ihre Berechtigung für den Profilspeicher bleibt unverändert, da das Datenvolumen insgesamt der ansprechbaren Zielgruppe entspricht, multipliziert mit Ihrer berechtigten durchschnittlichen Profilreichweite.

### Hat diese Änderung Auswirkungen auf die von mir gekauften Berechtigungspakete?

Nein. Sie erhalten weiterhin die Vorteile der Berechtigungspakete, die Sie zuvor gekauft haben.

### Wie kommt es, dass ich einen anderen Wert für mein Gesamtdatenvolumen im Vergleich zu meiner Profilspeicher-Berechtigung sehe?

Gesamtdatenvolumen stellt die **Gesamtsumme** an Daten dar, die für Profile zur Verwendung in Interaktions-Workflows verfügbar sind. Die Messung wurde aktualisiert, um deterministischer und erklärbarer zu werden. Die meisten Benutzer sollten **nicht** eine signifikante Änderung zwischen ihrem Gesamtdatenvolumen und ihrem gesamten Profilspeicher sehen. Wenn Sie Bedenken haben, wenden Sie sich bitte an Ihren Kundendienstmitarbeiter.

### Muss ich meine Änderungen neu erstellen, um weiterhin meine durchschnittliche Profilreichweite zu verwalten?

Nein. Alle Aktionen wie Filtern, Deaktivieren des Profils für Datensätze sowie Einrichten von Erlebnisereignisabläufen und pseudonymen Profildatenabläufen spielen weiterhin eine Rolle bei der Verwaltung des Gesamtdatenvolumens.

### Warum ist die Datei, die ich in die Sandbox aufgenommen habe, im Vergleich zum Gesamtdatenvolumen unterschiedlich groß?

Profil optimiert Daten für eine schnelle Verarbeitung, um die Personalisierungs- und Interaktionsarbeitsabläufe auszuführen, für die das System entwickelt wurde. Die Dateigröße auf Client-Seite kann sich aufgrund von Faktoren wie Kodierung, Komprimierung und Format vom Gesamtdatenvolumen unterscheiden.

### Gilt diese Änderung für SKUs, die über eine gemeinsame Beschränkung für Profil und Data Lake verfügen?

Kunden mit SKUs, die die Durchschnittliche Profilgenauigkeit zwischen Profil und Data Lake gemeinsam haben, sehen weiterhin die Metrik Gesamtnutzte Datenspeicherung und sehen **nicht** die Metrik Durchschnittliche Profilreichweite .
