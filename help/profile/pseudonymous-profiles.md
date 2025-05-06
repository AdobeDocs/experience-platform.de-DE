---
keywords: Experience Platform;Startseite;beliebte Themen;Datensatz;Datensatz;Live-Zeit;ttl;Time-to-Live;pseudonym;pseudonyme Profile;Datenablauf;Ablauf;
solution: Experience Platform
title: Ablauf von Daten pseudonymer Profile
description: Dieses Dokument enthält allgemeine Anleitungen zum Konfigurieren des Ablaufs von Daten pseudonymer Profile in Adobe Experience Platform.
exl-id: e8d31718-0b50-44b5-a15b-17668a063a9c
source-git-commit: 8734b85914d965eebc2f8ccd8c09dd1ffede8cf9
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 50%

---

# Ablauf von Daten pseudonymer Profile

In Adobe Experience Platform können Sie Datenablaufzeiten für pseudonyme Profile konfigurieren, sodass Sie automatisch Daten aus dem Profilspeicher entfernen können, die für Ihre Anwendungsfälle nicht mehr gültig oder nützlich sind.

## Pseudonymes Profil {#pseudonymous-profile}

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile"
>title="Was ist ein pseudonymes Profil?"
>abstract="Ein pseudonymes Profil ist ein Profil mit einem pseudonymen oder unbekannten Identity-Namespace oder ein Profil, bei dem während eines bestimmten Zeitraums keine Aktivität ausgeführt wurde."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile_dataexpiration"
>title="Ablaufen pseudonymer Profildaten"
>abstract="Ablauf von Daten pseudonymer Profile gibt die Anzahl der Tage an, die ein pseudonymes Profil in Adobe Experience Platform verbleibt, bevor es entfernt wird. Dieser Wert muss auf mindestens 1 gesetzt werden. Beachten Sie, dass es bis zu drei Tage dauern kann, bis das pseudonyme Profil entfernt wird."

Ein Profil kommt für den Ablauf von pseudonymen Daten infrage, wenn es die folgenden Bedingungen erfüllt:

- Die Identity-Namespaces des zugeordneten Profils stimmen mit denen überein, die der Kunde als pseudonymen oder unbekannten Identity-Namespace angegeben hat.
   - Wenn beispielsweise der Identity-Namespace des Profils `ECID`, `GAID` oder `AAID` ist. Das zusammengefügte Profil hat keine IDs aus einem anderen Identity-Namespace. In diesem Beispiel hat ein zusammengefügtes Profil **keine** E-Mail- oder CRM-Identität.
- In einem benutzerdefinierten Zeitraum hat keine Aktivität stattgefunden. Aktivität wird entweder durch alle erfassten Erlebnisereignisse oder durch von Kunden initiierte Aktualisierungen der Profilattribute definiert.
   - Beispielsweise wird ein neues Seitenansichtsereignis oder eine Aktualisierung des Seitenattributs als Aktivität angesehen. Eine nicht von Benutzenden initiierte Aktualisierung der Zielgruppenzugehörigkeit wird jedoch **nicht** als Aktivität angesehen. Zur Berechnung des Datenablaufs basiert das Tracking auf Profilebene derzeit für Erlebnisereignisse auf dem Zeitpunkt des Ereignisses und für Profilattribute auf dem Zeitpunkt der Aufnahme.

## Zugriff {#access}

