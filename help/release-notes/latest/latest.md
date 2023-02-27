---
title: Adobe Experience Platform – Versionshinweise
description: Die Versionshinweise für Adobe Experience Platform vom Februar 2023.
source-git-commit: 66ca8d3972045cffe4a1614f638546f4e7838680
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 37%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 22. Februar 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Destinations]](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Query Service](#query-service)
- [Real-Time Customer Data Platform B2B Edition](#b2b)
- [Quellen](#sources)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-features}

| Funktion | Beschreibung |
| ----------- | ----------- |
| [Verbesserung der Einwilligungsrichtlinie](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) für Integrationen mit [dateibasierte (Batch-)Ziele](/help/destinations/destination-types.md#file-based) | <p> Wenn Profile nicht mehr für eine Zustimmungsrichtlinie qualifiziert sind, kommuniziert Experience Platform jetzt proaktiv ihren Richtlinienausstieg an dateibasierte Ziele. Dies folgt dem [-Version im Februar 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) derselben Funktionalität für Streaming-Ziele. </p> <p> <b>Hinweis</b>: Diese Funktion steht nur Kunden von **[!UICONTROL Datenschutz und Sicherheitsschild]** und der **[!UICONTROL Gesundheitsschild]**. </p> |

{style=&quot;table-layout:auto&quot;}

**Neue oder aktualisierte Dokumentation** {#destinations-new-updated-documentation}

| Dokumentation | Beschreibung |
| ----------- | ----------- |
| Funktionsweise der Dokumentation zu Zielen | <p>Wir haben drei neue Erklärungsartikel zur Funktionsweise von Zielen veröffentlicht, die auf allgemeinen Fragen von Benutzern basieren:</p> <p><ul><li>[Konfigurierbare und allgemeine Exporteinstellungen in Zielen](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Profil-Exportverhalten für verschiedene Zieltypen](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Identitätsverarbeitung im Workflow für die Zielaktivierung](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Aktualisierte Funktionen**
&#x200B; | Funktion | Beschreibung | | — | — | | Einstellung von Feldern über die Benutzeroberfläche | Jetzt können Sie [veraltete Felder aus Ihren Schemata, nachdem Daten erfasst wurden](../../xdm/tutorials/field-deprecation-ui.md). Die Einstellung von XDM-Feldern ermöglicht es Ihnen, Felder aus der UI-Ansicht zu entfernen und sie gleichzeitig für die Verwendung beizubehalten. Bei Bedarf können veraltete Felder erneut angezeigt werden. Alle Segmente, Abfragen oder nachgelagerten Lösungen, die auf die Felder verweisen, werden wie gewohnt ausgeführt. |



**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Klasse | [[!UICONTROL XDM Individual Prospect Profile]](https://github.com/adobe/xdm/pull/1669/files) | Die Klasse &quot;XDM Individual Prospect Profile&quot;führt von Partnern bereitgestellte IDs ein. |

{style=&quot;table-layout:auto&quot;}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Feldergruppe | [!UICONTROL Begrenzung der Häufigkeit] | Die [!UICONTROL Begrenzung der Häufigkeit] Feldergruppe wurde [aktualisiert, um Wiederholungs- und benutzerdefinierte Ereignisse zu unterstützen](https://github.com/adobe/xdm/pull/1641/files). |
| Datentyp | [!UICONTROL Webverweiser] | Eigenschaften von Webverweisen [aktualisiert um `xdm:linkName` und `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). Dies sind jeweils der Name und die Region des HTML-Elements, das auf der vorherigen Seite ausgewählt wurde. |
| Feldergruppe | [!UICONTROL Adobe CJM ExperienceEvent – Details zur Nachrichteninteraktion] | [Die [!UICONTROL Tracker-URL] wurde hinzugefügt](https://github.com/adobe/xdm/pull/1665/files) der [!UICONTROL Adobe CJM ExperienceEvent]. Dieser Tracker stellt die vom Benutzer ausgewählte URL bereit. |
| Feldergruppe | [!UICONTROL Adobe CJM ExperienceEvent - Details zur Nachrichteninteraktion] | [Leer `meta:enum` Eigenschaft wurde entfernt](https://github.com/adobe/xdm/pull/1668/files) aus der URL [!UICONTROL Tracking-Typ] -Feld. |
| Datentyp | [!UICONTROL Media information] | [Das Regex-Muster aus dem `videoSegment` -Eigenschaft in [!UICONTROL Medieninformationen] Datentyp wurde entfernt](https://github.com/adobe/xdm/pull/1667/files). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie unter [XDM-System - Übersicht](../../xdm/home.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus Data Lake verbinden und die Abfrageergebnisse als neuen Datensatz erfassen, der für die Berichterstellung, Data Science Workspace oder für die Aufnahme in das Echtzeit-Kundenprofil verwendet werden kann.

**Aktualisierte Funktionen**
&#x200B; | Funktion | Beschreibung | | — | — | | Aktivieren von Datensätzen für Profile mit SQL | Verwenden Sie LABELs in CTAS-Abfragen, um einen Datensatz &quot;profile enabled&quot;zu machen, oder verwenden Sie ALTER, um vorhandene Datensätze zu aktualisieren und für Profile zu aktivieren. | | Planmäßige Abfragen überwachen | Im Tab Geplante Abfragen finden Sie wichtige Informationen zu Ihren Abfrageausführungen und abonnieren Warnhinweise. Überwachen Sie Abfragen auf Planungsdetails, Status und Fehlermeldungen/Codes, falls diese fehlschlagen.  | | Funktion zur automatischen Vervollständigung ein/aus | Beseitigen Sie bestimmte Metadatenbefehle und verbessern Sie die Verarbeitungszeiten, indem Sie die Funktion für die automatische Vervollständigung des Abfrage-Editors aktivieren. Diese Funktion schlägt während des Schreibens automatisch potenzielle SQL-Schlüsselwörter und Tabellendetails für die Abfrage vor. | | Datensatzbeispiele | Legen Sie eine Stichprobenrate in Ihrer Abfrage fest und verwenden Sie Datensatzbeispiele, um eine einheitliche Stichprobe zu erstellen, oder erstellen Sie bedingte Beispiele basierend auf bestimmten Kriterien. |

&#x200B; Weitere Informationen zu Query Services finden Sie im Abschnitt [Query Service - Übersicht](../../query-service/home.md). &#x200B;
<!-- Links for QS feature docs after release day: -->
<!-- Enable datasets for profile with SQL link: https://experienceleague.adobe.com/docs/experience-platform/query/sql/syntax.html#create-table-as-select -->
<!-- Monitor scheduled queries link: https://experienceleague.adobe.com/docs/experience-platform/query/monitor-queries.html  -->
<!-- Toggle auto-complete feature link: https://experienceleague.adobe.com/docs/experience-platform/query/ui/user-guide.html#auto-complete -->
<!-- dataset samples: https://experienceleague.adobe.com/docs/experience-platform/query/essential-concepts/dataset-samples.html -->

## Real-Time Customer Data Platform B2B Edition {#b2b}

Real-Time CDP B2B Edition basiert auf Real-time Customer Data Platform (Real-Time CDP) und wurde speziell für Marketingexpertinnen und -experten mit einem Business-to-Business-Service-Modell entwickelt. Es führt Daten aus verschiedenen Quellen zusammen und kombiniert sie zu einer einzigen Ansicht von Personen und Account-Profilen. Diese vereinheitlichten Daten ermöglichen es Marketing-Experten, bestimmte Zielgruppen präzise anzusprechen und über alle verfügbaren Kanäle anzusprechen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Zugehörige Kontodienste aktivieren | Mit der neuen Umschalter-Funktion können Sie den zugehörigen Kontodienst für Ihr Konto aktivieren. Weitere Informationen finden Sie im Handbuch unter [Aktivieren des zugehörigen Kontodienstes](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Real-Time CDP B2B Edition finden Sie im Abschnitt [Übersicht über Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und ermöglicht es Ihnen, diese Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Zugriff auf Abonnementebene festlegen mit [!DNL Google PubSub] | Sie können jetzt den Zugriff auf ein bestimmtes Themenabo definieren, wenn Sie die [!DNL Google PubSub] Quelle durch Angabe der Anmelde-ID bei der Authentifizierung. Weitere Informationen finden Sie im Abschnitt [!DNL Google PubSub] Authentifizierungs-Tutorial [Verwenden der Flow Service-API](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) oder [Platform-Benutzeroberfläche](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Erfassen benutzerdefinierter Aktivitätsdaten aus [!DNL Marketo] | Sie können jetzt benutzerdefinierte Aktivitätsdaten aus Ihren [!DNL Marketo] -Instanz zu Experience Platform. Um benutzerdefinierte Aktivitätsdaten zu erfassen, müssen Sie im Schema B2B-Aktivitäten benutzerdefinierte Aktivitätsfeldgruppen einrichten und einen Datenfluss mithilfe des Aktivitäts-Datensatzes erstellen. Sobald der Datenfluss abgeschlossen ist, enthält der aufgenommene Datensatz sowohl standardmäßige als auch benutzerdefinierte Aktivitäten aus Ihren [!DNL Marketo] -Instanz. Sie können dann [Query Service](../../query-service/home.md) , um auf Ihre benutzerdefinierten Aktivitätsdatensätze in Platform zuzugreifen. Weitere Informationen finden Sie im Handbuch unter [Erstellen eines Datenflusses für benutzerdefinierte Aktivitätsdaten](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Nicht beanspruchte Konten ausschließen von [!DNL Marketo] | Sie können jetzt konfigurieren, ob nicht beanspruchte Konten bei der Erfassung ausgeschlossen oder einbezogen werden sollen, wenn Sie einen Datenfluss für Unternehmensdaten erstellen. Weitere Informationen finden Sie im Handbuch unter [Erstellen einer Quellverbindung und eines Datenflusses für [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style=&quot;table-layout:auto&quot;}

Weiterführende Informationen zu Quellen finden Sie in der [Übersicht über Quellen](../../sources/home.md).
