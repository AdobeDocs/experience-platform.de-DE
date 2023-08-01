---
keywords: Luftschiff-Tags; Luftschiff-Ziel
title: Airship Tags-Verbindung
description: Nahtlose Weitergabe von Zielgruppendaten von Adobe an Airship als Zielgruppen-Tags für Targeting innerhalb von Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 31%

---

# [!DNL Airship Tags]-Verbindung {#airship-tags-destination}

## Übersicht

[!DNL Airship] ist die führende Plattform für Kundeninteraktionen, mit der Sie Ihren Benutzern in allen Phasen des Kundenlebenszyklus sinnvolle, personalisierte Omnichannel-Nachrichten bereitstellen können.

Diese Integration übergibt Adobe Experience Platform-Zielgruppendaten an [!DNL Airship] as [Tags](https://docs.airship.com/guides/audience/tags/) für Targeting oder Aktivierung.

Weitere Informationen zu [!DNL Airship], siehe [Dokumente für die Luftfahrt](https://docs.airship.com).


>[!TIP]
>
>Diese Ziel-Connector- und Dokumentationsseite wird von der [!DNL Airship] Team. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an [support.airship.com](https://support.airship.com/).

## Voraussetzungen

Bevor Sie Ihre Adobe Experience Platform-Zielgruppen an senden können [!DNL Airship]müssen Sie:

* Erstellen Sie eine Tag-Gruppe in Ihrem [!DNL Airship] Projekt.
* Generieren Sie ein Trägertoken zur Authentifizierung.

>[!TIP]
> 
>Erstellen Sie eine [!DNL Airship] Konto über [dieser Anmelde-Link](https://go.airship.eu/accounts/register/plan/starter/) wenn Sie noch nicht fertig sind.

## Unterstützung externer Zielgruppen {#external-audiences-support}

Alle Ziele unterstützen die Aktivierung von Zielgruppen, die durch die Experience Platform generiert wurden [Segmentierungsdienst](../../../segmentation/home.md).

Darüber hinaus unterstützt dieses Ziel auch die Aktivierung der externen Zielgruppen, die in der folgenden Tabelle beschrieben sind.

| Externer Zielgruppentyp | Beschreibung |
---------|----------|
| Benutzerdefinierte Uploads | Zielgruppen, die aus CSV-Dateien in Experience Platform aufgenommen werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den Kennungen, die im Ziel für Airship Tags verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform basierend auf der Zielgruppenbewertung aktualisiert wird, sendet der Connector das Update an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Tag-Gruppen

Das Konzept der Zielgruppen in Adobe Experience Platform ähnelt dem von [Tags](https://docs.airship.com/guides/audience/tags/) im Luftverkehr mit geringfügigen Abweichungen bei der Durchführung. Diese Integration ordnet den Status eines Benutzers zu [Mitgliedschaft in einem Experience Platform-Segment](../../../xdm/field-groups/profile/segmentation.md) das Vorhandensein oder Nichtvorhandensein einer [!DNL Airship] -Tag. Beispiel: In einer Platform-Audience, in der die Variable `xdm:status` Änderungen an `realized`, wird das Tag zum [!DNL Airship] -Kanal oder benannter Benutzer, dem dieses Profil zugeordnet ist. Wenn die Variable `xdm:status` Änderungen an `exited`, wird das Tag entfernt.

Um diese Integration zu aktivieren, erstellen Sie eine *Tag-Gruppe* in [!DNL Airship] benannt `adobe-segments`.

>[!IMPORTANT]
>
>Beim Erstellen einer neuen Tag-Gruppe **Nicht überprüfen** das Optionsfeld &quot;[!DNL Allow these tags to be set only from your server]&quot;. Andernfalls schlägt die Integration von Adobe-Tags fehl.

Siehe [Tag-Gruppen verwalten](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) für Anweisungen zum Erstellen der Tag-Gruppe.

## Bearer-Token generieren

Navigieren Sie zu **[!UICONTROL Einstellungen]** &quot; **[!UICONTROL APIs und Integrationen]** im [Airship Dashboard](https://go.airship.com) und wählen **[!UICONTROL Token]** im Menü links.

Klicks **[!UICONTROL Token erstellen]**.

Geben Sie einen benutzerfreundlichen Namen für Ihr Token ein, z. B. &quot;Ziel für Adobe-Tags&quot;und wählen Sie &quot;Zugriff auf alle&quot;für die Rolle.

Klicks **[!UICONTROL Token erstellen]** und speichern Sie die Angaben als vertraulich.

## Anwendungsfälle

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Airship Tags]-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel bewältigen können.

### Anwendungsfall 1

Einzelhändler oder Unterhaltungsplattformen können Benutzerprofile für ihre Treuekunden erstellen und diese Zielgruppen an [!DNL Airship] für Nachrichten-Targeting für mobile Kampagnen.

### Anwendungsfall 2

Trigger von Eins-zu-Eins-Nachrichten in Echtzeit, wenn Benutzer in bestimmte Zielgruppen in Adobe Experience Platform fallen oder aus diesen herausfallen.

So richtet beispielsweise ein Einzelhändler eine brandspezifische Zielgruppe für Jeans in Platform ein. Dieser Händler kann nun eine Mobilnachricht Trigger haben, sobald jemand seine Jeans-Voreinstellung auf eine bestimmte Marke setzt.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

* **[!UICONTROL Trägertoken]**: das Trägertoken, das Sie aus dem [!DNL Airship] Dashboard.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für dieses Ziel ein.
* **[!UICONTROL Domäne]**: Wählen Sie entweder ein US- oder EU-Rechenzentrum aus, je nachdem, welche [!DNL Airship] -Rechenzentrum gilt für dieses Ziel.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Streaming-Zielgruppenexport-Ziele](../../ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel.

## Zuordnungsüberlegungen {#mapping-considerations}

[!DNL Airship] -Tags können entweder für einen Kanal festgelegt werden, der die Geräteinstanz darstellt, z. B. iPhone, oder für einen benannten Benutzer, der alle Geräte eines Benutzers einer gemeinsamen Kennung wie einer Kunden-ID zuordnet. Wenn Sie in Ihrem Schema als primäre Identität Nur-Text-E-Mail-Adressen (ungehasht) verwenden, wählen Sie das E-Mail-Feld in Ihrem **[!UICONTROL Quellattribute]** und zugeordnet werden [!DNL Airship] benannter Benutzer in der rechten Spalte unter **[!UICONTROL Target-Identitäten]**, wie unten dargestellt.

![Zuordnung von benannten Benutzern](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Bei Kennungen, die einem Kanal zugeordnet werden sollen, d. h. einem Gerät, müssen Sie basierend auf der Quelle dem entsprechenden Kanal zuordnen. Die folgenden Abbildungen zeigen, wie Sie eine Google Advertising-ID einer [!DNL Airship] Android-Kanal.

![Verbindung zu Airship Tags](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Verbindung zu Airship Tags](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Kanalzuordnung](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](../../../data-governance/home.md).
