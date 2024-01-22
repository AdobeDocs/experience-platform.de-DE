---
title: Zendesk-Verbindung
description: Mit dem Zendesk-Ziel können Sie Ihre Kontodaten exportieren und innerhalb von Zendesk für Ihre geschäftlichen Anforderungen aktivieren.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: e7fcbbf4-5d6c-4abb-96cb-ea5b67a88711
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 42%

---

# [!DNL Zendesk]-Verbindung

[[!DNL Zendesk]](https://www.zendesk.de) ist eine Kundenservice-Lösung und ein Vertriebstool.

Diese [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt die [[!DNL Zendesk] Kontakt-API](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/), um **Erstellen und Aktualisieren von Identitäten** in einer Audience als Kontakte in [!DNL Zendesk].

[!DNL Zendesk] verwendet Trägertoken als Authentifizierungsmechanismus für die Kommunikation mit dem [!DNL Zendesk] Kontaktiert die API. Anweisungen zur Authentifizierung bei Ihrer [!DNL Zendesk]-Instanz sehen Sie weiter unten im Abschnitt [Authentifizieren bei Ziel](#authenticate).

## Anwendungsbeispiele {#use-cases}

Die Kundendienstabteilung einer mehrkanaligen B2C-Plattform möchte für ihre Kunden ein nahtloses personalisiertes Erlebnis gewährleisten. Die Abteilung kann Zielgruppen aus eigenen Offline-Daten erstellen, um neue Benutzerprofile zu erstellen oder vorhandene Profilinformationen aus verschiedenen Interaktionen zu aktualisieren (z. B. Käufe, Rückgaben usw.). und senden Sie diese Zielgruppen von Adobe Experience Platform an [!DNL Zendesk]. Aktualisierte Informationen finden Sie unter [!DNL Zendesk] stellt sicher, dass der Kundendienstmitarbeiter sofort über die neuesten Informationen des Kunden verfügt, was schnellere Antworten und eine schnellere Lösung ermöglicht.

## Voraussetzungen {#prerequisites}

### Voraussetzungen für Experience Platform {#prerequisites-in-experience-platform}

Vor der Aktivierung der Daten für das [!DNL Zendesk]-Ziel müssen Sie über ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=de) und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) verfügen, die in [!DNL Experience Platform] erstellt wurden.

Weitere Informationen finden Sie in der Experience Platform-Dokumentation für [Feldergruppe Zielgruppenzugehörigkeitsdetails](/help/xdm/field-groups/profile/segmentation.md) wenn Sie Anleitungen zum Zielgruppenstatus benötigen.

### Voraussetzungen für [!DNL Zendesk] {#prerequisites-destination}

So exportieren Sie Daten von Platform in Ihre [!DNL Zendesk] -Konto, über das Sie verfügen müssen, [!DNL Zendesk] -Konto.

#### Sammeln von [!DNL Zendesk]-Anmeldeinformationen {#gather-credentials}

Beachten Sie die folgenden Elemente, bevor Sie sich bei der [!DNL Zendesk] Ziel:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| `Bearer token` | Das Zugriffstoken, das Sie in Ihrer [!DNL Zendesk] -Konto. <br> Befolgen Sie die Dokumentation zum [generieren [!DNL Zendesk] Zugriffstoken](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) , wenn Sie keinen haben. | `a0b1c2d3e4...v20w21x22y23z` |

## Leitplanken {#guardrails}

Die [Preis- und Preisgrenzen](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) Seitendetails [!DNL Zendesk] API-Beschränkungen für Ihr Konto. Sie müssen sicherstellen, dass Ihre Daten und Payloads innerhalb dieser Beschränkungen liegen.

## Unterstützte Identitäten {#supported-identities}

[!DNL Zendesk] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/namespaces.md).

