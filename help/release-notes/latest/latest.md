---
title: Adobe Experience Platform – Versionshinweise April 2025
description: Versionshinweise April 2025 für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: e0740ca9cd6e1d0b92d5504a2869ac03c28d4980
workflow-type: tm+mt
source-wordcount: '2069'
ht-degree: 20%

---

# Adobe Experience Platform – Versionshinweise

>[!TIP]
>
>Versionshinweise zu anderen Adobe Experience Platform-Programmen finden Sie in der folgenden Dokumentation:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/de/docs/analytics-platform/using/releases/latest)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Veröffentlichungsdatum: Mittwoch, 29. April 2025**

Aktualisierungen vorhandener Funktionen und Dokumentationen in Adobe Experience Platform:

- [Experience League](#experience-league)
- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Experience-Datenmodell](#xdm)
- [Identity Service](#identity)
- [Abfrage-Service](#query-service)
- [Sandboxes](#sandboxes)
- [Quellen](#sources)
- [Anwendungsfall-Playbooks](#use-case-playbooks)

## Experience League {#experience-league}

Experience League ist eine umfassende Lernplattform, die Ihnen hilft, Ihre Kenntnisse mit Adobe-Produkten zu erweitern. Es bietet eine Vielzahl von Ressourcen, darunter: Kurse, Dokumentation, Community-Seiten, Veranstaltungen und Zugriff auf Zertifizierungen.

| Funktion | Beschreibung |
| --- | --- |
| Personalisierte Startseite | Greifen Sie auf Ihre personalisierte Startseite auf [Experience League zu und passen Sie diese ](https://experienceleague.adobe.com/en/home#) an. Melden Sie sich mit Ihren Adobe-Anmeldeinformationen an und wählen Sie dann im oberen **&#x200B;**&#x200B;Experience League&quot; aus, um mit der Optimierung Ihres Lernerlebnisses zu beginnen: <ul><li>**Lesezeichen**: Verwenden Sie die [!UICONTROL Lesezeichen]-Funktion, um Ihre bevorzugten Ressourcen an einem Ort zu speichern und zu sammeln. Sie können eine Vielzahl von Inhalten speichern, einschließlich Wiedergabelisten, Artikeln und Tutorials.</li><li>**Passen Sie Ihr** an: Verbessern Sie Ihr Lernerlebnis, indem Sie Ihr Experience League-Profil mit den Rollen, Branchen, Produkten und der Erlebnisebene aktualisieren, die Ihren Anforderungen am besten entsprechen.</li><li>**Recommendations**: Anzeigen von Lerninhalten, die auf Grundlage Ihrer letzten Aktivität empfohlen wurden.</li><li>**Kürzlich angezeigt**: Verwenden Sie den Abschnitt [!UICONTROL Kürzlich angezeigt], um schnell zu den kürzlich angezeigten Inhalten wie Dokumentation und Videos zurückzukehren.</li><li>**Lernressourcen**: Verwenden Sie das Bedienfeld [!UICONTROL Alle Lernressourcen] um zu Tutorials, Dokumentationen, Community, Veranstaltungen und Zertifizierungen zu navigieren.</li><li>**Neue Funktionen** Im Abschnitt [!UICONTROL Neue Funktionen] finden Sie einen Stream der neuesten Inhalte auf Experience League.</li><li>**Vergangene Events On-Demand ansehen**: Sehen Sie sich zuvor aufgezeichnete Live-Streams über Produkt-Spotlights, Anwendungsfälle und Tutorials im Abschnitt [!UICONTROL Vergangene Events On-Demand ansehen] an.</li></ul><br> ![Personalisierte Startseite auf Experience League.](../2025/assets/april/personalized-home-page.png "Personalisierte Startseite auf Experience League."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!DNL Adform]-Erweiterung | Die [!DNL Adform] Server-seitige Erweiterung ermöglicht es Marken, Zielgruppen mithilfe von ECIDs extern einfach neu anzusprechen. Diese Server-seitige Erweiterung ist nicht von Drittanbieter-Cookies oder alternativen Cookie-IDs abhängig. Da dies vollständig Server-seitig geschieht, sind außerdem keine zusätzlichen Pixel oder andere Client-seitige Änderungen erforderlich. Weitere Informationen finden Sie in der [Übersicht über die Adform-Erweiterung](/help/tags/extensions/server/adform/overview.md). |
| API-Erweiterung für [!DNL Amazon]-Web-Ereignisse | Die [!DNL Amazon] Conversions-API-Erweiterung ermöglicht es Werbetreibenden, Website-Interaktionen direkt mit [!DNL Amazon] zu teilen, was eine verbesserte Attribution, Datenzuverlässigkeit und Kampagnenoptimierung bietet. Diese Erweiterung unterstützt die Ereignisweiterleitung, sodass Sie Konversionsereignisse wie Käufe, Warenkorbhinzufügungen und mehr senden und gleichzeitig eine ordnungsgemäße Deduplizierung für genaues Reporting sicherstellen können. Weitere Informationen finden Sie in der Übersicht über die Erweiterung [Amazon](/help/tags/extensions/server/amazon/overview.md). |

{style="table-layout:auto"}

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen** {#new-updated-destinations}

| Ziel | Beschreibung |
| --- | --- |
| [Marketo Engage-Personensynchronisierung](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Adobe hat das [!DNL Marketo Engage Person Sync]-Ziel aktualisiert, um ein Problem zu beheben, das Kunden betraf, wenn mehrere E-Mails in der Identitätszuordnung vorhanden waren. |
| [(V2) Pega CDH RealTime Audience-Verbindung](/help/destinations/catalog/personalization/pega-v2.md) | Verwenden Sie das [!DNL (V2) Pega Customer Decision Hub Realtime Audience]-Ziel in Adobe Experience Platform, um Profilattribute und Zielgruppenzugehörigkeitsdaten zur nächstbesten Entscheidungsfindung an Pega Customer Decision Hub zu senden, wenn in Ihrem Pega-Konto mehrere Pega Customer Decision Hub-Anwendungen konfiguriert sind. |

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktion | Beschreibung |
| --- | --- |
| **Wöchentlich** und **Monatlich** Planungsoptionen für vollständige Dateiexporte | Sie können jetzt bei der Aktivierung für Cloud-Speicher-dateibasierte Ziele wöchentlich oder monatlich vollständige Dateiexporte für Personen und potenzielle Zielgruppen planen. [Weitere Informationen ](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) Planungsoptionen. |

{style="table-layout:auto"}

**Fehlerbehebungen, Verbesserungen und andere Ankündigungen** {#destinations-fixes-and-enhancements}

- **Die Durchsetzung der Enddaten für den Datensatzexport verzögerte sich auf den 1. September 2025**\
  Im Rahmen der Version [September 2024](/help/release-notes/2024/september-2024.md#destinations-new-updated-functionality) hat Adobe für alle Datensatzexport-Datenflüsse, die vor dieser Version erstellt wurden, *Standardenddatum 1. Mai 2025*. Adobe verlängert jetzt diese Durchsetzungsfrist bis zum **. September 2025** um Kunden zusätzliche Zeit für die Aktualisierung ihrer Zeitpläne zu geben. Im Planungsabschnitt des Tutorials [Exportieren von Datensätzen](../../destinations/ui/export-datasets.md#schedule-dataset-export) finden Sie Informationen zum Bearbeiten des Enddatums eines Datensatzexport-Datenflusses.

- **Verbesserte Handhabung fehlgeschlagener SFTP-Übertragungen für das LiveRamp-Onboarding**\
  Adobe hat eine Fehlerbehebung für ein Problem implementiert, das Dateiexporte über SFTP an das [LiveRamp-Onboarding](/help/destinations/catalog/advertising/liveramp-onboarding.md)-Ziel betrifft. Gelegentlich schlugen Dateiübertragungen aufgrund vorübergehender Server-seitiger Probleme fehl, und temporäre Dateien von fehlgeschlagenen Versuchen blieben auf dem Server. Diese nicht löschbaren Dateien blockierten nachfolgende erneute Versuche, da Adobe nicht berechtigt war, sie zu überschreiben.\
  Wenn ein Wiederholungsversuch die temporäre Datei nicht löschen kann, generiert Adobe mit der Korrektur eine neue Datei mit dem angehängten Suffix `attempt2` , um sicherzustellen, dass der Wiederholungsversuch erfolgreich abgeschlossen wird.

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Aktualisierte XDM-Komponenten**

| Funktion | Beschreibung |
| --- | --- |
| Zeichenfolgenfelder erhalten einen Mindestwert von einem | Neue Zeichenfolgenfelder haben standardmäßig eine Mindestlänge von einem Zeichen. Null-Werte für nicht erforderliche Felder sind weiterhin zulässig. Weitere Informationen zu Best Practices finden Sie im Handbuch zu [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md#data-integrity-tips) |

{style="table-layout:auto"}

Weitere Informationen zu XDM in Experience Platform finden Sie in der [XDM-Systemübersicht](../../xdm/home.md).

## Identity Service {#identity}

Verwenden Sie den Adobe Experience Platform Identity Service, um sich einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhaltensweisen zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle und persönliche digitale Erlebnisse sorgen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Eingeschränkte Verfügbarkeit]{type=Informative} [!DNL Identity Graph Linking Rules] Verknüpfungsregeln für Identitätsdiagramme können jetzt von allen Kundinnen und Kunden in Entwicklungs-Sandboxes aufgerufen werden. <ul><li>**Aktivierungsanforderungen**: Die Funktion bleibt inaktiv, bis Sie Ihre [!DNL Identity Settings] konfigurieren und speichern. Ohne diese Konfiguration funktioniert das System weiterhin normal, ohne dass sich das Verhalten ändert.</li><li>**Wichtige Hinweise**: Während dieser eingeschränkten Verfügbarkeitsphase kann die Segmentierung nach Edge zu unerwarteten Segmentzugehörigkeitsergebnissen führen. Streaming und Batch-Segmentierung funktionieren jedoch erwartungsgemäß.</li><li>**Nächste Schritte**: Informationen zum Aktivieren dieser Funktion in Produktions-Sandboxes erhalten Sie von Ihrem Adobe-Account-Team.</li></ul> |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [[!DNL Identity Graph Linking Rules] Dokumentation](../../identity-service/identity-graph-linking-rules/overview.md).

## Abfrage-Service {#query-service}

Abfragen von Daten im Data Lake von Adobe Experience Platform unter Verwendung von Standard-SQL mit dem Abfrage-Service. Nahtlose Kombination von Datensätzen und Generierung neuer Datensätze aus Ihren Abfrageergebnissen, um das Reporting zu optimieren, datenwissenschaftliche Workflows zu ermöglichen oder die Aufnahme in das Echtzeit-Kundenprofil zu erleichtern. Sie können beispielsweise Kundentransaktionsdaten mit Verhaltensdaten zusammenführen, um hochwertige Zielgruppen für zielgerichtete Marketing-Kampagnen zu identifizieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| SQL-Zielgruppe überschreiben | Aktualisieren Sie die Zielgruppenzugehörigkeit, indem Sie vorhandene Profile mit den Ergebnissen einer neuen SQL-Abfrage überschreiben. Auf diese Weise können Sie dynamische Zielgruppen effizienter verwalten, indem Sie veraltete Datensätze entfernen und aktualisierte Zielgruppen in einen einzigen Vorgang einfügen. Weitere Informationen finden Sie im [Handbuch zur Erweiterung der SQL-Zielgruppe](../../query-service/data-distiller-audiences/overview.md#replace-audience). |
| Abfrageergebnisse herunterladen und kopieren | [Laden Sie Abfrageergebnisse direkt aus dem Abfrage](../../query-service/ui/overview.md#download-query-results)Editor als CSV-, XLSX- oder JSON-Dateien herunter oder [kopieren Sie Ergebnisse in die Zwischenablage](../../query-service/ui/overview.md#copy-results) als kommagetrennte Werte (CSV) zur schnellen Verwendung in Tabellenkalkulationsprogrammen wie Excel. Diese Verbesserungen optimieren die Offline-Analyse, das Reporting und die Datenvalidierungs-Workflows. |
| Abfrageergebnisse im Vollbildmodus anzeigen | [Vorschau der Abfrage liefert ein Vollbilddialogfeld, ](../../query-service/ui/overview.md#view-results) die Lesbarkeit zu verbessern, große Datensätze einfach zu scannen und Zeilen zum Kopieren auszuwählen. Die Vollbildansicht bietet ein in der Größe veränderbares Rasterlayout, mit dem Sie breite Tabellen und detaillierte Ausgaben effizienter überprüfen können. |
| Verbesserte Spaltenauswahl in der Modellvorhersage | Wählen Sie bestimmte Spalten aus und wenden Sie Aliase mithilfe der erweiterten `model_predict` an. Abrufen von Zwischenprognoseergebnissen wie Funktionsvektoren und Wahrscheinlichkeitswerten. Die erweiterte Auswahl erfordert eine Aktivierung des Feature Flag. Syntaxbeispiele [ Details zu Feature Flag finden Sie ](../../query-service/advanced-statistics/models.md#select-specific-output-fields) der Dokumentation zum Modelllebenszyklus . |
| Speichern von Modellvorhersageausgaben mithilfe von CREATE TABLE und INSERT INTO | [Speichern Sie ausgewählte Prognoseausgaben in neue Tabellen, indem Sie CREATE TABLE AS SELECT verwenden, oder fügen Sie mithilfe von INSERT INTO SELECT in vorhandene Tabellen ein](../../query-service/advanced-statistics/models.md#predict). Wenn die erweiterte Spaltenauswahl aktiviert ist, können Zwischenergebnisse wie Merkmalsvektoren und Wahrscheinlichkeiten neben den endgültigen Prognosen auch beibehalten werden. Anwendungsbeispiele finden Sie in der [SQL-Syntaxdokumentation](../../query-service/sql/syntax.md#create-table-as-select). |

Weitere Informationen zu [!DNL Query Service] finden Sie in der [[!DNL Query Service] Übersicht](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Um diese Anforderung zu erfüllen, stellt Experience Platform Sandboxes bereit, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung der Erweiterung des Sandbox-Tooling-Plug-ins | Benutzerdefinierte Aktionen können jetzt beim Duplizieren von Journey-Objekten in Sandbox-Tools als abhängiges Objekt kopiert werden. Darüber hinaus können Sie vorhandene Aktionen auswählen, die in der Ziel-Sandbox wiederverwendet werden sollen. Sie können auch unabhängig zu einem Paket hinzugefügt werden. Vollständige Informationen zu unterstützten Adobe Journey Optimizer-Objekten finden Sie im [Sandbox-Tools](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects)Handbuch. |

{style="table-layout:auto"}

Weitere Informationen zu Sandboxes finden Sie unter [Sandbox-Übersicht](../../sandboxes/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

Verwenden Sie Quellen in Experience Platform, um Daten aus einer Adobe-Anwendung oder einer Datenquelle von Drittanbietern aufzunehmen.

**Neue Quellen**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Algolia User Profiles] | Die [[!DNL Algolia User Profiles]](../../sources/connectors/data-partners/algolia-user-profiles.md) ist jetzt verfügbar. Verwenden Sie diese Quelle, um Ihre [!DNL Algolia]-Benutzerprofildaten zu Experience Platform zu übertragen. Sie können diese Daten dann verwenden, um die Benutzerinteraktion, die Konversionsraten und das gesamte Kundenerlebnis zu verbessern, indem Sie leistungsstarke Suchlösungen für Websites, E-Commerce-Plattformen und Programme bereitstellen. Weitere Informationen finden Sie im Handbuch zum „Aufnehmen von Daten [ Experience Platform [!DNL Algolia User Profiles] . ](../../sources/tutorials/ui/create/data-partners/algolia-user-profiles.md) |
| [!BADGE Beta]{type=Informative}-API-Unterstützung für [!DNL Azure Databricks] | Die [!DNL Azure Databricks] ist jetzt in der API verfügbar. Verwenden Sie die [!DNL Flow Service]-API, um Ihr [!DNL Databricks]-Konto zu verbinden und Ihre [!DNL Databricks]-Daten an Experience Platform zu übertragen. Weitere Informationen finden Sie in der Dokumentation zu [[!DNL Azure Databricks]](../../sources/connectors/databases/databricks.md). |

{style="table-layout:auto"}

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| XDM-Felder für die Aufnahme von Streaming-Mediendaten in Experience Platform wurden aktualisiert. | Die neue XDM-Feldergruppe `mediaReporting` ist jetzt für die Aufnahme von Streaming-Mediendaten über die Adobe Analytics-Quelle in Experience Platform verfügbar. Dieses Feld ersetzt das `media.mediaTimed` Feld.</br> <br>Während einer Übergangszeit von drei Monaten wird die Datenaufnahme in `media.mediaTimed` Feldern fortgesetzt. Ende Juli 2025 werden die `media.mediaTimed` jedoch vollständig veraltet sein und nicht mehr in der Experience Platform-Schema-Benutzeroberfläche angezeigt. Daten werden nur mithilfe der `mediaReporting` Felder gesendet.</br><br>Wenn Sie die Analytics-Quelle zur Erfassung von Streaming-Mediendaten in Platform vor dem 22. April 2025 implementiert haben, müssen Sie Ihre vorhandenen Konfigurationen migrieren, um Daten mithilfe der neuen Feldergruppe zu senden. Diese Migration muss bis Ende Juli 2025 abgeschlossen sein. Wenden Sie sich an Ihr Adobe Account Team, um Migrationsunterstützung zu erhalten. |
| Neue Authentifizierungstypen für [!DNL MariaDB] und [!DNL PostgreSQL] | Sie können jetzt die Standardauthentifizierung verwenden, um Ihre [!DNL MariaDB] und [!DNL PostgreSQL] auf Experience Platform zu authentifizieren. Weitere Informationen finden Sie in der folgenden Dokumentation: <ul><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL PostgreSQL]](../../sources/connectors/databases/postgres.md) |
| Filterunterstützung auf Zeilenebene für [!DNL Amazon Redshift] | Sie können Filterfunktionen auf Zeilenebene für Ihre [!DNL Amazon Redshift] in Experience Platform verwenden. Weitere Informationen finden Sie im Handbuch unter [Filtern von Daten auf Zeilenebene nach Quellen in der API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../../sources/home.md).

## Anwendungsfall-Playbooks {#use-case-playbooks}

Anwendungsfall-Playbooks wurden ursprünglich entwickelt, um bei den ersten Schritten mit Real-Time Customer Data Platform oder Adobe Journey Optimizer zu helfen. Sie werden weiterentwickelt und ermöglichen es Ihnen jetzt, wichtige Marketing-Anwendungsfälle zu starten und Inspiration und vordefinierte Assets bereitzustellen, um sie zu testen und in die Produktion zu übernehmen.

Anwendungsfall-Playbooks sind von einem Erkennungs-Tool in ein kollaboratives Framework übergegangen. Sie helfen Ihnen jetzt dabei, eigene Playbooks zu erstellen, zu verwalten und unternehmensübergreifend freizugeben.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} Eigene Playbooks erstellen und freigeben | Ein neues Playbook Authoring-Framework ermöglicht das Erstellen, Verwalten und Freigeben eigener Playbooks für Anwendungsfälle. Dazu gehört die Unterstützung für die Erfassung wichtiger Metadaten, die Bearbeitung von Journey-Zuordnungen und die Verknüpfung relevanter technischer Assets. Sie können Playbooks organisationsübergreifend freigeben, um Marketing-Ansätze zu standardisieren und die Konsistenz zu gewährleisten. |

{style="table-layout:auto"}

Um zu erfahren, wie Sie Ihre eigenen Playbooks erstellen und freigeben können, lesen Sie das Dokument [Erstellen und Freigeben Ihrer eigenen Playbooks](/help/use-case-playbooks/playbooks/author.md).

Weitere Informationen finden Sie im Abschnitt [Übersicht über Playbooks - ](/help/use-case-playbooks/playbooks/overview.md), der einen Überblick über die Funktionen von Playbooks und deren Zweck sowie eine durchgängige Demonstration bietet, einschließlich der Erstellung von Instanzen und des Imports generierter Assets in andere Sandbox-Umgebungen.
