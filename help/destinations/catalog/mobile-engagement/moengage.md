---
title: Verbindungsverbindung
description: Moengage ist eine Kundeninteraktionsplattform, die kundenorientierte Interaktionen zwischen Verbrauchern und Marken in Echtzeit ermöglicht.
last-substantial-update: 2023-10-11T00:00:00Z
exl-id: 051f1a10-3c41-4c0a-b187-bf80de0565f0
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 37%

---

# [!DNL Moengage]-Verbindung

## Übersicht {#overview}

Verwenden Sie das Ziel &quot;[!DNL Moengage]&quot;, um Ihre Adobe-Daten (Benutzerattribute, Segmente und Ereignisse) in Echtzeit mit MoEngage zu verbinden und zuzuordnen. Kunden können dann auf diese Daten reagieren und personalisierte, zielgerichtete Erlebnisse bereitstellen.

Mit Adobe ist die Integration sehr einfach und intuitiv. Nehmen Sie einfach ein beliebiges Adobe-Benutzerprofil und ordnen Sie es einem MoEngage-Benutzerattribut zu.

>[!IMPORTANT]
>
>Diese Ziel-Connector- und Dokumentationsseite werden vom *Moengage*-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an *`https://help.moengage.com/hc/en-us`.*

## Anwendungsfälle {#use-cases}

Ein Marketing-Experte möchte ein (in Adobe Experience Platform integriertes) Benutzersegment über [!DNL Moengage] -Kampagnen ansprechen. Außerdem soll der Kampagneninhalt auf der Basis von Attributen aus Adobe Experience Platform-Profilen personalisiert werden. Mit dieser Integration werden Benutzer und Attribute in MoEngage aktualisiert, sobald Segmente und Profile in Adobe Experience Platform aktualisiert werden.

## Voraussetzungen {#prerequisites}

Bevor Sie Ihre Adobe Experience Platform-Daten an [!DNL Moengage] senden können, beachten Sie die folgenden Voraussetzungen:

* Um das MoEngage-Ziel mit Adobe Experience Platform zu verwenden, müssen Benutzer zunächst Zugriff auf ihr [!DNL Moengage]-Konto haben. Besuchen Sie die folgende Seite, um sich bei Ihrem MoEngage-Konto anzumelden oder anzumelden: https://app.moengage.com


## Unterstützte Identitäten {#supported-identities}

[!DNL Moengage] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| user_id | Eindeutige Kennung, die ein Benutzerprofil im System [!DNL Moengage] eindeutig identifiziert. | Diese Kennung unterstützt den String-Typ. Entweder &quot;user_id&quot;oder &quot;anonymous_id&quot;ist erforderlich |
| anonymous_id | Eine weitere Kennung für ein unbekanntes Benutzerprofil, d. h. ein Profil, das nicht im System vorhanden ist. | Diese Kennung unterstützt den String-Typ. Entweder &quot;user_id&quot;oder &quot;anonymous_id&quot;ist erforderlich |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den Kennungen (user_id, anonymous_id) zusammen mit benutzerdefinierten Attributen, die Sie nach [!DNL Moengage] exportiert haben. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

