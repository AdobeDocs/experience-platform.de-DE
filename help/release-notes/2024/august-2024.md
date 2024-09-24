---
title: Adobe Experience Platform – Versionshinweise August 2024
description: Versionshinweise August 2024 für Adobe Experience Platform.
exl-id: 153891e9-fd82-4894-a047-c8d82f214fef
source-git-commit: 4fecb47084a522b4eb9808dc317e0d70e7ef42c6
workflow-type: ht
source-wordcount: '1562'
ht-degree: 100%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 20. August 2024**

>[!TIP]
>
>Sehen Sie sich einen [Überblick der Dokumentation zu Beispielanwendungsfällen](https://experienceleague.adobe.com/de/docs/experience-platform/rtcdp/use-cases/overview) an, um mehr über verschiedene Anwendungsfälle wie Kundengewinnung und Akquise zu erfahren, die Ihr Unternehmen mit Real-Time CDP erreichen kann.

Aktualisierungen vorhandener Funktionen und Dokumentation in Experience Platform:

- [Attributbasierte Zugriffssteuerung](#abac)
- [Datenaufnahme](#data-ingestion)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Identity Service](#identity-service)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Attributbasierte Zugriffssteuerung {#abac}

Die attributbasierte Zugriffssteuerung ist eine Funktion von Adobe Experience Platform, die datenschutzbewussten Marken größere Flexibilität bei der Verwaltung von Benutzerzugriffen gibt. Einzelne Objekte wie Schemafelder und Segmente können Benutzerrollen zugewiesen werden. Mit dieser Funktion können Sie bestimmten Platform-Benutzenden in Ihrer Organisation den Zugriff auf einzelne Objekte gewähren oder sperren.

Mit der attributbasierten Zugriffssteuerung können Admins Ihres Unternehmens den Zugriff von Benutzenden auf sensible persönliche Daten (SPD), persönlich identifizierbare Informationen (PII) und andere benutzerdefinierte Datentypen in allen Workflows und Ressourcen von Platform steuern. Admins können Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.

**Neue Funktion**

| Funktionsaktualisierung | Beschreibung |
| --- | --- |
| Neue Funktion „Berechtigungs-Manager“ | Sie können jetzt den [Berechtigungs-Manager](../../access-control/abac/permission-manager/overview.md) verwenden, um Berichte mithilfe einfacher Abfragen zu erstellen. Dies hilft Ihnen, die Zugriffsverwaltung zu verstehen und Zeit zu sparen, indem Sie Zugriffsberechtigungen für mehrere Workflows und Granularitätsebenen überprüfen. Weitere Informationen zum Erstellen von Berichten für Benutzende und Rollen finden Sie im [Benutzerhandbuch zum Berechtigungs-Manager](../../access-control/abac/permission-manager/permissions.md). ![Bild der Experience Platform-Benutzeroberfläche, auf dem der Berechtigungs-Manager im linken Navigationsbereich hervorgehoben ist.](assets/august/permission-manager-rn.png "Berechtigungs-Manager in der Benutzeroberfläche."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](../../access-control/abac/overview.md). Eine umfassende Anleitung zum attributbasierten Zugriffssteuerungs-Workflow finden Sie im [Handbuch zur attributbasierten Zugriffskontrolle](../../access-control/abac/end-to-end-guide.md).

## Datenaufnahme (aktualisiert am 23. August) {#data-ingestion}

Adobe Experience Platform bietet eine Vielzahl von Funktionen zur Aufnahme von Datentypen aller Art und beliebiger Latenz. Die Datenaufnahme kann anhand von Batch- oder Streaming-APIs, von Adobe bereitgestellten Quellen, Datenintegrationspartnern oder der Benutzeroberfläche von Adobe Experience Platform erfolgen.

**Aktualisierung der Verarbeitung des Datumsformats bei der Batch-Datenaufnahme**

Diese Version behebt ein Problem mit der *Verarbeitung des Datumsformats* bei der Batch-Datenaufnahme. Zuvor wandelte das System die von den Clients als `Date` eingefügten Datumsfelder in das Format `DateTime` um. Das bedeutet, dass die Zeitzone automatisch zu Feldern hinzugefügt wurde und bei Benutzenden, die das Format `Date` bevorzugen oder benötigen, Schwierigkeiten auftraten. In Zukunft wird die Zeitzone nicht automatisch zu Feldern vom Typ `Date` hinzugefügt. Durch diese Aktualisierung wird sichergestellt, dass das exportierte Datenformat mit dem Format übereinstimmt, das im Profil für dieses Feld angezeigt wird, wie von Kundinnen und Kunden angefordert.

`Date`-Felder vor der Veröffentlichung: `"birthDate": "2018-01-12T00:00:00Z"`
`Date`-Felder nach der Veröffentlichung: `"birthDate": "2018-01-12"`

Lesen Sie mehr über die [Batch-Aufnahme](/help/ingestion/batch-ingestion/overview.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Ziele** {#new-updated-destinations}

| Ziel | Beschreibung |
| ----------- | ----------- |
| [Braze](/help/destinations/catalog/mobile-engagement/braze.md) | [!UICONTROL Braze] verwaltet eine Reihe verschiedener Instanzen für das Dashboard und die REST-Endpunkte. [!UICONTROL Braze]-Kundinnen und -Kunden sollten den richtigen REST-Endpunkt verwenden, je nachdem, für welche Instanz Sie eine Bereitstellung erhalten haben. Diese Version fügt einen neuen US-07-Endpunkt hinzu, den Sie beim Herstellen einer Verbindung zu [!UICONTROL Braze] auswählen können. |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktion | Beschreibung |
| ----------- | ----------- |
| Der Export von Dateien nach Bedarf an Batch-Ziele ist jetzt allgemein verfügbar. | Die Option zum Exportieren von Dateien nach Bedarf an Batch-Ziele ist jetzt für alle Kundinnen und Kunden verfügbar. Weitere Informationen dazu finden Sie in der [dedizierten Dokumentation](../../destinations/ui/export-file-now.md). |
| Bearbeiten Sie Exportpläne für mehrere exportierte Zielgruppen im [Planungsschritt](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | Die Option zum Bearbeiten der Exportpläne für mehrere exportierte Zielgruppen direkt über den Planungsschritt des Workflows von Audience Activation ist jetzt für alle Kundinnen und Kunden verfügbar. ![Bild der Experience Platform-Benutzeroberfläche, auf dem die Option „Zeitplan bearbeiten“ im Planungsschritt hervorgehoben ist.](assets/august/edit-schedule.png "Option „Zeitplan bearbeiten“ im Planungsschritt."){width="250" align="center" zoomable="yes"} |
| Bearbeiten Sie die Dateinamen für mehrere exportierte Zielgruppen im [Planungsschritt](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | Die Option zum Bearbeiten der Namen für mehrere exportierte Dateien direkt über den Planungsschritt des Workflows von Audience Activation ist jetzt für alle Kundinnen und Kunden verfügbar. ![Bild der Experience Platform-Benutzeroberfläche, auf dem die Option „Dateinamen bearbeiten“ im Planungsschritt hervorgehoben ist.](assets/august/edit-file-name.png "Option „Dateinamen bearbeiten“ im Planungsschritt."){width="250" align="center" zoomable="yes"} |
| Entfernen Sie mehrere Zielgruppen aus einem Datenfluss auf der Seite [Zieldetails](../../destinations/ui/destination-details-page.md#bulk-remove). | Die Option zum Entfernen mehrerer Zielgruppen aus vorhandenen Datenflüssen auf der Seite **[!UICONTROL Zieldetails]** ist jetzt für alle Kundinnen und Kunden verfügbar. ![Bild der Experience Platform-Benutzeroberfläche, auf dem die Option „Zielgruppen entfernen“ auf der Seite „Zieldetails“ hervorgehoben ist.](assets/august/bulk-remove-audiences.png "Entfernen Sie die Option „Zielgruppen“ auf der Seite „Zieldetails“."){width="250" align="center" zoomable="yes"} |
| Exportieren Sie mehrere Dateien bei Bedarf auf der Seite [Zieldetails](../../destinations/ui/destination-details-page.md#bulk-export) an Batch-Ziele. | Die Option zum Exportieren mehrerer Dateien nach Bedarf an Batch-Ziele über die Seite **[!UICONTROL Zieldetails]** ist jetzt für alle Kundinnen und Kunden verfügbar. ![Bild der Experience Platform-Benutzeroberfläche, auf dem die Option „Datei jetzt exportieren“ auf der Seite „Zieldetails“ hervorgehoben ist.](assets/august/bulk-export-file-now.png "Option „Datei jetzt exportieren“ auf der Seite „Zieldetails“."){width="250" align="center" zoomable="yes"} |
| Bearbeiten Sie Dateinamen für mehrere exportierte Zielgruppen auf der Seite [Zieldetails](../../destinations/ui/destination-details-page.md#bulk-edit-file-names). | Sie können jetzt die Namen mehrerer exportierter Dateien direkt auf der Seite **[!UICONTROL Zieldetails]** bearbeiten. ![Bild der Experience Platform-Benutzeroberfläche, auf dem die Option „Dateinamen bearbeiten“ auf der Seite „Zieldetails“ hervorgehoben ist.](assets/august/edit-file-name-destination-details.png "Option „Dateinamen bearbeiten“ auf der Seite „Zieldetails“."){width="250" align="center" zoomable="yes"} |
| Entfernen Sie mehrere Datensätze aus einem Datenfluss auf der Seite [Zieldetails](../../destinations/ui/export-datasets.md#remove-dataset). | Die Option zum Entfernen mehrerer Datensätze aus einem Datenfluss ist jetzt für alle Kundinnen und Kunden verfügbar. ![Bild der Experience Platform-Benutzeroberfläche, auf dem die Option „Datensätze entfernen“ auf der Seite „Zieldetails“ hervorgehoben ist.](assets/august/bulk-remove-datasets.png "Option „Datensätze entfernen“ auf der Seite „Zieldetails“."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Lesen Sie für Weitere Informationen den [Überblick über die Ziele](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| ML-gestützter Erstellungsfluss für Schemata | Verwenden Sie erweiterte Algorithmen des maschinellen Lernens, um Ihre Beispieldatendateien zu analysieren und automatisch optimierte Schemata mithilfe von Standard- und benutzerdefinierten Feldern zu erstellen.<br>Wichtigste Funktionen:<br><ul><li>Schnellere Schemaerstellung: Schemata werden direkt aus Beispieldatendateien mithilfe XDM-Feldern generiert, die von ML empfohlen und generiert wurden.</li><li>Flexible Schemaentwicklung: Felder lassen sich ganz einfach im generierten Schema hinzufügen oder aktualisieren.</li><li>Nahtlose Integration: Vollständig in den Erstellungsfluss des Kernschemas in der Schema-Benutzeroberfläche integriert, sodass ein reibungsloses und einheitliches Anwendererlebnis gewährleistet ist.</li><li>Effiziente Überprüfung und Bearbeitung: Schnelles Anzeigen und Aktualisieren Ihres Schemas mit dem Editor für einfache Ansichten, wodurch der Erstellungsprozess effizienter und benutzerfreundlicher wird.</li></ul><br>Weitere Informationen finden Sie im [Handbuch zum Workflow für den ML-gestützten Erstellungsfluss für Schemata](../../xdm/ui/ml-assisted-schema-creation.md). |

{style="table-layout:auto"}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Identity Service {#identity-service}

Verwenden Sie den Adobe Experience Platform Identity Service, um sich einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhaltensweisen zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle und persönliche digitale Erlebnisse sorgen.

**Aktualisierte Dokumentation**

| Funktion | Beschreibung |
| --- | --- |
| Handbuch zu Diagrammkonfigurationen | Informationen zu gängigen Diagrammszenarien, auf die Sie beim Arbeiten mit Regeln zur Verknüpfung von Identitätsdiagrammen und Identitätsdaten stoßen können, finden Sie im [Handbuch für Diagrammkonfigurationen](../../identity-service/identity-graph-linking-rules/example-configurations.md). Das Handbuch zu Diagrammkonfigurationen enthält Beispiele für einfache Diagrammszenarien für eine Person bis hin zu komplexen und hierarchischen Diagrammszenarien für mehrere Personen. Sie können das Handbuch auch für Beispiele von Ereignis- und Algorithmuskonfigurationen verwenden, die Sie in die [Benutzeroberfläche für die Diagrammsimulation](../../identity-service/identity-graph-linking-rules/graph-simulation.md) eingeben können, sowie für Aufschlüsselungen dazu, wie primäre Identitäten in bestimmten Diagrammszenarien ausgewählt werden. |

{style="table-layout:auto"}

Weiterführende Informationen zu Identity Service finden Sie in der [Übersicht zu Identity Service](../../identity-service/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht es Ihnen, in [!DNL Experience Platform] gespeicherte Daten, die sich auf Einzelpersonen (wie Kundinnen und Kunden, Interessierte, Benutzerinnen und Benutzer oder Organisationen) beziehen, in Zielgruppen zu segmentieren. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten erstellen. Diese Zielgruppen werden zentral auf [!DNL Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Aufnahmedetails | Bei Zielgruppen, deren Quelle der benutzerdefinierte Upload ist, können Sie Details zur Aufnahme der Zielgruppe auf der Seite mit den Zielgruppendetails umfassender anzeigen. Darüber hinaus können Sie Beschriftungen auf die Payload-Attribute anwenden, indem Sie das Schema und die gewünschten Attribute zur Beschriftung auswählen. Weitere Informationen zum Abschnitt „Aufnahmedetails“ finden Sie im [Handbuch zu Audience Portal](../../segmentation/ui/audience-portal.md#ingestion-details). |

{style="table-layout:auto"}

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md).

## Quellen

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

Verwenden Sie Quellen in Experience Platform, um Daten aus einer Adobe-Anwendung oder einer Datenquelle von Drittanbietern aufzunehmen.

**Aktualisierte Funktion**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierungen des Adobe Analytics-Quell-Connector | Auf der Seite „Datensatzaktivität“ werden keine Informationen zu Batches angezeigt, da der Analytics-Quell-Connector vollständig von Adobe verwaltet wird. Sie können überwachen, dass Daten fließen, indem Sie sich die Metriken um die erfassten Datensätze ansehen. Weitere Informationen finden Sie im Handbuch zum Erstellen einer [Quellverbindung für Analytics-Daten](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

**Aktualisierte Dokumentation**

| Aktualisierte Dokumentation | Beschreibung |
| --- | --- |
| Erweiterte Dokumentation zur Aktualisierung von Datenflüssen | Das Handbuch zum [Aktualisieren vorhandener Datenflüsse für Quellen in der Benutzeroberfläche](../../sources/tutorials/ui/update-dataflows.md) wurde aktualisiert und enthält jetzt weitere Informationen zu den verschiedenen Konfigurationen, die Sie an einem vorhandenen Datenfluss vornehmen können. Das Handbuch wurde außerdem aktualisiert, um das erwartete Verhalten bei der erneuten Aktivierung eines deaktivierten Datenflusses zu verdeutlichen. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../../sources/home.md).
