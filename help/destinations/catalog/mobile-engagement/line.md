---
keywords: Mobile; Ziele für mobile Interaktion; LINE; LINE für mobile Interaktionen
title: LINE-Verbindung
description: Mit dem LINE-Ziel können Sie Profile zu Ihrer Platform-Audience hinzufügen und personalisierte Erlebnisse für verbundene Benutzer bereitstellen.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 42%

---

# [!DNL LINE]-Verbindung

## Übersicht {#overview}

[[!DNL LINE]](https://line.me/en/) ist eine beliebte Kommunikationsplattform, die Menschen, Dienste und Informationen verbindet und sich von einer Chat-App zu einem Zentrum für Unterhaltung, soziale und tägliche Aktivitäten entwickelt hat.

Dieses [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt die [[!DNL LINE] Messaging-API](https://developers.line.biz/en/reference/messaging-api/). Sie können Profile aus Ihren Experience Platform-Audiences als Verbindungen innerhalb von [!DNL LINE] für Ihre geschäftlichen Anforderungen aktivieren.

[!DNL LINE] verwendet Trägertoken als Authentifizierungsmechanismus für die Kommunikation mit der [!DNL LINE] Messaging-API. Anweisungen zum Authentifizieren bei Ihrer [!DNL LINE]-Instanz finden Sie weiter unten im Abschnitt [Für Ziel authentifizieren](#authenticate) .

## Anwendungsfälle {#use-cases}

Marketingexperten können Benutzer in einem mobilen Interaktionsziel mit in [!DNL Adobe Experience Platform] integrierten Zielgruppen ansprechen. Darüber hinaus können Sie ihnen personalisierte Erlebnisse basierend auf Attributen aus ihren [!DNL Adobe Experience Platform] Profilen bereitstellen, sobald Audiences und Profile in [!DNL Adobe Experience Platform] aktualisiert werden.

## Voraussetzungen {#prerequisites}

### Voraussetzungen für [!DNL LINE] {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen in [!DNL LINE], um Daten von Platform in Ihr [!DNL LINE]-Konto zu exportieren:

#### Sie benötigen ein [!DNL LINE]-Konto {#prerequisites-account}

Sie müssen sich registrieren und ein [!DNL LINE] -Konto erstellen, falls noch keines vorhanden ist. So erstellen Sie ein Konto:

1. Navigieren Sie zur Seite [!DNL LINE] [Kontoanmeldung](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) .
2. Wählen Sie **[!UICONTROL Konto erstellen]** aus.

#### Erfassen Sie die [!DNL LINE channel access token (long-lived)] aus der [!DNL LINE]-Entwicklerkonsole. {#gather-credentials}

Damit Platform auf [!DNL LINE] -Ressourcen zugreifen kann, benötigen Sie den *[!DNL Channel access token (long-lived)]* aus dem gewünschten Kanal [!DNL LINE] *Messaging API* .

1. Melden Sie sich mit Ihrem [!DNL LINE] -Konto bei der [[!DNL LINE] Entwicklerkonsole](https://developers.line.biz/console) an.
1. Rufen Sie als Nächstes die Liste *[!DNL Providers]* auf, wählen Sie dann den Kanal *[!DNL Provider]* von Interesse aus und wählen Sie schließlich den Kanal *Messaging API* aus, um auf seine Einstellungen zuzugreifen. Wenn Sie zum ersten Mal auf die Entwicklerkonsole zugreifen, führen Sie die zum Erstellen eines Providers erforderlichen Schritte in der [[!DNL LINE] Dokumentation](https://developers.line.biz/en/docs/messaging-api/getting-started/) aus.
1. Navigieren Sie schließlich zum Abschnitt ***[!DNL Channel access token]*** und kopieren Sie den im Schritt [Authentifizierung an Ziel](#authenticate) erforderlichen Wert für ***[!DNL Channel access token (long-lived)]***.

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | Ihr [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

Eine Anleitung zum Erstellen eines Kanals oder zum Hinzufügen eines Kanals zu Ihrem vorhandenen [!DNL LINE]-Konto über die Entwicklerkonsole [!DNL LINE] finden Sie in der [[!DNL LINE] Dokumentation](https://developers.line.biz/en/docs/messaging-api/getting-started/) .

## Unterstützte Identitäten {#supported-identities}

[!DNL LINE] unterstützt die Aktualisierung und den Export von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung |
|---|---|
| ID für Advertiser (IFAs) | Wählen Sie die ID für die Zielidentität der Advertiser (IFAs) aus, wenn die Quellidentitäten IFA *(Apple ID for Advertisers)* oder GAID *(Google Advertising ID)-Namespaces sind. |
| LINE-Benutzer-IDs | Wählen Sie die UserID-Zielidentität aus, wenn die Quellidentitäten LINE-Benutzer-IDs sind. |

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder sonstiges), die im [!DNL LINE]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** nach [!DNL LINE]. Alternativ können Sie sie unter der Kategorie **[!UICONTROL Mobile Interaktion]** finden.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Mit Ziel verbinden]**.
![Screenshot der Platform-Benutzeroberfläche, auf dem die Authentifizierung gezeigt wird.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

Füllen Sie unten die erforderlichen Felder aus.
* **[!UICONTROL Trägertoken]**: Ihr [!DNL LINE Channel access token (long-lived)] in der [!DNL LINE] -Entwicklerkonsole. Siehe Abschnitt [Anmeldedaten sammeln](#gather-credentials) .

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche den Status **[!UICONTROL Verbunden]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
![Screenshot der Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Zielgruppentyp]**: Wählen Sie **[!UICONTROL ID für Advertiser(IFAs)]** aus, wenn die Identitäten, die Sie exportieren möchten, vom Typ *ID für Advertiser(IFAs)* sind. Wählen Sie **[!UICONTROL LINE-Benutzer-IDs]** aus, wenn die Identitäten, die Sie exportieren möchten, vom Typ *LINE-Benutzer-IDs* sind. Weitere Informationen zu den Identitätstypen finden Sie im Abschnitt [Unterstützte Identitäten](#supported-identities) .

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Um Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an das [!DNL LINE]-Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodells (XDM) in Ihrem Platform-Konto und den jeweiligen Entsprechungen vom Ziel zu erstellen. Um Ihre XDM-Felder den [!DNL LINE]-Zielfeldern korrekt zuzuordnen, führen Sie die folgenden Schritte aus:

Abhängig von Ihrer Quellidentität müssen die folgenden Zielidentitäts-Namespaces zugeordnet werden:

| Ziel-Identität | Quellfeld | Zielfeld |
| --- | --- | --- |
| ID für Advertiser (IFAs) | `IDFA` oder `GAID` | `LineId` |
| LINE-Benutzer-IDs | `UserID` | `LineId` |

Wenn Ihre Zielidentitäten *LINE-Benutzer-IDs* sind, benötigen Sie Folgendes:
![Screenshot der Platform-Benutzeroberfläche, das die Zielgruppen-Zuordnung bei der Verwendung von LINE-Benutzer-IDs für Zielidentitäten zeigt.](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

Wenn Ihre Zielidentität *ID für Advertiser(IFAs)* ist, benötigen Sie Folgendes:
![Screenshot der Platform-Benutzeroberfläche, das die Zielgruppen-Zuordnung zeigt, wenn die ID für Advertiser (IFAs) für Zielidentitäten verwendet wird.](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## Überprüfen des Datenexports {#exported-data}

Nach erfolgreichem Datenexport aus Experience Platform erstellt das Ziel [!DNL LINE] eine neue Zielgruppe in [!DNL LINE] unter Verwendung des ausgewählten Zielgruppennamen.

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Melden Sie sich in [!DNL LINE] bei der [Manager-Konsole](https://manager.line.biz/) an.

1. Navigieren Sie anschließend zu **[!UICONTROL Datensteuerung]** > **[!UICONTROL Zielgruppen]** und überprüfen Sie den Namen, der mit der ausgewählten Zielgruppe übereinstimmt, in der Spalte **[!UICONTROL Zielgruppenname]** .

1. Das aktualisierte Volumen würde mit der Anzahl im Segment übereinstimmen.

1. In der Spalte *Typ* wird **[!UICONTROL UserID]** aufgeführt, wenn die von Ihnen exportierten Identitäten vom Typ *UserID* sind. Gleichermaßen wird in der Spalte *Typ* der Wert **[!UICONTROL Mobile Anzeigen-ID]** angezeigt, wenn die von Ihnen exportierten Identitäten vom Typ *IDFA* sind.

Nachfolgend finden Sie ein Beispiel für die Einrichtung in [!DNL LINE]:
![Screenshot der LINE-Benutzeroberfläche mit dem Volumen der Audience.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).
