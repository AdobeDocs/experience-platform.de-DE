---
title: Zielgruppenanalyse-Ziel
description: Sehen Sie sich Zielgruppen an, für die sich Kunden im Customer Journey Analytics qualifizieren.
badgeLimitedAvailability: label="Eingeschränkte Verfügbarkeit" type="Informative"
source-git-commit: 83b3d40e17f444555769020526bb723265a09eb9
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 37%

---

# Zielgruppenanalyse-Ziel

Die [!UICONTROL Zielgruppenanalyse] Mit dem Ziel können Sie Adobe Experience Platform-Zielgruppendaten in [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=de). Sie können auswählen, welche Zielgruppen in die resultierenden angereicherten Daten aufgenommen werden sollen. Zielgruppenqualifikationen sind dann als Dimensionen in [Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html) Berichterstellung.

>[!AVAILABILITY]
>
>Dieses Ziel befindet sich in einer begrenzten Testphase. Wenden Sie sich an Ihr Adobe-Account-Team, wenn Sie an diesem Ziel interessiert sind.

## Voraussetzungen

Vor Verwendung dieses Ziels ist Folgendes erforderlich:

* Sie müssen für die Verwendung des Zielgruppenanalyseziels bereitgestellt werden. Wenn Sie noch nicht für die Verwendung dieses Ziels freigeschaltet sind, wenden Sie sich an Ihr Adobe-Account-Team.
* Sie müssen für die Verwendung von Customer Journey Analytics freigeschaltet sein.
* Mindestens eine Zielgruppe muss in Adobe Experience Platform erstellt sein.

## Unterstützte Identitäten

Die Zielgruppenanalyse unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md). Experience Cloud ID (ECID) wird normalerweise verwendet.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | Google Advertising ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| ECID | Experience Cloud ID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Siehe folgendes Dokument unter [ECID](/help/identity-service/features/ecid.md) für weitere Informationen. |
| phone_sha256 | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | Es werden sowohl einfache als auch SHA256-Hash-Telefonnummern von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| extern_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen

Bei Verwendung dieses Ziels werden die folgenden Arten von Zielgruppen unterstützt:

| Audience Origin | Unterstützt | Beschreibung |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder andere), die im Ziel der Zielgruppenanalyse verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Wenn ein Profil auf der Grundlage einer Zielgruppenbewertung im Experience Platform aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Neues Ziel konfigurieren

>[!IMPORTANT]
> 
>Zum Erstellen eines Ziels benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md).

### Zieldetails

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Der Zielname.
* **[!UICONTROL Beschreibung]**: Die Zielbeschreibung.
* **[!UICONTROL Datenspeicher-ID]**: Die Datastream-ID, die Sie mit qualifizierten Zielgruppen anreichern möchten. Sie können diese ID im [Datenspeicher-Manager](/help/datastreams/overview.md).
* **[!UICONTROL Integrationsalias]**: Der Integrationsalias.

### Warnhinweise

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

* **[!UICONTROL Aktivierungsübersprungene Rate überschritten]**: Werden Sie benachrichtigt, wenn die Aktivierungsrate einen Schwellenwert überschreitet.

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

### Governance-Richtlinie und Durchsetzungsmaßnahmen

In diesem optionalen Abschnitt können Sie Ihre Data Governance-Richtlinien definieren und sicherstellen, dass die verwendeten Daten konform sind, wenn Zielgruppen gesendet und aktiv sind.

Wenn Sie mit der Auswahl der gewünschten Marketing-Aktionen für das Ziel fertig sind, wählen Sie **[!UICONTROL Erstellen]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Nachdem das Ziel erstellt wurde, können Sie die gewünschten Zielgruppen für das Ziel aktivieren.

1. Wenn Sie sich noch nicht im erstellten Ziel befinden, können Sie es erneut finden, indem Sie zu **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]**.
1. Auswählen **[!UICONTROL Aktivieren von Zielgruppen]**.
1. Wählen Sie die gewünschten Zielgruppen aus, für die Sie Qualifikationen analysieren möchten. Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.
1. Überprüfen Sie die Zielkonfiguration und die Zielgruppeneinstellungen und wählen Sie dann **[!UICONTROL Beenden]**.

Sie können weitere Zielgruppen hinzufügen, die in der Zukunft analysiert werden sollen, indem Sie zur **[!UICONTROL Aktivieren von Zielgruppen]** Seite. Zielgruppen können nicht entfernt werden, nachdem sie aktiviert wurden.
