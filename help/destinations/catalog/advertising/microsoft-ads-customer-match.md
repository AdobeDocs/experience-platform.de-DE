---
keywords: Werbung; Microsoft Ads; Kundenabstimmung;
title: Microsoft Ads Customer Match-Verbindung
description: Verwenden Sie das Ziel Microsoft Ads-Kundenabgleich , um Kundinnen und Kunden nach E-Mail-Adresse abzugleichen und erneut mit ihnen über das Microsoft Advertising-Netzwerk zu interagieren, einschließlich Such- und Zielgruppenanzeigen.
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 6f246d87f44cd1fa9b22e40e9ee7b5d8250452e7
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 18%

---

# [!DNL Microsoft Ads Customer Match]-Verbindung {#microsoft-ads-customer-match-destination}

>[!AVAILABILITY]
>
>Dieser Ziel-Connector ist derzeit eingeschränkt verfügbar. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff zu erhalten.</br>

## Überblick {#overview}

Verwenden Sie das [!DNL Microsoft Ads Customer Match] Ziel, um Kundinnen und Kunden nach E-Mail-Adresse abzugleichen und mit ihnen über die gesamte [!DNL Microsoft Advertising Network] hinweg erneut zu interagieren, einschließlich Such- und Zielgruppenanzeigen. Verknüpfen Sie Ihr [!DNL Microsoft Advertising]-Konto mit Real-Time CDP, um die Erstellung und Verwaltung von Kundenauswahllisten direkt aus Experience Platform zu automatisieren.

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Microsoft Ads Customer Match]-Ziel verwenden, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit dieser Funktion bewältigen können.

### Anwendungsfall #1

Eine E-Commerce-Marke möchte Bestandskunden über [!DNL Microsoft Search] und [!DNL Microsoft Audience Network] ansprechen, um Angebote basierend auf ihren früheren Käufen und dem Navigationsverlauf zu personalisieren. Die Marke kann E-Mail-Adressen aus ihrem eigenen CRM in Experience Platform aufnehmen, Zielgruppen aus ihren eigenen Offline-Daten erstellen und diese Zielgruppen an [!DNL Microsoft Ads Customer Match] senden, die über Such- und Zielgruppenanzeigen hinweg verwendet werden können, und so ihre Werbeausgaben optimieren.

### Anwendungsfall #2

Ein Technologieunternehmen hat ein neues Produkt auf den Markt gebracht. Um dieses neue Produkt zu bewerben, möchten sie das Bewusstsein der Kunden schärfen, die zuvor verwandte Produkte gekauft haben. Sie laden E-Mail-Adressen aus ihrer CRM-Datenbank in Experience Platform hoch, wobei die E-Mail-Adressen als Kennungen verwendet werden. Zielgruppen werden basierend auf Kunden erstellt, denen zugehörige Produkte gehören. Diese Zielgruppen werden an [!DNL Microsoft Ads Customer Match] gesendet, damit das Unternehmen aktuelle Kunden und ähnliche Kunden in der gesamten [!DNL Microsoft Advertising Network] ansprechen kann.

## Unterstützte Identitäten {#supported-identities}

