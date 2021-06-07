---
keywords: mobil; einatmen; Messaging;
title: Bremsverbindung
description: Braze ist eine umfassende Kundeninteraktionsplattform, die relevante und unvergessliche Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 66c3e81dfdbf6f6c3ff9a127fbca8943c0e32279
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 4%

---

# (Beta) [!DNL Braze] Verbindung

>[!IMPORTANT]
>
>Das Ziel &quot;Braze&quot;in Adobe Experience Platform befindet sich derzeit in der Betaversion. Dokumentation und Funktionalität können sich ändern.

## Übersicht {#overview}

Mit dem [!DNL Braze]-Ziel können Sie Profildaten an [!DNL Braze] senden.

[!DNL Braze] ist eine umfassende Kundeninteraktionsplattform, die relevante und unvergessliche Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht.

Um Profildaten an [!DNL Braze] zu senden, müssen Sie zunächst eine Verbindung zum Ziel herstellen.

## Zielspezifikationen {#specifics}

Beachten Sie die folgenden Details, die speziell für das Ziel [!DNL Braze] gelten:

* [!DNL Adobe Experience Platform] -Segmente werden  [!DNL Braze] unter dem - `AdobeExperiencePlatformSegments` Attribut nach exportiert.

>[!NOTE]
>
>Beachten Sie, dass das Senden zusätzlicher benutzerdefinierter Attribute an [!DNL Braze] zu einem Anstieg des [!DNL Braze] Datenpunktverbrauchs führen kann. Wenden Sie sich an Ihren [!DNL Braze]-Kundenbetreuer, bevor Sie zusätzliche benutzerdefinierte Attribute senden.

## Anwendungsbeispiele {#use-cases}

Als Marketer möchte ich Benutzer in einem Ziel für mobile Interaktionen ansprechen, wobei Segmente in [!DNL Adobe Experience Platform] integriert sind. Darüber hinaus möchte ich ihnen personalisierte Erlebnisse basierend auf Attributen aus ihren [!DNL Adobe Experience Platform]-Profilen bereitstellen, sobald Segmente und Profile in [!DNL Adobe Experience Platform] aktualisiert werden.

## Unterstützte Identitäten {#supported-identities}

[!DNL Braze] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten.

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| external_id | Benutzerdefinierte [!DNL Braze]-Kennung, die die Zuordnung einer beliebigen Identität unterstützt. | Sie können jede [Identität](../../../identity-service/namespaces.md) an das [!DNL Braze]-Ziel senden, sofern Sie sie [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation) zuordnen. |

## Exporttyp {#export-type}

**[!DNL Profile-based]** - Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname) und/oder Identitäten, entsprechend Ihrer Feldzuordnung.
[!DNL Adobe Experience Platform] -Segmente werden  [!DNL Braze] unter dem - `AdobeExperiencePlatformSegments` Attribut nach exportiert.

## Mit Ziel verbinden {#connect-destination}

Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** die Option [!DNL Braze] und klicken Sie auf **[!UICONTROL Konfigurieren]**.

![Konfigurieren des Braze-Ziels](../../assets/catalog/mobile-engagement/braze/configure.png)

