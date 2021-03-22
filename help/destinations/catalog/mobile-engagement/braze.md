---
keywords: mobil; einblenden; Messaging;
title: Verbindung bremsen
description: Braze ist eine umfassende Kundenbindungsplattform, die relevante und unvergessliche Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 5%

---


# (Beta) [!DNL Braze]-Verbindung

>[!IMPORTANT]
>
>Das Braze-Ziel in Adobe Experience Platform befindet sich derzeit in Beta. Die Dokumentation und Funktionalität können sich ändern.

Mit dem [!DNL Braze]-Ziel können Sie Profil-Daten an [!DNL Braze] senden.

[!DNL Braze] ist eine umfassende Kundenbindungsplattform, die relevante und unvergessliche Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht.

Um Profil-Daten an [!DNL Braze] zu senden, müssen Sie zunächst eine Verbindung zum Ziel herstellen.

## Zielspezifikationen {#destination-specs}

Beachten Sie die folgenden Details, die für das [!DNL Braze]-Ziel spezifisch sind:

* [!DNL Adobe Experience Platform] Segmente werden  [!DNL Braze] unter dem  `AdobeExperiencePlatformSegments` Attribut exportiert.

>[!NOTE]
>
>Beachten Sie, dass das Senden zusätzlicher benutzerdefinierter Attribute an [!DNL Braze] zu einer Steigerung des [!DNL Braze] Datenpunktverbrauchs führen kann. Bitte wenden Sie sich an Ihren [!DNL Braze]-Kundenbetreuer, bevor Sie zusätzliche benutzerdefinierte Attribute senden.

## Anwendungsbeispiele {#use-cases}

Als Marketingspezialist möchte ich Benutzer an einem Ziel für die Interaktion mit Mobilgeräten mit Segmenten, die in [!DNL Adobe Experience Platform] integriert sind, Zielgruppe haben. Darüber hinaus möchte ich ihnen personalisierte Erlebnisse bereitstellen, die auf Attributen aus ihren [!DNL Adobe Experience Platform]-Profilen basieren, sobald Segmente und Profil in [!DNL Adobe Experience Platform] aktualisiert werden.

## Unterstützte Identitäten {#supported-identities}

[!DNL Google Ad Manager] unterstützt die Aktivierung der Identitäten, die in der folgenden Tabelle beschrieben sind.

| Zielgruppe | Beschreibung | Zu beachten |
|---|---|---|
| external_id | Benutzerdefinierter [!DNL Braze]-Bezeichner, der die Zuordnung einer beliebigen Identität unterstützt. | Sie können beliebige [Identität](../../../identity-service/namespaces.md) an das [!DNL Braze]-Ziel senden, solange Sie sie dem [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation) zuordnen. |

## Exporttyp {#export-type}

**[!DNL Profile-based]** - Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname) und/oder Identitäten entsprechend Ihrer Feldzuordnung.
[!DNL Adobe Experience Platform] Segmente werden  [!DNL Braze] unter dem  `AdobeExperiencePlatformSegments` Attribut exportiert.

## Mit Ziel verbinden {#connect-destination}

Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** [!DNL Braze] aus und wählen Sie **[!UICONTROL Konfigurieren]**.

![Braze-Ziel konfigurieren](../../assets/catalog/mobile-engagement/braze/configure.png)