[!DNL Microsoft Ads Customer Match] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| `email` | Nur-Text-E-Mail-Adressen | Die [!DNL Microsoft Ads Customer Match]-Verbindung unterstützt nur E-Mail-Adressen im Klartext. Experience Platform hasht E-Mail-Adressen beim Export automatisch, um die Anforderungen von Microsoft zu erfüllen. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Alle anderen Ursprünge der Zielgruppe | Ja | Diese Kategorie enthält alle Ursprünge der Zielgruppe außerhalb der Zielgruppen, die durch die [!DNL Segmentation Service] generiert wurden. Lesen Sie mehr über [verschiedene Ursprünge von Audiences](/help/segmentation/ui/audience-portal.md#customize). Einige Beispiele: <ul><li> benutzerdefinierte Upload-Zielgruppen [importiert](../../../segmentation/ui/audience-portal.md#import-audience) aus CSV-Dateien in Experience Platform,</li><li> Lookalike-Zielgruppen, </li><li> Federated Audiences, </li><li> Zielgruppen, die in anderen Experience Platform-Apps wie Adobe Journey Optimizer generiert wurden, </li><li> und mehr. </li></ul> |

{style="table-layout:auto"}

Unterstützte Zielgruppen nach Zielgruppen-Datentyp:

| Datentyp der Zielgruppe | Unterstützt | Beschreibung | Anwendungsfälle |
|--------------------|-----------|-------------|-----------|
| [Personen-Zielgruppen](/help/segmentation/types/people-audiences.md) | Ja | Basierend auf Kundenprofilen können Sie bestimmte Personengruppen für Marketing-Kampagnen ansprechen. | Häufige Käufer, Warenkorbabbrüche |
| [Konto-Zielgruppen](/help/segmentation/types/account-audiences.md) | Nein | Targeting von Personen in bestimmten Organisationen für Account-basierte Marketing-Strategien. | B2B-Marketing |
| [Interessenten-Zielgruppen](/help/segmentation/types/prospect-audiences.md) | Nein | Targeting von Personen, die noch keine Kunden sind, aber Merkmale mit Ihrer Zielgruppe teilen. | Akquise mit Drittanbieterdaten |
| [Datensatzexporte](/help/catalog/datasets/overview.md) | Nein | Im Data Lake von Adobe Experience Platform gespeicherte Sammlungen strukturierter Daten. | Reporting, Datenwissenschaft-Workflows |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Sie exportieren alle Mitglieder einer Audience mit den IDs (E-Mail-Adressen), die im [!DNL Microsoft Ads Customer Match]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

Um Zielgruppendaten an [!DNL Microsoft Ads] zu senden, benötigen Sie ein aktives [!DNL Microsoft Advertising]. Weitere Informationen zum Erstellen eines Kontos finden Sie in der [Dokumentation zu Microsoft Advertising](https://help.ads.microsoft.com/#apex/ads/en/53090/0).

### Accept Customer Match Terms and Conditions {#accept-customer-match-terms}

Bevor Sie Zielgruppen über dieses Ziel aktivieren, müssen Sie zunächst manuell eine Kundenabgleichsliste in Ihrem [!DNL Microsoft Advertising]-Konto erstellen. Diese anfängliche manuelle Erstellung ist erforderlich, um die Geschäftsbedingungen für die Kundenübereinstimmung zu akzeptieren, sodass von Experience Platform gesendete Zielgruppen automatisch erstellt werden können. Wenn dieser Schritt nicht abgeschlossen wird, kann dies zu Fehlern bei der Aktivierung von Zielgruppen führen.

### Kontokonfiguration {#account-configuration}

Beim Konfigurieren des -Ziels müssen Sie die folgenden Informationen angeben:

* [!UICONTROL Customer ID]: Ihre [!DNL Microsoft Ads] Kunden-ID (CID) im ganzzahligen Format. Anweisungen zum Ermitteln Ihrer Kunden-ID finden Sie [&#x200B; der Dokumentation zu Microsoft Advertising &#x200B;](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids).
* [!UICONTROL Customer Account ID]: Ihre [!DNL Microsoft Ads] Kundenkonto-ID. Anweisungen zum Ermitteln Ihrer Kundenkonto-ID [&#x200B; Sie in der Dokumentation zu Microsoft Advertising &#x200B;](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids).

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. &#x200B;](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Ausfüllen der Zieldetails {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_customer_id"
>title="Kunden-ID"
>abstract="Ihre Microsoft Advertising-Kunden-ID, auch als Manager-Konto-ID bezeichnet. Dies ist die Kennung auf oberster Ebene in Microsoft Advertising, die mehrere Advertiser-Konten (Kundenkonto-IDs) enthalten kann."
>additional-url="https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids" text="Ermitteln der Kunden-ID"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_customer_account_id"
>title="Kundenkonto-ID"
>abstract="Ihre Microsoft Advertising-Kundenkonto-ID, auch als Advertiser-Konto-ID bezeichnet. Dadurch wird ein bestimmtes Advertiser-Konto unter Ihrer Kunden-ID identifiziert."
>additional-url="https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids" text="Ermitteln der Kundenkonto-ID"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_membership_duration"
>title="Dauer der Mitgliedschaft"
>abstract="Die Anzahl der Tage, die eine Benutzerin oder ein Benutzer in der Kundenabgleichliste verbleibt. Akzeptierte Werte liegen zwischen 1 und 390 Tagen."

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_list_availability"
>title="Verfügbarkeit der Kundenauswahlliste"
>abstract="Wählen Sie aus, ob die Kundenabgleichliste für ein einzelnes Advertiser-Konto oder für alle Konten unter dem Manager-Konto verfügbar ist. Wählen Sie Kunden-ID aus, um die Liste für alle Advertiser-Konten unter Ihrer Kunden-ID verfügbar zu machen. Wählen Sie Kundenkonto-ID aus, um die Liste auf die bestimmte Kundenkonto-ID zu beschränken."
>additional-url="https://help.ads.microsoft.com/apex/index/3/en/56727" text="Weitere Informationen zur Freigabe von Audiences-Listen in Microsoft Advertising"

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Customer ID]**: Ihre [!DNL Microsoft Ads] Kunden-ID (CID). Anweisungen zum Ermitteln Ihrer Kunden-ID finden Sie [&#x200B; der Dokumentation zu Microsoft Advertising &#x200B;](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids).
* **[!UICONTROL Customer Account ID]**: Ihre [!DNL Microsoft Ads] Kundenkonto-ID. Anweisungen zum Ermitteln Ihrer Kundenkonto-ID [&#x200B; Sie in der Dokumentation zu Microsoft Advertising &#x200B;](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids).
* **[!UICONTROL Membership Duration]**: Die Anzahl der Tage, die eine Benutzerin oder ein Benutzer in der Kundenabgleichliste verbleibt. Akzeptierte Werte liegen zwischen 1 und 390 Tagen.
* **[!UICONTROL Customer Match List Availability]**: Wählen Sie die Verfügbarkeit der Kundenabgleichliste aus. [!DNL Microsoft Advertising] kann eine Kunden-ID mehrere Kundenkonto-IDs (Advertiser-Konten) enthalten. Wählen Sie **[!UICONTROL Customer ID (all advertising accounts)]** aus, um die Liste für alle Advertiser-Konten unter Ihrer Kunden-ID verfügbar zu machen, oder **[!UICONTROL Customer Account ID (single advertising account)]** Sie die Liste auf die spezifische Kundenkonto-ID beschränken, die Sie oben angegeben haben. Weitere Informationen finden Sie in der Dokumentation [&#x200B; Microsoft Advertising .](https://help.ads.microsoft.com/apex/index/3/en/56727)

![Platform-UI-Bild, das die Zieldetailfelder für das Microsoft Ads-Ziel „Customer Match“ anzeigt.](../../assets/catalog/advertising/microsoft-ads-customer-match/destination-details.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *Identitäten* an Ziele zu exportieren, benötigen Sie die **[!UICONTROL View Identity Graph]**&#x200B;[&#x200B; Zugriffssteuerungsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

### Zuordnung {#mapping}

Im **[!UICONTROL Mapping]** Schritt müssen Sie die E-Mail-Identität aus Ihren Quellprofilen der Zielidentität in [!DNL Microsoft Ads Customer Match] zuordnen.

* **Source-Feld**: Wählen Sie `IdentityMap: Email` als Quellfeld aus, um E-Mail-Identitäten aus Ihren Profilen zuzuordnen. Alternativ können Sie ein XDM-Attribut wie `personalEmail.address` als Quellfeld auswählen.
* **Zielfeld**: Wählen Sie `Identity: email` als Zielfeld aus.

>[!IMPORTANT]
>
>Sie müssen ungehashte (Nur-Text-)Quellfelder verwenden. Verwenden Sie keine vorab gehashten Quellidentitäten wie `Emails (SHA256, lowercased)`. Experience Platform hasht die E-Mail-Adressen beim Export automatisch, um die Anforderungen von Microsoft zu erfüllen.

![UI-Bild, das den Zuordnungsschritt mit der IdentityMap-E-Mail zeigt, die der Identity-E-Mail zugeordnet ist.](../../assets/catalog/advertising/microsoft-ads-customer-match/mapping.png)

## Exportierte Daten {#exported-data}

Um sich zu vergewissern, dass die Daten erfolgreich in das [!DNL Microsoft Ads Customer Match]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Microsoft Advertising]-Konto. Wenn die Aktivierung erfolgreich war, werden Zielgruppen in Ihrem Konto als Kundenabgleichlisten ausgefüllt.

## Weitere Ressourcen {#additional-resources}

Weitere Informationen finden Sie im [Microsoft Advertising](https://help.ads.microsoft.com/)Hilfezentrum.