>[!AVAILABILITY]
>
>Um auf diese Funktion zugreifen zu können, benötigen Sie die folgenden Berechtigungen:
>
>- Profileinstellungen verwalten
>- Anzeigen von Profilen
>- Anzeigen von Identitäts-Namensräumen
>
>Mit der Berechtigung **Profileinstellungen verwalten** können Sie die Gültigkeitsdauern von Daten festlegen, mit der Berechtigung **Profile anzeigen** können Sie die Gültigkeitsdauern von Daten anzeigen und mit der Berechtigung **Identity-Namespaces anzeigen** können Sie die verfügbaren Identity-Namespaces anzeigen, die Sie verwenden können.
>
>Weitere Informationen zu Berechtigungen in Experience Platform finden Sie unter [Zugriffssteuerung - Übersicht](../access-control/home.md#permissions).

Um Ablauf von Daten pseudonymer Profile zu Ihrer Organisation hinzuzufügen, gehen Sie zum Profil-Dashboard und wählen Sie **[!UICONTROL Einstellungen]** aus.

![Die Schaltfläche „Einstellungen“ im Profil-Dashboard ist hervorgehoben.](./images/pseudonymous-profiles/profile-settings.png)

Das [!UICONTROL Profileinstellungen] wird angezeigt. In diesem Popover können Sie die Anzahl der Tage für den Ablauf von Daten pseudonymer Profile sowie den Identity-Namespace festlegen, der für den Ablauf von Daten verwendet wird.

Bei Produktions-Sandboxes beträgt der standardmäßige Ablauf von Daten pseudonymer Profile 14 Tage, wobei der Mindestzeitraum 1 Tag und der Höchstzeitraum 365 Tage beträgt. Bei Entwicklungs-Sandboxes beträgt der standardmäßige Ablauf von Daten pseudonymer Profile 3 Tage, wobei der Mindestzeitraum 1 Tag und der Höchstzeitraum 365 Tage beträgt.

Wählen Sie **[!UICONTROL Anwenden]**, um Ihre Einstellungen für den Datenablauf zu speichern.

![Das Popover zum Hinzufügen von Ablauf von Daten pseudonymer Profile zu den Profilen Ihres Unternehmens. Die Schaltfläche „Anwenden“ ist hervorgehoben.](./images/pseudonymous-profiles/profile-settings-data-expiry.png){width="800" zoomable="yes"}

## Häufig gestellte Fragen {#faq}

Im folgenden Abschnitt finden Sie häufig gestellte Fragen zu Ablauf von Daten pseudonymer Profile:

### Wie unterscheidet sich Ablauf von Daten pseudonymer Profile vom Ablauf von Erlebnisereignisdaten?

+++ Antwort

Ablauf von Daten pseudonymer Profile und Ablauf von Erlebnisereignisdaten sind komplementäre Funktionen.

#### Granularität

Ablauf von Daten pseudonymer Profile funktioniert auf **Sandbox**-Ebene. Das bedeutet, dass sich der Ablauf von Daten auf alle Profile in der Sandbox auswirkt.

Ablauf von Erlebnisereignisdaten funktioniert auf **Datensatz**-Ebene. Daher kann jeder Datensatz eine andere Datenablaufeinstellung haben.

#### Identitätstypen

Ablauf von Daten pseudonymer Profile berücksichtigt **nur** Profile mit Identitätsdiagrammen, die vom Kunden ausgewählte Identity-Namespaces enthalten, z. B. `ECID`, `AAID` oder andere Arten von Cookies. Wenn das Profil **irgendeine Art von** zusätzlichen Identity-Namespaces hat, die **nicht** in der ausgewählten Liste des Kunden waren, wird das Profil **nicht** gelöscht.

Ablauf von Erlebnisereignisdaten entfernt Ereignisse **nur** basierend auf dem Zeitstempel des Ereignisdatensatzes. Die darin enthaltenen Identity-Namespaces werden für den Zweck des Datenablaufs **ignoriert**.

#### Entfernte Elemente

Ablauf von Daten pseudonymer Profile entfernt Ereignis- **und** Profildatensätze. Daher werden auch die Profilklassendaten entfernt.

Ablauf von Erlebnisereignisdaten entfernt **nur** Ereignisse, **keine** Profilklassendaten. Die Profilklassendaten werden nur entfernt, wenn alle Daten über **alle** Datensätze hinweg entfernt werden und es **keine** Profilklassendatensätze gibt, die für das Profil verbleiben.

+++

### Wie kann Ablauf von Daten pseudonymer Profile in Verbindung mit Ablauf von Erlebnisereignisdaten verwendet werden?

+++ Antwort

Ablauf von Daten pseudonymer Profile und Ablauf von Erlebnisereignisdaten können sich gegenseitig ergänzen.

Sie sollten **immer** Ablauf von Erlebnisereignisdaten in Ihren Datensätzen eingerichtet haben, je nach Ihrem Aufbewahrungsbedarf für die Daten Ihrer bekannten Kunden. Sobald Ablauf von Erlebnisereignisdaten eingerichtet ist, können Sie Ablauf von Daten pseudonymer Profile verwenden, um pseudonyme Profile automatisch zu entfernen. In der Regel ist der Datenablaufzeitraum für pseudonyme Profile kürzer als der Datenablaufzeitraum für Erlebnisereignisse.

Für einen typischen Anwendungsfall können Sie den Ablauf von Erlebnisereignisdaten auf der Grundlage der Werte Ihrer bekannten Benutzerdaten festlegen und den Ablauf von Daten pseudonymer Profile auf eine viel kürzere Dauer festlegen, um die Auswirkungen pseudonymer Profile auf die Einhaltung Ihrer Experience Platform-Lizenzverträge zu begrenzen.

+++

### Für welche Arten von Anwendungsfällen sollte ich Ablauf von Daten pseudonymer Profile verwenden?

+++ Antwort

- Wenn Sie Web SDK verwenden, um Daten direkt an Experience Platform zu senden.
- Wenn Sie eine Website haben, die nicht-authentifizierte Kundinnen und Kunden en masse bedient.
- Wenn Sie in Ihren Datensätzen eine übermäßige Anzahl an Profilen haben und bestätigt haben, dass diese auf Identity-Namespaces zurückzuführen sind, die auf anonymen Cookies basieren.
   - Um dies zu bestimmen, sollten Sie den Bericht zur Überschneidung von Identity-Namespaces verwenden. Weitere Informationen zu diesem Bericht finden Sie im [Berichtabschnitt zur Identitätsüberschneidung](./api/preview-sample-status.md#identity-overlap-report) im Handbuch für die Vorschau der Beispiel-Status-API.

+++

### Welche Einschränkungen sollten Sie beachten, bevor Sie Ablauf von Daten pseudonymer Profile verwenden?

+++ Antwort

- Der Ablauf von Daten pseudonymer Profile erfolgt auf **Sandbox**-Ebene. Sie können unterschiedliche Konfigurationen für Produktions- und Entwicklungs-Sandboxes auswählen.
- Wenn Sie diese Funktion aktiviert haben, wird das Löschen von Profilen **dauerhaft**. Es gibt **keine** Möglichkeit, die gelöschten Profile zurückzusetzen oder wiederherzustellen.
- Dies ist **kein** einmaliger Bereinigungsvorgang. Ablauf von Daten pseudonymer Profile wird einmal täglich ausgeführt und löscht Profile, die mit der Eingabe des Kunden übereinstimmen.
- **Alle** Profile, die als pseudonyme Profile definiert sind, sind von Ablauf von Daten pseudonymer Profile betroffen. Es kommt dabei **nicht** darauf an, ob das Profil nur ein Erlebnisereignis ist oder nur Profilattribute enthält.
- Diese Bereinigung findet **nur** im Profil statt. Identity Service kann die gelöschten Identitäten innerhalb des Diagramms nach der Bereinigung weiterhin anzeigen, wenn das Profil zwei oder mehr pseudonyme Identitäten aufweist (z. B. `AAID` und `ECID`). Diese Diskrepanz wird in naher Zukunft angegangen.
- Ablauf von Daten pseudonymer Profile **nicht** sofort ausgeführt und kann bis zu drei Tage dauern, bis sie verarbeitet werden.

+++

### Wie interagiert Ablauf von Daten pseudonymer Profile mit Leitplanken für Identity Service-Daten?

+++ Antwort

- Das Identity Service-[ „first-in, first-out“-Löschsystem ](../identity-service/guardrails.md) ECIDs aus dem Identitätsdiagramm löschen, die in Identity Service gespeichert sind.
- Wenn dieses Löschverhalten dazu führt, dass ein Nur-ECID-Profil im Echtzeit-Kundenprofil (Profilspeicher) gespeichert wird, wird dieses Profil nach Ablauf von Daten pseudonymer Profile aus dem Profilspeicher gelöscht.

+++

## Nächste Schritte

Nach dem Lesen dieses Handbuchs wissen Sie, wie Sie Ablauf von Daten pseudonymer Profile anzeigen und erstellen können. Weitere Informationen zum Daten-Management für Experience Platform als Ganzes finden Sie im [Handbuch zu Best Practices für die Verwaltung von Datenlizenzen](../landing/license-usage-and-guardrails/data-management-best-practices.md).

