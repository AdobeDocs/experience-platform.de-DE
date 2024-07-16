---
keywords: Luftschiff-Tags; Luftschiff-Ziel
title: Airship Tags-Verbindung
description: Nahtlose Weitergabe von Adobe-Zielgruppendaten an Airship als Zielgruppen-Tags für Targeting innerhalb von Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 32%

---

# [!DNL Airship Tags]-Verbindung {#airship-tags-destination}

## Übersicht

[!DNL Airship] ist die führende Customer Engagement-Plattform, mit der Sie Ihren Benutzern in jeder Phase des Kundenlebenszyklus sinnvolle, personalisierte Omnichannel-Botschaften bereitstellen können.

Durch diese Integration werden Adobe Experience Platform-Zielgruppendaten zum Targeting oder Auslösen als [Tags](https://docs.airship.com/guides/audience/tags/) an [!DNL Airship] übergeben.

Weitere Informationen zu [!DNL Airship] finden Sie in den [Luftschiffsdokumenten](https://docs.airship.com).


>[!TIP]
>
>Diese Ziel-Connector- und Dokumentationsseite werden vom [!DNL Airship]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an [support.airship.com](https://support.airship.com/).

## Voraussetzungen

Bevor Sie Ihre Adobe Experience Platform-Zielgruppen an [!DNL Airship] senden können, müssen Sie Folgendes tun:

* Erstellen Sie eine Tag-Gruppe in Ihrem [!DNL Airship] -Projekt.
* Generieren Sie ein Trägertoken zur Authentifizierung.

>[!TIP]
> 
>Erstellen Sie ein [!DNL Airship] -Konto über [diesen Anmelde-Link](https://go.airship.eu/accounts/register/plan/starter/) , falls noch nicht geschehen.

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die durch den Experience Platform [Segmentierungsdienst](../../../segmentation/home.md) generiert wurden. |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den Kennungen, die im Ziel für Airship Tags verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Tag-Gruppen

Das Konzept der Zielgruppen in Adobe Experience Platform ähnelt dem in Airship verwendeten Tag [Tags](https://docs.airship.com/guides/audience/tags/), allerdings mit geringfügigen Abweichungen bei der Implementierung. Diese Integration ordnet den Status der [Mitgliedschaft eines Benutzers in einem Experience Platform-Segment](../../../xdm/field-groups/profile/segmentation.md) dem Vorhandensein oder Nichtvorhandensein eines [!DNL Airship] -Tags zu. Beispiel: In einer Platform-Audience, in der sich die `xdm:status` in `realized` ändert, wird das Tag dem Kanal [!DNL Airship] hinzugefügt oder dem benannten Benutzer, dem dieses Profil zugeordnet ist. Wenn sich die `xdm:status` in `exited` ändert, wird das Tag entfernt.

Um diese Integration zu aktivieren, erstellen Sie eine *Tag-Gruppe* in [!DNL Airship] mit dem Namen `adobe-segments`.

>[!IMPORTANT]
>
>Aktivieren Sie beim Erstellen der neuen Tag-Gruppe **nicht** die Optionsschaltfläche mit &quot;[!DNL Allow these tags to be set only from your server]&quot;. Andernfalls schlägt die Adobe-Tags-Integration fehl.

Anweisungen zum Erstellen der Tag-Gruppe finden Sie unter [Tag-Gruppen verwalten](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) .

## Bearer-Token generieren

Navigieren Sie zu **[!UICONTROL Einstellungen]**&quot; **[!UICONTROL APIs &amp; Integrationen]** im [Airship Dashboard](https://go.airship.com) und wählen Sie im Menü links die Option **[!UICONTROL Token]** aus.

Klicken Sie auf **[!UICONTROL Token erstellen]**.

Geben Sie einen benutzerfreundlichen Namen für Ihr Token ein, z. B. &quot;Adobe-Tags-Ziel&quot;und wählen Sie &quot;Zugriff auf alle&quot;für die Rolle.

Klicken Sie auf **[!UICONTROL Token erstellen]** und speichern Sie die Details als vertraulich.

## Anwendungsfälle

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das [!DNL Airship Tags]-Ziel verwenden sollten, finden Sie hier Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall 1

Einzelhändler oder Unterhaltungsplattformen können Benutzerprofile für ihre Treuekunden erstellen und diese Zielgruppen für Nachrichten-Targeting auf mobilen Kampagnen an [!DNL Airship] übergeben.

### Anwendungsfall 2

Trigger von Eins-zu-Eins-Nachrichten in Echtzeit, wenn Benutzer in bestimmte Zielgruppen in Adobe Experience Platform fallen oder aus diesen herausfallen.

So richtet beispielsweise ein Einzelhändler eine brandspezifische Zielgruppe für Jeans in Platform ein. Dieser Händler kann nun eine Mobilnachricht Trigger haben, sobald jemand seine Jeans-Voreinstellung auf eine bestimmte Marke setzt.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

* **[!UICONTROL Trägertoken]**: das Trägertoken, das Sie im [!DNL Airship] -Dashboard generiert haben.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für dieses Ziel ein.
* **[!UICONTROL Domäne]**: Wählen Sie entweder ein US- oder ein EU-Rechenzentrum aus, je nachdem, welches [!DNL Airship] Rechenzentrum für dieses Ziel gilt.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

## Zuordnungsüberlegungen {#mapping-considerations}

[!DNL Airship] -Tags können entweder für einen Kanal festgelegt werden, der die Geräteinstanz darstellt, z. B. iPhone, oder für einen benannten Benutzer, der alle Geräte eines Benutzers einer gemeinsamen Kennung wie einer Kunden-ID zuordnet. Wenn Sie in Ihrem Schema als primäre Identität Nur-Text-E-Mail-Adressen (ungehasht) verwenden, wählen Sie das E-Mail-Feld in Ihren **[!UICONTROL Source-Attributen]** aus und ordnen Sie es wie unten dargestellt dem benannten [!DNL Airship] Benutzer in der rechten Spalte unter **[!UICONTROL Zielidentitäten]** zu.

![ Zuordnung von benannten Benutzern](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Bei Kennungen, die einem Kanal zugeordnet werden sollen, d. h. einem Gerät, müssen Sie basierend auf der Quelle dem entsprechenden Kanal zuordnen. Die folgenden Abbildungen zeigen, wie Sie eine Google Advertising ID einem Android-Kanal mit dem Wert [!DNL Airship] zuordnen.

![Verbindung zu Airship Tags herstellen](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Verbindung zu Airship Tags herstellen](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Kanalzuordnung](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen dazu, wie [!DNL Adobe Experience Platform] Data Governance durchsetzt, finden Sie unter [Data Governance - Übersicht](../../../data-governance/home.md).
