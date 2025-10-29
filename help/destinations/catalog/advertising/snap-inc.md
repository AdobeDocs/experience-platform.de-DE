---
title: Snap Inc-Verbindung
description: Erfahren Sie, wie Sie eine Verbindung zur Snapchat Ads-Plattform herstellen und Ihre Zielgruppen aus Experience Platform exportieren.
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 23%

---

# Snap Inc-Verbindung

## Überblick {#overview}

[Snapchat Ads](https://forbusiness.snapchat.com/) werden für jedes Unternehmen, unabhängig von Größe oder Branche, hergestellt. Werden Sie Teil der täglichen Gespräche von Snapchatters mit digitalen Vollbild-Anzeigen, die die Menschen inspirieren, die für Ihr Unternehmen am wichtigsten sind.

>[!IMPORTANT]
>
>Dieser Ziel-Connector und diese Dokumentationsseite werden vom Team von *Snap Inc* erstellt und verwaltet. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an *dev-support@snap.com*

## Anwendungsfälle {#use-cases}

Mit diesem Ziel können Marketing-Fachleute in Experience Platform erstellte Benutzer-Zielgruppen in Snapchat Ads importieren und für das Targeting von Anzeigen verwenden.

## Voraussetzungen {#prerequisites}

Um dieses Ziel verwenden zu können, müssen Sie über ein Snapchat Ads-Konto verfügen. Weitere Informationen zur Erstellung einer solchen finden Sie in dieser Dokumentation:

[Erste Schritte mit Snapchat Advertising](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Einschränkungen {#limitations}

* Snap Inc unterstützt nicht mehrere Identitäten für ein bestimmtes Zielgruppensegment. Bitte ordnen Sie beim Aktivieren eines Segments nur eine Identität zu.
* Snap Inc unterstützt nicht das Umbenennen von Segmenten. Um ein Segment umzubenennen, müssen Sie es deaktivieren, umbenennen und dann aktivieren.
* Es ist nicht möglich, einen Aufbewahrungszeitraum für die Mitglieder eines Zielgruppensegments zu definieren. Alle Mitglieder verfügen über eine lebenslange Beibehaltung und sind in der Zielgruppe, bis sie entfernt werden.

## Unterstützte Identitäten {#supported-identities}

Das *Snap Inc*-Ziel unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

Alle Kennungen, die an das Ziel *Snap Inc* gesendet werden, müssen im SHA-256-Format gehasht werden. Um Textkennungen vor dem Senden an das Ziel zu hashen, aktivieren Sie die Option **[!UICONTROL Apply transformation]** beim Zuordnen von Zielkennungen für das Ziel.

>[!WARNING]
> 
> Ungehashte Kennungen werden vom Snap Inc-Ziel nicht akzeptiert und ihr Versand könnte zu Fehlern führen.


>[!IMPORTANT]
> 
> Das Snap Inc -Ziel unterstützt nicht mehrere Identitäten. Bitte nur eine Identität auswählen.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail-Adresse | SHA-256 gehashte E-Mail-Adresse | Ordnen Sie E-Mail-Adressen dem Zielidentitätsfeld (*-Adresse* zu. |
| Telefonnummer | SHA-256 Hash-Telefonnummer | Ordnen Sie E-Mail-Adressen dem Zielidentitätsfeld (*)*. |
| GAID | SHA-256 hashte Google Advertising ID | Ordnen Sie Google Advertising-IDs dem Zielidentitätsfeld (*)*. |
| IDFA | SHA-256 hashte Apple Advertising ID | Ordnen Sie Apple Advertising-IDs dem Zielidentitätsfeld (*)*. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |
| [!DNL Federated Audience Composition] | ✓ | Zielgruppen, die über die [Federated Audience Composition“ in Experience Platform importiert ](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/audiences). |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder sonstiges), die im Snap Inc -Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbindung mit Snap Inc. herstellen {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

### Beim Ziel authentifizieren {#authenticate}

Gehen Sie wie folgt vor, um sich beim Ziel zu authentifizieren:

1. Suchen Sie das *Snap Inc*-Ziel im Zielkatalog von Adobe Experience Platform und wählen Sie **Einrichten**.
2. Wählen Sie **[!UICONTROL Connect to destination]** aus. Sie werden zum folgenden Bildschirm weitergeleitet:
   ![Authentifizierungsbildschirm 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Geben Sie Ihre Snapchat-Anmeldeinformationen ein und wählen Sie **Anmelden** aus.
4. Ihnen werden die Snapchat-Daten angezeigt, auf die Adobe Experience Platform zugreifen kann. Wählen **Weiter**, um mit dem Verbindungsprozess fortzufahren.

![Authentifizierungsbildschirm 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

Nachdem Sie auf Weiter geklickt haben, warten Sie, bis Sie wieder zu Adobe Experience Platform weitergeleitet werden.

### Ausfüllen der Zieldetails {#destination-details}

![Zieldetails](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Um Details für das Ziel zu konfigurieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Next]** aus.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Account ID]**: Die ID des Werbekontos, das mit dem Werbekonto verknüpft ist, in das Sie Ihre Zielgruppen importieren möchten. Weitere Informationen dazu finden Sie in [ Dokumentation im Snapchat Business Help Center](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>Die Eingabe einer falschen oder ungültigen Snapchat-Anzeigenkonto-ID führt dazu, dass die Zielgruppenaktivierung fehlschlägt. Bitte überprüfen Sie, ob Sie die richtige Werbekonto-ID eingegeben haben.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

## Überprüfen des Datenexports {#exported-data}

Nach der Aktivierung der Zielgruppen für *Ziel „Snap*&quot; werden die Zielgruppen im Abschnitt „Zielgruppen“ des [**-**-Managers ](https://businesshelp.snapchat.com/s/article/audience-sharing). Gehen Sie wie folgt vor, um zu diesem Abschnitt zu navigieren:

1. Melden Sie sich beim [Snap Ads Manager](https://ads.snapchat.com/) an
2. Wählen **Zielgruppen** aus dem Pulldown-Menü in der oberen linken Ecke des Bildschirms aus. Die Zielgruppen, die Sie in Adobe Experience Platform aktiviert haben, werden in der Zielgruppenbibliothek angezeigt:

![Zielgruppen](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Beachten Sie, dass eine Adobe-Zielgruppe bei der ersten Aktivierung für Snap Inc zunächst als leere Zielgruppe angezeigt wird. Dies liegt daran, dass Adobe Experience Platform Mitgliedsdaten erst dann in Snap Inc. exportiert, wenn es die Zielgruppe bewertet. Weitere Informationen zur Auswertung von Zielgruppen in Experience Platform finden Sie unter [Segmentierungs-Service - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html#evaluate-segments).

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).
