---
title: Zendesk-Verbindung
description: Mit dem Zendesk-Ziel können Sie Ihre Kontodaten exportieren und in Zendesk für Ihre Geschäftsanforderungen aktivieren.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: e7fcbbf4-5d6c-4abb-96cb-ea5b67a88711
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1408'
ht-degree: 35%

---

# [!DNL Zendesk]-Verbindung

[[!DNL Zendesk]](https://www.zendesk.de) ist eine Kundendienstlösung und ein Vertriebswerkzeug.

Dieses [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt die [[!DNL Zendesk] Kontakte-API](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/), um **Identitäten zu erstellen und zu aktualisieren** in einer Zielgruppe als Kontakte innerhalb von [!DNL Zendesk].

[!DNL Zendesk] verwendet Träger-Token als Authentifizierungsmechanismus für die Kommunikation mit der [!DNL Zendesk] Contacts-API. Anweisungen zur Authentifizierung bei Ihrer [!DNL Zendesk]-Instanz sehen Sie weiter unten im Abschnitt [Authentifizieren bei Ziel](#authenticate).

## Anwendungsbeispiele {#use-cases}

Die Kundendienstabteilung einer Multi-Channel B2C-Plattform möchte ihren Kunden ein nahtloses personalisiertes Erlebnis bieten. Die Abteilung kann Zielgruppen aus ihren eigenen Offline-Daten erstellen, um neue Benutzerprofile zu erstellen oder vorhandene Profilinformationen aus verschiedenen Interaktionen (z. B. Käufe, Rücksendungen usw.) zu aktualisieren und diese Zielgruppen von Adobe Experience Platform an [!DNL Zendesk] zu senden. Durch die Aktualisierung der Informationen in [!DNL Zendesk] wird sichergestellt, dass der Kundendienstmitarbeiter die aktuellen Kundeninformationen sofort verfügbar hat, was schnellere Reaktionen und eine schnellere Lösung ermöglicht.

## Voraussetzungen {#prerequisites}

### Voraussetzungen für Experience Platform {#prerequisites-in-experience-platform}

Vor der Aktivierung der Daten für das [!DNL Zendesk]-Ziel müssen Sie über ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) verfügen, die in [!DNL Experience Platform] erstellt wurden.

Weitere Informationen finden Sie in der Experience Platform[Dokumentation für die Schemafeldgruppe „Details zur Zielgruppenzugehörigkeit](/help/xdm/field-groups/profile/segmentation.md) , wenn Sie Anleitungen zu Zielgruppenstatus benötigen.

### Voraussetzungen für [!DNL Zendesk] {#prerequisites-destination}

Um Daten aus Experience Platform in Ihr [!DNL Zendesk]-Konto zu exportieren, benötigen Sie ein [!DNL Zendesk].

#### Sammeln von [!DNL Zendesk]-Anmeldedaten {#gather-credentials}

Beachten Sie die folgenden Punkte, bevor Sie sich beim [!DNL Zendesk]-Ziel authentifizieren:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| `Bearer token` | Das Zugriffstoken, das Sie in Ihrem [!DNL Zendesk]-Konto generiert haben. <br> Befolgen Sie die Dokumentation zum [Generieren eines  [!DNL Zendesk] -Zugriffstokens](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token), wenn Sie noch keines haben. | `a0b1c2d3e4...v20w21x22y23z` |

## Leitlinien {#guardrails}

Auf [&#x200B; Seite „Preise und &#x200B;](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing)&quot; werden die [!DNL Zendesk] API-Limits für Ihr Konto beschrieben. Sie müssen sicherstellen, dass Ihre Daten und Payloads innerhalb dieser Beschränkungen liegen.

## Unterstützte Identitäten {#supported-identities}

[!DNL Zendesk] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beispiel | Beschreibung | Obligatorisch |
|---|---|---|---|
| `email` | `test@test.com` | E-Mail-Adresse des Kontakts. | Ja |

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern *(z. B.: E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Jeder Segmentstatus in [!DNL Zendesk] wird mit dem entsprechenden Zielgruppenstatus von Experience Platform aktualisiert, basierend auf dem **[!UICONTROL Mapping ID]** Wert, der im Schritt [Zielgruppen-Planung](#schedule-segment-export-example) angegeben wurde.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | <ul><li>Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. &#x200B;](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** nach [!DNL Zendesk]. Alternativ können Sie es unter der Kategorie **[!UICONTROL CRM]** finden.

### Beim Ziel authentifizieren {#authenticate}

Füllen Sie die erforderlichen Felder aus. Eine Anleitung dazu finden [&#x200B; im Abschnitt  [!DNL Zendesk] Sammeln](#gather-credentials)Anmeldeinformationen“.

* **[!UICONTROL Bearer Token]**: Das Zugriffstoken, das Sie in Ihrem [!DNL Zendesk]-Konto generiert haben.

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Connect to destination]** aus.
Screenshot der ![Experience Platform-Benutzeroberfläche, auf dem die Authentifizierung gezeigt wird.](../../assets/catalog/crm/zendesk/authenticate-destination.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche einen **[!UICONTROL Connected]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
Screenshot der ![Experience Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[&#x200B; &#x200B;](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

Um Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an das [!DNL Zendesk]-Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodells (XDM) in Ihrem Experience Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen.

Die in der **[!UICONTROL Target field]** angegebenen Attribute sollten genau wie in der Tabelle der Attributzuordnungen beschrieben benannt werden, da diese Attribute den Anfragetext bilden.

Die in der **[!UICONTROL Source field]** angegebenen Attribute entsprechen keiner dieser Einschränkungen. Sie können sie nach Bedarf zuordnen. Wenn das Datenformat jedoch beim Pushen in [!DNL Zendesk] nicht korrekt ist, führt dies zu einem Fehler.

Um Ihre XDM-Felder den [!DNL Zendesk]-Zielfeldern korrekt zuzuordnen, führen Sie die folgenden Schritte aus:

1. Wählen Sie im **[!UICONTROL Mapping]** Schritt **[!UICONTROL Add new mapping]** aus. Auf dem Bildschirm wird eine neue Zuordnungszeile angezeigt.
1. Wählen Sie im **[!UICONTROL Select source field]** die Kategorie **[!UICONTROL Select attributes]** und dann das XDM-Attribut aus, oder wählen Sie die **[!UICONTROL Select identity namespace]** und dann eine Identität aus.
1. Wählen Sie im Fenster **[!UICONTROL Select target field]** die Kategorie **[!UICONTROL Select identity namespace]** und dann eine Zielidentität aus, oder wählen Sie die Kategorie **[!UICONTROL Select attributes]** und dann eines der unterstützten Schemaattribute aus.

   * Wiederholen Sie diese Schritte, um die folgenden obligatorischen Zuordnungen hinzuzufügen. Sie können auch alle anderen Attribute hinzufügen, die Sie zwischen Ihrem XDM-Profilschema und Ihrer [!DNL Zendesk]-Instanz aktualisieren möchten:

     | Quellfeld | Zielfeld | Obligatorisch |
     |---|---|---|
     | `xdm: person.name.lastName` | `xdm: last_name` | Ja |
     | `IdentityMap: Email` | `Identity: email` | Ja |
     | `xdm: person.name.firstName` | `xdm: first_name` | |

   * Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Zuordnungen:
     Beispiel-Screenshot der ![Experience Platform-Benutzeroberfläche mit Attributzuordnungen.](../../assets/catalog/crm/zendesk/mappings.png)

>[!IMPORTANT]
>
>Die `Attribute: last_name`- und `Identity: email` Zielgruppen-Mappings sind für dieses Ziel obligatorisch. Wenn diese Zuordnungen fehlen, werden alle anderen Zuordnungen ignoriert und nicht an [!DNL Zendesk] gesendet.

Wenn Sie mit dem Eingeben der Zuordnungen für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

### Planen des Zielgruppenexports und Beispiel {#schedule-segment-export-example}

Im [[!UICONTROL Schedule audience export]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) Schritt des Aktivierungs-Workflows müssen Sie Experience Platform-Zielgruppen manuell dem benutzerdefinierten Feldattribut in [!DNL Zendesk] zuordnen.

Wählen Sie dazu jedes Segment aus und geben Sie dann das entsprechende benutzerdefinierte Feldattribut aus [!DNL Zendesk] in das **[!UICONTROL Mapping ID]** Feld ein.

Nachfolgend finden Sie ein Beispiel:
Beispiel-Screenshot der Experience Platform-Benutzeroberfläche mit der Option „Zielgruppenexport planen“.![](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Wählen Sie **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** aus und navigieren Sie zur Liste der Ziele.
1. Wählen Sie anschließend das Ziel aus, wechseln Sie zur Registerkarte **[!UICONTROL Activation data]** und wählen Sie dann einen Zielgruppennamen aus.
   Beispiel-Screenshot der Experience Platform-Benutzeroberfläche mit Daten zur Aktivierung von Zielen.![](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. Überwachen Sie die Zielgruppenzusammenfassung und stellen Sie sicher, dass die Anzahl der Profile der Anzahl innerhalb des Segments entspricht.
   Beispiel-Screenshot der Experience Platform-Benutzeroberfläche mit Segment.![](../../assets/catalog/crm/zendesk/segment.png)

1. Melden Sie sich bei der [!DNL Zendesk]-Website an und navigieren Sie dann zur Seite **[!UICONTROL Contacts]** , um zu überprüfen, ob die Profile aus der Audience hinzugefügt wurden. Diese Liste kann so konfiguriert werden, dass Spalten für die zusätzlichen Felder angezeigt werden, die mit den Zielgruppen-**[!UICONTROL Mapping ID]**- und Zielgruppenstatus erstellt wurden.
   ![Screenshot der Zendesk-Benutzeroberfläche mit der Seite „Kontakte“ mit den zusätzlichen Feldern, die mit dem Zielgruppennamen erstellt wurden.](../../assets/catalog/crm/zendesk/contacts.png)

1. Alternativ können Sie einen Drilldown in eine einzelne **[!UICONTROL Person]** durchführen und den Abschnitt **[!UICONTROL Additional fields]** mit dem Zielgruppennamen und den Zielgruppenstatus überprüfen.
   ![Screenshot der Zendesk-Benutzeroberfläche, der die Seite Person mit dem Abschnitt „Zusätzliche Felder“ zeigt, auf der der Zielgruppenname und der Zielgruppenstatus angezeigt werden.](../../assets/catalog/crm/zendesk/contact.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Weitere Ressourcen {#additional-resources}

Weitere nützliche Informationen aus der [!DNL Zendesk] Dokumentation finden Sie unten:

* [Erster Anruf](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [Benutzerdefinierte Felder](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)

### Änderungsprotokoll

In diesem Abschnitt werden aktualisierte Funktionen und wesentliche Dokumentationsänderungen für diesen Ziel-Connector erfasst.

+++ Änderungsprotokoll anzeigen

| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| April 2023 | Dokumentation aktualisieren | <ul><li>Wir haben den Abschnitt [Anwendungsfälle](#use-cases) mit einem klareren Beispiel dafür aktualisiert, wann Kundinnen und Kunden von der Verwendung dieses Ziels profitieren würden.</li> <li>Der Abschnitt [Zuordnung](#mapping-considerations-example) wurde aktualisiert, um die richtigen erforderlichen Zuordnungen widerzuspiegeln. Die `Attribute: last_name`- und `Identity: email` Zielgruppen-Mappings sind für dieses Ziel obligatorisch. Wenn diese Zuordnungen fehlen, werden alle anderen Zuordnungen ignoriert und nicht an [!DNL Zendesk] gesendet.</li> <li>Der Abschnitt [Zuordnung](#mapping-considerations-example) wurde mit klaren Beispielen für obligatorische und optionale Zuordnungen aktualisiert.</li></ul> |
| März 2023 | Erstmalige Veröffentlichung | Erstmalige Zielveröffentlichung und Dokumentation. |

{style="table-layout:auto"}

+++
