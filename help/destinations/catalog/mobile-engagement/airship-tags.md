---
keywords: Airship Tags;Airship Destination
title: Airship Tags-Verbindung
description: Nahtlose Übergabe von Adobe-Zielgruppendaten an Airship als Zielgruppen-Tags für das Targeting innerhalb von Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 32%

---

# [!DNL Airship Tags]-Verbindung {#airship-tags-destination}

## Übersicht

[!DNL Airship] ist die führende Plattform für Kundeninteraktion, mit der Sie Ihren Benutzern in jeder Phase des Kundenlebenszyklus aussagekräftige, personalisierte Omni-Channel-Messaging bereitstellen können.

Diese Integration übergibt Adobe Experience Platform-Zielgruppendaten als [-Tags ](https://docs.airship.com/guides/audience/tags/) Targeting oder Triggern an [!DNL Airship].

Weitere Informationen zu [!DNL Airship] finden Sie unter [Airship Docs](https://docs.airship.com).


>[!TIP]
>
>Dieser Ziel-Connector und diese Dokumentationsseite werden vom [!DNL Airship]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an [support.airship.com](https://support.airship.com/).

## Voraussetzungen

Bevor Sie Ihre Adobe Experience Platform-Zielgruppen an [!DNL Airship] senden können, müssen Sie:

* Erstellen Sie eine Tag-Gruppe in Ihrem [!DNL Airship].
* Erzeugt ein Bearer-Token zur Authentifizierung.

>[!TIP]
> 
>Erstellen Sie über [diesen Anmelde-Link](https://go.airship.eu/accounts/register/plan/starter/) ein [!DNL Airship]-Konto, falls noch nicht geschehen.

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform ([-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs, die im Ziel „Airship Tags“ verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Tag-Gruppen

Das Konzept der Zielgruppen in Adobe Experience Platform ähnelt [Tags](https://docs.airship.com/guides/audience/tags/) in Airship, mit leichten Unterschieden in der Implementierung. Diese Integration ordnet den Status der Benutzermitgliedschaft [ einem Experience Platform-Segment dem ](../../../xdm/field-groups/profile/segmentation.md) oder Nicht-Vorhandensein eines [!DNL Airship]-Tags zu. Beispiel: In einer Platform-Zielgruppe, in der sich der `xdm:status` in &quot;`realized`&quot; ändert, wird das Tag dem [!DNL Airship]-Kanal oder dem benannten Benutzer hinzugefügt, dem dieses Profil zugeordnet ist. Wenn sich die `xdm:status` in `exited` ändert, wird das Tag entfernt.

Um diese Integration zu aktivieren, erstellen Sie eine *Tag-Gruppe* in [!DNL Airship] namens `adobe-segments`.

>[!IMPORTANT]
>
>Wählen Sie beim Erstellen Ihrer neuen Tag **Gruppe „Nicht**&quot; das Optionsfeld aus, auf dem &quot;[!DNL Allow these tags to be set only from your server]&quot; steht. Dadurch schlägt die Adobe-Tag-Integration fehl.

Anweisungen [ Erstellen der Tag](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups)Gruppe finden Sie unter „Verwalten von Tag-Gruppen“.

## Bearer-Token generieren

Navigieren Sie **[!UICONTROL Einstellungen]**&quot; **[!UICONTROL APIs und Integrationen]** im [Airship-Dashboard](https://go.airship.com) und wählen Sie **[!UICONTROL Token]** im linken Menü aus.

Klicken Sie **[!UICONTROL Token erstellen]**.

Geben Sie einen benutzerfreundlichen Namen für Ihr Token an, z. B. &quot;Adobe-Tags-Ziel“, und wählen Sie „Alle Zugriffe“ für die Rolle aus.

Klicken Sie **[!UICONTROL Token erstellen]** und speichern Sie die Details als vertraulich.

## Anwendungsfälle

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Airship Tags]-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel bewältigen können.

### Anwendungsfall #1

Einzelhändler oder Unterhaltungsplattformen können Benutzerprofile für ihre Treuekunden erstellen und diese Zielgruppen an [!DNL Airship] für das Nachrichten-Targeting in Mobile-Kampagnen weiterleiten.

### Anwendungsfall #2

Trigger von Eins-zu-eins-Nachrichten in Echtzeit, wenn Benutzende in bestimmte Zielgruppen in Adobe Experience Platform fallen oder aus ihnen herausfallen.

Ein Einzelhändler richtet in Platform beispielsweise eine markenspezifische Zielgruppe für Jeans ein. Dieser Einzelhändler kann jetzt eine Mobile-Nachricht als Trigger senden, sobald jemand seine Jeans-Präferenz auf eine bestimmte Marke festlegt.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

* **[!UICONTROL Bearer-Token]**: Das Bearer-Token, das Sie aus dem [!DNL Airship]-Dashboard generiert haben.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für dieses Ziel ein.
* **[!UICONTROL Domain]**: Wählen Sie entweder ein US- oder EU-Rechenzentrum aus, je nachdem, welches [!DNL Airship] Rechenzentrum für dieses Ziel gilt.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

## Zuordnungsüberlegungen {#mapping-considerations}

[!DNL Airship] Tags können entweder auf einem Kanal, der die Geräteinstanz darstellt, festgelegt werden, z. B. auf iPhone, oder auf einen benannten Benutzer, der alle Geräte eines Benutzers einer gemeinsamen Kennung wie einer Kunden-ID zuordnet. Wenn Sie in Ihrem Schema E-Mail-Adressen im Klartext (ungehasht) als primäre Identität haben, wählen Sie das E-Mail-Feld in Ihren **[!UICONTROL Source-]** aus und ordnen Sie sie dem [!DNL Airship] namens Benutzer in der rechten Spalte unter **[!UICONTROL Zielidentitäten]** zu, wie unten dargestellt.

![Benannte Benutzerzuordnung](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Für Kennungen, die einem Kanal, d. h. einem Gerät, zugeordnet werden sollen, ordnen Sie sie dem entsprechenden Kanal basierend auf der Quelle zu. Die folgenden Bilder zeigen, wie Sie einem [!DNL Airship] Android-Kanal eine Google Advertising ID zuordnen.

![Mit Airship Tags verbinden](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Mit Airship Tags verbinden](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Kanalzuordnung](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](../../../data-governance/home.md).
