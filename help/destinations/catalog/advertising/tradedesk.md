---
keywords: Werbung; The Trade Desk; Advertising Trade Desk
title: Verbindung mit The Trade Desk
description: The Trade Desk ist eine Self-Service-Plattform für Anzeigenkäufer, um Retargeting und zielgruppenorientierte digitale Kampagnen für Display-, Video- und mobile Inventarquellen auszuführen.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 0954b5f22d609b0b12352de70f6c618cc88757c8
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 29%

---

# [!DNL The Trade Desk]-Verbindung

## Übersicht {#overview}

>[!IMPORTANT]
>
>* Ab dem 31. Juli 2025 können Sie im Zielkatalog zwei **[!DNL The Trade Desk]** nebeneinander sehen. Dies ist auf ein internes Upgrade des Ziel-Service zurückzuführen. Der vorhandene **[!DNL The Trade Desk]**-Ziel-Connector wurde in **[!UICONTROL (veraltet) umbenannt. The Trade Desk]** und eine neue Karte mit dem Namen **[!UICONTROL The Trade Desk]** ist jetzt für Sie verfügbar.
>* Verwenden Sie die neue **[!UICONTROL The Trade Desk]**-Verbindung im Katalog für neue Aktivierungsdatenflüsse. Wenn Sie aktive Datenflüsse zum Ziel **[!UICONTROL (veraltet) The Trade Desk]** haben, werden diese automatisch aktualisiert, sodass keine Aktion von Ihnen erforderlich ist.
>* Wenn Sie Datenflüsse über die [Flow Service-API](https://developer.adobe.com/experience-platform-apis/references/destinations/) erstellen, müssen Sie Ihre [!DNL flow spec ID] und [!DNL connection spec ID] auf die folgenden Werte aktualisieren:
>   * Flussspezifikations-ID: `86134ea1-b014-49e8-8bd3-689f4ce70578`
>   * Verbindungsspezifikations-ID: `1029798b-a97f-4c21-81b2-e0301471166e`

Verwenden Sie diesen Ziel-Connector, um Profildaten an [!DNL The Trade Desk] zu senden. Dieser Connector sendet Daten an den [!DNL The Trade Desk] Erstanbieter-Endpunkt. Die Integration zwischen Adobe Experience Platform und [!DNL The Trade Desk] unterstützt nicht den Export von Daten an den [!DNL The Trade Desk] Drittanbieterendpunkt.

[!DNL The Trade Desk] ist eine Self-Service-Plattform für Anzeigenkäufer, um Retargeting und zielgruppenorientierte digitale Kampagnen für Display-, Video- und mobile Inventarquellen auszuführen.

Um Profildaten an [!DNL The Trade Desk] zu senden, müssen Sie zunächst eine Verbindung zum Ziel herstellen, wie in den folgenden Abschnitten dieser Seite beschrieben.

## Anwendungsfälle {#use-cases}

Als Marketing-Experte möchte ich in der Lage sein, Zielgruppen, die aus [!DNL Trade Desk IDs]- oder Geräte-IDs bestehen, zur Erstellung digitaler Retargeting- oder Zielgruppen-bezogener Kampagnen zu verwenden.

## Unterstützte Identitäten {#supported-identities}

[!DNL The Trade Desk] unterstützt die Aktivierung von Zielgruppen basierend auf den in der folgenden Tabelle aufgeführten Identitäten. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

Im Folgenden finden Sie die von [!DNL The Trade Desk] Ziel unterstützten Identitäten. Diese Identitäten können verwendet werden, um Zielgruppen für die [!DNL The Trade Desk] zu aktivieren.

Alle Identitäten in der folgenden Tabelle sind obligatorische Zuordnungen.

| Zielidentität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple-ID für Werbetreibende | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| ECID | Experience Cloud ID | Diese Identität ist erforderlich, damit die Integration ordnungsgemäß funktioniert, wird aber nicht zur Zielgruppenaktivierung verwendet. |
| Die Trade Desk-ID | Advertiser-ID in der [!DNL The Trade Desk] | Verwenden Sie diese Identität, wenn Sie Zielgruppen aktivieren, die auf der proprietären ID von The Trade Desk basieren. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe an das Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit [!DNL The Trade Desk] erstellen möchten und die [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/de/docs/id-service/using/id-service-api/methods/idsync) im Experience Cloud ID-Service noch nicht aktiviert haben (mit Adobe Audience Manager oder anderen Programmen), wenden Sie sich an Adobe Consulting oder die Kundenunterstützung, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor [!DNL The Trade Desk] Integrationen in Audience Manager eingerichtet hatten, werden die von Ihnen eingerichteten ID-Synchronisierungen auf Experience Platform übertragen.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre [!DNL The Trade Desk] [!UICONTROL Konto-ID].
* **[!UICONTROL Server-Standort]**: Fragen Sie Ihren [!DNL The Trade Desk], welchen regionalen Server Sie verwenden sollten. Nachfolgend sind die verfügbaren regionalen Server aufgeführt, aus denen Sie wählen können:

   * **[!UICONTROL APAC]**
   * **[!UICONTROL China]**
   * **[!UICONTROL Tokio]**
   * **[!UICONTROL UK/EU]**
   * **[!UICONTROL US-Ostküste]**
   * **[!UICONTROL US-Westküste]**

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

Im Schritt [Zielgruppen](../../ui/activate-segment-streaming-destinations.md#scheduling) müssen Sie Ihre Zielgruppen manuell ihrer entsprechenden ID oder ihrem Anzeigenamen in der Zielplattform zuordnen.

Für die Zuordnung von Zielgruppen empfiehlt Adobe zur Vereinfachung die Verwendung des Experience Platform-Zielgruppennamen oder einer kürzeren Form des Namens. Die Zielgruppen-ID oder der Name in Ihrem Ziel muss jedoch nicht mit der ID in Ihrem Experience Platform-Konto übereinstimmen. Jeder Wert, den Sie in das Zuordnungsfeld einfügen, wird vom Ziel übernommen.

### Obligatorische Zuordnungen {#mandatory-mappings}

Alle im Abschnitt [Unterstützte Identitäten](#supported-identities) beschriebenen Zielidentitäten sind obligatorisch und müssen während des Zielgruppenaktivierungsprozesses zugeordnet werden. Dazu gehören:

* **GAID** (Google Advertising ID)
* **IDFA** (Apple ID für Advertiser)
* **ECID** (Experience Cloud ID)
* **The Trade Desk ID**

Wenn nicht alle erforderlichen Identitäten zugeordnet werden, kann die Zielgruppe nicht erfolgreich für [!DNL The Trade Desk] aktiviert werden. Jede Identität erfüllt einen bestimmten Zweck in der Integration, und alle sind erforderlich, damit das Ziel ordnungsgemäß funktioniert.

![Screenshot mit den obligatorischen Zuordnungen](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

## Exportierte Daten {#exported-data}

Um sich zu vergewissern, dass die Daten erfolgreich in das [!DNL The Trade Desk]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL The Trade Desk]-Konto. Wenn die Aktivierung erfolgreich war, werden in Ihrem Konto Zielgruppen ausgefüllt.
