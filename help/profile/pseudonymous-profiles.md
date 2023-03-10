---
keywords: Experience Platform; Startseite; beliebte Themen; Datensatz; Datensatz; Live-Zeit; ttl; Time-to-Live; pseudonyme; pseudonyme Profile; Datenablauf; Ablauf;
solution: Experience Platform
title: Pseudonyme Profildaten - Ablauf
description: Dieses Dokument enthält allgemeine Anleitungen zum Konfigurieren des Datenablaufs für Pseudonyme Profile in Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: a6173860adda4bd71c94750e5cce6dd4cbe820c6
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---


# Datenablauf bei Pseudonymen Profilen [!BADGE Eingeschränkte Veröffentlichung]

In Adobe Experience Platform wird ein Profil für den Ablauf von Pseudonymen Daten berücksichtigt, wenn es die folgenden Bedingungen erfüllt:

- Die Identitätstypen des zugeordneten Profils stimmen mit denen überein, die der Kunde als pseudonymen oder unbekannten Identitätstyp angegeben hat.
   - Wenn der Identitätstyp des Profils beispielsweise `ECID`, `GAID`oder `AAID`. Das zugeordnete Profil hat keine IDs eines anderen Identitätstyps. In diesem Beispiel wird ein zugeordnetes Profil **not** entweder eine E-Mail- oder eine CRM-Identität aufweisen.
- In einem benutzerdefinierten Zeitraum hat keine Aktivität stattgefunden. Aktivität wird entweder durch alle erfassten Erlebnisereignisse oder durch Kunden initiierte Aktualisierungen der Profilattribute definiert.
   - Beispielsweise wird ein neues Seitenansichtsereignis oder eine Aktualisierung des Seitenattributs als Aktivität betrachtet. Eine nicht vom Benutzer initiierte Aktualisierung der Segmentmitgliedschaft ist jedoch **not** als Aktivität betrachtet werden. Zur Berechnung des Datenablaufs basiert das Tracking auf Profilebene derzeit auf dem Zeitpunkt der Erfassung.

## Zugriff auf {#access}

Der Ablauf der pseudonymen Profildaten kann nicht über die Platform-Benutzeroberfläche oder APIs konfiguriert werden. Stattdessen müssen Sie sich an den Support wenden, um diese Funktion zu aktivieren. Bitte geben Sie bei der Kontaktaufnahme mit dem Support die folgenden Informationen an:

- Die Identitätstypen, die für das Löschen eines Pseudonymen Profils berücksichtigt werden sollen.
   - Beispiel: `ECID` nur `AAID` nur oder eine Kombination aus `ECID` und `AAID`.
- Die Wartezeit vor dem Löschen eines pseudonymen Profils. Die Standardempfehlung für Kunden beträgt 14 Tage. Dieser Wert kann jedoch je nach Anwendungsfall unterschiedlich sein.
- Die aktuelle Profilanzahl im Vergleich zur Lizenzprofilanzahl.

## Häufig gestellte Fragen {#faq}

Im folgenden Abschnitt finden Sie häufig gestellte Fragen zum Ablauf der Daten von Pseudonymen Profilen:

### Welche Benutzer sollten das Ablaufdatum der Pseudonymen Profildaten verwenden?