| Ziel-Identität | Beispiel | Beschreibung | Obligatorisch |
|---|---|---|---|
| `email` | `test@test.com` | Email-Adresse des Kontakts. | Ja |

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern *(z. B.: E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Jeder Segmentstatus in [!DNL Zendesk] wird mit dem entsprechenden Zielgruppenstatus von Platform aktualisiert, basierend auf dem **[!UICONTROL Zuordnungs-ID]** Wert, der während der [Zielgruppenplanung](#schedule-segment-export-example) Schritt.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | <ul><li>Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** nach [!DNL Zendesk]. Alternativ können Sie es unter der **[!UICONTROL CRM]**-Kategorie finden.

### Beim Ziel authentifizieren {#authenticate}

Füllen Sie die erforderlichen Felder aus. Siehe Abschnitt [Gather [!DNL Zendesk] Anmeldeinformationen](#gather-credentials) für Hinweise.
* **[!UICONTROL Trägertoken]**: Das Zugriffstoken, das Sie in Ihrer [!DNL Zendesk] -Konto.

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Mit Ziel verbinden]**.
![Screenshot der Platform-Benutzeroberfläche, auf dem die Authentifizierung gezeigt wird.](../../assets/catalog/crm/zendesk/authenticate-destination.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche den Status **[!UICONTROL Verbunden]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
![Screenshot der Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

Um Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an das [!DNL Zendesk]-Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodell (XDM) in Ihrem Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen.

In der Variablen **[!UICONTROL Zielfeld]** sollte genau wie in der Tabelle der Attributzuordnungen beschrieben benannt werden, da diese Attribute den Anfragetext bilden.

In der Variablen **[!UICONTROL Quellfeld]** keine solchen Einschränkungen befolgen. Sie können sie jedoch nach Bedarf zuordnen, wenn das Datenformat beim Senden an [!DNL Zendesk] wird ein Fehler ausgegeben.

Um Ihre XDM-Felder den [!DNL Zendesk]-Zielfeldern korrekt zuzuordnen, führen Sie die folgenden Schritte aus:

1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird eine neue Zuordnungszeile angezeigt.
1. Im **[!UICONTROL Quellfeld auswählen]** Fenster, wählen Sie die **[!UICONTROL Attribute auswählen]** und wählen Sie das XDM-Attribut oder die **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie eine Identität.
1. Im **[!UICONTROL Zielgruppenfeld auswählen]** Fenster, wählen Sie die **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie eine Zielidentität aus oder wählen Sie die **[!UICONTROL Attribute auswählen]** und wählen Sie eines der unterstützten Schemaattribute aus.
   * Wiederholen Sie diese Schritte, um die folgenden obligatorischen Zuordnungen hinzuzufügen. Sie können auch alle anderen Attribute hinzufügen, die Sie zwischen Ihrem XDM-Profilschema und Ihrem [!DNL Zendesk] instance: |Quellfeld|Zielfeld| Obligatorisch| |—|—|—| |`xdm: person.name.lastName`|`xdm: last_name`| Ja | |`IdentityMap: Email`|`Identity: email`| Ja | |`xdm: person.name.firstName`|`xdm: first_name`| |

   * Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Zuordnungen:
     ![Screenshot der Platform-Benutzeroberfläche mit Attributzuordnungen.](../../assets/catalog/crm/zendesk/mappings.png)

>[!IMPORTANT]
>
>Die `Attribute: last_name` und `Identity: email` Zielgruppen-Mappings sind für dieses Ziel obligatorisch. Wenn diese Zuordnungen fehlen, werden alle anderen Zuordnungen ignoriert und nicht an gesendet [!DNL Zendesk].

Wenn Sie mit der Bereitstellung der Zuordnungen für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Nächste]**.

### Zielgruppenexport und Beispiel planen {#schedule-segment-export-example}

Im [[!UICONTROL Zielgruppenexport planen]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) Schritt des Aktivierungs-Workflows müssen Sie Platform-Zielgruppen manuell dem benutzerdefinierten Feldattribut in [!DNL Zendesk].

Wählen Sie dazu jedes Segment aus und geben Sie dann das entsprechende benutzerdefinierte Feldattribut aus [!DNL Zendesk] im Feld **[!UICONTROL Zuordnungs-ID]** an.

Nachfolgend finden Sie ein Beispiel:
![Screenshot-Beispiel der Platform-Benutzeroberfläche mit der Option Zielgruppenexport planen](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Auswählen **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** und navigieren Sie zur Liste der Ziele.
1. Wählen Sie als Nächstes das Ziel aus und wechseln Sie zur **[!UICONTROL Aktivierungsdaten]** und wählen Sie einen Zielgruppennamen aus.
   ![Beispiel-Screenshot der Platform-Benutzeroberfläche mit Daten zur Aktivierung von Zielen.](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. Überwachen Sie die Zielgruppenzusammenfassung und stellen Sie sicher, dass die Anzahl der Profile der Anzahl innerhalb des Segments entspricht.
   ![Beispiel-Screenshot der Platform-Benutzeroberfläche mit Segment.](../../assets/catalog/crm/zendesk/segment.png)

1. Melden Sie sich bei [!DNL Zendesk] Website und navigieren Sie dann zur **[!UICONTROL Kontakte]** -Seite, um zu überprüfen, ob die Profile aus der Audience hinzugefügt wurden. Diese Liste kann so konfiguriert werden, dass Spalten für die zusätzlichen Felder angezeigt werden, die mit der Audience erstellt wurden**[!UICONTROL Zuordnungs-ID]** und Zielgruppenstatus.
   ![Screenshot der Zendesk-Benutzeroberfläche mit der Seite Kontakte mit den zusätzlichen Feldern, die mit dem Zielgruppennamen erstellt wurden.](../../assets/catalog/crm/zendesk/contacts.png)

1. Alternativ können Sie einen Drilldown in eine einzelne **[!UICONTROL Person]** und überprüfen Sie die **[!UICONTROL Zusätzliche Felder]** -Bereich, der den Zielgruppennamen und den Zielgruppenstatus anzeigt.
   ![Screenshot der Zendesk-Benutzeroberfläche mit der Seite &quot;Person&quot;und dem Abschnitt mit den zusätzlichen Feldern, in dem der Zielgruppenname und der Zielgruppenstatus angezeigt werden.](../../assets/catalog/crm/zendesk/contact.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

Zusätzliche nützliche Informationen aus dem [!DNL Zendesk] Die Dokumentation finden Sie unten:
* [Erstmaliger Aufruf](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [Benutzerdefinierte Felder](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)

### Änderungsprotokoll

In diesem Abschnitt werden aktualisierte Funktionen und wesentliche Dokumentationsänderungen für diesen Ziel-Connector erfasst.

+++ Änderungsprotokoll anzeigen

| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| April 2023 | Aktualisierung der Dokumentation | <ul><li>Wir haben die [Anwendungsfälle](#use-cases) mit einem klareren Beispiel dafür, wann Kunden von der Verwendung dieses Ziels profitieren würden.</li> <li>Wir haben die [Mapping](#mapping-considerations-example) , um die richtigen erforderlichen Zuordnungen widerzuspiegeln. Die `Attribute: last_name` und `Identity: email` Zielgruppen-Mappings sind für dieses Ziel obligatorisch. Wenn diese Zuordnungen fehlen, werden alle anderen Zuordnungen ignoriert und nicht an gesendet [!DNL Zendesk].</li> <li>Wir haben die [Mapping](#mapping-considerations-example) mit klaren Beispielen für obligatorische und optionale Zuordnungen.</li></ul> |
| März 2023 | Erstmalige Veröffentlichung | Erste Zielversion und Veröffentlichung der Dokumentation. |

{style="table-layout:auto"}

+++
