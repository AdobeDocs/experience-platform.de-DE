---
keywords: Luftschiff-Tags; Luftschiff-Ziel
title: Airship Tags-Verbindung
description: Nahtlose Weitergabe von Adobe-Zielgruppendaten an Airship als Zielgruppen-Tags für Targeting innerhalb von Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 8%

---

# [!DNL Airship Tags]-Verbindung {#airship-tags-destination}

## Übersicht

[!DNL Airship] ist die führende Plattform für Kundeninteraktionen, mit der Sie Ihren Benutzern in allen Phasen des Kundenlebenszyklus sinnvolle, personalisierte Omnichannel-Nachrichten bereitstellen können.

Diese Integration übergibt Adobe Experience Platform-Segmentdaten an [!DNL Airship] as [Tags](https://docs.airship.com/guides/audience/tags/) für Targeting oder Aktivierung.

Weitere Informationen finden Sie unter [!DNL Airship], siehe [Dokumente für die Luftfahrt](https://docs.airship.com).


>[!TIP]
>
>Diese Dokumentationsseite wurde von der [!DNL Airship] Team. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an [support.airship.com](https://support.airship.com/).

## Voraussetzungen

Bevor Sie Ihre Adobe Experience Platform-Segmente an senden können [!DNL Airship]müssen Sie:

* Erstellen Sie eine Tag-Gruppe in Ihrem [!DNL Airship] Projekt.
* Generieren Sie ein Trägertoken zur Authentifizierung.

>[!TIP]
> 
>Erstellen Sie eine [!DNL Airship] Konto über [dieser Anmelde-Link](https://go.airship.eu/accounts/register/plan/starter/) wenn Sie noch nicht fertig sind.

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den Kennungen, die im Ziel für Airship Tags verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Tag-Gruppen

Das Konzept der Segmente in Adobe Experience Platform ähnelt dem [Tags](https://docs.airship.com/guides/audience/tags/) im Luftverkehr mit geringfügigen Abweichungen bei der Durchführung. Diese Integration ordnet den Status eines Benutzers zu [Mitgliedschaft in einem Experience Platform-Segment](../../../xdm/field-groups/profile/segmentation.md) wenn eine [!DNL Airship] -Tag. Beispiel: In einem Platform-Segment, in dem die Variable `xdm:status` Änderungen an `realized`, wird das Tag zum [!DNL Airship] Kanal oder benannter Benutzer, dem dieses Profil zugeordnet ist. Wenn die Variable `xdm:status` Änderungen an `exited`, wird das Tag entfernt.

Um diese Integration zu aktivieren, erstellen Sie eine *Tag-Gruppe* in [!DNL Airship] benannt `adobe-segments`.

>[!IMPORTANT]
>
>Beim Erstellen einer neuen Tag-Gruppe **Nicht überprüfen** das Optionsfeld &quot;[!DNL Allow these tags to be set only from your server]&quot;. Andernfalls schlägt die Integration von Adobe-Tags fehl.

Siehe [Tag-Gruppen verwalten](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) für Anweisungen zum Erstellen der Tag-Gruppe.

## Bearer-Token generieren

Navigieren Sie zu **[!UICONTROL Einstellungen]** &quot; **[!UICONTROL APIs und Integrationen]** im [Airship Dashboard](https://go.airship.com) und wählen Sie **[!UICONTROL Token]** im Menü links.

Klicken **[!UICONTROL Token erstellen]**.

Geben Sie einen benutzerfreundlichen Namen für Ihr Token ein, z. B. &quot;Ziel für Adobe-Tags&quot;und wählen Sie &quot;Zugriff auf alle&quot;für die Rolle.

Klicken **[!UICONTROL Token erstellen]** und speichern Sie die Angaben als vertraulich.

## Anwendungsfälle

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die [!DNL Airship Tags] Ziel, hier finden Sie Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall 1

Einzelhändler oder Unterhaltungsplattformen können Benutzerprofile für ihre Treuekunden erstellen und diese Segmente an [!DNL Airship] für Nachrichten-Targeting für mobile Kampagnen.

### Anwendungsfall 2

Trigger von Eins-zu-Eins-Nachrichten in Echtzeit, wenn Benutzer in bestimmte Segmente innerhalb von Adobe Experience Platform fallen oder aus diesen herausfallen.

So richtet beispielsweise ein Einzelhändler ein markenspezifisches Jeans-Segment in Platform ein. Dieser Händler kann nun eine Mobilnachricht Trigger haben, sobald jemand seine Jeans-Voreinstellung auf eine bestimmte Marke setzt.

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Trägertoken]**: das Trägertoken, das Sie aus dem [!DNL Airship] Dashboard.
* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für dieses Ziel ein.
* **[!UICONTROL Domäne]**: Wählen Sie entweder ein US- oder EU-Rechenzentrum aus, je nachdem, welche [!DNL Airship] -Rechenzentrum gilt für dieses Ziel.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Zuordnungsüberlegungen {#mapping-considerations}

[!DNL Airship] -Tags können entweder für einen Kanal festgelegt werden, der die Geräteinstanz darstellt, z. B. iPhone, oder für einen benannten Benutzer, der alle Geräte eines Benutzers einer gemeinsamen Kennung wie einer Kunden-ID zuordnet. Wenn Sie in Ihrem Schema als primäre Identität Nur-Text-E-Mail-Adressen (ungehasht) verwenden, wählen Sie das E-Mail-Feld in Ihrem **[!UICONTROL Quellattribute]** und zugeordnet werden [!DNL Airship] benannter Benutzer in der rechten Spalte unter **[!UICONTROL Target-Identitäten]**, wie unten dargestellt.

![Zuordnung von benannten Benutzern](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Bei Kennungen, die einem Kanal zugeordnet werden sollen, d. h. einem Gerät, müssen Sie basierend auf der Quelle dem entsprechenden Kanal zuordnen. Die folgenden Abbildungen zeigen, wie Sie eine Google Advertising-ID einer [!DNL Airship] Android-Kanal.

![Verbindung zu Airship Tags](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Verbindung zu Airship Tags](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Kanalzuordnung](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](../../../data-governance/home.md).
