---
title: HubSpot-Verbindung
description: Mit dem HubSpot-Ziel können Sie Kontaktdatensätze in Ihrem HubSpot-Konto verwalten.
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: e2114bde-b7c3-43da-9f3a-919322000ef4
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 36%

---

# [!DNL HubSpot]-Verbindung

[[!DNL HubSpot]](https://www.hubspot.com) ist eine CRM-Plattform mit allen Software, Integrationen und Ressourcen, die Sie für die Verbindung von Marketing, Vertrieb, Content Management und Kundendienst benötigen. Dadurch können Sie Ihre Daten, Teams und Kunden auf einer CRM-Plattform verbinden.

Dieses [!DNL Adobe Experience Platform] [ Ziel](/help/destinations/home.md) nutzt die [[!DNL HubSpot] Kontakte-API](https://developers.hubspot.com/docs/api/crm/contacts), um Kontakte innerhalb von [!DNL HubSpot] nach der Aktivierung von einer bestehenden Experience Platform-Audience zu aktualisieren.

Anweisungen zur Authentifizierung bei Ihrer [!DNL HubSpot]-Instanz sehen Sie weiter unten im Abschnitt [Authentifizieren bei Ziel](#authenticate).

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL HubSpot]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

[!DNL HubSpot] -Kontakte speichern Informationen über die Kontakte, die mit Ihrem Unternehmen interagieren. Ihr Team verwendet die in [!DNL HubSpot] vorhandenen Kontakte, um die Experience Platform-Zielgruppen zu erstellen. Nachdem diese Zielgruppen an [!DNL HubSpot] gesendet wurden, werden ihre Informationen aktualisiert und jedem Kontakt wird eine Eigenschaft mit dem Wert als Zielgruppenname zugewiesen, der angibt, zu welcher Zielgruppe der Kontakt gehört.

## Voraussetzungen {#prerequisites}

In den folgenden Abschnitten finden Sie alle Voraussetzungen, die Sie in Experience Platform und [!DNL HubSpot] einrichten müssen, sowie Informationen, die Sie vor der Arbeit mit dem [!DNL HubSpot]-Ziel erfassen müssen.

### Voraussetzungen für Experience Platform {#prerequisites-in-experience-platform}

Bevor Sie Daten für das Ziel [!DNL HubSpot] aktivieren, müssen Sie über ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) und [Zielgruppen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) verfügen, die in [!DNL Experience Platform] erstellt wurden.

Informationen zum Zielgruppenstatus finden Sie in der Experience Platform-Dokumentation für die Schemakonferenz [Zielgruppenzugehörigkeitsdetails](/help/xdm/field-groups/profile/segmentation.md) .

### Voraussetzungen für das [!DNL HubSpot]-Ziel {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen, um Daten von Platform in Ihr [!DNL HubSpot] -Konto zu exportieren:

#### Sie müssen über ein [!DNL HubSpot] -Konto verfügen. {#prerequisites-account}

Um Daten von Platform in Ihr [!DNL Hubspot] -Konto zu exportieren, benötigen Sie ein [!DNL HubSpot] -Konto. Wenn Sie noch kein Konto haben, besuchen Sie die Seite [Einrichten Ihres HubSpot-Kontos](https://knowledge.hubspot.com/get-started/set-up-your-account) und befolgen Sie die Anweisungen zum Registrieren und Erstellen Ihres Kontos.

#### Erfassen des Zugriffs-Tokens für die private App [!DNL HubSpot] {#gather-credentials}

Sie benötigen Ihre [!DNL HubSpot] `Access token`, damit das [!DNL HubSpot]-Ziel API-Aufrufe über Ihre [!DNL HubSpot] private App innerhalb Ihres [!DNL HubSpot]-Kontos tätigen kann. Die `Access token` dient als `Bearer token`, wenn Sie [das Ziel authentifizieren](#authenticate).

Wenn Sie keine private App haben, befolgen Sie die Dokumentation zu [Erstellen einer privaten App in  [!DNL HubSpot]](https://developers.hubspot.com/docs/api/private-apps).

>[!IMPORTANT]
>
> Der privaten App sollten die folgenden Bereiche zugewiesen werden:
> `crm.objects.contacts.write`, `crm.objects.contacts.read`
> `crm.schemas.contacts.write`, `crm.schemas.contacts.read`

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| `Bearer token` | Die `Access token` Ihrer privaten [!DNL HubSpot] App. <br> Um Ihre [!DNL HubSpot] `Access token` zu erhalten, befolgen Sie die [!DNL HubSpot] -Dokumentation, um [API-Aufrufe mit dem Zugriffstoken Ihrer App durchzuführen](https://developers.hubspot.com/docs/api/private-apps#make-api-calls-with-your-app-s-access-token). | `pat-na1-11223344-abcde-12345-9876-1234a1b23456` |

## Leitplanken {#guardrails}

[!DNL HubSpot] private Apps unterliegen den [Ratenbeschränkungen](https://developers.hubspot.com/docs/api/usage-details). Die Anzahl der Aufrufe, die Ihre private App tätigen kann, hängt von Ihrem [!DNL HubSpot] -Kontoabonnement und davon ab, ob Sie das API-Add-on erworben haben. Weitere Informationen finden Sie unter [Sonstige Beschränkungen](https://developers.hubspot.com/docs/api/usage-details#other-limits).

## Unterstützte Identitäten {#supported-identities}

[!DNL HubSpot] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beispiel | Beschreibung | Zu beachten |
|---|---|---|---|
| `email` | `test@test.com` | Email-Adresse des Kontakts. | Obligatorisch |

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt werden alle Zielgruppen beschrieben, die Sie an dieses Ziel exportieren können.

Dieses Ziel unterstützt die Aktivierung aller durch die Experience Platform generierten Zielgruppen über den [Segmentierungsdienst](../../../segmentation/home.md).

Dieses Ziel unterstützt auch die Aktivierung der in der folgenden Tabelle beschriebenen Zielgruppen.

| Zielgruppentyp | Beschreibung |
|---------|----------|
| Benutzerdefinierte Uploads | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder einer Zielgruppe zusammen mit den gewünschten Schemafeldern *(z. B. E-Mail-Adresse, Telefonnummer, Nachname)* gemäß Ihrer Feldzuordnung.</li><li> Darüber hinaus wird in [!DNL HubSpot] eine neue Eigenschaft mit dem Zielgruppennamen erstellt und ihr Wert weist für jede der ausgewählten Zielgruppen den entsprechenden Zielgruppenstatus von Platform auf.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | <ul><li>Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** nach [!DNL HubSpot]. Alternativ können Sie es unter der **[!UICONTROL CRM]**-Kategorie finden.

### Beim Ziel authentifizieren {#authenticate}

Füllen Sie die erforderlichen Felder aus. Eine Anleitung dazu finden Sie im Abschnitt [Zugriffstoken für private Apps sammeln [!DNL HubSpot] 2} .](#gather-credentials)
* **[!UICONTROL Trägertoken]**: Das Zugriffstoken für Ihre [!DNL HubSpot] private App.

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Mit Ziel verbinden]**.
![Screenshot der Platform-Benutzeroberfläche, auf dem die Authentifizierung gezeigt wird.](../../assets/catalog/crm/hubspot/authenticate-destination.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche den Status **[!UICONTROL Verbunden]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
![Screenshot der Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/crm/hubspot/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
>
>Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Um Ihre Zielgruppendaten korrekt von Adobe Experience Platform an das Ziel [!DNL HubSpot] zu senden, müssen Sie den Schritt für die Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodell (XDM) in Ihrem Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen.

Gehen Sie wie folgt vor, um Ihre XDM-Felder korrekt den [!DNL HubSpot] -Zielfeldern zuzuordnen:

#### Zuordnen der `Email`-Identität

Die `Email` -Identität ist eine obligatorische Zuordnung für dieses Ziel. Gehen Sie wie folgt vor, um sie zuzuordnen:
1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird jetzt eine neue Zuordnungszeile angezeigt.
   ![Screenshot der Platform-Benutzeroberfläche mit hervorgehobener Schaltfläche zum Hinzufügen einer neuen Zuordnung.](../../assets/catalog/crm/hubspot/mapping-add-new-mapping.png)
1. Wählen Sie im Fenster **[!UICONTROL Quellfeld auswählen]** den Namen **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie eine Identität aus.
   ![Screenshot der Platform-Benutzeroberfläche, in dem E-Mail als Quellattribut ausgewählt wird, das als Identität zugeordnet werden soll.](../../assets/catalog/crm/hubspot/mapping-select-source-identity.png)
1. Wählen Sie im Fenster **[!UICONTROL Zielfeld auswählen]** die Option **[!UICONTROL Attribute auswählen]** und danach `email` aus.
   ![Screenshot der Platform-Benutzeroberfläche, in dem E-Mail als Zielattribut ausgewählt wird, das als Identität zugeordnet werden soll.](../../assets/catalog/crm/hubspot/mapping-select-target-identity.png)

| Quellfeld | Zielfeld | Obligatorisch |
| --- | --- | --- |
| `IdentityMap: Email` | `Identity: email` | Ja |

Nachfolgend finden Sie ein Beispiel mit der Identitätszuordnung:
![Screenshot der Platform-Benutzeroberfläche mit E-Mail-Identitätszuordnung.](../../assets/catalog/crm/hubspot/mapping-identities.png)

#### Zuordnen von **optionalen** Attributen

Um weitere Attribute hinzuzufügen, die Sie zwischen Ihrem XDM-Profilschema und Ihrem [!DNL HubSpot]-Konto aktualisieren möchten, wiederholen Sie die folgenden Schritte:
1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird jetzt eine neue Zuordnungszeile angezeigt.
   ![Screenshot der Platform-Benutzeroberfläche mit hervorgehobener Schaltfläche zum Hinzufügen einer neuen Zuordnung.](../../assets/catalog/crm/hubspot/mapping-add-new-mapping.png)
1. Wählen Sie im Fenster **[!UICONTROL Quellfeld auswählen]** die Kategorie **[!UICONTROL Attribute auswählen]** und danach das XDM-Attribut aus.
   ![Screenshot der Platform-Benutzeroberfläche, in dem Vorname als Quellattribut ausgewählt wird.](../../assets/catalog/crm/hubspot/mapping-select-source-attribute.png)
1. Wählen Sie im Fenster **[!UICONTROL Zielfeld auswählen]** die Kategorie **[!UICONTROL Attribute auswählen]** und wählen Sie aus der Liste der Attribute aus, die automatisch aus Ihrem [!DNL HubSpot]-Konto gefüllt werden. Das Ziel verwendet die API [[!DNL HubSpot] Eigenschaften](https://developers.hubspot.com/docs/api/crm/properties) , um diese Informationen abzurufen. Sowohl [!DNL HubSpot] [Standardeigenschaften](https://knowledge.hubspot.com/contacts/hubspots-default-contact-properties) als auch benutzerdefinierte Eigenschaften werden zur Auswahl als Zielfelder abgerufen.
   ![Screenshot der Platform-Benutzeroberfläche zur Auswahl des Vornamens als Zielattribut.](../../assets/catalog/crm/hubspot/mapping-select-target-attribute.png)

Nachfolgend finden Sie einige verfügbare Zuordnungen zwischen Ihrem XDM-Profilschema und [!DNL Hubspot]:

| Quellfeld | Zielfeld |
| --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstname` |
| `xdm: person.name.lastName` | `Attribute: lastname` |
| `xdm: workAddress.street1` | `Attribute: address` |
| `xdm: workAddress.city` | `Attribute: city` |
| `xdm: workAddress.country` | `Attribute: country` |

Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Attributzuordnungen:
![Screenshot der Platform-Benutzeroberfläche mit Attributzuordnungen.](../../assets/catalog/crm/hubspot/mapping-attributes.png)

Wenn Sie die Zuordnungen für Ihre Zielverbindung bereitgestellt haben, wählen Sie **[!UICONTROL Weiter]** aus.

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Melden Sie sich bei der [!DNL HubSpot] -Website an und navigieren Sie dann zur Seite **[!UICONTROL Kontakte]** , um den Zielgruppenstatus zu überprüfen. Diese Liste kann so konfiguriert werden, dass Spalten für die benutzerdefinierten Eigenschaften angezeigt werden, die mit dem Zielgruppennamen erstellt wurden, wobei ihr Wert dem Zielgruppenstatus entspricht.
   ![HubSpot UI-Screenshot mit der Seite Kontakte mit Spaltenüberschriften, die den Zielgruppennamen und den Status der Zellen-Zielgruppe anzeigen](../../assets/catalog/crm/hubspot/contacts.png)

1. Alternativ können Sie einen Drilldown zu einer einzelnen Seite mit dem Namen **[!UICONTROL Person]** durchführen und zu den Eigenschaften navigieren, die den Zielgruppennamen und den Zielgruppenstatus anzeigen.
   ![HubSpot UI-Screenshot mit der Kontaktseite mit benutzerdefinierten Eigenschaften, die den Zielgruppennamen und den Zielgruppenstatus anzeigen.](../../assets/catalog/crm/hubspot/contact.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

Weitere nützliche Informationen aus der [!DNL HubSpot] -Dokumentation finden Sie unten:
* [Authentifizierungsmethoden für HubSpot](https://developers.hubspot.com/docs/api/intro-to-auth)
* [!DNL HubSpot] API-Referenzen für die APIs [Contacts](https://developers.hubspot.com/docs/api/crm/contacts) und [Properties](https://developers.hubspot.com/docs/api/crm/properties).

### Änderungsprotokoll

In diesem Abschnitt werden aktualisierte Funktionen und wesentliche Dokumentationsänderungen für diesen Ziel-Connector erfasst.

+++ Änderungsprotokoll anzeigen

| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| September 2023 | Erstmalige Veröffentlichung | Erste Zielversion und Veröffentlichung der Dokumentation. |

{style="table-layout:auto"}

+++
