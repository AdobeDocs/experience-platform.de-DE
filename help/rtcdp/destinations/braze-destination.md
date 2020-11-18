---
keywords: mobile; braze; messaging;
title: Ziel abbremsen
seo-title: Ziel abbremsen
description: Braze ist eine umfassende Kundenbindungsplattform, die relevante und unvergessliche Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht.
seo-description: Braze ist eine umfassende Kundenbindungsplattform, die relevante und unvergessliche Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht.
translation-type: tm+mt
source-git-commit: 4b1bf5bbce57a22529c5d025c5bae10557400d54
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 5%

---


# (Beta) [!DNL Braze] Ziel

>[!IMPORTANT]
>
>Das Braze-Ziel in Adobe Experience Platform befindet sich derzeit in Beta. Die Dokumentation und Funktionalität können sich ändern.

## Übersicht {#overview}

Das [!DNL Braze] Ziel hilft Ihnen, Profil-Daten an zu senden [!DNL Braze].

[!DNL Braze] ist eine umfassende Kundenbindungsplattform, die relevante und unvergessliche Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht.

Um Profil-Daten an [!DNL Braze]zu senden, müssen Sie zunächst eine Verbindung zum Ziel herstellen.

## Zielspezifikationen {#destination-specs}

Note the following details that are specific to the [!DNL Braze] destination:

* Sie können eine beliebige [Identität](../../identity-service/namespaces.md) an das [!DNL Braze] Ziel senden, solange Sie sie dem [!DNL Braze] Ziel zuordnen [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation).
* [!DNL Adobe Experience Platform] Segmente werden [!DNL Braze] unter dem `AdobeExperiencePlatformSegments` Attribut exportiert.

## Anwendungsbeispiele {#use-cases}

Als Marketingspezialist möchte ich Benutzer in einem Ziel für die Interaktion mit Mobilgeräten mit integrierten Segmenten Zielgruppe [!DNL Adobe Experience Platform]leisten. Darüber hinaus möchte ich ihnen personalisierte Erlebnisse auf Grundlage von Attributen aus ihren [!DNL Adobe Experience Platform] Profilen bereitstellen, sobald Segmente und Profil aktualisiert werden [!DNL Adobe Experience Platform].

## Exporttyp {#export-type}

**[!DNL Profile-based]** - Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname) und/oder Identitäten entsprechend Ihrer Feldzuordnung.
[!DNL Adobe Experience Platform] Segmente werden [!DNL Braze] unter dem `AdobeExperiencePlatformSegments` Attribut exportiert.


## Mit Ziel verbinden {#connect-destination}

1. Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** die Option [!DNL Braze]und wählen Sie **[!UICONTROL Konfigurieren]**.

   ![Braze-Ziel konfigurieren](assets/braze-destination-configure.png)

   >[!NOTE]
   >
   >Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche &quot; **[!UICONTROL Aktivieren]** &quot;angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Aktivieren]** und **[!UICONTROL Konfigurieren]** finden Sie im Abschnitt &quot; [Katalog](../destinations/destinations-workspace.md#catalog) &quot;der Dokumentation zum Zielarbeitsbereich.
   >
   >![Ziel der Fixierung aktivieren](assets/braze-destination-activate.png)

1. Im Schritt [!UICONTROL Konto] müssen Sie Ihr [!DNL Braze] Konto-Token angeben. Das ist dein [!DNL Braze][!DNL API] Schlüssel. Ausführliche Anweisungen zum Abrufen des [!DNL API] Schlüssels finden Sie hier: [REST-API-Schlüssel - Übersicht](https://www.braze.com/docs/api/api_key/). Geben Sie das Token ein und klicken Sie auf Mit Ziel **[!UICONTROL verbinden]**.

   ![Endkontoschritt festhalten](assets/braze-destination-account.png)

1. Klicken Sie auf **[!UICONTROL Weiter]**.

1. Im Schritt [!UICONTROL Authentifizierung] müssen Sie die [!DNL Braze] Verbindungsdetails eingeben:
   * **[!UICONTROL Name]**: Geben Sie einen Namen ein, unter dem Sie dieses Ziel in Zukunft erkennen werden.
   * **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung ein, mit der Sie dieses Ziel in Zukunft identifizieren können.
   * **[!UICONTROL Endpunktinstanz]**: fragen Sie Ihren [!DNL Braze] Kundenbetreuer, welche Endpunktinstanz Sie verwenden sollten.
   * **[!UICONTROL Anwendungsfall]** für das Marketing: Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Adobe Experience Platform](../privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen Anwendungsfällen für Marketingzwecke, die von der Adobe definiert wurden, finden Sie in der Übersicht über [Datenverwendungsrichtlinien](../../data-governance/policies/overview.md#core-actions).

   ![Authentifizierungsschritt](assets/braze-destination-authentication.png)

1. Klicken Sie auf Ziel **[!UICONTROL erstellen]**. Ihr Ziel wird jetzt erstellt. You can click **[!UICONTROL Save &amp; Exit]** if you want to activate segments later, or you can select **[!UICONTROL Next]** to continue the workflow and select segments to activate. In either case, see the next section, [Activate Segments](#activate-segments), for the rest of the workflow.

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](activate-destinations.md#select-attributes).

## Feldzuordnung {#field-mapping}

Um Ihre Audiencen korrekt von [!DNL Adobe Experience Platform] an das [!DNL Braze] Ziel zu senden, müssen Sie den Feldzuordnungsschritt durchführen.

Die Zuordnung besteht darin, eine Verknüpfung zwischen Ihren [!DNL Experience Data Model] (XDM-)Schema-Feldern in Ihrem [!DNL Platform] Konto und den entsprechenden Entsprechungen aus dem Zielort der Zielgruppe zu erstellen.

Gehen Sie wie folgt vor, um die XDM-Felder den [!DNL Braze] Zielfeldern korrekt zuzuordnen:

1. Klicken Sie im Schritt [!UICONTROL Zuordnung] auf **[!UICONTROL Hinzufügen neue Zuordnung]**.

   ![Zuordnung von Hinzufügen](assets/braze-destination-mapping.png)

2. Klicken Sie im Abschnitt [!UICONTROL Quellfeld] auf die Pfeilschaltfläche neben dem leeren Feld.

   ![Zuordnung der Zielquelle definieren](assets/braze-destination-mapping-source.png)

3. Im Fenster &quot;Quellfeld  auswählen&quot;können Sie zwischen zwei Kategorien von XDM-Feldern wählen:
   * [!UICONTROL Attribute]auswählen: Verwenden Sie diese Option, um ein bestimmtes Feld aus Ihrem XDM-Schema einem [!DNL Braze] Attribut zuzuordnen.

      ![Quellenattribut &quot;Zielzuordnung nachweisen&quot;](assets/braze-destination-mapping-attributes.png)

   * [!UICONTROL Identitäts-Namensraum]auswählen: Verwenden Sie diese Option, um einem [!DNL Platform] Namensraum einen [!DNL Braze] Identitäts-Namensraum zuzuordnen.

      ![Namensraum für die Zuordnung von Zielquellen](assets/braze-destination-mapping-namespaces.png)
   Wählen Sie das Quellfeld aus und klicken Sie dann auf **[!UICONTROL Auswählen]**.

4. Klicken Sie im Bereich &quot;Feld [!UICONTROL Zielgruppe] &quot;auf das Zuordnungssymbol rechts neben dem Feld.

   ![Zielgruppen-Mapping für das Ziel bremsen](assets/braze-destination-mapping-target.png)

5. Im Fenster &quot;Zielgruppe [!UICONTROL auswählen] &quot;können Sie zwischen drei Kategorien von Zielgruppen wählen:
   * [!UICONTROL Attribute]auswählen: Verwenden Sie diese Option, um Ihre XDM-Attribute Standardattributen [!DNL Braze] zuzuordnen.
   * [!UICONTROL Identitäts-Namensraum]auswählen: Verwenden Sie diese Option, um [!DNL Platform] Identitäts-Namensraum [!DNL Braze] -Namensräumen zuzuordnen.
   * [!UICONTROL Wählen Sie benutzerdefinierte Attribute]aus: Verwenden Sie diese Option, um XDM-Attribute benutzerdefinierten [!DNL Braze] Attributen zuzuordnen, die Sie in Ihrem [!DNL Braze] Konto definiert haben.
      * Sie können diese Option auch verwenden, um vorhandene XDM-Attribute umzubenennen in [!DNL Braze]. Wenn Sie beispielsweise ein `lastName` XDM-Attribut einem benutzerdefinierten `Last_Name` Attribut in zuordnen, wird das [!DNL Braze]Attribut in erstellt, `Last_Name` sofern es nicht bereits vorhanden ist, und es wird das XDM- [!DNL Braze]`lastName` Attribut zugeordnet.

   ![Zielgruppen-Mapping-Felder für Zielversion beschädigen](assets/braze-destination-mapping-target-fields.png)

   Wählen Sie das Feld Zielgruppe und klicken Sie dann auf **[!UICONTROL Auswählen]**.

6. Die Feldzuordnung sollte nun in der Liste angezeigt werden.

   ![Abschließen der Zielzuordnung verhindern](assets/braze-destination-mapping-complete.png)

7. Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die Schritte 1 bis 6.

### Beispiel {#mapping-example}

Angenommen, Ihr XDM-Profil-Schema und Ihre [!DNL Braze] Instanz enthalten die folgenden Attribute und Identitäten:

|  | XDM-Profil-Schema | [!DNL Braze] Instanz |
|---|---|---|
| Attribute | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| Identitäten | <ul><li>E-Mail </code></li><li>Google Ad ID (GAID)</code></li><li>Apple ID for Advertisers (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

Die richtige Zuordnung würde wie folgt aussehen:

![Beispiel für die Zuordnung von Endpunkten](assets/braze-destination-mapping-example.png)

## Exportierte Daten {#exported-data}

Um zu überprüfen, ob die Daten erfolgreich an das [!DNL Braze] Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Braze] Konto. [!DNL Adobe Experience Platform] Segmente werden [!DNL Braze] unter dem `AdobeExperiencePlatformSegments` Attribut exportiert.

## Nutzung und Verwaltung von Daten {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] Ziele sind beim Umgang mit Ihren Daten mit den Datenverwendungsrichtlinien konform. Ausführliche Informationen zur [!DNL Adobe Experience Platform] Durchsetzung der Datenverwaltung finden Sie unter [Datenverwaltung in Echtzeit-CDP](/help/rtcdp/privacy/data-governance-overview.md).

