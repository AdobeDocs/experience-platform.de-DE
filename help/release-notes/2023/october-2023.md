---
title: Adobe Experience Platform – Versionshinweise, Oktober 2023
description: Versionshinweise von Oktober 2023 für Adobe Experience Platform.
exl-id: e9cf5299-8350-4b40-8f56-05e598846875
source-git-commit: d6e306294d0a119108e2de7ba03ebed4f633fba1
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 37%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Donnerstag, 25. Oktober 2023**

Aktualisierungen vorhandener Funktionen im Experience Platform:

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
| Verwendungsmetriken für Ziele | Dem Dashboard zur Lizenznutzung wurden neue Messmetriken hinzugefügt. Die Metriken **[!UICONTROL Audience Activation-Größe]** und **[!UICONTROL Datenexportgröße]** bieten eine praktische Möglichkeit, um nachzuverfolgen, wie viele Daten Sie aus Platform in Bezug auf Ihre Lizenznutzungsberechtigungen exportiert haben. Beschreibungen dieser und anderer Lizenzverwendungsmetriken finden Sie in der Dokumentation zu [verfügbaren Metriken](../../dashboards/guides/license-usage.md#available-metrics) . |

{style="table-layout:auto"}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, erhalten Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Typ | Funktion | Beschreibung |
| --- | --- | --- |
| Erweiterungen | [!DNL Meta] API-Erweiterung für Konversionen | Die Erweiterung [Meta Conversions API](/help/tags/extensions/server/meta/overview.md) wurde um drei Verbesserungen erweitert: <ul><li>Integration mit [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): Erstellt eine nahtlose Anmeldung, indem Sie Ihre pixelID und das Zugriffstoken für die Conversions-API-Integration mit Adobe freigeben können.</li><li>Integration in [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): Ermöglicht die Bereitstellung von Werbung für Personen, die mit höherer Wahrscheinlichkeit eine gewünschte Aktion durchführen und die Aktion mit den gelieferten Anzeigen verknüpfen.</li><li>Integration mit [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): Ermöglicht die Weitergabe der RampID von LiveRamp im Feld CIP, sodass personenbezogene Daten nicht direkt an Partner oder Meta weitergegeben werden müssen. </li></ul> |
| Erweiterungen | [!DNL LinkedIn] Konversions-API | Mit der Erweiterung [[!DNL LinkedIn] Conversions API](../../tags/extensions/server/linkedin/overview.md) können Sie die Effektivität Ihrer LinkedIn-Marketingkampagnen bewerten, indem Sie Experience Platform-Ereignisdaten an LinkedIn weiterleiten. |
| Geheimnis | [!DNL LinkedIn] OAuth 2 Secret | Mit dem [[!DNL LinkedIn] OAuth 2 Secret](../../tags/ui/event-forwarding/secrets.md#linkedin-oauth-2) können Sie Server-Server-Interaktionen an [!DNL LinkedIn] in der Ereignisweiterleitung senden. |
| Ereignisweiterleitung | Aktualisierung auf Tags und Ereignisweiterleitung | Damit die Leistung von [Tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=de) und [Ereignisweiterleitung](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) in Platform erhalten bleibt, werden nur die neuesten, erfolgreichen und nicht erfolgreichen Entwicklungs- und Staging-Builds beibehalten. Alle nicht mehr verwendeten Builds werden entfernt. Darüber hinaus wurden Drosselung und Ratenbegrenzung implementiert, um sicherzustellen, dass die API-Leistung bei einigen umfangreichen API-Verwendungen nicht durch andere beeinträchtigt wird. |
| Erweiterungen | Elemente, Regeln und Erweiterungen | [Elemente, Regeln und Erweiterungen](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html) werden jetzt in der Bibliotheksausgabe sortiert, um eine größere Konsistenz zwischen mehreren Builds und Implementierungen derselben Bibliothek sicherzustellen. |

Weitere Informationen zur Datenerfassung finden Sie in der [Übersicht der Datenerfassungen](../../tags/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Ziele** {#new-updated-destinations}

| Ziel | Neu oder aktualisiert | Beschreibung |
| ----------- |----------------|----------- |
| [[!DNL MoEngage]](/help/destinations/catalog/mobile-engagement/moengage.md) | Neu | Verwenden Sie das Ziel &quot;Interagieren&quot;, um Ihre Adobe-Daten (Benutzerattribute, Segmente und Ereignisse) in Echtzeit mit MoEngage zu verbinden und zuzuordnen. Kunden können dann auf diese Daten reagieren und personalisierte, zielgerichtete Erlebnisse bereitstellen. |
| [[!DNL Qualtrics Automations]](/help/destinations/catalog/survey/qualtrics-automations.md) | Neu | Verwenden Sie die Aggregation mehrerer Quellen operativer Daten in Adobe Experience Platform als Eingabe für die Qualtrics Experience ID, um Ihre Kunden besser zu verstehen und zielgerichtete Kontakte zu ermöglichen, um die Lücke im Hinblick auf das Verständnis von Intent-, Emotions- und Erlebnistreibern zu schließen. |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| (Beta) Unterstützung für Hashing-Funktionen in berechneten Feldern | Zusätzlich zu den Funktionen, die für den [Export von Arrays](../../destinations/ui/export-arrays-calculated-fields.md) oder Elementen aus einem Array spezifisch sind, können Sie jetzt zusätzliche [Hashing-Funktionen](../../destinations/ui/export-arrays-calculated-fields.md#hashing-functions) verwenden, um Attribute in den exportierten Dateien zu hash. Folgende Hashing-Funktionen werden unterstützt: `sha`, `sha256`, `sha512`, `hash`, `md5`, `crc32`. |
| (Eingeschränkte allgemeine Verfügbarkeit) Konto-Zielgruppen für bestimmte Ziele aktivieren | Real-Time CDP-B2B-Kunden können jetzt [Kontozielgruppen](../../segmentation/ui/account-audiences.md) für bestimmte Ziele aktivieren. Weitere Informationen zu dieser Funktion finden Sie im Tutorial [Kontozielgruppen aktivieren](/help/destinations/ui/activate-account-audiences.md) . |

{style="table-layout:auto"}

**Korrekturen und Verbesserungen** {#destinations-fixes-and-enhancements}

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Um dies zu erreichen, stellt Experience Platform Sandboxes bereit, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

**Neue Funktion**

| Funktion | Beschreibung |
| --- | --- |
| Sandbox-Werkzeuge | Mit der Sandbox-Tool-Funktion können Sie die Konfigurationsgenauigkeit über Sandboxes hinweg verbessern und Sandbox-Konfigurationen nahtlos zwischen Sandboxes exportieren und importieren. Sie können die Sandbox-Tool-Funktion verwenden, um verschiedene Objekte auszuwählen und sie in ein Paket zu exportieren. Weitere Informationen finden Sie im Leitfaden für die Sandbox-Tools-Benutzeroberfläche ](../../sandboxes/ui/sandbox-tooling.md).[ |

Weiterführende Informationen zu Sandboxes finden Sie in der [Sandbox-Übersicht](../../sandboxes/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht es Ihnen, in [!DNL Experience Platform] gespeicherte Daten, die sich auf Einzelpersonen (wie Kundinnen und Kunden, Interessierte, Benutzerinnen und Benutzer oder Organisationen) beziehen, in Zielgruppen zu segmentieren. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten erstellen. Diese Zielgruppen werden zentral auf [!DNL Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

**Neue Funktion**

| Funktion | Beschreibung |
| ------- | ----------- |
| Kontozielgruppen (beschränkte allgemeine Verfügbarkeit) | In Real-time Customer Data Platform B2B edition können Sie jetzt die Kontosegmentierung verwenden, um die gesamte Einfachheit und Komplexität der Marketing-Segmentierungserfahrung von benutzerbezogenen Zielgruppen zu kontobasierten Zielgruppen zu erzielen. Weitere Informationen zu dieser Funktion finden Sie in der [Übersicht über Kontozielgruppen](../../segmentation/ui/account-audiences.md) . |

Weiterführende Informationen zu Segmentation Service finden Sie in der [Segmentation Service - Übersicht](../../segmentation/home.md) .

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierte Authentifizierung für Data Landing Zone | Sie können jetzt das vorgesehene Ablaufdatum Ihrer Dateneinstiegszone sehen, wenn Sie Ihre Anmeldedaten anzeigen. Sie müssen Ihr Token vor dem Ablaufdatum aktualisieren, damit Sie es weiterhin in Ihrer Anwendung verwenden können. Wenn Sie Ihr Token nicht vor dem angegebenen Ablaufdatum manuell aktualisieren, wird es automatisch aktualisiert und beim nächsten Abrufen Ihrer Anmeldeinformationen ein neues Token bereitgestellt. Weitere Informationen finden Sie in der Dokumentation zu [Verwendung der Dateneinstiegszone](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Weitere Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md).
