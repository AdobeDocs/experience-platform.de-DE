---
keywords: Experience Platform;Startseite;beliebte Themen;Datensatz;Datensatz;Live-Zeit;ttl;Time-to-Live;pseudonym;pseudonyme Profile;Datenablauf;Ablauf;
solution: Experience Platform
title: Ablauf von Daten pseudonymer Profile
description: Dieses Dokument enthält allgemeine Anleitungen zum Konfigurieren des Ablaufs von Daten pseudonymer Profile in Adobe Experience Platform.
exl-id: e8d31718-0b50-44b5-a15b-17668a063a9c
source-git-commit: 07ed7eb9644b2e8cc4da02743c48037afc247614
workflow-type: ht
source-wordcount: '912'
ht-degree: 100%

---

# Ablauf von Daten pseudonymer Profile

In Adobe Experience Platform können Sie Ablaufzeiten für pseudonyme Profile konfigurieren, sodass Sie automatisch Daten aus dem Profilspeicher entfernen lassen können, die für Ihre Anwendungsfälle nicht mehr gültig oder nützlich sind.

## Pseudonymes Profil {#pseudonymous-profile}

Ein Profil kommt für den Ablauf von pseudonymen Daten infrage, wenn es die folgenden Bedingungen erfüllt:

- Die Identity-Namespaces des zugeordneten Profils stimmen mit denen überein, die der Kunde als pseudonymen oder unbekannten Identity-Namespace angegeben hat.
   - Wenn beispielsweise der Identity-Namespace des Profils `ECID`, `GAID` oder `AAID` ist. Das zusammengefügte Profil hat keine IDs aus einem anderen Identity-Namespace. In diesem Beispiel hat ein zusammengefügtes Profil **keine** E-Mail- oder CRM-Identität.
- In einem benutzerdefinierten Zeitraum hat keine Aktivität stattgefunden. Aktivität wird entweder durch alle erfassten Erlebnisereignisse oder durch von Kunden initiierte Aktualisierungen der Profilattribute definiert.
   - Beispielsweise wird ein neues Seitenansichtsereignis oder eine Aktualisierung des Seitenattributs als Aktivität angesehen. Eine nicht vom Benutzer initiierte Aktualisierung der Segmentzugehörigkeit wird jedoch **nicht** als Aktivität angesehen. Zur Berechnung des Datenablaufs basiert das Tracking auf Profilebene derzeit für Erlebnisereignisse auf dem Zeitpunkt des Ereignisses und für Profilattribute auf dem Zeitpunkt der Aufnahme.

## Zugriff auf {#access}

Ablauf von Daten pseudonymer Profile kann nicht über die Platform-Benutzeroberfläche oder APIs konfiguriert werden. Stattdessen müssen Sie sich an den Support wenden, um diese Funktion zu aktivieren. Bitte geben Sie bei der Kontaktaufnahme mit dem Support die folgenden Informationen an:

- Die Identity-Namespaces, die für das Löschen eines pseudonymen Profils berücksichtigt werden sollen.
   - Beispiel: Nur `ECID`, nur `AAID` oder eine Kombination aus `ECID` und `AAID`.
- Die Wartezeit, bevor ein pseudonymes Profil gelöscht wird. Die Standardempfehlung für Kunden beträgt 14 Tage. Dieser Wert kann jedoch je nach Anwendungsfall unterschiedlich sein.

## Häufig gestellte Fragen {#faq}

Im folgenden Abschnitt finden Sie häufig gestellte Fragen zu Ablauf von Daten pseudonymer Profile:

### Wie unterscheidet sich Ablauf von Daten pseudonymer Profile vom Ablauf von Erlebnisereignisdaten?

Ablauf von Daten pseudonymer Profie und Ablauf von Erlebnisereignisdaten sind komplementäre Funktionen.

#### Granularität

Ablauf von Daten pseudonymer Profile funktioniert auf **Sandbox**-Ebene. Das bedeutet, dass sich der Ablauf von Daten auf alle Profile in der Sandbox auswirkt.

Ablauf von Erlebnisereignisdaten funktioniert auf **Datensatz**-Ebene. Daher kann jeder Datensatz eine andere Datenablaufeinstellung haben.

#### Identitätstypen

Ablauf von Daten pseudonymer Profile berücksichtigt **nur** Profile mit Identitätsdiagrammen, die vom Kunden ausgewählte Identity-Namespaces enthalten, z. B. `ECID`, `AAID` oder andere Arten von Cookies. Wenn das Profil **irgendeine Art von** zusätzlichen Identity-Namespaces hat, die **nicht** in der ausgewählten Liste des Kunden waren, wird das Profil **nicht** gelöscht.

