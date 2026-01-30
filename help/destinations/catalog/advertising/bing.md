---
keywords: Werbung; Bing;
title: Microsoft Bing-Verbindung
description: Mit dem Microsoft Bing-Verbindungsziel können Sie Retargeting- und zielgruppenorientierte digitale Kampagnen für das gesamte Microsoft Advertising-Netzwerk ausführen, einschließlich Display-Werbung, Suche und nativer Kampagnen.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: ec31c1d967be4764b22f735429e2f9437f31ed20
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 30%

---

# [!DNL Microsoft Bing]-Verbindung {#bing-destination}

## Übersicht {#overview}

Verwenden Sie das [!DNL Microsoft Bing] Ziel, um Profildaten an die gesamte [!DNL Microsoft Advertising Network] zu senden, einschließlich [!DNL Display Advertising], [!DNL Search] und [!DNL Native].

Das [!DNL Microsoft Bing]-Ziel erstellt *[!DNL Custom Audiences]* in Microsoft. Diese sind sowohl in der [!DNL Microsoft Search Network] als auch in der [!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic]) verfügbar, wie in der [Dokumentation zu Microsoft Advertising &#x200B;](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500).

Um Profildaten an [!DNL Microsoft Bing] zu senden, müssen Sie zunächst eine Verbindung mit dem Ziel herstellen.

## Anwendungsfälle {#use-cases}

Als Marketing-Experte möchte ich in der Lage sein, Zielgruppen aus [!DNL Microsoft Advertising IDs] zu verwenden, um Benutzende per Display- oder Suchwerbung über [!DNL Microsoft Advertising] Kanäle hinweg anzusprechen.

## Unterstützte Identitäten {#supported-identities}

[!DNL Microsoft Bing] unterstützt die Aktivierung von Zielgruppen basierend auf den in der folgenden Tabelle aufgeführten Identitäten. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

Alle Identitäten in der folgenden Tabelle sind vorkonfiguriert und werden während der Aktivierung automatisch zugeordnet. Sie müssen diese Zuordnungen nicht manuell konfigurieren.

| Identität | Beschreibung | Zu beachten |
|---|---|---|
| MAID | MICROSOFT ADVERTISING ID | Wird aktiviert, wenn eine Microsoft Advertising ID im Profil vorhanden ist. |
| ECID | Experience Cloud ID | **Erforderlich.** Alle Profile müssen über eine ECID mit einer entsprechenden Microsoft Advertising-ID-Zuordnung verfügen, um exportiert werden zu können. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

**[!DNL Audience Export]** : Sie exportieren alle Mitglieder einer Zielgruppe an das [!DNL Microsoft Bing] Ziel.

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Sie exportieren alle Mitglieder einer Zielgruppe an das [!DNL Microsoft Bing] Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

Das [!DNL Microsoft Bing]-Ziel erfordert die folgende Einrichtung, um ordnungsgemäß zu funktionieren:

1. **ID-Synchronisierungsfunktion aktivieren**: Wenn Sie [!DNL Microsoft Bing] Aktivierung zum ersten Mal einrichten und die [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=de) im Experience Cloud ID-Service noch nicht aktiviert haben (mit Adobe Audience Manager oder anderen Anwendungen), wenden Sie sich an Adobe Consulting oder die Kundenunterstützung, um ID-Synchronisierungen zu aktivieren.
   * Wenn Sie zuvor [!DNL Microsoft Bing] Integrationen in Audience Manager eingerichtet haben, werden Ihre bestehenden ID-Synchronisierungen automatisch auf Experience Platform übertragen.

2. **ECID für Profile sicherstellen**: Für den erfolgreichen Export muss für alle Profile eine ECID vorhanden sein. ECID **für** Ziel (obligatorisch).

Beim Konfigurieren des -Ziels müssen Sie die folgenden Informationen angeben:

* [!UICONTROL Account ID]: Dies ist Ihr [!DNL Bing Ads CID] im Integer-Format.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. &#x200B;](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Ausfüllen der Zieldetails {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Account ID]**: Ihre [!DNL Bing Ads Customer ID] (CID). Ihre CID ist eine Ganzzahl, die in der URL enthalten ist, wenn Sie sich bei [!DNL Microsoft Advertising] anmelden.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="Zuordnungs-ID"
>abstract="Geben Sie die numerische Bing-Zielgruppen-ID ein, der Sie das ausgewählte Segment zuordnen möchten. Wenn die angegebene [!UICONTROL Mapping ID] keiner Zielgruppen-ID im Bing-Ziel entspricht, werden die erwarteten Zielgruppendaten in Ihrem Bing-Konto nicht angezeigt."

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_bing"
>title="Vorkonfigurierte Zuordnungssätze"
>abstract="Wir haben diese beiden Zuordnungssätze für Sie vorkonfiguriert. Wenn Sie Daten für Microsoft Bing aktivieren, müssen die für die aktivierten Zielgruppen qualifizierten Profile mindestens über eine ECID-Identität verfügen, die mit ihrem Profil verknüpft ist, damit sie erfolgreich in das Ziel exportiert werden können."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/advertising/bing#preconfigured-mappings" text="Weitere Informationen zu den vorkonfigurierten Zuordnungen"

>[!IMPORTANT]
> 
>Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

Im Schritt [Zielgruppen-Zeitplan](../../ui/activate-segment-streaming-destinations.md#scheduling) müssen Sie den Zielgruppennamen im Feld [!UICONTROL Mapping ID] manuell zuordnen. Dadurch wird sichergestellt, dass Zielgruppen-Metadaten korrekt an [!DNL Bing] weitergeleitet werden.

![UI-Bild, das den Bildschirm für den Zielgruppen-Zeitplan mit einem Beispiel für die Zuordnung des Zielgruppennamen zur Bing-Zuordnungs-ID zeigt.](../../assets/catalog/advertising/bing/mapping-id.png)

### Vorkonfigurierte Zuordnungen {#preconfigured-mappings}

Die folgenden Identitätszuordnungen sind **vorkonfiguriert und werden** Workflow für die Zielgruppenaktivierung automatisch ausgefüllt:

* **MAID** (Microsoft Advertising ID)
* **ECID** (Experience Cloud ID)

Diese Zuordnungen sind ausgegraut und schreibgeschützt. In diesem Schritt ist keine Konfiguration erforderlich. Wählen Sie **[!UICONTROL Next]** aus, um fortzufahren.

>[!IMPORTANT]
>
>**ECID ist erforderlich, damit der Export erfolgreich ist.** Profile ohne ECID oder ohne ID-Sync-Zuordnung zwischen ECID und Microsoft Advertising ID werden nicht exportiert.

### Beispiele für Aktivierungen

* **Profil mit ECID- und Microsoft Advertising-ID-Zuordnung:** Profil wurde erfolgreich exportiert und aktiviert
* **Nur Profil mit ECID (keine Microsoft Advertising ID-Zuordnung):** Profil wird **exportiert**. Die ID-Synchronisierungszuordnung zwischen ECID und MAID ist erforderlich.
* **Profil ohne ECID:** Profil wird **exportiert**. ECID ist für dieses Ziel obligatorisch.

## Exportierte Daten {#exported-data}

Um sich zu vergewissern, dass die Daten erfolgreich in das [!DNL Microsoft Bing]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Microsoft Bing Ads]-Konto. Wenn die Aktivierung erfolgreich war, werden in Ihrem Konto Zielgruppen ausgefüllt.
