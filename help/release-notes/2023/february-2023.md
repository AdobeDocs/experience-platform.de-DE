---
title: Adobe Experience Platform - Versionshinweise - Februar 2023
description: Die Versionshinweise für Adobe Experience Platform vom Februar 2023.
source-git-commit: ff276de35ca2aaeec168f4c4386d849f3352ad57
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 35%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 22. Februar 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Destinations]](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Query Service](#query-service)
- [Verwandte Konten in Real-Time CDP B2B Edition](#related-accounts)
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
&#x200B; | Funktion | Beschreibung | | — | — | | Einstellung von Feldern über die Benutzeroberfläche | Nach der Erfassung von Daten können Sie Felder aus Ihren Schemata jetzt nicht mehr unterstützen. Die Einstellung von XDM-Feldern ermöglicht es Ihnen, Felder aus der UI-Ansicht zu entfernen und sie gleichzeitig für die Verwendung beizubehalten. Bei Bedarf können veraltete Felder erneut angezeigt werden. Alle Segmente, Abfragen oder nachgelagerten Lösungen, die auf die Felder verweisen, werden wie gewohnt ausgeführt. |

{style=&quot;table-layout:auto&quot;} &#x200B; Weitere Informationen zu XDM in Platform finden Sie im Abschnitt [XDM-System - Übersicht](../../xdm/home.md). &#x200B;
<!-- Field deprecation: https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/field-deprecation.html -->

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus Data Lake verbinden und die Abfrageergebnisse als neuen Datensatz erfassen, der für die Berichterstellung, Data Science Workspace oder für die Aufnahme in das Echtzeit-Kundenprofil verwendet werden kann.

**Aktualisierte Funktionen**
&#x200B; | Funktion | Beschreibung | | — | — | | Aktivieren von Datensätzen für Profile mit SQL | Verwenden Sie LABELs in CTAS-Abfragen, um einen Datensatz &quot;profile enabled&quot;zu machen, oder verwenden Sie ALTER, um vorhandene Datensätze zu aktualisieren und für Profile zu aktivieren. | | Planmäßige Abfragen überwachen | Im Tab Geplante Abfragen finden Sie wichtige Informationen zu Ihren Abfrageausführungen und abonnieren Warnhinweise. Überwachen Sie Abfragen auf Planungsdetails, Status und Fehlermeldungen/Codes, falls diese fehlschlagen.  | | Funktion zur automatischen Vervollständigung ein/aus | Beseitigen Sie bestimmte Metadatenbefehle und verbessern Sie die Verarbeitungszeiten, indem Sie die Funktion für die automatische Vervollständigung des Abfrage-Editors aktivieren. Diese Funktion schlägt während des Schreibens automatisch potenzielle SQL-Schlüsselwörter und Tabellendetails für die Abfrage vor. | | Datensatzbeispiele | Legen Sie eine Stichprobenrate in Ihrer Abfrage fest und verwenden Sie Datensatzbeispiele, um eine einheitliche Stichprobe zu erstellen, oder erstellen Sie bedingte Beispiele basierend auf bestimmten Kriterien. |

{style=&quot;table-layout:auto&quot;} &#x200B; Weitere Informationen zu Query Services finden Sie im Abschnitt [Query Service - Übersicht](../../query-service/home.md). &#x200B;
<!-- Links for QS feature docs after release day: -->
<!-- Enable datasets for profile with SQL link: https://experienceleague.adobe.com/docs/experience-platform/query/sql/syntax.html#create-table-as-select -->
<!-- Monitor scheduled queries link: https://experienceleague.adobe.com/docs/experience-platform/query/monitor-queries.html  -->
<!-- Toggle auto-complete feature link: https://experienceleague.adobe.com/docs/experience-platform/query/ui/user-guide.html#auto-complete -->
<!-- dataset samples: https://experienceleague.adobe.com/docs/experience-platform/query/essential-concepts/dataset-samples.html -->

## Verwandte Konten in Real-Time CDP B2B Edition {#related-accounts}

>[!NOTE]
>
>Die Funktion „verwandte Konten“ ist nur für Kunden der Real-Time CDP B2B Edition verfügbar.

Verwandte Konten, [!DNL Real-Time CDP B2B] bietet Ihnen die Möglichkeit, eine Liste von Konten anzuzeigen, die dem von Ihnen verwendeten Konto ähnlich sind. Sie können die verwandten Konten in Ihre Segmentdefinitionen einbeziehen, um Ihre Reichweite zu erweitern oder umfassendere Kriterien auf Ihre Segmente anzuwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Zugehörige Kontodienste aktivieren | Mit der neuen Umschalter-Funktion können Sie den zugehörigen Kontodienst für Ihr Konto aktivieren. Weitere Informationen finden Sie im Handbuch unter [Aktivieren des zugehörigen Kontodienstes](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu verwandten Kontofunktionen finden Sie auf den folgenden Dokumentationsseiten:

- [Übersicht über verwandte Konten in Real-Time CDP B2B Edition](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Registerkarte „Verwandte Konten“ im Handbuch zur Benutzeroberfläche für Kontoprofile](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Verwendung verwandter Konten in Segmentdefinitionen](../../rtcdp/segmentation/b2b.md#related-accounts)

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