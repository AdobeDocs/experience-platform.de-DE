---
title: TikTok-Verbindung
description: Erstellen Sie benutzerdefinierte Zielgruppen in TikTok mit Ihren Daten für das Targeting mit Ihren Werbekampagnen. Diese Zielgruppen können von Personen sein, die Ihre Website besucht oder mit Ihrem Inhalt interagiert haben. Durch die Echtzeit-Integration von Adobe mit TikTok Ads Manager können Sie die gewünschte Zielgruppe schnell und sicher von Adobe Experience Platform an TikTok übertragen.
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 39%

---

# TikTok-Verbindung

## Übersicht {#overview}

Erstellen Sie benutzerdefinierte Zielgruppen in TikTok mit Ihren Daten für das Targeting mit Ihren Werbekampagnen. Diese Zielgruppen können von Personen sein, die Ihre Website besucht oder mit Ihrem Inhalt interagiert haben. Durch die Echtzeit-Integration von Adobe mit TikTok Ads Manager können Sie die gewünschte Zielgruppe schnell und sicher von Adobe Experience Platform an TikTok übertragen. Weitere Informationen finden Sie im geschäftlichen Hilfezentrum von TikTok ](https://ads.tiktok.com/help/article/audiences).[

>[!IMPORTANT]
>
>Diese Ziel-Connector- und Dokumentationsseite werden vom TikTok-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## Anwendungsfälle {#use-cases}

Hier finden Sie ein Anwendungsbeispiel für Adobe Experience Platform-Kunden, das Ihnen hilft, besser zu verstehen, wie und wann Sie das TikTok-Ziel verwenden sollten.

### Anwendungsfall {#use-case-1}

Eine Marke für Sportbekleidung möchte bestehende Kunden über ihre Social-Media-Konten erreichen. Die Bekleidungsmarke kann E-Mail-Adressen aus ihrem eigenen CRM-System in Adobe Experience Platform erfassen, Zielgruppen aus ihren eigenen Offline-Daten erstellen und diese Zielgruppen an TikTok senden, um Anzeigen in den Social-Media-Feeds ihrer Kunden anzuzeigen.

## Voraussetzungen {#prerequisites}

Sie benötigen [!DNL Admin] oder [!DNL Operator] Zugriff auf das TikTok Ads Manager-Konto, an das Sie Zielgruppen senden möchten. Weitere Anweisungen finden Sie im [TikTok Help Center](https://ads.tiktok.com/help/article/add-users-tiktok-business-center).

Bevor Sie Daten an Ihr TikTok Ads Manager-Konto senden, müssen Sie Adobe Experience Platform die Berechtigung erteilen, für `Audience Management` auf Ihr Anzeigenkonto zuzugreifen. Diese Berechtigung kann erteilt werden, indem [Ihre Anzeigen-Manager-ID](#authenticate) in der Experience Platform-Benutzeroberfläche eingeben und die Berechtigung erteilt wird, nachdem sie an Ihr TikTok Ads Manager-Konto weitergeleitet wurde.

## Unterstützte Identitäten {#supported-identities}

TikTok unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| Telefonnummer | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | Sowohl einfache als auch SHA256-Hash-Telefonnummern werden von Adobe Experience Platform unterstützt und müssen im E.164-Format vorliegen. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| E-Mail | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder andere), die im TikTok-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, werden Sie weitergeleitet, um sich bei Ihrem [!DNL TikTok Ads Manager] -Konto anzumelden und Adobe zu autorisieren, Zielgruppen in Ihrem Namen zu verwalten.

![TikTok-Berechtigungsauswahl](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "Bild der TikTok-Benutzeroberfläche für die Auswahl von Berechtigungen")

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Details zur Zielverbindung](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Bild der Platform-Benutzeroberfläche, in dem Details zur Zielverbindung angezeigt werden, die ausgefüllt werden sollen")

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL TikTok Ads Manager ID]**: Ihre [!DNL TikTok Ads Manager ID]. Sie finden dies in Ihrem [!DNL TikTok Ads manager] -Konto.

![TikTok Ads Manager-ID](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "Bild der TikTok Ads Manager-Benutzeroberfläche, das zeigt, wie die TikTok Ads Manager-ID abgerufen wird")

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Identitäten {#map}

Im Folgenden finden Sie ein Beispiel für die korrekte Identitätszuordnung beim Exportieren von Zielgruppen in TikTok Ads Manager.

Quellfelder auswählen:

* Wählen Sie eine Kennung (z. B. ` Email_LC_SHA256`) als Quellidentität aus, die ein Profil in Adobe Experience Platform eindeutig identifiziert und [!DNL TikTok Ads Manager].

Zielgruppenfelder auswählen:

* Wählen Sie den E-Mail-Namespace als Zielidentität aus.

![Identitätszuordnung](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Bild der Platform-Benutzeroberfläche, Zuordnung der Identitäten")

## Exportierte Daten {#exported-data}

Überprüfen Sie Ihr [!DNL TikTok Ads Manager]-Konto (unter **Assets > Zielgruppen**), um zu überprüfen, ob Ihre Experience Platform-Zielgruppe erfolgreich exportiert wurde. Die Audience wird als Audience-Typ ausgefüllt: `Partner Audience`.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Informationen finden Sie auf der Seite [TikTok Help Center page](https://ads.tiktok.com/help/article/audiences) .