- Wenn Sie eine Streaming-Quelle verwenden, die direkt Daten an Platform sendet.
- Wenn Sie eine Website haben, die nicht authentifizierte Kunden en masse bereitstellt.
- Wenn Sie in Ihren Datensätzen übermäßige Profilzahlen haben und bestätigt haben, dass diese übermäßige Profilanzahl auf einem anonymen Cookie-basierten Identitätstyp basiert.
   - Um dies zu ermitteln, sollten Sie den Bericht zur Identitätstypüberschneidung verwenden. Weitere Informationen zu diesem Bericht finden Sie im [Berichtabschnitt zur Identitätsüberschneidung](./api/preview-sample-status.md#identity-overlap-report) im Beispiel-Status-API-Handbuch für die Vorschau.

### Welche Einschränkungen sollten Sie beachten, bevor Sie die Datengültigkeit von Pseudonymen-Profilen verwenden?

- Der Ablauf der pseudonymen Profildaten wird auf der **production** Sandbox.
- Nachdem Sie diese Funktion aktiviert haben, wird das Löschen von Profilen **dauerhaft**. Es gibt **no** Möglichkeit zur Zurücksetzung oder Wiederherstellung der gelöschten Profile.
- Dies ist **not** einen einmaligen Bereinigungsauftrag. Der Ablauf der pseudonymen Profildaten wird täglich einmal ausgeführt und Profile gelöscht, die mit der Eingabe des Kunden übereinstimmen.
- **Alle** Profile, die als Pseudonyme Profile definiert sind, werden vom Ablauf der Profildaten für Pseudonyme beeinflusst. Sie **not** ist wichtig, ob das Profil nur Erlebnisereignis ist oder nur Profilattribute enthält.
- Diese Bereinigung wird **only** im Profil angezeigt werden. Identity Service kann die gelöschten Identitäten innerhalb des Diagramms nach der Bereinigung weiterhin anzeigen, wenn das Profil zwei oder mehr Pseudonyme Identitäten aufweist (z. B. `AAID` und `ECID`). Diese Diskrepanz wird in naher Zukunft angegangen werden.

### Wie unterscheidet sich das Ablaufdatum von Pseudonymen Profildaten vom Ablauf der vorhandenen Erlebnisereignisdaten?

Pseudonyme Profildaten ablaufen und Erlebnisereignis-Datenablauf sind komplementäre Funktionen.

#### Granularität

Der Ablauf von Erlebnisereignisdaten funktioniert auf einer **Datensatz** Ebene. Daher kann jeder Datensatz eine andere Datenablaufeinstellung haben.

Der Ablauf von Pseudonymen Profildaten funktioniert in einer **Sandbox** Ebene. Das bedeutet, dass sich die Datengültigkeit auf alle Profile in der Sandbox auswirkt.

#### Identitätstypen

Datenablauf für Erlebnisereignisse entfernt Ereignisse **only** basierend auf dem Zeitstempel des Ereignisdatensatzes. Die enthaltenen Identitätstypen sind **Ignoriert** für Ablaufzwecke.

Pseudonyme Profildaten - Ablauf **only** berücksichtigt Profile mit Identitätsdiagrammen, die vom Kunden ausgewählte Identitätstypen enthalten, z. B. `ECID`, `AAID`oder andere Cookie-Typen. Wenn das Profil **any** zusätzlicher Identitätstyp, der **not** in der ausgewählten Liste des Kunden wird das Profil **not** gelöscht werden.

#### Entfernte Elemente

Ablauf der Erlebnisereignisdaten **only** entfernt Ereignisse und führt Aktionen aus **not** Entfernen von Profilklassendaten. Die Profilklassendaten werden nur entfernt, wenn alle Daten über **all** -Datensätze und es gibt **no** Profilklassendatensätze, die für das Profil verbleiben.

Pseudonyme Profildaten werden entfernt **both** Ereignis- und Profildatensätze. Daher werden auch die Profilklassendaten entfernt.

### Wie kann das Ablaufdatum von Pseudonymen Profildaten in Verbindung mit dem Ablauf von Erlebnisereignisdaten verwendet werden?

Pseudonyme Profildaten ablaufen und Erlebnisereignis-Datenablauf können als Ergänzung verwendet werden.

Sie sollten **always** richten Sie den Ablauf von Erlebnisereignis-Daten in Ihren Datensätzen ein, basierend auf Ihren Anforderungen, Daten über Ihre bekannten Kunden zu speichern. Sobald der Ablauf der Erlebnisereignisdaten eingerichtet ist, können Sie mit dem Ablauf der pseudonymen Profildaten automatisch Pseudonyme Profile entfernen. In der Regel liegt der Datenablaufzeitraum für Pseudonyme Profile unter dem Datenablaufzeitraum für Erlebnisereignisse.

Für einen typischen Anwendungsfall können Sie das Ablaufdatum Ihrer Erlebnisereignisdaten auf der Grundlage der Werte Ihrer bekannten Benutzerdaten festlegen und Ihren Pseudonymen Profildaten eine wesentlich kürzere Gültigkeit geben, um die Auswirkungen von Pseudonymen Profilen auf die Einhaltung Ihrer Plattformlizenzverträge zu begrenzen.
