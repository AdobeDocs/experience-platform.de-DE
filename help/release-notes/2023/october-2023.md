---
title: Adobe Experience Platform – Versionshinweise, Oktober 2023
description: Versionshinweise von Oktober 2023 für Adobe Experience Platform.
exl-id: e9cf5299-8350-4b40-8f56-05e598846875
source-git-commit: 2d640b282feb783694276c69366b1fccadddfd78
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 36%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 25. Oktober 2023**

Aktualisierungen vorhandener Funktionen in Experience Platform:

- [Dashboards](#dashboards)
- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Sandboxes](#sandboxes)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, über die Sie wichtige Einblicke zu den Daten Ihres Unternehmens erhalten, die in täglichen Schnappschüssen erfasst werden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Nutzungsmetriken für Ziele | Dem Dashboard zur Lizenznutzung wurden neue Metriken hinzugefügt. Die Metriken **[!UICONTROL Audience Activation-]** und **[!UICONTROL Datenexportgröße]** bieten eine praktische Möglichkeit, um zu verfolgen, wie viele Daten Sie aus Platform in Bezug auf Ihre Lizenznutzungsberechtigungen exportiert haben. In der [Verfügbare Metriken](../../dashboards/guides/license-usage.md#available-metrics) finden Sie Beschreibungen zu diesen und anderen Lizenznutzungsmetriken. |

{style="table-layout:auto"}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, erhalten Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Typ | Funktion | Beschreibung |
| --- | --- | --- |
| Erweiterungen | Verbesserung der [!DNL Meta] Conversions-API | Es gibt drei Verbesserungen bei der Erweiterung [Meta Conversions-API](/help/tags/extensions/server/meta/overview.md): <ul><li>Integration mit [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): Ermöglicht die nahtlose Anmeldung, indem Sie Ihre Pixel-ID und Ihr Zugriffstoken für die Conversions-API-Integration mit Adobe freigeben.</li><li>Integration mit [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): Ermöglicht das Bereitstellen von Werbung für Personen, die mit höherer Wahrscheinlichkeit eine gewünschte Aktion durchführen, und das Verknüpfen der Aktion mit den bereitgestellten Anzeigen.</li><li>Integration mit [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): Ermöglicht die Übergabe der LiveRamp-Ramp-ID im CIP-Feld, sodass keine personenbezogenen Daten direkt mit Partnern oder Meta geteilt werden müssen. </li></ul> |
| Erweiterungen | [!DNL LinkedIn]-Konversions-API | Mit der [[!DNL LinkedIn] Conversions API](../../tags/extensions/server/linkedin/overview.md)-Erweiterung können Sie die Effektivität Ihrer LinkedIn-Marketing-Kampagnen bewerten, indem Sie Experience Platform-Ereignisdaten an LinkedIn weiterleiten. |
| Geheimnis | OAuth 2-Geheimnis [!DNL LinkedIn] | Das [[!DNL LinkedIn] OAuth 2-Geheimnis](../../tags/ui/event-forwarding/secrets.md#linkedin-oauth-2) ermöglicht es Ihnen, Server-zu-Server-Interaktionen an [!DNL LinkedIn] in der Ereignisweiterleitung zu senden. |
| Ereignisweiterleitung | Aktualisierung für Tags und Ereignisweiterleitung | Um die Leistung [Tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=de) und [Ereignisweiterleitung](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) in Platform beizubehalten, werden nur die letzten erfolgreichen und nicht erfolgreichen Entwicklungs- und Staging-Builds beibehalten. Alle nicht mehr verwendeten Builds werden entfernt. Darüber hinaus wurden Drosselung und Ratenbegrenzung implementiert, um sicherzustellen, dass einige wenige starke API-Verwendungen die API-Leistung für andere nicht beeinträchtigen. |
| Erweiterungen | Elemente, Regeln und Erweiterungen | [Elemente, Regeln und Erweiterungen](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html) werden jetzt in der Bibliotheksausgabe sortiert, um mehr Konsistenz zwischen mehreren Builds und Bereitstellungen derselben Bibliothek sicherzustellen. |

Weitere Informationen zur Datenerfassung finden Sie in der [Übersicht der Datenerfassungen](../../tags/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Ziele** {#new-updated-destinations}

| Ziel | Neu oder aktualisiert | Beschreibung |
| ----------- |----------------|----------- |
| [[!DNL MoEngage]](/help/destinations/catalog/mobile-engagement/moengage.md) | Neu | Verwenden Sie das Moengage-Ziel, um Ihre Adobe-Daten (Benutzerattribute, Segmente und Ereignisse) mit MoEngage in Echtzeit zu verbinden und zuzuordnen. Kunden können diese Daten dann nutzen und personalisierte, zielgerichtete Erlebnisse bereitstellen. |
| [[!DNL Qualtrics Automations]](/help/destinations/catalog/survey/qualtrics-automations.md) | Neu | Verwenden Sie die Aggregation mehrerer betrieblicher Datenquellen in Adobe Experience Platform als Eingabe in der Qualtrics Experience ID, um Ihre Kunden besser zu verstehen und eine gezielte Kontaktaufnahme zu ermöglichen, um die Lücke zu schließen, wenn es um das Verständnis von Intent-, Emotions- und Erlebnistreibenden geht. |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| (Beta) Unterstützung für Hash-Funktionen in berechneten Feldern | Zusätzlich zu den Funktionen für den [Export von Arrays](../../destinations/ui/export-arrays-maps-objects.md) oder Elementen aus einem Array können Sie jetzt zusätzliche [Hashing-Funktionen](../../destinations/ui/export-arrays-maps-objects.md#hashing-functions) verwenden, um Attribute in den exportierten Dateien zu hashen. Die unterstützten Hash-Funktionen sind: `sha`, `sha256`, `sha512`, `hash`, `md5`, `crc32`. |
| (Eingeschränkte GA) Aktivieren von Konto-Zielgruppen für bestimmte Ziele | Real-Time CDP B2B-Kunden können jetzt [Account-Zielgruppen](../../segmentation/types/account-audiences.md) für bestimmte Ziele aktivieren. Weitere Informationen zu dieser Funktion finden Sie im Tutorial [Aktivieren von Konto-Zielgruppen](/help/destinations/ui/activate-account-audiences.md). |

{style="table-layout:auto"}

**Korrekturen und Verbesserungen** {#destinations-fixes-and-enhancements}

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Um diese Anforderung zu erfüllen, stellt Experience Platform Sandboxes bereit, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

**Neue Funktion**

| Funktion | Beschreibung |
| --- | --- |
| Sandbox-Werkzeuge | Mit der Sandbox-Tooling-Funktion können Sie die Konfigurationsgenauigkeit in Sandboxes verbessern und Sandbox-Konfigurationen zwischen Sandboxes nahtlos exportieren und importieren. Sie können die Sandbox-Tooling-Funktion verwenden, um verschiedene Objekte auszuwählen und sie in ein Paket zu exportieren. Weitere Informationen finden Sie im [Handbuch zur Sandbox-Tooling-Benutzeroberfläche](../../sandboxes/ui/sandbox-tooling.md). |

Weiterführende Informationen zu Sandboxes finden Sie in der [Sandbox-Übersicht](../../sandboxes/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht es Ihnen, in [!DNL Experience Platform] gespeicherte Daten, die sich auf Einzelpersonen (wie Kundinnen und Kunden, Interessierte, Benutzerinnen und Benutzer oder Organisationen) beziehen, in Zielgruppen zu segmentieren. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten erstellen. Diese Zielgruppen werden zentral auf [!DNL Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

**Neue Funktion**

| Funktion | Beschreibung |
| ------- | ----------- |
| Account Audiences (begrenzte GA) | In Real-Time Customer Data Platform B2B edition können Sie jetzt die Kontosegmentierung verwenden, um das Marketing-Segmentiererlebnis von personenbasierten Zielgruppen bis hin zu Account-basierten Zielgruppen vollständig zu vereinfachen und zu verfeinern. Weitere Informationen zu dieser Funktion finden Sie im Abschnitt [Übersicht über Kontozielgruppen](../../segmentation/types/account-audiences.md). |

Weitere Informationen zum Segmentierungs-Service finden Sie unter [Segmentierungs-Service - Übersicht](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierung der Authentifizierung für die Data Landing Zone | Sie können jetzt das vorgesehene Ablaufdatum Ihrer Data Landing Zone sehen, wenn Sie Ihre Anmeldedaten anzeigen. Sie müssen Ihr Token vor dem Ablaufdatum aktualisieren, um es in Ihrer Anwendung weiterhin verwenden zu können. Wenn Sie Ihr Token nicht vor dem angegebenen Ablaufdatum manuell aktualisieren, wird es automatisch aktualisiert und ein neues Token bereitgestellt, wenn Sie das nächste Mal Ihre Anmeldeinformationen abrufen. Weitere Informationen finden Sie in der Dokumentation unter [Verwenden der Data Landing Zone](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen - Übersicht](../../sources/home.md).