![Moengage Destination Authentication](../../assets/catalog/mobile-engagement/moengage/authentication.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
![Moengage Destination Authentication](../../assets/catalog/mobile-engagement/moengage/settings.png)
* **[!UICONTROL BENUTZERNAME]**: DATA APP ID der Einstellungsseite des [!DNL Moengage] Dashboards.
* **[!UICONTROL KENNWORT]**: DATEN-APP-SCHLÜSSEL von der Einstellungsseite des [!DNL Moengage]-Dashboards.

![Moengage Destination Authentication](../../assets/catalog/mobile-engagement/moengage/destination_details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Region]**: Ihre App *Rechenzentrum*.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Um Ihre Zielgruppendaten korrekt von [!DNL Adobe Experience Platform] an das Ziel [!DNL Moengage] zu senden, müssen Sie den Schritt für die Feldzuordnung durchlaufen.

Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern [!DNL Experience Data Model] (XDM) in Ihrem [!DNL Platform]-Konto und den entsprechenden Entsprechungen zum Ziel zu erstellen.

Um Ihre XDM-Felder den [!DNL Moengage]-Zielfeldern korrekt zuzuordnen, führen Sie die folgenden Schritte aus:

Wählen Sie im Schritt [!UICONTROL Zuordnung] die Option **[!UICONTROL Kontrollkästchen]** aus.

![Moengage Destination Add Mapping](../../assets/catalog/mobile-engagement/moengage/segments.png)

Wählen Sie im Schritt [!UICONTROL Zuordnung] die Option **[!UICONTROL Neue Zuordnung hinzufügen]**.

![Moengage Destination Add Mapping](../../assets/catalog/mobile-engagement/moengage/mapping.png)

Wählen Sie im Bereich [!UICONTROL Source-Feld] die Pfeilschaltfläche neben dem leeren Feld aus.

![Moengage Destination Source Mapping](../../assets/catalog/mobile-engagement/moengage/mapping-source.png)

Im Fenster [!UICONTROL Quellfeld auswählen] können Sie zwischen zwei Kategorien von XDM-Feldern wählen:
* [!UICONTROL Attribute auswählen]: Verwenden Sie diese Option, um ein bestimmtes Feld aus Ihrem XDM-Schema einem [!DNL Moengage] -Attribut zuzuordnen.

![Source-Attribut für die Moengage-Zielzuordnung](../../assets/catalog/mobile-engagement/moengage/mapping-attributes.png)

Wählen Sie Ihr Quellfeld aus und wählen Sie dann **[!UICONTROL Auswählen]** aus.

Wählen Sie im Abschnitt [!UICONTROL Zielfeld] das Zuordnungssymbol rechts neben dem Feld aus.

![Zielzuordnung für den Zielkontakt festlegen](../../assets/catalog/mobile-engagement/moengage/mapping-target.png)

Im Fenster [!UICONTROL Zielfeld auswählen] können Sie zwischen zwei Kategorien von Zielfeldern wählen:
* [!UICONTROL Identitäts-Namespace auswählen]: Verwenden Sie diese Option, um [!DNL Platform] Identitäts-Namespaces [!DNL Moengage] Identitäts-Namespaces zuzuordnen.
* [!UICONTROL Benutzerdefinierte Attribute auswählen]: Mit dieser Option können Sie XDM-Attribute benutzerdefinierten [!DNL Moengage] Attributen zuordnen, die Sie in Ihrem [!DNL Moengage]-Konto definiert haben. <br> Sie können diese Option auch verwenden, um vorhandene XDM-Attribute in [!DNL Moengage] umzubenennen. Wenn Sie beispielsweise ein XDM-Attribut `lastName` in [!DNL Moengage] einem benutzerdefinierten Attribut `Last_Name` zuordnen, wird das Attribut `Last_Name` in [!DNL Moengage] erstellt, sofern es noch nicht vorhanden ist, und das XDM-Attribut `lastName` zugeordnet.

![ Zielzuordnungsfelder für das Ziel für die Verschiebung ](../../assets/catalog/mobile-engagement/moengage/mapping-target-fields.png)

Wählen Sie Ihr Zielfeld und dann **[!UICONTROL Auswählen]** aus.

Ihr Feld-Mapping sollte jetzt in der Liste angezeigt werden.

![ Abschluss der Moengage Destination Mapping Complete](../../assets/catalog/mobile-engagement/moengage/mapping-complete.png)

Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die vorherigen Schritte.

## Exportierte Daten/Datenexport validieren {#exported-data}

Um zu überprüfen, ob die Daten erfolgreich in das Ziel [!DNL Moengage] exportiert wurden, gehen Sie zum Benutzerprofil in Ihrem [!DNL Moengage] -Konto. Es wird ein Benutzerattribut mit dem Namen AEP Segment angezeigt.

![ Abschluss der Moengage Destination Mapping Complete](../../assets/catalog/mobile-engagement/moengage/validation.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
