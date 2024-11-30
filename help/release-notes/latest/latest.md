---
title: Adobe Experience Platform – Versionshinweise November 2024
description: Die Versionshinweise von November 2024 für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 3f43e120225bcca640cc46ebdce1e4d61100ad45
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 19%

---

# Adobe Experience Platform – Versionshinweise

>[!TIP]
>
>Die neue Produktdokumentation für den [AI-Assistenten](../../ai-assistant/landing.md) ist jetzt verfügbar. Verwenden Sie diese Seite als Hub für alle Ressourcen, die mit AI Assistant verbunden sind.

**Versionsdatum: Mittwoch, 26. November 2024**

Aktualisierungen vorhandener Funktionen und Dokumentationen in Adobe Experience Platform:

- [KI-Assistent](#ai-assistant)
- [Ziele](#destinations)
- [Abfrage-Service](#query-service)
- [Sandboxes](#sandboxes)
- [Dokumentationsaktualisierungen](#documentation-updates)
   - [Dokumentation zur interaktiven Experience Platform-API](#interactive-experience-platform-api-documentation)
   - [Neues Inhaltsverzeichnis auf Experience League](#new-table-of-contents-on-experience-league)
   - [Neue Landingpage des KI-Assistenten](#new-ai-assistant-landing-page)

## KI-Assistent {#ai-assistant}

AI Assistant in Adobe Experience Platform ist eine Dialogerfahrung, mit der Sie Ihre Workflows in Adobe-Applikationen beschleunigen können. Sie können den AI-Assistenten verwenden, um Produktwissen besser zu verstehen, Probleme zu beheben oder Informationen zu durchsuchen und operative Einblicke zu erhalten. Der AI-Assistent unterstützt Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer und Customer Journey Analytics.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Alpha]{type=Informative} Überwachen Sie wichtige Änderungen und prognostizieren Sie das Zielgruppenwachstum. | Verwenden Sie den KI-Assistenten, um signifikante Änderungen zu überwachen und Wachstumsprognosen für Ihre Zielgruppe und Datensatzgrößen bereitzustellen. Anschließend können Sie diese Informationen verwenden, um die Integrität Ihrer Zielgruppendaten sicherzustellen und zukunftsorientierte Projektionen zur Unterstützung datenbasierter Entscheidungen anzubieten. Weitere Informationen finden Sie im Handbuch zum [Überwachen bedeutender Änderungen und Vorhersagen des Zielgruppenwachstums](../../ai-assistant/new-features/audience-forecasting.md). |
| [!BADGE Alpha]{type=Informative} Schätzung der natürlichen Sprache | Verwenden Sie die Funktionen zur Schätzung der natürlichen Sprache des KI-Assistenten, um die Größe der Zielgruppe zu schätzen und die Tendenzen der Zielgruppe auf der Grundlage einfacher, kommunikativer Fragen vorherzusagen. Weitere Informationen finden Sie in der Anleitung zu [Verwenden der Schätzung natürlicher Sprachen mit dem KI-Assistenten](../../ai-assistant/new-features/natural-language.md). |

{style="table-layout:auto"}

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Ziele** {#new-updated-destinations}

| Ziel | Beschreibung |
| --- | --- |
| [ Magnite-Streaming in Echtzeit](/help/destinations/catalog/advertising/magnite-streaming.md) | Exportieren Sie Zielgruppen für Aktivierung, Targeting oder Unterdrückung in die Magnite-Streaming-Plattform. Beachten Sie, dass Sie für den korrekten Export von Zielgruppen nach Magnite sowohl die Echtzeit- als auch die Batch-Ziele verwenden müssen. |
| [Magnite-Streaming-Batch](/help/destinations/catalog/advertising/magnite-batch.md) | Exportieren Sie Zielgruppen für Aktivierung, Targeting oder Unterdrückung in die Magnite-Streaming-Plattform. Beachten Sie, dass Sie für den korrekten Export von Zielgruppen nach Magnite sowohl die Echtzeit- als auch die Batch-Ziele verwenden müssen. |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktion | Beschreibung |
| --- | --- |
| [Suchen nach Profilattributen in Echtzeit am Edge](/help/destinations/ui/activate-edge-profile-lookup.md) | Erfahren Sie, wie Sie in Echtzeit nach Edge-Profilattributen suchen, um Personalisierungserlebnisse bereitzustellen, oder Entscheidungsregeln über nachgelagerte Anwendungen mithilfe der benutzerdefinierten Personalization-Ziel- und Edge Network-API informieren. |

{style="table-layout:auto"}

Lesen Sie für Weitere Informationen den [Überblick über die Ziele](../../destinations/home.md).

## Abfrage-Service {#query-service}

Abfragen von Daten im Adobe Experience Platform Data Lake mithilfe von SQL mit Query Service. Nahtloses Kombinieren von Datensätzen und Generieren neuer Datensätze aus Ihren Abfrageergebnissen zur Leistungsverbesserung von Berichten, zur Aktivierung von Datenwissenschaft-Workflows oder zur Erleichterung der Aufnahme in das Echtzeit-Kundenprofil. Beispielsweise können Sie Kundentransaktionsdaten mit Verhaltensdaten zusammenführen, um hochwertige Zielgruppen für zielgerichtete Marketing-Kampagnen zu identifizieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Dater Distiller Authorization API | Verwalten und erzwingen IP-basierte Zugriffsbeschränkungen für Query Service-Sandboxes, um die Datensicherheit zu erhöhen und die Einhaltung von Unternehmensrichtlinien sicherzustellen. Weitere Informationen zu den wichtigsten Funktionen finden Sie im [Data Distiller Authorization API guide](../../query-service/auth-api/overview.md) (Handbuch zur Data Authorization API) oder in der [OpenAPI-Dokumentation](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/) . Dort finden Sie umfassende Informationen einschließlich Endpunktdetails, Parameterlisten, Anforderungs-/Antwortbeispielen und Testfunktionen. |

Weitere Informationen zu [!DNL Query Service] finden Sie in der [[!DNL Query Service] Übersicht](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Um dies zu erreichen, stellt Experience Platform Sandboxes bereit, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Package-Freigabe mit der Sandbox-Tool-API | Verwenden Sie zwei neue API-Endpunkte, [`/handshake`](../../sandboxes/sandbox-tooling-api/packages.md#org-linking) und [`/transfers`](../../sandboxes/sandbox-tooling-api/packages.md#transfer-packages), um die organisationsübergreifende Freigabe von Paketen zu handhaben, z. B. die Validierung von Anforderungen, die Paketanzeige und den Import von Paketen mithilfe der Sandbox-Tool-API. |

Weitere Informationen zu Sandboxes finden Sie in der [Sandbox-Übersicht](../../sandboxes/home.md).

## Dokumentationsaktualisierungen {#documentation-updates}

### Dokumentation zur interaktiven Experience Platform-API {#interactive-api-documentation}

Die [Experience Platform API-Dokumentation](https://developer.adobe.com/experience-platform-apis/) ist jetzt vollständig interaktiv, sodass Sie APIs direkt auf der Seite mit der API-Referenzdokumentation authentifizieren und untersuchen können. Sie können jetzt die gewünschte API-Referenzdokumentationsseite aufrufen, Ihre API-Authentifizierungsberechtigungen erstellen oder abrufen, sie in den Block **[!UICONTROL Testen Sie es]** einfügen und den Aufruf ausführen. Alles auf einer Seite. [Mehr dazu](/help/landing/api-authentication.md#get-credentials-functionality) über die Funktionalität.

### Neues Inhaltsverzeichnis auf Experience League {#new-table-of-contents-on-experience-league}

Das Inhaltsverzeichnis auf den Experience League-Dokumentationsseiten wurde verbessert, um Lesern ein besseres Erlebnis zu bieten, einschließlich eines Keyword-Filters, um die genaue Seite zu ermitteln, die Sie benötigen, der Möglichkeit, alle Seiten zu erweitern und mehr. <br> ![Neues Inhaltsverzeichnis einschließlich Keyword-Filter und Möglichkeit, alle Seiten zu erweitern.](../2024/assets/november/new-toc-experience.gif "Neues Inhaltsverzeichnis einschließlich Keyword-Filter und Möglichkeit, alle Seiten zu erweitern."){width="250" align="center" zoomable="yes"}

### Neue Landingpage des KI-Assistenten {#new-ai-assistant-landing-page}

Verwenden Sie die neue Seite mit der Produktdokumentation für den [AI-Assistenten](../../ai-assistant/landing.md) als Hub für alle Elemente des AI-Assistenten. In der Produktdokumentation finden Sie Video-Tutorials, technische Dokumentation, Anwendungsbeispiele und Links zu Blog-Beiträgen zum AI-Assistenten.