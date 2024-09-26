---
keywords: mobil; braze; messaging;
title: Braze-Verbindung
description: Braze ist eine umfassende Kundeninteraktionsplattform, die relevante und unvergessliche Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht.
last-substantial-update: 2024-08-20T00:00:00Z
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 2b84b5106105339ab243a9f4412b47692caedf3c
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 31%

---

# [!DNL Braze]-Verbindung

## Übersicht {#overview}

Mit dem Ziel [!DNL Braze] können Sie Profildaten an [!DNL Braze] senden.

[!DNL Braze] ist eine umfassende Kundeninteraktionsplattform, die relevante und unvergessliche Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht.

Um Profildaten an [!DNL Braze] zu senden, müssen Sie zunächst eine Verbindung zum Ziel herstellen.

## Zielspezifikationen {#specifics}

Beachten Sie die folgenden Details, die speziell für das Ziel [!DNL Braze] gelten:

* [!DNL Adobe Experience Platform] Zielgruppen werden unter dem Attribut `AdobeExperiencePlatformSegments` nach [!DNL Braze] exportiert.

>[!NOTE]
>
>Beachten Sie, dass das Senden zusätzlicher benutzerdefinierter Attribute an [!DNL Braze] zu einem Anstieg des [!DNL Braze] Datenpunktverbrauchs führen kann. Wenden Sie sich an Ihren [!DNL Braze] -Kundenbetreuer, bevor Sie zusätzliche benutzerdefinierte Attribute senden.

## Anwendungsfälle {#use-cases}

Als Marketing-Experte möchte ich Benutzer in einem Mobile-Interaktionsziel ansprechen, wobei Zielgruppen in [!DNL Adobe Experience Platform] integriert sind. Darüber hinaus möchte ich ihnen personalisierte Erlebnisse basierend auf Attributen aus ihren [!DNL Adobe Experience Platform] Profilen bereitstellen, sobald Audiences und Profile in [!DNL Adobe Experience Platform] aktualisiert werden.

## Unterstützte Identitäten {#supported-identities}

[!DNL Braze] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| external_id | Benutzerdefinierte [!DNL Braze]-Kennung, die die Zuordnung einer beliebigen Identität unterstützt. | Sie können jede [Identität](../../../identity-service/features/namespaces.md) an das [!DNL Braze] Ziel senden, solange Sie sie den [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation) zuordnen. |

{style="table-layout:auto"}

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
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname) und/oder Identitäten entsprechend Ihrer Feldzuordnung.[!DNL Adobe Experience Platform] Zielgruppen werden unter dem Attribut `AdobeExperiencePlatformSegments` nach [!DNL Braze] exportiert. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

