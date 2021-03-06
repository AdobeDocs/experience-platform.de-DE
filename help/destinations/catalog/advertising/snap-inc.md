---
title: (Beta) Snap Inc-Verbindung
description: Erfahren Sie, wie Sie eine Verbindung zur Snapchat Ads-Plattform herstellen und Ihre Zielgruppensegmente aus Experience Platform exportieren.
source-git-commit: 734d66cc881ab1b691c13ef446331d0c51851cf9
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 6%

---


# (Beta) Snap Inc

## Übersicht {#overview}

[Snapchat-Anzeigen](https://forbusiness.snapchat.com/) werden für jedes Geschäft gemacht, unabhängig von Größe oder Industrie. Werden Sie Teil der alltäglichen Gespräche von Snapchattern mit digitalen Vollbild-Anzeigen, die von den Menschen, die für Ihr Unternehmen am wichtigsten sind, zum Handeln inspirieren.

>[!IMPORTANT]
>
>Diese Dokumentationsseite wurde von der *Snap Inc* Team. Dies ist derzeit ein Beta-Produkt und die Funktionalität kann sich ändern. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an *dev-support@snap.com*

## Anwendungsfälle {#use-cases}

Mit diesem Ziel können Marketing-Experten in Experience Platform erstellte Benutzersegmente in Momentaufnahmen-Anzeigen importieren und für das Targeting ihrer Anzeigen verwenden.

## Voraussetzungen {#prerequisites}

Um dieses Ziel zu verwenden, müssen Sie über ein Snapchat Ads-Konto verfügen. Informationen zum Erstellen einer solchen Dokumentation finden Sie in dieser Dokumentation:

[Erste Schritte mit Snapchat-Werbung](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Einschränkungen {#limitations}

* Snap Inc unterstützt nicht mehrere Identitäten für ein bestimmtes Zielgruppensegment. Bitte beim Aktivieren eines Segments nur eine Identität zuordnen.
* Snap Inc unterstützt keine Umbenennung von Segmenten. Um ein Segment umzubenennen, müssen Sie es deaktivieren, umbenennen und dann aktivieren.
* Es ist nicht möglich, einen Aufbewahrungszeitraum für die Mitglieder eines Zielgruppensegments zu definieren. Alle Mitglieder verfügen über eine lebenslange Beibehaltung und werden im Segment verbleiben, bis sie entfernt werden.

## Unterstützte Identitäten {#supported-identities}

Die *Snap Inc* Das Ziel unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Weitere Informationen [identities](/help/identity-service/namespaces.md).

Alle an die *Snap Inc* Das Ziel muss im SHA-256-Format gehasht werden. Um Nur-Text-IDs zu hashen, bevor sie an das Ziel gesendet werden, überprüfen Sie die **[!UICONTROL Umwandlung anwenden]** Option bei der Zuordnung von Zielkennungen für das Ziel.

>[!WARNING]
> 
> Nicht gehashte IDs werden vom Snap Inc-Ziel nicht akzeptiert und das Senden dieser IDs kann zu Fehlern führen.


>[!IMPORTANT]
> 
> Das Snap Inc-Ziel unterstützt nicht mehrere Identitäten. Bitte nur eine Identität auswählen.

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail-Adresse | SHA-256-Hash-E-Mail-Adresse | E-Mail-Adressen in das Zielidentitätsfeld zuordnen *emailAddress*. |
| Telefonnummer | SHA-256 Hash-Telefonnummer | E-Mail-Adressen in das Zielidentitätsfeld zuordnen *phoneNumber*. |
| GAID | SHA-256-Hash-Google Advertising ID | Zuordnen von Google Advertising-IDs zum Zielidentitätsfeld *gaid*. |
| IDFA | SHA-256-Hash-Apple Advertising ID | Zuordnen von Apple Advertising-IDs zum Zielidentitätsfeld *idfa*. |

{style=&quot;table-layout:auto&quot;}

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer oder andere), die im *YOURDESTINATION* Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Verbindung zu Snap Inc {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

### An Ziel authentifizieren {#authenticate}

Gehen Sie wie folgt vor, um sich beim Ziel zu authentifizieren:

1. Suchen Sie die *Snap Inc* Ziel aus dem Zielkatalog von Adobe Experience Platform und wählen Sie **Einrichten**.
2. Auswählen **[!UICONTROL Mit Ziel verbinden]**. Sie werden zum folgenden Bildschirm weitergeleitet:
   ![Authentifizierungsbildschirm 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Geben Sie Ihre Snapchat-Anmeldedaten ein und wählen Sie **Anmelden**.
4. Ihnen werden die Snapchat-Daten angezeigt, auf die Adobe Experience Platform zugreifen kann. Auswählen **Weiter** , um mit dem Verbindungsprozess fortzufahren.

![Authentifizierungsbildschirm 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

Nachdem Sie &quot;Weiter&quot;ausgewählt haben, warten Sie, bis Sie zu Adobe Experience Platform zurückgeleitet werden.

### Zieldetails ausfüllen {#destination-details}

![Zieldetails](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Nächste]**.

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Die ID des Anzeigenkontos, die mit dem Anzeigenkonto verknüpft ist, in das Sie Ihre Segmente importieren möchten. Weitere Informationen hierzu finden Sie unter [Diese Dokumentation zum Snapchat Business Help Center](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>Wenn Sie eine falsche oder ungültige Snapchat-Konto-ID eingeben, schlägt die Segmentaktivierung fehl. Vergewissern Sie sich bitte, dass Sie die richtige Anzeigenkonto-ID eingegeben haben.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen über den Status des Datenflusses an Ihr Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Datenexport überprüfen {#exported-data}

Nachdem Sie Segmente für die *Snap Inc* Ziel, können Sie die Segmente im Snap Ads Manager der [**Zielgruppen** Abschnitt](https://businesshelp.snapchat.com/s/article/audience-sharing). Gehen Sie wie folgt vor, um zu diesem Abschnitt zu navigieren:

1. Melden Sie sich bei der [Anzeigen-Manager ausrichten](https://ads.snapchat.com/)
2. Auswählen **Zielgruppen** aus dem Pulldown-Menü in der oberen linken Ecke des Bildschirms. Sie sehen die Segmente, die Sie in Adobe Experience Platform in der Zielgruppenbibliothek aktiviert haben:

![Zielgruppen](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Beachten Sie bitte, dass ein Adobe-Segment, das zum ersten Mal für Snap Inc aktiviert wird, zunächst als leere Zielgruppe betrachtet wird. Dies liegt daran, dass Adobe Experience Platform keine Mitgliedsdaten an Snap Inc exportiert, bis das Segment ausgewertet wird. Weiterführende Informationen zur Auswertung von Segmenten in Experience Platform finden Sie im Abschnitt [Übersicht über den Segmentierungsdienst](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=en#evaluate-segments).

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](/help/data-governance/home.md).