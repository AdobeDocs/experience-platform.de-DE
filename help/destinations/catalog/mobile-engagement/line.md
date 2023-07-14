---
keywords: Mobile; Ziele für mobile Interaktion; LINE; LINE für mobile Interaktionen
title: LINE-Verbindung
description: Mit dem LINE-Ziel können Sie Profile zu Ihrer Platform-Audience hinzufügen und personalisierte Erlebnisse für verbundene Benutzer bereitstellen.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 41%

---

# [!DNL LINE]-Verbindung

## Übersicht {#overview}

[[!DNL LINE]](https://line.me/en/) ist eine beliebte Kommunikationsplattform, die Menschen, Dienstleistungen und Informationen verbindet und sich von einer Chat-App zu einem Zentrum für Unterhaltung, soziale Aktivitäten und tägliche Aktivitäten entwickelt hat.

Diese [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt die [[!DNL LINE] Messaging-API](https://developers.line.biz/en/reference/messaging-api/). Sie können Profile aus Ihren Experience Platform-Zielgruppen als Verbindungen in [!DNL LINE] für Ihre Geschäftsanforderungen.

[!DNL LINE] verwendet Trägertoken als Authentifizierungsmechanismus für die Kommunikation mit dem [!DNL LINE] Messaging-API. Anweisungen zur Authentifizierung bei Ihrem [!DNL LINE] -Instanz befindet sich weiter unten in [An Ziel authentifizieren](#authenticate) Abschnitt.

## Anwendungsfälle {#use-cases}

Marketingexperten können Benutzer in einem mobilen Interaktionsziel mit integrierten Zielgruppen ansprechen [!DNL Adobe Experience Platform]. Darüber hinaus können Sie ihnen personalisierte Erlebnisse bereitstellen, die auf Attributen ihrer [!DNL Adobe Experience Platform] Profile, sobald Audiences und Profile in [!DNL Adobe Experience Platform].

## Voraussetzungen {#prerequisites}

### Voraussetzungen für [!DNL LINE] {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen in [!DNL LINE], um Daten von Platform in Ihr [!DNL LINE]-Konto zu exportieren:

#### Sie benötigen ein [!DNL LINE]-Konto {#prerequisites-account}

Sie müssen sich registrieren und eine [!DNL LINE] , wenn Sie noch keinen haben. So erstellen Sie ein Konto:

1. Navigieren Sie zum [!DNL LINE] [Kontoanmeldung](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) page
2. Auswählen **[!UICONTROL Konto erstellen]**.

#### Sammeln Sie die [!DNL LINE channel access token (long-lived)] von [!DNL LINE] Entwicklerkonsole {#gather-credentials}

So lassen Sie Platform den Zugriff zu [!DNL LINE] -Ressourcen, benötigen Sie die *[!DNL Channel access token (long-lived)]* aus dem gewünschten [!DNL LINE] *Messaging-API* -Kanal.

1. Melden Sie sich bei [!DNL LINE] dem [[!DNL LINE] Entwicklerkonsole](https://developers.line.biz/console).
1. Rufen Sie als Nächstes die *[!DNL Providers]* Liste und wählen Sie dann die *[!DNL Provider]* und wählen Sie schließlich die *Messaging-API* -Kanal, um auf seine Einstellungen zuzugreifen. Wenn Sie zum ersten Mal auf die Entwicklerkonsole zugreifen, folgen Sie dem [[!DNL LINE] Dokumentation](https://developers.line.biz/en/docs/messaging-api/getting-started/) , um die zum Erstellen eines Providers erforderlichen Schritte auszuführen.
1. Navigieren Sie schließlich zum ***[!DNL Channel access token]*** und kopieren Sie die ***[!DNL Channel access token (long-lived)]*** -Wert erforderlich in [An Ziel authentifizieren](#authenticate) Schritt.

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | Ihre [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

Siehe Abschnitt [[!DNL LINE] Dokumentation](https://developers.line.biz/en/docs/messaging-api/getting-started/) für Anleitungen zum Erstellen eines Kanals oder Hinzufügen eines Kanals zu einer vorhandenen [!DNL LINE] über das [!DNL LINE] Entwicklerkonsole.

## Unterstützte Identitäten {#supported-identities}

[!DNL LINE] unterstützt die Aktualisierung und den Export von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/namespaces.md).

| Ziel-Identität | Beschreibung |
|---|---|
| ID für Advertiser (IFAs) | Wählen Sie die Zielidentität der ID für Advertisers (IFAs) aus, wenn die Quellidentitäten IFA sind. *(Apple ID für Advertiser)* oder GAID * (Google Advertising ID)-Namespaces. |
| LINE-Benutzer-IDs | Wählen Sie die UserID-Zielidentität aus, wenn die Quellidentitäten LINE-Benutzer-IDs sind. |

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder andere), die im [!DNL LINE] Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform basierend auf der Zielgruppenbewertung aktualisiert wird, sendet der Connector das Update an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** nach [!DNL LINE]. Alternativ können Sie sie unter der **[!UICONTROL Interaktion mit Mobilgeräten]** Kategorie.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Mit Ziel verbinden]**.
![Screenshot der Platform-Benutzeroberfläche, auf dem die Authentifizierung gezeigt wird.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

Füllen Sie die erforderlichen Felder aus.
* **[!UICONTROL Trägertoken]**: Ihre [!DNL LINE Channel access token (long-lived)] von [!DNL LINE] Entwicklerkonsole. Siehe Abschnitt [Anmeldedaten erfassen](#gather-credentials) Abschnitt.

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche den Status **[!UICONTROL Verbunden]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
![Screenshot der Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Zielgruppentyp]**: Auswählen **[!UICONTROL ID für Advertiser (IFAs)]** , wenn die Identitäten, die Sie exportieren möchten, vom Typ *ID für Advertiser (IFAs)*. Auswählen **[!UICONTROL LINE-Benutzer-IDs]** , wenn die Identitäten, die Sie exportieren möchten, vom Typ *LINE-Benutzer-IDs*. Siehe Abschnitt [Unterstützte Identitäten](#supported-identities) für weitere Informationen zu den Identitätstypen.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
>
>Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppenexport-Ziele](/help/destinations/ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel.

### Zuordnen von Attributen und Identitäten {#map}

Um Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an das [!DNL LINE]-Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodells (XDM) in Ihrem Platform-Konto und den jeweiligen Entsprechungen vom Ziel zu erstellen. Um Ihre XDM-Felder den [!DNL LINE]-Zielfeldern korrekt zuzuordnen, führen Sie die folgenden Schritte aus:

Abhängig von Ihrer Quellidentität müssen die folgenden Zielidentitäts-Namespaces zugeordnet werden: | Target Identity | Quellfeld | Zielfeld | | — | — | — | | ID für Advertiser(IFAs) | `IDFA` oder `GAID` | `LineId` | | LINE-Benutzer-IDs | `UserID` | `LineId` |

Wenn Ihre Zielidentitäten *LINE-Benutzer-IDs* benötigen Sie Folgendes:
![Screenshot-Beispiel der Platform-Benutzeroberfläche, das die Zielgruppen-Zuordnung bei der Verwendung von LINE-Benutzer-IDs für Zielidentitäten zeigt.](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

Wenn Ihre Zielidentität *ID für Advertiser (IFAs)* benötigen Sie Folgendes:
![Screenshot-Beispiel der Platform-Benutzeroberfläche, das die Target-Zuordnung bei Verwendung der ID für Advertiser (IFAs) für Zielidentitäten zeigt.](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## Überprüfen des Datenexports {#exported-data}

Nach erfolgreichem Datenexport aus Experience Platform wird die [!DNL LINE] Das Ziel erstellt eine neue Zielgruppe in [!DNL LINE] unter Verwendung des ausgewählten Zielgruppennamen.

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. In [!DNL LINE], melden Sie sich bei der [Manager Console](https://manager.line.biz/).

1. Navigieren Sie als Nächstes zu **[!UICONTROL Datenkontrollen]** > **[!UICONTROL Zielgruppen]** und überprüfen Sie den Namen der ausgewählten Zielgruppe im **[!UICONTROL Zielgruppenname]** Spalte.

1. Das aktualisierte Volumen würde mit der Anzahl im Segment übereinstimmen.

1. Die *Typ* -Spalte **[!UICONTROL UserID]** , wenn die von Ihnen exportierten Identitäten vom Typ *UserID*. Auf ähnliche Weise wird die *Typ* -Spalte **[!UICONTROL Mobile Anzeigen-ID]** , wenn die von Ihnen exportierten Identitäten vom Typ *IDFA*.

Beispiel-Setup in [!DNL LINE] ist unten dargestellt:
![Screenshot der LINE-Benutzeroberfläche mit dem Volumen der Audience.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).
