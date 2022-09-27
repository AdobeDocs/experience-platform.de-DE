---
title: Adobe Experience Platform - Versionshinweise - September 2022
description: Die Versionshinweise für Adobe Experience Platform vom September 2022.
source-git-commit: 5335c77b4636d10064e8786525c9f8f893371b9b
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 38%

---

# Adobe Experience Platform – Versionshinweise

**Release-Datum: 28. September 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Experience-Datenmodell (XDM)](#xdm)
- [Identity Service](#identity-service)
- [Quellen](#sources)

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Benutzeroberflächenunterstützung für Auflistungen und empfohlene Werte | Zusätzlich zu den Auflistungen, die die Datenvalidierung ermöglichen, können Sie jetzt [vorgeschlagene Werte hinzufügen oder entfernen](../../xdm/ui/fields/enum.md) für standardmäßige oder benutzerdefinierte Zeichenfolgenfelder, sodass Platform-Benutzer über eine benutzerfreundliche Liste von Werten verfügen, aus denen sie beim Erstellen von Segmenten auswählen können. |

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Feldergruppe | [[!UICONTROL AJO-Klassifizierungsfelder]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Eigenschaften eines bestimmten Elements, mit dem interagiert wurde, wodurch das Vorschlagsereignis ausgelöst wurde. |
| Feldergruppe | [[!UICONTROL Details zur MediaAnalytics-Interaktion]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Verfolgt Medieninteraktionen im Zeitverlauf. |
| Feldergruppe | [[!UICONTROL Informationen zu Mediendetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Verfolgt Mediendetailinformationen. |
| Feldergruppe | [[!UICONTROL Adobe CJM ExperienceEvent - Oberflächen]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Beschreibt Oberflächen für Erlebnisereignisse in Adobe Journey Optimizer. |

{style=&quot;table-layout:auto&quot;}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Verhalten | [[!UICONTROL Zeitreihen]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Werte hinzugefügt für `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Entfernte Werte für `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Feldergruppe | (Mehrfach) | [Mehrere Feldbeschreibungen wurden aktualisiert.](https://github.com/adobe/xdm/pull/1628/files) über Journey Orchestration-Komponenten hinweg. |
| Feldergruppe | (Mehrfach) | [Die Titel für mehrere Adobe Workfront-Komponenten wurden aktualisiert.](https://github.com/adobe/xdm/pull/1634/files) für Konsistenz. |
| Feldergruppe | [[!UICONTROL AJO-Klassifizierungsfelder]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Die Namespaces mehrerer Felder wurden in `xdm`. |
| Feldergruppe | [[!UICONTROL Gemeinsame Felder für Journey Orchestration-Step-Ereignisse]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Es wurde ein neues Feld hinzugefügt. `isReadSegmentTriggerStartEvent`. |
| Feldergruppe | [[!UICONTROL Prognostizierte Wetter]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Die `xdm:uvIndex` -Feld zu einem ganzzahligen Typ hinzu und das `xdm` -Namespace in mehrere Felder, in denen fehlt. |
| Feldergruppe | [[!UICONTROL Informationen zu Mediendetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` und `xdm:implementationDetails` wurden aus der Feldergruppe entfernt. |
| Datentyp | (Mehrfach) | [Mehrere Namen von Medieneigenschaften wurden aktualisiert](https://github.com/adobe/xdm/pull/1626/files) für Konsistenz über verschiedene Datentypen hinweg. |
| Datentyp | [[!UICONTROL Implementierungsdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Es wurden bekannte Namen für Flutter hinzugefügt. |
| Datentyp | [[!UICONTROL Details zum POI]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | Der Datentyp kann jetzt eine Liste von Schlüssel-Wert-Paaren für Metadaten akzeptieren, die mit dem Zielpunkt verknüpft sind. |
| Datentyp | [[!UICONTROL Vorschlagsaktion]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] wurde in [!UICONTROL Vorschlagsaktion]. |
| Datentyp | [[!UICONTROL Vorschlagsereignistyp]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] wurde in [!UICONTROL Vorschlagsaktion]. |
| (Mehrfach) | (Mehrfach) | Experimentelle Eigenschaften wurden [stabilisiert über alle B2B-Komponenten hinweg](https://github.com/adobe/xdm/pull/1617/files). |
| (Mehrfach) | (Mehrfach) | Adobe Journey Optimizer-Entitäten wurden [stabilisiert](https://github.com/adobe/xdm/pull/1625/files). |
| (Mehrfach) | (Mehrfach) | Die Namespaces bestimmter Felder für verschiedene experimentelle Komponenten wurden [für Konsistenz aktualisiert](https://github.com/adobe/xdm/pull/1626/files). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Identity Service {#identity-service}

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihres Kunden erforderlich. Dies wird schwieriger, wenn Ihre Kundendaten über verschiedene Systeme verteilt sind, wodurch jeder Kunde über mehrere &quot;Identitäten&quot;verfügt.

Mit Adobe Experience Platform Identity Service erhalten Sie einen besseren Überblick über Ihren Kunden und sein Verhalten, indem Identitäten zwischen Geräten und Systemen überbrückt werden, sodass Sie in Echtzeit für effektive, persönliche digitale Erlebnisse sorgen können.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für das Löschen von Datensätzen | Identity Service unterstützt jetzt das Löschen von Datensätzen, wenn über die [Catalog Service-API](https://developer.adobe.com/experience-platform-apis/references/catalog/), Benutzeroberfläche oder Datenhygiene. Lesen Sie das Handbuch unter [Löschen von Datensätzen in der Benutzeroberfläche](../../catalog/datasets/user-guide.md#delete-a-dataset) für weitere Informationen. |

Weitere Informationen zum Identity Service finden Sie im Abschnitt [Identity Service - Übersicht](../../identity-service/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Auswirkungen der Population des Audience Manager-Segments auf das Echtzeit-Kundenprofil | Die Erfassung umfangreicher Audience Manager-Segmentpopulationen hat einen direkten Einfluss auf Ihre Gesamtprofilanzahl, wenn Sie zum ersten Mal ein Audience Manager-Segment mit der Audience Manager-Quelle an Platform senden. Das bedeutet, dass die Auswahl aller Segmente potenziell zu einer Profilanzahl führen kann, die über Ihrer Lizenznutzungsberechtigung liegt. Weitere Informationen finden Sie im Abschnitt [Übersicht über die Audience Manager-Quelle](../../sources/connectors/adobe-applications/audience-manager.md). Informationen zur Verwendung Ihrer Lizenz finden Sie in der Dokumentation unter [Verwenden des Dashboards zur Lizenznutzung](../../dashboards/guides/license-usage.md). |

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen - Übersicht](../../sources/home.md).