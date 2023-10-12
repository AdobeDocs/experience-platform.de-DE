---
title: Verbindungsverbindung
description: Moengage ist eine Kundeninteraktionsplattform, die kundenorientierte Interaktionen zwischen Verbrauchern und Marken in Echtzeit ermöglicht.
last-substantial-update: 2023-10-11T00:00:00Z
source-git-commit: 3d5a3ce18e7f1c0e06246faf8ec4403871e1a1a9
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 41%

---


# [!DNL Moengage]-Verbindung

## Übersicht {#overview}

Verwenden Sie die [!DNL Moengage] Ziel, um Ihre Adobe-Daten (Benutzerattribute, Segmente und Ereignisse) in Echtzeit mit MoEngage zu verbinden und zuzuordnen. Kunden können dann auf diese Daten reagieren und personalisierte, zielgerichtete Erlebnisse bereitstellen.

Mit Adobe ist die Integration sehr einfach und intuitiv. Nehmen Sie einfach ein beliebiges Adobe-Benutzerprofil und ordnen Sie es einem MoEngage-Benutzerattribut zu.

>[!IMPORTANT]
>
>Diese Ziel-Connector- und Dokumentationsseite wird von der *Motivation* Team. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an *`[amc-support@amazon.com](https://help.moengage.com/hc/en-us)`.*

## Anwendungsfälle {#use-cases}

Ein Marketing-Experte möchte ein (in Adobe Experience Platform integriertes) Benutzersegment über [!DNL Moengage] Kampagnen. Außerdem soll der Kampagneninhalt auf der Basis von Attributen aus Adobe Experience Platform-Profilen personalisiert werden. Mit dieser Integration werden Benutzer und Attribute in MoEngage aktualisiert, sobald Segmente und Profile in Adobe Experience Platform aktualisiert werden.

## Voraussetzungen {#prerequisites}

Bevor Sie Ihre Adobe Experience Platform-Daten an senden können [!DNL Moengage], beachten Sie die folgenden Voraussetzungen:

* Um das MoEngage-Ziel mit Adobe Experience Platform zu verwenden, müssen Benutzer zunächst Zugriff auf ihre [!DNL Moengage] Konto. Besuchen Sie die folgende Seite, um sich bei Ihrem MoEngage-Konto anzumelden oder anzumelden: https://app.moengage.com


## Unterstützte Identitäten {#supported-identities}

[!DNL Moengage] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| user_id | Eindeutige Kennung, die ein Benutzerprofil im [!DNL Moengage] System. | Diese Kennung unterstützt den String-Typ. Entweder &quot;user_id&quot;oder &quot;anonymous_id&quot;ist erforderlich |
| anonymous_id | Eine weitere Kennung für ein unbekanntes Benutzerprofil, d. h. ein Profil, das nicht im System vorhanden ist. | Diese Kennung unterstützt den String-Typ. Entweder &quot;user_id&quot;oder &quot;anonymous_id&quot;ist erforderlich |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den Kennungen (user_id, anonymous_id) zusammen mit benutzerdefinierten Attributen, die von Ihnen nach [!DNL Moengage]. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

![Moengage Destination Authentication](../../assets/catalog/mobile-engagement/moengage/authentication.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
![Moengage Destination Authentication](../../assets/catalog/mobile-engagement/moengage/settings.png)
* **[!UICONTROL USERNAME]**: DATA APP ID-Einstellungsseite von [!DNL Moengage] Dashboard.
* **[!UICONTROL KENNWORT]**: DATEN-APP-SCHLÜSSEL von der Einstellungsseite von [!DNL Moengage] Dashboard.

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
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

So senden Sie die Zielgruppendaten ordnungsgemäß von [!DNL Adobe Experience Platform] der [!DNL Moengage] Ziel, müssen Sie den Schritt zur Feldzuordnung durchlaufen.

Mapping besteht aus der Erstellung einer Verknüpfung zwischen [!DNL Experience Data Model] (XDM)-Schemafelder in Ihrer [!DNL Platform] und ihre entsprechenden Entsprechungen vom Zielort.

Um Ihre XDM-Felder den [!DNL Moengage]-Zielfeldern korrekt zuzuordnen, führen Sie die folgenden Schritte aus:

Im [!UICONTROL Zuordnung] Schritt auswählen **[!UICONTROL Kontrollkästchen]**.

![Moengage Destination Add Mapping](../../assets/catalog/mobile-engagement/moengage/segments.png)

Wählen Sie Im Schritt [!UICONTROL Zuordnung] die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus.

![Moengage Destination Add Mapping](../../assets/catalog/mobile-engagement/moengage/mapping.png)

Im [!UICONTROL Quellfeld] Wählen Sie neben dem leeren Feld die Pfeilschaltfläche aus.

![Zuordnung der Zielquelle von Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-source.png)

Im [!UICONTROL Quellfeld auswählen] -Fenster können Sie zwischen zwei Kategorien von XDM-Feldern wählen:
* [!UICONTROL Attribute auswählen]: Verwenden Sie diese Option, um ein bestimmtes Feld aus Ihrem XDM-Schema einem [!DNL Moengage] -Attribut.

![Quell-Attribut für Moengage Destination Mapping Source](../../assets/catalog/mobile-engagement/moengage/mapping-attributes.png)

Wählen Sie Ihr Quellfeld aus und klicken Sie auf **[!UICONTROL Auswählen]**.

Im [!UICONTROL Zielfeld] das Zuordnungssymbol rechts neben dem Feld.

![Zielgruppen-Mapping von Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-target.png)

Im [!UICONTROL Zielgruppenfeld auswählen] -Fenster können Sie zwischen zwei Kategorien von Zielfeldern wählen:
* [!UICONTROL Identitäts-Namespace auswählen]: Verwenden Sie diese Option für die Zuordnung [!DNL Platform] Identitäts-Namespaces zu [!DNL Moengage] Identitäts-Namespaces.
* [!UICONTROL Benutzerdefinierte Attribute auswählen]: Verwenden Sie diese Option, um XDM-Attribute benutzerdefinierten Attributen zuzuordnen [!DNL Moengage] -Attribute, die Sie in Ihren [!DNL Moengage] -Konto. <br> Sie können diese Option auch verwenden, um vorhandene XDM-Attribute in [!DNL Moengage]. Sie können beispielsweise eine `lastName` XDM-Attribut zu einem benutzerdefinierten `Last_Name` -Attribut in [!DNL Moengage], erstellt die `Last_Name` -Attribut in [!DNL Moengage], falls noch nicht vorhanden, und ordnen Sie die `lastName` XDM-Attribut.

![Zielgruppen-Mapping-Felder von Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-target-fields.png)

Wählen Sie Ihr Zielfeld aus und wählen Sie dann **[!UICONTROL Auswählen]**.

Ihr Feld-Mapping sollte jetzt in der Liste angezeigt werden.

![Abschluss der Moengage-Zielzuordnung](../../assets/catalog/mobile-engagement/moengage/mapping-complete.png)

Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die vorherigen Schritte.

## Exportierte Daten/Datenexport validieren {#exported-data}

So überprüfen Sie, ob die Daten erfolgreich in die [!DNL Moengage] Ziel, navigieren Sie zum Benutzerprofil in Ihrem [!DNL Moengage] -Konto. Es wird ein Benutzerattribut mit dem Namen AEP Segment angezeigt.

![Abschluss der Moengage-Zielzuordnung](../../assets/catalog/mobile-engagement/moengage/validation.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