>[!NOTE]
>
>Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche **[!UICONTROL Aktivieren]** angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Aktivieren]** und **[!UICONTROL Konfigurieren]** finden Sie im Abschnitt [Katalog](../../ui/destinations-workspace.md#catalog) der Dokumentation zum Zielarbeitsbereich.
>
>![Ziel der Fixierung aktivieren](../../assets/catalog/mobile-engagement/braze/activate.png)

Im Schritt [!UICONTROL Konto] müssen Sie Ihr [!DNL Braze]-Konto-Token angeben. Dies ist Ihre [!DNL Braze] [!DNL API]-Taste. Ausführliche Anweisungen zum Abrufen des Schlüssels [!DNL API] finden Sie hier: [Übersicht über den REST-API-Schlüssel](https://www.braze.com/docs/api/api_key/). Geben Sie das Token ein und klicken Sie auf **[!UICONTROL Mit Ziel verbinden]**.

![Endkontoschritt festhalten](../../assets/catalog/mobile-engagement/braze/account.png)

Klicken Sie auf **[!UICONTROL Weiter]**. Geben Sie im Schritt [!UICONTROL Authentication] die Verbindungsdetails [!DNL Braze] ein:
* **[!UICONTROL Name]**: Geben Sie einen Namen ein, unter dem Sie dieses Ziel in Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung ein, mit der Sie dieses Ziel in Zukunft identifizieren können.
* **[!UICONTROL Endpunktinstanz]**: fragen Sie Ihren  [!DNL Braze] Kundenbetreuer, welche Endpunktinstanz Sie verwenden sollten.
* **[!UICONTROL Marketingaktion]**: Marketingaktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketingaktionen auswählen oder eine eigene Marketingaktion erstellen. Weitere Informationen zu Marketingaktionen finden Sie auf der Seite [Datenverwaltung in Adobe Experience Platform](../../../data-governance/policies/overview.md). Informationen zu den einzelnen, von der Adobe definierten Marketingaktionen finden Sie unter [Übersicht über Datenverwendungsrichtlinien](../../../data-governance/policies/overview.md).

![Authentifizierungsschritt](../../assets/catalog/mobile-engagement/braze/authentication.png)

Klicken Sie auf **[!UICONTROL Ziel erstellen]**. Ihr Ziel wird jetzt erstellt. Sie können auf **[!UICONTROL Speichern und beenden]** klicken, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** auswählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In beiden Fällen finden Sie den Rest des Workflows im nächsten Abschnitt [Segmente aktivieren](#activate-segments).

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-destinations.md#select-attributes).

## Feldzuordnung {#field-mapping}

Um Ihre Audiencen korrekt von [!DNL Adobe Experience Platform] an das [!DNL Braze]-Ziel zu senden, müssen Sie den Feldzuordnungsschritt durchführen.

Die Zuordnung besteht darin, eine Verknüpfung zwischen den Feldern Ihres [!DNL Experience Data Model]-Schemas (XDM) in Ihrem [!DNL Platform]-Konto und den entsprechenden Entsprechungen aus dem Zielort der Zielgruppe zu erstellen.

Gehen Sie wie folgt vor, um Ihre XDM-Felder den Bestimmungsfeldern [!DNL Braze] richtig zuzuordnen:

Klicken Sie im Schritt [!UICONTROL Zuordnung] auf **[!UICONTROL Hinzufügen neue Zuordnung]**.

![Zuordnung von Hinzufügen](../../assets/catalog/mobile-engagement/braze/mapping.png)

Klicken Sie im Abschnitt [!UICONTROL Quellfeld] auf die Pfeilschaltfläche neben dem leeren Feld.

![Zuordnung der Zielquelle definieren](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Im Fenster [!UICONTROL Quellfeld] auswählen können Sie zwischen zwei Kategorien von XDM-Feldern wählen:
* [!UICONTROL Attribute] auswählen: Verwenden Sie diese Option, um ein bestimmtes Feld aus Ihrem XDM-Schema einem  [!DNL Braze] Attribut zuzuordnen.

![Quellenattribut &quot;Zielzuordnung nachweisen&quot;](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Identitäts-Namensraum] auswählen: Verwenden Sie diese Option, um einem  [!DNL Platform] Namensraum einen  [!DNL Braze] Identitäts-Namensraum zuzuordnen.

![Namensraum für die Zuordnung von Zielquellen](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Wählen Sie Ihr Quellfeld und klicken Sie dann auf **[!UICONTROL Wählen Sie]**.

Klicken Sie im Bereich [!UICONTROL Zielgruppe] auf das Zuordnungssymbol rechts neben dem Feld.

![Zielgruppen-Mapping für das Ziel bremsen](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Im Fenster [!UICONTROL Zielgruppe auswählen] können Sie zwischen drei Kategorien von Zielgruppe-Feldern wählen:
* [!UICONTROL Attribute] auswählen: Verwenden Sie diese Option, um Ihre XDM-Attribute den standardmäßigen  [!DNL Braze] Attributen zuzuordnen.
* [!UICONTROL Identitäts-Namensraum] auswählen: Verwenden Sie diese Option, um  [!DNL Platform] Identitäts-Namensraum  [!DNL Braze] Identitäts-Namensräumen zuzuordnen.
* [!UICONTROL Wählen Sie benutzerdefinierte Attribute] aus: Verwenden Sie diese Option, um XDM-Attribute benutzerdefinierten  [!DNL Braze] Attributen zuzuordnen, die Sie in Ihrem  [!DNL Braze] Konto definiert haben.
* Sie können diese Option auch verwenden, um vorhandene XDM-Attribute in [!DNL Braze] umzubenennen. Wenn beispielsweise ein `lastName`-XDM-Attribut einem benutzerdefinierten `Last_Name`-Attribut in [!DNL Braze] zugeordnet wird, wird das `Last_Name`-Attribut in [!DNL Braze] erstellt, sofern es noch nicht vorhanden ist, und es wird das `lastName`-XDM-Attribut zugeordnet.

![Zielgruppen-Mapping-Felder für Zielversion beschädigen](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Wählen Sie das Feld Zielgruppe und klicken Sie dann auf **[!UICONTROL Select]**.

Die Feldzuordnung sollte nun in der Liste angezeigt werden.

![Abschließen der Zielzuordnung verhindern](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die vorherigen Schritte.

## Zuordnungsbeispiel {#mapping-example}

Angenommen, Ihr XDM-Profil-Schema und Ihre [!DNL Braze]-Instanz enthalten die folgenden Attribute und Identitäten:

|  | XDM-Profil-Schema | [!DNL Braze] Instanz |
|---|---|---|
| Attribute | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| Identitäten | <ul><li>E-Mail </code></li><li>Google Ad ID (GAID)</code></li><li>Apple ID for Advertisers (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

Die richtige Zuordnung würde wie folgt aussehen:

![Beispiel für die Zuordnung von Endpunkten](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Exportierte Daten {#exported-data}

Um zu überprüfen, ob Daten erfolgreich in das [!DNL Braze]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Braze]-Konto. [!DNL Adobe Experience Platform] Segmente werden  [!DNL Braze] unter dem  `AdobeExperiencePlatformSegments` Attribut exportiert.

## Datenverwendung und -verwaltung {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit den Datenverwendungsrichtlinien konform. Detaillierte Informationen dazu, wie [!DNL Adobe Experience Platform] die Datenverwaltung erzwingt, finden Sie unter [Übersicht über die Datenverwaltung](../../../data-governance/home.md).