>[!NOTE]
>
>Wenn bereits eine Verbindung mit diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche **[!UICONTROL Aktivieren]** angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Activate]** und **[!UICONTROL Configure]** finden Sie im Abschnitt [Catalog](../../ui/destinations-workspace.md#catalog) der Dokumentation zum Ziel-Workspace.
>
>![Braze Destination aktivieren](../../assets/catalog/mobile-engagement/braze/activate.png)

Im Schritt [!UICONTROL Konto] müssen Sie Ihr [!DNL Braze]-Konto-Token angeben. Dies ist Ihr [!DNL Braze] [!DNL API] -Schlüssel. Ausführliche Anweisungen zum Abrufen Ihres [!DNL API]-Schlüssels finden Sie hier: [REST API Key Overview](https://www.braze.com/docs/api/api_key/). Geben Sie das Token ein und klicken Sie auf **[!UICONTROL Mit Ziel verbinden]**.

![Schritt &quot;Ziel-Konto löschen&quot;](../../assets/catalog/mobile-engagement/braze/account.png)

Klicken Sie auf **[!UICONTROL Weiter]**. Geben Sie im Schritt [!UICONTROL Authentifizierung] die Verbindungsdetails [!DNL Braze] ein:
* **[!UICONTROL Name]**: Geben Sie einen Namen ein, mit dem Sie dieses Ziel in Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung ein, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Endpunktinstanz]**: Fragen Sie Ihren  [!DNL Braze] Kundenbetreuer, welche Endpunktinstanz Sie verwenden sollten.
* **[!UICONTROL Marketing-Aktion]**: Marketing-Aktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketing-Aktionen auswählen oder eine eigene Marketing-Aktion erstellen. Weitere Informationen zu Marketing-Aktionen finden Sie auf der Seite [Data Governance in Adobe Experience Platform](../../../data-governance/policies/overview.md) . Informationen zu den einzelnen von der Adobe definierten Marketing-Aktionen finden Sie unter [Übersicht über Datennutzungsrichtlinien](../../../data-governance/policies/overview.md).

![Authentifizierungsschritt &quot;Blitzen&quot;](../../assets/catalog/mobile-engagement/braze/authentication.png)

Klicken Sie auf **[!UICONTROL Ziel erstellen]**. Ihr Ziel wird jetzt erstellt. Sie können auf **[!UICONTROL Speichern und beenden]** klicken, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** auswählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In beiden Fällen finden Sie den Rest des Workflows im nächsten Abschnitt [Segmente aktivieren](#activate-segments).

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-destinations.md#select-attributes).

## Feldzuordnung {#field-mapping}

Um Ihre Zielgruppendaten korrekt von [!DNL Adobe Experience Platform] an das [!DNL Braze]-Ziel zu senden, müssen Sie den Schritt für die Feldzuordnung durchlaufen.

Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern [!DNL Experience Data Model] (XDM) in Ihrem [!DNL Platform]-Konto und den entsprechenden Entsprechungen zum Zielziel zu erstellen.

Gehen Sie wie folgt vor, um Ihre XDM-Felder den Zielfeldern [!DNL Braze] richtig zuzuordnen:

Klicken Sie im Schritt [!UICONTROL Mapping] auf **[!UICONTROL Neue Zuordnung hinzufügen]**.

![Zielzuordnung löschen](../../assets/catalog/mobile-engagement/braze/mapping.png)

Klicken Sie im Abschnitt [!UICONTROL Quellfeld] auf die Pfeilschaltfläche neben dem leeren Feld.

![Zielquellenzuordnung löschen](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Im Fenster [!UICONTROL Quellfeld] auswählen können Sie zwischen zwei Kategorien von XDM-Feldern wählen:
* [!UICONTROL Attribute auswählen]: Verwenden Sie diese Option, um ein bestimmtes Feld aus Ihrem XDM-Schema einem  [!DNL Braze] Attribut zuzuordnen.

![Quell-Attribut für Zielzuordnung ausblenden](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Identitäts-Namespace] auswählen: Verwenden Sie diese Option, um einen  [!DNL Platform] Identitäts-Namespace einem  [!DNL Braze] Namespace zuzuordnen.

![Braze Destination Mapping Source Namespace](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Wählen Sie das Quellfeld aus und klicken Sie dann auf **[!UICONTROL Auswählen]**.

Klicken Sie im Abschnitt [!UICONTROL Zielfeld] auf das Zuordnungssymbol rechts neben dem Feld.

![Zielgruppen-Mapping für Braze](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Im Fenster [!UICONTROL Zielfeld] auswählen können Sie zwischen drei Kategorien von Zielfeldern wählen:
* [!UICONTROL Attribute auswählen]: Verwenden Sie diese Option, um Ihre XDM-Attribute Standardattributen  [!DNL Braze] zuzuordnen.
* [!UICONTROL Identitäts-Namespace] auswählen: Verwenden Sie diese Option, um  [!DNL Platform] Identitäts-Namespaces  [!DNL Braze] Identitäts-Namespaces zuzuordnen.
* [!UICONTROL Wählen Sie benutzerdefinierte Attribute] aus: Verwenden Sie diese Option, um XDM-Attribute benutzerdefinierten  [!DNL Braze] Attributen zuzuordnen, die Sie in Ihrem  [!DNL Braze] Konto definiert haben.
* Sie können diese Option auch verwenden, um vorhandene XDM-Attribute in [!DNL Braze] umzubenennen. Wenn Sie beispielsweise ein `lastName` XDM-Attribut einem benutzerdefinierten `Last_Name`-Attribut in [!DNL Braze] zuordnen, wird das `Last_Name`-Attribut in [!DNL Braze] erstellt, sofern es noch nicht vorhanden ist, und das `lastName`-XDM-Attribut zugeordnet.

![Zielgruppen-Mapping-Felder von Braze Destination](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Wählen Sie Ihr Zielfeld aus und klicken Sie dann auf **[!UICONTROL Auswählen]**.

Ihr Feld-Mapping sollte jetzt in der Liste angezeigt werden.

![Abschließen der Zielzuordnung verhindern](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die vorherigen Schritte.

## Zuordnungsbeispiel {#mapping-example}

Angenommen, Ihr XDM-Profilschema und Ihre [!DNL Braze]-Instanz enthalten die folgenden Attribute und Identitäten:

|  | XDM-Profilschema | [!DNL Braze] Instanz |
|---|---|---|
| Attribute | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| Identitäten | <ul><li>E-Mail </code></li><li>Google Ad ID (GAID)</code></li><li>Apple-ID für Advertiser (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

Die korrekte Zuordnung würde wie folgt aussehen:

![Beispiel für die Braze Destination Mapping](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Exportierte Daten {#exported-data}

Um zu überprüfen, ob die Daten erfolgreich an das [!DNL Braze]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Braze]-Konto. [!DNL Adobe Experience Platform] -Segmente werden  [!DNL Braze] unter dem - `AdobeExperiencePlatformSegments` Attribut nach exportiert.

## Datennutzung und Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen dazu, wie [!DNL Adobe Experience Platform] Data Governance durchsetzt, finden Sie unter [Übersicht über Data Governance](../../../data-governance/home.md).
