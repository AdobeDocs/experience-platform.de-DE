---
title: Bombora-Verbindung
description: Aktivieren Sie Profile für Ihre Bombora-Kampagnen zum Zielgruppen-Targeting, zur Personalisierung und zur Unterdrückung, basierend auf den Konto-Zielgruppen.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P-Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: a2f8e399-e192-4104-876a-fe60f8403143
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 25%

---

# Bombora-Verbindung {#bombora}

>[!AVAILABILITY]
>
>Die Funktion zum Aktivieren von Account-Zielgruppen für das Bombora-Ziel ist für Unternehmen verfügbar, die die [Business-to](/help/rtcdp/overview.md#rtcdp-b2b)- und [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p)-Editionen von Real-Time Customer Data Platform erwerben.

Aktivieren Sie Profile für Ihre Bombora-Kampagnen zum Zielgruppen-Targeting, zur Personalisierung und zur Unterdrückung, basierend auf [Account-Zielgruppen](/help/segmentation/types/account-audiences.md).

## Anwendungsfälle {#use-case}

Damit Sie besser verstehen können, wie und wann Sie das Bombora-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel bewältigen können.

### DSP-Integration {#dsp-integration}

Als B2B-Marketing-Experte können Sie in Real-time CDP eine Account-Liste erstellen, um Unternehmen zu identifizieren, die eine hohe Absicht für Ihre Produkte haben, und dann dieses Ziel verwenden, um diese Liste in Bombora zu aktivieren.

Durch die Integration von Bombora mit DSPs können Sie zielgerichtete Anzeigenkampagnen mit Bombora-Daten durchführen. Dadurch wird sichergestellt, dass sich Ihre Werbeausgaben auf Unternehmen konzentrieren, die am ehesten konvertieren werden.

### Account-Based Marketing {#abm}

Als B2B-Marketing-Experte können Sie eine Account-Liste auf der Grundlage von CRM- und Marketing-Signalen erstellen. Dann können Sie dieses Ziel verwenden, um diese Liste in Bombora zu aktivieren, wo ABM-fähige Steuerelemente Ihnen helfen, Entscheidungsträger dieser Unternehmen anzusprechen.

### Account-basierte Marketing-Aktivierung über mehrere Kanäle {#multi-channel-abm}

Als B2B-Marketing-Experte können Sie in Real-time CDP eine Account-Liste erstellen, um Unternehmen mit hohen Absichten zu identifizieren. Dann können Sie dieses Ziel verwenden, um die Liste in Bombora zu aktivieren und zielgerichtete Kampagnen über mehrere Kanäle auszuführen.

In bezahlten sozialen Medien können Sie auf Zielkonten auf Plattformen wie [!DNL LinkedIn] und [!DNL Facebook] personalisierte Anzeigen für Fachleute schalten. Mit nativen Anzeigenplattformen können Sie sicherstellen, dass die Inhalte relevante Entscheidungsträger erreichen.

Sie können Kampagnen auch auf das erweiterte Fernsehen ausweiten und Anzeigen an Schlüsselkonten senden.

Dieser Multi-Channel-Ansatz sorgt für konsistentes Messaging über Plattformen hinweg und maximiert Interaktions- und Konversionsraten.

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Art von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | X | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Unterstützte Identitäten {#supported-identities}

Bombora erfordert die Zuordnung der Zielidentität, die in der folgenden Tabelle beschrieben ist. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung |
|---|---|
| `primaryId` | Bombora erfordert die Zuordnung dieser Zielidentität, damit die Integration ordnungsgemäß funktioniert. Sie können dieser Identität ein beliebiges Quellfeld zuordnen. Diese Zuordnung ist obligatorisch, exportiert jedoch keine Daten nach Bombora. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-and-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder sonstiges), die im [!DNL Bombora]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

Um Account-Zielgruppen nach Bombora zu exportieren, benötigen Sie die folgenden Informationen.

1. Ein Bombora-Konto.
2. Ein Bombora **[!UICONTROL client ID]** und **[!UICONTROL client secret]**.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigung[. &#x200B;](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Connect to destination]** aus.

![Bearer-Token hinzufügen](../../assets/catalog/advertising/bombora/add-bearer-token.png)

* **[!UICONTROL Client ID]**: Geben Sie Ihre [!DNL Bombora]-Client-ID ein.
* **[!UICONTROL Client secret]**: Geben Sie Ihr [!DNL Bombora]-Client-Geheimnis ein.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Fügen Sie Informationen über die Zielverbindung hinzu](../..//assets/catalog/advertising/bombora/name-and-description.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

Jetzt können Sie Ihre Zielgruppen in Bombora aktivieren.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[&#x200B; &#x200B;](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen [&#x200B; Aktivieren von Konto-Zielgruppen für &#x200B;](/help/destinations/ui/activate-account-audiences.md) Ziel finden Sie unter „Aktivieren von Konto-Zielgruppen“.

### Obligatorische Zuordnungen {#mapping}

Für das Bombora-Ziel müssen Sie die folgenden Zuordnungen konfigurieren, um eine erfolgreiche Datenaktivierung zu ermöglichen.



| Quellfeld | Zielfeld | Beschreibung |
|---------|----------|---------|
| Beliebiger Wert | `Identity: primaryId` | Diese Zuordnung ist für Experience Platform zum Aufbau einer Verbindung mit Bombora zwingend erforderlich. Dieser Wert wird nicht nach Bombora exportiert, sondern ist für die Zielkonfiguration erforderlich. Sie können ein beliebiges Attribut für das Quellfeld auswählen. |
| `xdm: accountOrganization.domain` | `xdm: companyWebsiteDomain` | Bombora verwendet Website- oder Domain-Adressen zur Erstellung einer Kontoliste. |

![Obligatorische Zuordnungen hinzufügen](../..//assets/catalog/advertising/bombora/mappings.png)


## Zusätzliche Hinweise und wichtige Hinweise {#additional-notes}

Wenn eine Konto-Zielgruppe mit demselben Namen zuvor für Bombora aktiviert wurde, erhalten Sie einen Fehler, wenn Sie versuchen, sie über einen anderen Datenfluss zum Bombora-Ziel erneut zu aktivieren.
