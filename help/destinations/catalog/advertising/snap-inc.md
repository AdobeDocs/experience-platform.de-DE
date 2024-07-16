---
title: Verbindung Snap Inc
description: Erfahren Sie, wie Sie eine Verbindung zur Snapchat Ads-Plattform herstellen und Ihre Audiences vom Experience Platform exportieren können.
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 26%

---

# Verbindung Snap Inc

## Übersicht {#overview}

[Snapchat-Anzeigen](https://forbusiness.snapchat.com/) werden für jedes Unternehmen unabhängig von Größe oder Branche erstellt. Werden Sie Teil der alltäglichen Gespräche von Snapchattern mit digitalen Vollbild-Anzeigen, die von den Menschen, die für Ihr Unternehmen am wichtigsten sind, zum Handeln inspirieren.

>[!IMPORTANT]
>
>Diese Ziel-Connector- und Dokumentationsseite werden vom Team von *Snap Inc* erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an *dev-support@snap.com*

## Anwendungsfälle {#use-cases}

Mit diesem Ziel können Marketingexperten in Experience Platform erstellte Benutzerzielgruppen in Momentaufnahmen-Anzeigen importieren und für das Targeting ihrer Anzeigen verwenden.

## Voraussetzungen {#prerequisites}

Um dieses Ziel zu verwenden, müssen Sie über ein Snapchat Ads-Konto verfügen. Informationen zum Erstellen einer solchen Dokumentation finden Sie in dieser Dokumentation:

[Erste Schritte mit Snapchat Advertising](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Einschränkungen {#limitations}

* Snap Inc unterstützt nicht mehrere Identitäten für ein bestimmtes Zielgruppensegment. Bitte beim Aktivieren eines Segments nur eine Identität zuordnen.
* Snap Inc unterstützt keine Umbenennung von Segmenten. Um ein Segment umzubenennen, müssen Sie es deaktivieren, umbenennen und dann aktivieren.
* Es ist nicht möglich, einen Aufbewahrungszeitraum für die Mitglieder eines Zielgruppensegments zu definieren. Alle Mitglieder haben eine lebenslange Beibehaltung und befinden sich in der Zielgruppe, bis sie entfernt werden.

## Unterstützte Identitäten {#supported-identities}

Das Ziel *Snap Inc* unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

Alle an das Ziel *Snap Inc* gesendeten Kennungen müssen im SHA-256-Format gehasht werden. Um Klartext-IDs zu hash, bevor sie an das Ziel gesendet werden, aktivieren Sie die Option **[!UICONTROL Transformation anwenden]** , wenn Sie Zielkennungen für das Ziel zuordnen.

>[!WARNING]
> 
> Nicht gehashte IDs werden vom Snap Inc-Ziel nicht akzeptiert und das Senden dieser IDs kann zu Fehlern führen.


>[!IMPORTANT]
> 
> Das Snap Inc-Ziel unterstützt nicht mehrere Identitäten. Bitte nur eine Identität auswählen.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail-Adresse | SHA-256-Hashemail-Adresse | Ordnen Sie E-Mail-Adressen dem Zielidentitätsfeld *emailAddress* zu. |
| Telefonnummer | SHA-256 Hash-Telefonnummer | Ordnen Sie E-Mail-Adressen dem Zielidentitätsfeld *phoneNumber* zu. |
| GAID | SHA-256-Hash Google Advertising ID | Ordnen Sie Google Advertising IDs dem Zielidentitätsfeld *gaid* zu. |
| IDFA | SHA-256-Hash Apple Advertising ID | Ordnen Sie Apple Advertising IDs dem Zielidentitätsfeld *idfa* zu. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder andere), die im Ziel *YOURDESTINATION* verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbindung zu Snap Inc {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

### Beim Ziel authentifizieren {#authenticate}

Gehen Sie wie folgt vor, um sich beim Ziel zu authentifizieren:

1. Suchen Sie das Ziel *Snap Inc* aus dem Zielkatalog von Adobe Experience Platform und wählen Sie **Einrichten** aus.
2. Wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus. Sie werden zum folgenden Bildschirm weitergeleitet:
   ![Authentifizierungsbildschirm 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Geben Sie Ihre Snapchat-Anmeldedaten ein und wählen Sie **Anmelden** aus.
4. Ihnen werden die Snapchat-Daten angezeigt, auf die Adobe Experience Platform zugreifen kann. Wählen Sie **Weiter** aus, um mit dem Verbindungsprozess fortzufahren.

![Authentifizierungsbildschirm 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

Nachdem Sie &quot;Weiter&quot;ausgewählt haben, warten Sie, bis Sie zu Adobe Experience Platform zurückgeleitet werden.

### Ausfüllen der Zieldetails {#destination-details}

![Zieldetails](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Um Details für das Ziel zu konfigurieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Weiter]** aus.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Die ID des Anzeigenkontos, die mit dem Anzeigenkonto verknüpft ist, in das Sie Ihre Zielgruppen importieren möchten. Weitere Informationen dazu, wie Sie dies finden, finden Sie in [dieser Dokumentation im Snapchat Business Help Center](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>Wenn Sie eine falsche oder ungültige Snapchat-Konto-ID eingeben, schlägt die Aktivierung der Zielgruppe fehl. Vergewissern Sie sich bitte, dass Sie die richtige Anzeigenkonto-ID eingegeben haben.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

## Überprüfen des Datenexports {#exported-data}

Nachdem Sie Zielgruppen für das Ziel *Snap Inc* aktiviert haben, können Sie die Zielgruppen im Abschnitt [**Zielgruppen** des Snap Ads Manager](https://businesshelp.snapchat.com/s/article/audience-sharing) sehen. Gehen Sie wie folgt vor, um zu diesem Abschnitt zu navigieren:

1. Melden Sie sich beim [Anzeigen-Manager ausrichten](https://ads.snapchat.com/) an
2. Wählen Sie **Zielgruppen** aus dem Pulldown-Menü in der oberen linken Ecke des Bildschirms aus. Sie sehen die Zielgruppen, die Sie in Adobe Experience Platform in der Zielgruppenbibliothek aktiviert haben:

![Zielgruppen](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Beachten Sie bitte, dass eine Adobe-Audience, die zum ersten Mal für Snap Inc aktiviert wird, zunächst als leere Audience betrachtet wird. Dies liegt daran, dass Adobe Experience Platform keine Mitgliedsdaten an Snap Inc exportiert, bis die Audience ausgewertet wird. Weitere Informationen dazu, wie Zielgruppen in Experience Platform ausgewertet werden, finden Sie in der [Segmentation Service - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html#evaluate-segments) .

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).
