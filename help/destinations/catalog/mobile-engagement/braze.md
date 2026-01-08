---
keywords: Mobil; Hartlöten; Messaging;
title: Braze-Verbindung
description: Braze ist eine umfassende Plattform zur Kundeninteraktion, die relevante und einprägsame Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht.
last-substantial-update: 2024-08-20T00:00:00Z
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: cc97efec5fba090378ceaf73441d0b4bd7fbf51f
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 30%

---

# [!DNL Braze]-Verbindung

## Übersicht {#overview}

Mit dem [!DNL Braze] Ziel können Sie Profildaten an [!DNL Braze] senden.

[!DNL Braze] ist eine umfassende Plattform zur Kundeninteraktion, die relevante und einprägsame Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht.

Um Profildaten an [!DNL Braze] zu senden, müssen Sie zunächst eine Verbindung mit dem Ziel herstellen.

## Zielspezifikationen {#specifics}

Beachten Sie folgende Details, die speziell für das [!DNL Braze]-Ziel gelten:

* [!DNL Adobe Experience Platform] Zielgruppen werden unter dem [!DNL Braze] Attribut in `AdobeExperiencePlatformSegments` exportiert.

>[!NOTE]
>
>Beachten Sie, dass das Senden zusätzlicher benutzerdefinierter Attribute an [!DNL Braze] zu einer erhöhten Nutzung Ihrer [!DNL Braze] führen kann. Wenden Sie sich an Ihren [!DNL Braze] Account Manager, bevor Sie zusätzliche benutzerdefinierte Attribute senden.

## Anwendungsfälle {#use-cases}

Als Marketing-Experte möchte ich Benutzende in einem Ziel für mobile Interaktion ansprechen, wobei Zielgruppen in [!DNL Adobe Experience Platform] integriert sind. Darüber hinaus möchte ich ihnen personalisierte Erlebnisse auf der Grundlage von Attributen aus ihren [!DNL Adobe Experience Platform] bereitstellen, sobald Zielgruppen und Profile in [!DNL Adobe Experience Platform] aktualisiert werden.

## Unterstützte Identitäten {#supported-identities}

[!DNL Braze] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| EXTERNAL_ID | Benutzerdefinierte [!DNL Braze], die die Zuordnung beliebiger Identitäten unterstützt. | Sie können jede [Identität](../../../identity-service/features/namespaces.md) an das [!DNL Braze] Ziel senden, sofern Sie sie dem [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation) zuordnen. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname) und/oder Identitäten, entsprechend Ihrer Feldzuordnung.[!DNL Adobe Experience Platform] Zielgruppen werden unter dem [!DNL Braze] Attribut in `AdobeExperiencePlatformSegments` exportiert. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. &#x200B;](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Connect to destination]** aus.