Ablauf von Erlebnisereignisdaten entfernt Ereignisse **nur** basierend auf dem Zeitstempel des Ereignisdatensatzes. Die darin enthaltenen Identity-Namespaces werden für den Zweck des Datenablaufs **ignoriert**.

#### Entfernte Elemente

Ablauf von Daten pseudonymer Profile entfernt Ereignis- **und** Profildatensätze. Daher werden auch die Profilklassendaten entfernt.

Ablauf von Erlebnisereignisdaten entfernt **nur** Ereignisse, **keine** Profilklassendaten. Die Profilklassendaten werden nur entfernt, wenn alle Daten über **alle** Datensätze hinweg entfernt werden und es **keine** Profilklassendatensätze gibt, die für das Profil verbleiben.

### Wie kann Ablauf von Daten pseudonymer Profile in Verbindung mit Ablauf von Erlebnisereignisdaten verwendet werden?

Ablauf von Daten pseudonymer Profile und Ablauf von Erlebnisereignisdaten können ergänzend zueinander verwendet werden.

Sie sollten **immer** Ablauf von Erlebnisereignisdaten in Ihren Datensätzen eingerichtet haben, je nach Ihrem Aufbewahrungsbedarf für die Daten Ihrer bekannten Kunden. Wenn Ablauf von Erlebnisereignisdaten eingerichtet ist, können Sie Ablauf von Daten pseudonymer Profile verwenden, um pseudonyme Profile automatisch zu entfernen. In der Regel ist der Datenablaufzeitraum für pseudonyme Profile kürzer als der Datenablaufzeitraum für Erlebnisereignisse.

Für einen typischen Anwendungsfall können Sie den Ablauf von Erlebnisereignisdaten auf der Grundlage der Werte von Daten Ihrer bekannten Benutzer festlegen und für Ablauf von Daten pseudonymer Profile eine wesentlich kürzere Dauer wählen, um die Auswirkungen von pseudonymen Profilen auf die Einhaltung Ihrer Platform-Lizenzverträge zu begrenzen.

### Wann sollten Benutzer Ablauf von Daten pseudonymer Profile verwenden?

- Wenn Sie das Web SDK verwenden, um Daten direkt an Platform zu senden.
- Wenn Sie eine Website haben, die nicht-authentifizierte Kundinnen und Kunden en masse bedient.
- Wenn Sie in Ihren Datensätzen eine übermäßige Anzahl an Profilen haben und bestätigt haben, dass diese auf Identity-Namespaces zurückzuführen sind, die auf anonymen Cookies basieren.
   - Um dies zu bestimmen, sollten Sie den Bericht zur Überschneidung von Identity-Namespaces verwenden. Weitere Informationen zu diesem Bericht finden Sie im [Berichtabschnitt zur Identitätsüberschneidung](./api/preview-sample-status.md#identity-overlap-report) im Handbuch für die Vorschau der Beispiel-Status-API.

### Welche Einschränkungen sollten Sie beachten, bevor Sie Ablauf von Daten pseudonymer Profile verwenden?

- Ablauf von Daten pseudonymer Profile läuft auf der **Produktions**-Sandbox.
- Wenn Sie diese Funktion aktiviert haben, wird das Löschen von Profilen **dauerhaft**. Es gibt **keine** Möglichkeit, die gelöschten Profile zurückzusetzen oder wiederherzustellen.
- Dies ist **kein** einmaliger Bereinigungsvorgang. Ablauf von Daten pseudonymer Profile wird täglich einmal ausgeführt und es werden dabei Profile gelöscht, die mit der Eingabe der Kundin bzw. des Kunden übereinstimmen.
- **Alle** Profile, die als pseudonyme Profile definiert sind, sind von Ablauf von Daten pseudonymer Profile betroffen. Es kommt dabei **nicht** darauf an, ob das Profil nur ein Erlebnisereignis ist oder nur Profilattribute enthält.
- Diese Bereinigung findet **nur** im Profil statt. Identity Service kann die gelöschten Identitäten innerhalb des Diagramms nach der Bereinigung weiterhin anzeigen, wenn das Profil zwei oder mehr pseudonyme Identitäten aufweist (z. B. `AAID` und `ECID`). Diese Diskrepanz wird in naher Zukunft angegangen.

