---
title: Adobe Experience Platform – Versionshinweise
description: Die Versionshinweise für Adobe Experience Platform vom Februar 2023.
source-git-commit: ccd3df0bc045f98306901b2d734cf17262275f18
workflow-type: tm+mt
source-wordcount: '1292'
ht-degree: 100%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 22. Februar 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Datenerfassung](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Query Service](#query-service)
- [Real-Time Customer Data Platform B2B Edition](#b2b)
- [Quellen](#sources)

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

### Assurance {#assurance}

Mit Adobe Assurance können Sie die Datenerfassung und die Bereitstellung von Erlebnissen in Ihrer App untersuchen, testen, simulieren und überprüfen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Öffentliche APIs | Die Adobe Assurance-APIs sind jetzt verfügbar. Die Assurance-APIs sind eine Sammlung von APIs, mit denen Benutzende ihre eigenen Web- und mobilen Apps testen und debuggen können, wenn sie mit der Adobe Assurance-Erweiterung mit dem Mobile SDK ausgestattet sind. Weitere Informationen zu den Assurance-APIs finden Sie in der [Übersicht über die Assurance-API](https://developer.adobe.com/adobe-assurance-public-apis/). |

{style="table-layout:auto"}

Weitere Informationen zu Assurance finden Sie in der [Assurance-Dokumentation](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-features}

| Funktion | Beschreibung |
| ----------- | ----------- |
| [Verbesserung der Einverständnisrichtlinie](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) für Integrationen in [dateibasierte (Batch-)Ziele](/help/destinations/destination-types.md#file-based) | <p> Wenn Profile nicht mehr für eine Einverständnisrichtlinie qualifiziert sind, wird deren Richtlinienausstieg nun proaktiv von Experience Platform an dateibasierten Zielen mitgeteilt. Dies folgt der [Freigabe im Februar 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) der gleichen Funktionalität für Streaming-Ziele. </p> <p> <b>Hinweis</b>: Diese Funktion steht nur Kunden von **[!UICONTROL Privacy und Security Shield]** sowie **[!UICONTROL Healthcare Shield]** zur Verfügung. </p> |

{style="table-layout:auto"}

**Neue oder aktualisierte Dokumentation** {#destinations-new-updated-documentation}

| Dokumentation | Beschreibung |
| ----------- | ----------- |
| Funktionsweise der Dokumentation zu Zielen | <p>Wir haben drei neue Erklärungsartikel zur Funktionsweise von Zielen veröffentlicht, die auf allgemeinen Fragen von Benutzenden basieren:</p> <p><ul><li>[Konfigurierbare und allgemeine Exporteinstellungen in Zielen](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Profilexportverhalten für verschiedene Zieltypen](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Umgang mit Identitäten im Aktivierungs-Workflow für Ziele](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Einstellung von Feldern über die Benutzeroberfläche | Sie können jetzt [Felder aus Ihren Schemata verwerfen, nachdem Daten erfasst wurden](../../xdm/tutorials/field-deprecation-ui.md). Das Verwerfen von XDM-Feldern ermöglicht es Ihnen, Felder aus der Ansicht der Benutzeroberfläche zu entfernen und sie gleichzeitig für die Verwendung beizubehalten. Bei Bedarf können verworfene Felder erneut angezeigt werden. Alle Segmente, Abfragen oder nachgelagerten Lösungen, die auf die Felder verweisen, werden wie gewohnt ausgeführt. |

{style="table-layout:auto"}

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Klasse | [[!UICONTROL XDM Individual Prospect Profile]](https://github.com/adobe/xdm/pull/1669/files) | Die Klasse „XDM Individual Prospect Profile“ führt IDs ein, die von Partnerseite bereitgestellt werden. |

{style="table-layout:auto"}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Feldergruppe | [!UICONTROL Frequency Capping Constraints] | Die Feldergruppe [!UICONTROL Frequency Capping Constraints] wurde [aktualisiert, um Wiederholungs- und benutzerdefinierte Ereignisse zu unterstützen](https://github.com/adobe/xdm/pull/1641/files). |
| Datentyp | [!UICONTROL Web-Referrer] | Eigenschaften der Web-Referrer wurden [aktualisiert, sodass sie `xdm:linkName` und `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files) beinhalten. Dabei handelt es sich um den Namen und die Region des HTML-Elements, das auf der vorherigen Seite ausgewählt wurde. |
| Feldergruppe | [!UICONTROL Adobe CJM ExperienceEvent – Details zur Nachrichteninteraktion] | [Das Feld [!UICONTROL Tracker URL] wurde](https://github.com/adobe/xdm/pull/1665/files) der Klasse [!UICONTROL Adobe CJM ExperienceEvent] hinzugefügt. Dieser Tracker stellt die von Benutzenden ausgewählte URL bereit. |
| Feldergruppe | [!UICONTROL Adobe CJM ExperienceEvent – Details zur Nachrichteninteraktion] | [Die leere Eigenschaft `meta:enum` wurde](https://github.com/adobe/xdm/pull/1668/files) aus dem Feld URL [!UICONTROL Tracking Type] entfernt. |
| Datentyp | [!UICONTROL Media information] | [Das Regex-Muster wurde aus der Eigenschaft `videoSegment` im Datentyp [!UICONTROL Medieninformationen] entfernt](https://github.com/adobe/xdm/pull/1667/files). |

{style="table-layout:auto"}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem Data Lake verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktivieren von Datensätzen für Profile mit SQL | [Verwenden Sie LABELs in CTAS-Abfragen, um einen Datensatz als „profile enabled“ zu markieren](../../query-service/sql/syntax.md#create-table-as-select), oder verwenden Sie ALTER, um vorhandene Datensätze zu aktualisieren, damit sie für das Profil aktiviert werden. Sie können dieses erweiterte SQL-Konstrukt verwenden, um nahtlose Unterstützung für abgeleitete Attribute für Ihre geschäftlichen Anwendungsfälle des Echtzeit-Kundenprofils bereitzustellen. Weitere Informationen finden Sie unter [Nahtloser SQL-Ablauf für das Dokument mit abgeleiteten Attributen](../../query-service/data-distiller/derived-attributes/seamless-sql-flow.md). |
| Überwachen von geplanten Abfragen  | Verwenden Sie die [Registerkarte „Geplante Abfragen“](../../query-service/ui/monitor-queries.md), um wichtige Informationen zur Ausführung Ihrer Abfragen zu erhalten und Warnhinweise zu abonnieren. Überwachen Sie Abfragen auf Planungsdetails, Status und Fehlermeldungen/-codes, falls sie fehlschlagen. |
| Umschalten der Funktion zur automatischen Vervollständigung | Beseitigen Sie bestimmte Metadatenbefehle und verbessern Sie die Verarbeitungszeiten durch [Umschalten der Funktion zum automatischen Vervollständigen des Abfrage-Editors](../../query-service/ui/user-guide.md#auto-complete). Diese Funktion schlägt während des Schreibens automatisch potenzielle SQL-Schlüsselwörter und Tabellendetails für die Abfrage vor. |
| Datensatzbeispiele | Geben Sie in Ihrer Abfrage eine Sampling-Rate an und [verwenden Sie Datensatzbeispiele, um eine einheitliche Stichprobe zu erstellen](../../query-service/essential-concepts/dataset-samples.md), oder erstellen Sie bedingte Beispiele basierend auf bestimmten Kriterien. |

{style="table-layout:auto"}

Weitere Informationen über Abfrage-Services finden Sie unter [Abfrage-Service – Übersicht](../../query-service/home.md).

## Real-Time Customer Data Platform B2B Edition {#b2b}

Real-Time CDP B2B Edition basiert auf Real-time Customer Data Platform (Real-Time CDP) und wurde speziell für Marketingexpertinnen und -experten mit einem Business-to-Business-Service-Modell entwickelt. Es führt Daten aus verschiedenen Quellen zusammen und kombiniert sie zu einer einzigen Ansicht von Personen und Account-Profilen. Diese vereinheitlichten Daten ermöglichen es Marketing-Experten, bestimmte Zielgruppen präzise anzusprechen und über alle verfügbaren Kanäle anzusprechen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktivieren zugehöriger Kontodienste | Mit der neuen Umschalter-Funktion können Sie den zugehörigen Kontodienst für Ihr Konto aktivieren. Weitere Informationen finden sich im Handbuch unter [Aktivieren des zugehörigen Kontodienstes](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style="table-layout:auto"}

Weitere Informationen über Real-Time CDP B2B Edition finden Sie in der [Übersicht zu Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen aufnehmen und mithilfe von Platform-Services strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Festlegen des Zugriffs auf Abonnementebene mit [!DNL Google PubSub] | Sie können jetzt den Zugriff auf ein bestimmtes Themenabonnement definieren, wenn Sie die Quelle [!DNL Google PubSub] durch Angabe der Anmelde-ID bei der Authentifizierung verwenden. Weitere Informationen finden sich im [!DNL Google PubSub]-Authentifizierungs-Tutorial im Abschnitt [Verwenden der Flow Service-API](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) oder [Platform-Benutzeroberfläche](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Aufnehmen benutzerdefinierter Aktivitätsdaten aus [!DNL Marketo] | Jetzt können benutzerdefinierte Aktivitätsdaten aus Ihrer [!DNL Marketo]-Instanz zu Experience Platform hinzugefügt werden. Um benutzerdefinierte Aktivitätsdaten aufzunehmen, müssen im Schema „B2B-Aktivitäten“ benutzerdefinierte Aktivitätsfeldgruppen eingerichtet und ein Datenfluss mithilfe des Aktivitäts-Datensatzes erstellt werden. Sobald der Datenfluss abgeschlossen ist, enthält der aufgenommene Datensatz sowohl standardmäßige als auch benutzerdefinierte Aktivitäten aus Ihrer [!DNL Marketo]-Instanz. Sie können dann den [Abfrage-Service](../../query-service/home.md) verwenden, um in Platform auf die Datensätze der benutzerdefinierten Aktivitäten zuzugreifen. Weitere Informationen finden sich im Handbuch unter [Erstellen eines Datenflusses für Daten zu benutzerdefinierten Aktivitäten](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Ausschließen nicht beanspruchter Konten von [!DNL Marketo] | Jetzt kann beim Erstellen eines Datenflusses für Unternehmensdaten konfiguriert werden, ob nicht beanspruchte Konten bei der Erfassung ausgeschlossen oder einbezogen werden sollen. Weitere Informationen finden sich im Handbuch unter [Erstellen einer Quellverbindung und eines Datenflusses für [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style="table-layout:auto"}

Weiterführende Informationen zu Quellen finden Sie in der [Übersicht über Quellen](../../sources/home.md).