* **[!UICONTROL Braze account token]**: Dies ist Ihr [!DNL Braze] [!DNL API] Schlüssel. Ausführliche Anweisungen zum Abrufen Ihres [!DNL API]-Schlüssels finden Sie hier: [REST API Key Overview](https://www.braze.com/docs/api/api_key/) .

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, mit dem Sie dieses Ziel in Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung ein, mit der Sie dieses Ziel in Zukunft identifizieren können.
* **[!UICONTROL Endpunktinstanz]**: Fragen Sie Ihren [!DNL Braze]-Support-Mitarbeiter, welche Endpunktinstanz Sie verwenden sollten.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

## Zuordnungsüberlegungen {#mapping-considerations}

Um Ihre Zielgruppendaten korrekt von [!DNL Adobe Experience Platform] an das Ziel [!DNL Braze] zu senden, müssen Sie den Schritt für die Feldzuordnung durchlaufen.

Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern [!DNL Experience Data Model] (XDM) in Ihrem [!DNL Platform]-Konto und den entsprechenden Entsprechungen zum Ziel zu erstellen.

Um Ihre XDM-Felder den [!DNL Braze]-Zielfeldern korrekt zuzuordnen, führen Sie die folgenden Schritte aus:

Klicken Sie im Schritt [!UICONTROL Zuordnung] auf **[!UICONTROL Neue Zuordnung hinzufügen]**.

![Prägen des Ziels hinzufügen, Zuordnung hinzufügen](../../assets/catalog/mobile-engagement/braze/mapping.png)

Klicken Sie im Bereich [!UICONTROL Source-Feld] auf die Pfeilschaltfläche neben dem leeren Feld.

![Source-Zielzuordnung nachblenden](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Im Fenster [!UICONTROL Quellfeld auswählen] können Sie zwischen zwei Kategorien von XDM-Feldern wählen:
* [!UICONTROL Attribute auswählen]: Verwenden Sie diese Option, um ein bestimmtes Feld aus Ihrem XDM-Schema einem [!DNL Braze] -Attribut zuzuordnen.

![Source-Attribut für die Zielzuordnung einblenden](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Identitäts-Namespace auswählen]: Verwenden Sie diese Option, um einen [!DNL Platform] Identitäts-Namespace einem [!DNL Braze]-Namespace zuzuordnen.

![Source-Namespace-Zielzuordnung begrenzen](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Wählen Sie Ihr Quellfeld aus und klicken Sie dann auf **[!UICONTROL Auswählen]**.

Klicken Sie im Abschnitt [!UICONTROL Zielfeld] auf das Zuordnungssymbol rechts neben dem Feld.

![Zielzuordnung in Brand Brand&#39;](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Im Fenster [!UICONTROL Zielfeld auswählen] können Sie zwischen zwei Kategorien von Zielfeldern wählen:
* [!UICONTROL Identitäts-Namespace auswählen]: Verwenden Sie diese Option, um [!DNL Platform] Identitäts-Namespaces [!DNL Braze] Identitäts-Namespaces zuzuordnen.
* [!UICONTROL Benutzerdefinierte Attribute auswählen]: Mit dieser Option können Sie XDM-Attribute benutzerdefinierten [!DNL Braze] Attributen zuordnen, die Sie in Ihrem [!DNL Braze]-Konto definiert haben. <br> Sie können diese Option auch verwenden, um vorhandene XDM-Attribute in [!DNL Braze] umzubenennen. Wenn Sie beispielsweise ein XDM-Attribut `lastName` in [!DNL Braze] einem benutzerdefinierten Attribut `Last_Name` zuordnen, wird das Attribut `Last_Name` in [!DNL Braze] erstellt, sofern es noch nicht vorhanden ist, und das XDM-Attribut `lastName` zugeordnet.

![Reduzieren der Zielzuordnungsfelder für Ziel ](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Wählen Sie Ihr Zielfeld aus und klicken Sie dann auf **[!UICONTROL Auswählen]**.

Ihr Feld-Mapping sollte jetzt in der Liste angezeigt werden.

![Abschluss der Braze Destination Mapping](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die vorherigen Schritte.

## Zuordnungsbeispiel {#mapping-example}

Angenommen, Ihr XDM-Profilschema und Ihre [!DNL Braze]-Instanz enthalten die folgenden Attribute und Identitäten:

|  | XDM-Profilschema | [!DNL Braze] Instanz |
|---|---|---|
| Attribute | <ul><li><code>person.name.firstName</code></li><li><code>person.name.lastName</code></li><li><code>mobilePhone.number</code></li></ul> | <ul><li><code>FirstName</code></li><li><code>LastName</code></li><li><code>PhoneNumber</code></li></ul> |
| Identitäten | <ul><li><code>E-Mail</code></li><li><code>Google Ad ID (GAID)</code></li><li><code>Apple ID für Advertiser (IDFA)</code></li></ul> | <ul><li><code>external_id</code></li></ul> |

Die korrekte Zuordnung würde wie folgt aussehen:

![Beispiel für die Braze Destination Mapping](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Exportierte Daten {#exported-data}

Um sich zu vergewissern, dass die Daten erfolgreich in das [!DNL Braze]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Braze]-Konto. [!DNL Adobe Experience Platform] Zielgruppen werden unter dem Attribut `AdobeExperiencePlatformSegments` nach [!DNL Braze] exportiert.

## Fehlerbehebung {#troubleshooting}

**Ich habe beim Aktivieren meiner Zielgruppen für dieses Ziel einen Timeout-Fehler erhalten. Was soll ich tun?**

Gelegentlich kann die Aktivierung der Zielgruppe für dieses Ziel zu einem Timeout-Fehler führen. Dieser Fehler wird nicht analysiert, was auf ein Aktivierungsproblem hinweist.

Wenn Sie einen Timeout-Fehler erhalten, überprüfen Sie die Zielgruppengröße in der Zielplattform. Wenn die Zielgruppengröße korrekt ist, funktioniert die Integration erwartungsgemäß.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen dazu, wie [!DNL Adobe Experience Platform] Data Governance durchsetzt, finden Sie unter [Data Governance - Übersicht](../../../data-governance/home.md).