* **[!UICONTROL Braze account token]**: Dies ist Ihr [!DNL Braze] [!DNL API]. Detaillierte Anweisungen zum Abrufen Ihres [!DNL API] finden Sie hier: [REST API Key Overview](https://www.braze.com/docs/api/api_key/).

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, um dieses Ziel in Zukunft zu erkennen.
* **[!UICONTROL Description]**: Geben Sie eine Beschreibung ein, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Endpoint Instance]**: Alle [regionsspezifischen Endpunkte](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) die von [!DNL Braze] unterstützt werden, können ausgewählt werden. Fragen Sie Ihren [!DNL Braze], welche Endpunktinstanz Sie verwenden sollten.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[&#x200B; &#x200B;](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

## Zuordnungsüberlegungen {#mapping-considerations}

Um Ihre Zielgruppendaten ordnungsgemäß von [!DNL Adobe Experience Platform] an das [!DNL Braze] Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen.

Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres [!DNL Experience Data Model] (XDM) in Ihrem [!DNL Experience Platform]-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen.

Um Ihre XDM-Felder den [!DNL Braze]-Zielfeldern korrekt zuzuordnen, führen Sie die folgenden Schritte aus:

Klicken Sie im [!UICONTROL Mapping] Schritt auf **[!UICONTROL Add new mapping]**.

![Braze-Ziel - Zuordnung hinzufügen](../../assets/catalog/mobile-engagement/braze/mapping.png)

Klicken Sie im Abschnitt [!UICONTROL Source Field] auf die Pfeilschaltfläche neben dem leeren Feld.

![Braze-Ziel-Source-Zuordnung](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Im [!UICONTROL Select source field] können Sie zwischen zwei Kategorien von XDM-Feldern wählen:

* [!UICONTROL Select attributes]: Verwenden Sie diese Option, um ein bestimmtes Feld aus Ihrem XDM-Schema einem [!DNL Braze] zuzuordnen.

![Braze-Zielzuordnung - Source-Attribut](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Select identity namespace]: Verwenden Sie diese Option, um einen [!DNL Experience Platform] Identity-Namespace einem [!DNL Braze]-Namespace zuzuordnen.

![Braze-Zielzuordnung - Source-Namespace](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Wählen Sie Ihr Quellfeld aus und klicken Sie dann auf **[!UICONTROL Select]**.

Klicken Sie im Abschnitt [!UICONTROL Target Field] auf das Zuordnungssymbol rechts neben dem Feld .

![Braze-Ziel-Mapping](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Im [!UICONTROL Select target field] können Sie zwischen zwei Kategorien von Zielfeldern wählen:

* [!UICONTROL Select identity namespace]: Verwenden Sie diese Option, um [!DNL Experience Platform] Identity-Namespaces [!DNL Braze] Identity-Namespaces zuzuordnen.
* [!UICONTROL Select custom attributes]: Verwenden Sie diese Option, um XDM-Attribute benutzerdefinierten [!DNL Braze] zuzuordnen, die Sie in Ihrem [!DNL Braze]-Konto definiert haben. <br> Sie können diese Option auch verwenden, um vorhandene XDM-Attribute in [!DNL Braze] umzubenennen. Wenn Sie beispielsweise ein `lastName` XDM-Attribut einem benutzerdefinierten `Last_Name`-Attribut in [!DNL Braze] zuordnen, wird das `Last_Name`-Attribut in [!DNL Braze] erstellt, falls es noch nicht vorhanden ist, und ihm wird das `lastName` XDM-Attribut zugeordnet.

![Braze-Ziel-Mapping-Felder](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Wählen Sie Ihr Zielfeld aus und klicken Sie dann auf **[!UICONTROL Select]**.

Die Feldzuordnung sollte nun in der Liste angezeigt werden.

![Braze-Zielzuordnung abgeschlossen](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die vorherigen Schritte.

## Zuordnungsbeispiel {#mapping-example}

Nehmen wir an, Ihr XDM-Profilschema und Ihre [!DNL Braze]-Instanz enthalten die folgenden Attribute und Identitäten:

|  | XDM-Profilschema | Instanz [!DNL Braze] |
|---|---|---|
| Attribute | <ul><li><code>person.name.firstName</code></li><li><code>person.name.lastName</code></li><li><code>mobilePhone.number</code></li></ul> | <ul><li><code>FirstName</code></li><li><code>Nachname</code></li><li><code>Telefonnummer</code></li></ul> |
| Identitäten | <ul><li><code>email</code></li><li><code>Google-Werbe-ID (GAID)</code></li><li><code>Apple-ID für Werbetreibende (IDFA)</code></li></ul> | <ul><li><code>external_id</code></li></ul> |

Die korrekte Zuordnung würde wie folgt aussehen:

![Beispiel für Braze-Zielzuordnung](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Exportierte Daten {#exported-data}

Um sich zu vergewissern, dass die Daten erfolgreich in das [!DNL Braze]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Braze]-Konto. [!DNL Adobe Experience Platform] Zielgruppen werden unter dem [!DNL Braze] Attribut in `AdobeExperiencePlatformSegments` exportiert.

## Fehlerbehebung {#troubleshooting}

**Ich habe beim Aktivieren meiner Zielgruppen für dieses Ziel einen Zeitüberschreitungsfehler erhalten. Was soll ich tun?**

Gelegentlich kann die Zielgruppenaktivierung für dieses Ziel zu einem Zeitüberschreitungsfehler führen. Dieser Fehler weist nicht immer auf ein Aktivierungsproblem hin.

Wenn Sie einen Zeitüberschreitungsfehler erhalten, überprüfen Sie die Zielgruppengröße in der Zielplattform. Wenn die Zielgruppengröße korrekt ist, funktioniert die Integration erwartungsgemäß.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](../../../data-governance/home.md).
