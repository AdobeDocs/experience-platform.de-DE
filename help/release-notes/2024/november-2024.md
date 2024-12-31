---
title: Adobe Experience Platform – Versionshinweise November 2024
description: Die Versionshinweise von November 2024 für Adobe Experience Platform.
exl-id: e3969f8b-70b2-40f8-bb9b-5be6e3d8f722
source-git-commit: f71fc1d4ad51af52046caeee289546e05967d5bd
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 19%

---

# Adobe Experience Platform – Versionshinweise

>[!TIP]
>
>Die neue [KI-Assistent](../../ai-assistant/landing.md)Produktdokumentation) ist jetzt verfügbar. Verwenden Sie diese Seite als Hub für alle Ressourcen im Zusammenhang mit dem KI-Assistenten.

**Versionsdatum: Mittwoch, 26. November 2024**

Aktualisierungen vorhandener Funktionen und Dokumentationen in Adobe Experience Platform:

- [KI-Assistent](#ai-assistant)
- [Ziele](#destinations)
- [Abfrage-Service](#query-service)
- [Sandboxes](#sandboxes)
- [Dokumentationsaktualisierungen](#documentation-updates)
   - [Dokumentation zur Interactive Experience Platform API](#interactive-experience-platform-api-documentation)
   - [Neues Inhaltsverzeichnis auf Experience League](#new-table-of-contents-on-experience-league)
   - [Neue Landingpage des KI-Assistenten](#new-ai-assistant-landing-page)

## KI-Assistent {#ai-assistant}

Der KI-Assistent in Adobe Experience Platform ist ein Gesprächserlebnis, mit dem Sie Ihre Workflows in Adobe-Anwendungen beschleunigen können. Sie können den KI-Assistenten verwenden, um Produktkenntnisse besser zu verstehen, Probleme zu beheben oder Informationen zu durchsuchen und betriebliche Erkenntnisse zu gewinnen. Der KI-Assistent unterstützt Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer und Customer Journey Analytics.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Alpha ]{type=Informative} Überwachen Sie signifikante Änderungen und prognostizieren Sie das Zielgruppenwachstum | Verwenden Sie den KI-Assistenten, um signifikante Änderungen zu überwachen und Wachstumsprognosen für Ihre Audience und Datensatzgrößen bereitzustellen. Anschließend können Sie diese Informationen verwenden, um die Integrität Ihrer Zielgruppendaten sicherzustellen und zukunftsgerichtete Prognosen anzubieten, um dateninformierte Entscheidungsfindungen zu unterstützen. Weitere Informationen finden Sie im Handbuch unter [Überwachen signifikanter Änderungen und Prognostizieren des Zielgruppenwachstums](../../ai-assistant/new-features/audience-forecasting.md). |
| [!BADGE Alpha ]{type=Informative} Schätzung der natürlichen Sprache | Nutzen Sie die Funktionen des KI-Assistenten zur Schätzung natürlicher Sprachen, um die Größe von Zielgruppen zu schätzen und die Neigung von Zielgruppen auf der Grundlage einfacher, dialogorientierter Fragen vorherzusagen. Weitere Informationen finden Sie im Handbuch unter [Verwenden der Schätzung natürlicher Sprache mit dem KI-Assistenten](../../ai-assistant/new-features/natural-language.md). |

{style="table-layout:auto"}

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Ziele** {#new-updated-destinations}

| Ziel | Beschreibung |
| --- | --- |
| [Magnite-Streaming in Echtzeit](/help/destinations/catalog/advertising/magnite-streaming.md) | Exportieren Sie Zielgruppen für Aktivierung, Targeting oder Unterdrückung in der Magnite-Streaming-Plattform. Damit Zielgruppen korrekt in Magnitre exportiert werden können, müssen Sie sowohl die Echtzeit- als auch die Batch-Ziele verwenden. |
| [Magnite Streaming Batch](/help/destinations/catalog/advertising/magnite-batch.md) | Exportieren Sie Zielgruppen für Aktivierung, Targeting oder Unterdrückung in der Magnite-Streaming-Plattform. Damit Zielgruppen korrekt in Magnitre exportiert werden können, müssen Sie sowohl die Echtzeit- als auch die Batch-Ziele verwenden. |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktion | Beschreibung |
| --- | --- |
| [Profilattribute in Echtzeit am Edge nachschlagen](/help/destinations/ui/activate-edge-profile-lookup.md) | Erfahren Sie, wie Sie mithilfe der benutzerdefinierten Ziel- und Edge Network-API von Personalization Edge-Profilattribute in Echtzeit nachschlagen können, um Personalisierungserlebnisse bereitzustellen oder Entscheidungsregeln über nachgelagerte Anwendungen zu informieren. |

{style="table-layout:auto"}

Lesen Sie für Weitere Informationen den [Überblick über die Ziele](../../destinations/home.md).

## Abfrage-Service {#query-service}

Abfragen von Daten im Data Lake von Adobe Experience Platform unter Verwendung von Standard-SQL mit dem Abfrage-Service. Nahtlose Kombination von Datensätzen und Generierung neuer Datensätze aus Ihren Abfrageergebnissen, um das Reporting zu optimieren, datenwissenschaftliche Workflows zu ermöglichen oder die Aufnahme in das Echtzeit-Kundenprofil zu erleichtern. Sie können beispielsweise Kundentransaktionsdaten mit Verhaltensdaten zusammenführen, um hochwertige Zielgruppen für zielgerichtete Marketing-Kampagnen zu identifizieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Dater Distiller Authorization API | Verwalten und Erzwingen von IP-basierten Zugriffsbeschränkungen für Query Service-Sandboxes, um die Datensicherheit zu erhöhen und die Einhaltung von Unternehmensrichtlinien sicherzustellen. Weitere Informationen, einschließlich Details zu Endpunkten[ Parameterlisten, Anfrage-/Antwortbeispielen und Testfunktionen, finden Sie im Data Distiller Authorization API](../../query-service/auth-api/overview.md)Handbuch für weitere Informationen zu den wichtigsten Funktionen und Funktionen oder in der [OpenAPI](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/)Dokumentation. |

Weitere Informationen zu [!DNL Query Service] finden Sie in der [[!DNL Query Service] Übersicht](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Um diese Anforderung zu erfüllen, stellt Experience Platform Sandboxes bereit, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Package-Freigabe mit der Sandbox-Tooling-API | Verwenden Sie zwei neue API-Endpunkte, [`/handshake`](../../sandboxes/sandbox-tooling-api/packages.md#org-linking) und [`/transfers`](../../sandboxes/sandbox-tooling-api/packages.md#transfer-packages), um die Paketfreigabe zwischen Organisationen zu verarbeiten, z. B. Anforderungsgenehmigungen, Paketsichtbarkeit und den Import von Paketen mithilfe der Sandbox-Tool-API. |

Weitere Informationen zu Sandboxes finden Sie unter [Sandbox-Übersicht](../../sandboxes/home.md).

## Dokumentationsaktualisierungen {#documentation-updates}

### Dokumentation zur Interactive Experience Platform API {#interactive-api-documentation}

Die [Experience Platform-API-Dokumentation](https://developer.adobe.com/experience-platform-apis/) ist jetzt vollständig interaktiv, sodass Sie sich authentifizieren und APIs direkt auf der Seite mit der API-Referenzdokumentation erkunden können. Sie können jetzt zur gewünschten Seite zur API-Referenzdokumentation wechseln, Ihre API-Authentifizierungsdaten erstellen oder abrufen, sie in den Block &quot;**[!UICONTROL versuchen]** einfügen und den Aufruf ausführen. Alles auf einer Seite. [Weitere Informationen](/help/landing/api-authentication.md#get-credentials-functionality) über die Funktion.

### Neues Inhaltsverzeichnis auf Experience League {#new-table-of-contents-on-experience-league}

Das Inhaltsverzeichnis auf Experience League-Dokumentationsseiten wurde verbessert, um den Lesern ein besseres Erlebnis zu bieten, einschließlich eines Keyword-Filters, um die genaue benötigte Seite zu ermitteln, der Möglichkeit, alle Seiten zu erweitern und mehr. <br> ![Neues Inhaltsverzeichnis-Erlebnis einschließlich Keyword-Filter und Möglichkeit, alle Seiten zu erweitern.](../2024/assets/november/new-toc-experience.gif "Neues Inhaltsverzeichnis-Erlebnis einschließlich Keyword-Filter und Möglichkeit, alle Seiten zu erweitern."){width="250" align="center" zoomable="yes"}

### Neue Landingpage des KI-Assistenten {#new-ai-assistant-landing-page}

Verwenden Sie die neue Seite [KI-Assistent](../../ai-assistant/landing.md)Produktdokumentation) als Drehscheibe für alle Dinge mit dem KI-Assistenten. Siehe die Produktdokumentation für Video-Tutorials, technische Dokumentation, Anwendungsfälle und Links zu Blog-Beiträgen über AI Assistant.
