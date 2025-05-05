---
title: TikTok-Verbindung
description: Erstellen Sie auf TikTok benutzerdefinierte Zielgruppen mit Ihren Daten für das Targeting mit Ihren Werbekampagnen. Bei diesen Zielgruppen kann es sich um Personen handeln, die Ihre Website besucht oder mit Ihren Inhalten interagiert haben. Übertragen Sie die gewünschte Zielgruppe schnell und sicher von Adobe Experience Platform nach TikTok mithilfe der Echtzeit-Integration von Adobe mit TikTok Ads Manager.
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 38%

---

# TikTok-Verbindung

## Überblick {#overview}

Erstellen Sie auf TikTok benutzerdefinierte Zielgruppen mit Ihren Daten für das Targeting mit Ihren Werbekampagnen. Bei diesen Zielgruppen kann es sich um Personen handeln, die Ihre Website besucht oder mit Ihren Inhalten interagiert haben. Übertragen Sie die gewünschte Zielgruppe schnell und sicher von Adobe Experience Platform nach TikTok mithilfe der Echtzeit-Integration von Adobe mit TikTok Ads Manager. Besuchen Sie das Business Help Center von [TikTok](https://ads.tiktok.com/help/article/audiences) um weitere Informationen zu erhalten.

>[!IMPORTANT]
>
>Dieser Ziel-Connector und diese Dokumentationsseite werden vom TikTok-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## Anwendungsszenarien {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das TikTok-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel für Kundinnen und Kunden von Adobe Experience Platform.

### Anwendungsfall {#use-case-1}

Eine Sportbekleidungsmarke möchte Bestandskunden über ihre Social-Media-Konten erreichen. Die Bekleidungsmarke kann E-Mail-Adressen aus ihrem eigenen CRM in Adobe Experience Platform aufnehmen, Zielgruppen aus ihren eigenen Offline-Daten erstellen und diese Zielgruppen an TikTok senden, um Anzeigen in den Social-Media-Feeds ihrer Kunden anzuzeigen.

## Voraussetzungen {#prerequisites}

Sie benötigen [!DNL Admin] oder [!DNL Operator] Zugriff auf das TikTok Ads Manager-Konto, an das Sie Zielgruppen senden möchten. Weitere Informationen finden Sie im [TikTok-Hilfezentrum](https://ads.tiktok.com/help/article/add-users-tiktok-business-center).

Bevor Sie Daten an Ihr TikTok Ads Manager-Konto senden, müssen Sie Adobe Experience Platform die Berechtigung erteilen, für `Audience Management` auf Ihr Ad-Konto zuzugreifen. Diese Berechtigung kann erteilt werden, indem [Ihre Ads Manager-ID eingeben](#authenticate) in der Experience Platform-Benutzeroberfläche und die Berechtigung erteilt wird, nachdem sie zu Ihrem TikTok Ads Manager-Konto weitergeleitet wurde.

## Unterstützte Identitäten {#supported-identities}

TikTok unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple-ID für Werbetreibende | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| Telefonnummer | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | Sowohl Nur-Text- als auch SHA256-Hash-Telefonnummern werden von Adobe Experience Platform unterstützt und müssen im E.164-Format vorliegen. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Experience Platform] die Daten bei Aktivierung automatisch hasht. |
| E-Mail | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Experience Platform] die Daten bei Aktivierung automatisch hasht. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |
| [!DNL Federated Audience Composition] | ✓ | Zielgruppen, die über die [Federated Audience Composition“ in Experience Platform importiert ](https://experienceleague.adobe.com/de/docs/federated-audience-composition/using/start/audiences). |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder sonstiges), die im TikTok-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, werden Sie umgeleitet, um sich bei Ihrem [!DNL TikTok Ads Manager]-Konto anzumelden und Adobe zu autorisieren, Zielgruppen in Ihrem Namen zu verwalten.

![TikTok-Berechtigungsauswahl](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "Bild der TikTok-Benutzeroberfläche zum Auswählen von Berechtigungen")

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Details zur Zielverbindung](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Bild der Experience Platform-Benutzeroberfläche mit den einzufüllenden Details zur Zielverbindung")

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL TikTok Ads Manager-ID]**: Ihr [!DNL TikTok Ads Manager ID]. Diese finden Sie in Ihrem [!DNL TikTok Ads manager].

![TikTok Ads Manager-ID](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "Bild der TikTok Ads Manager-Benutzeroberfläche, das zeigt, wie die TikTok Ads Manager-ID abgerufen wird")

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Identitäten {#map}

Nachfolgend finden Sie ein Beispiel für die korrekte Identitätszuordnung beim Exportieren von Zielgruppen in TikTok Ads Manager.

Auswahl der Quellfelder:

* Wählen Sie eine Kennung (zum Beispiel: ` Email_LC_SHA256`) als Quellidentität aus, die ein Profil in Adobe Experience Platform und [!DNL TikTok Ads Manager] eindeutig identifiziert.

Auswählen der Zielfelder:

* Wählen Sie den E-Mail-Namespace als Zielidentität aus.

![Identitätszuordnung](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Bild der Experience Platform-Benutzeroberfläche, Zuordnung von Identitäten")

## Exportierte Daten {#exported-data}

Überprüfen Sie Ihr [!DNL TikTok Ads Manager] (unter **Assets > Zielgruppen**, um festzustellen, ob Ihre Experience Platform-Zielgruppe erfolgreich exportiert wurde. Die Zielgruppe wird als Zielgruppentyp ausgefüllt: `Partner Audience`.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Informationen finden Sie auf der Seite zum [TikTok](https://ads.tiktok.com/help/article/audiences)Hilfezentrum .
