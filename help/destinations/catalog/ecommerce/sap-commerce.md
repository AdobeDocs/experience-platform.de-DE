---
title: SAP Commerce-Verbindung
description: Verwenden Sie den SAP Commerce-Ziel-Connector, um Kundendatensätze in Ihrem SAP-Konto zu aktualisieren.
last-substantial-update: 2024-02-20T00:00:00Z
source-git-commit: 9bb2cf5adcd48f9d111ba04b8c93129367dd12f8
workflow-type: tm+mt
source-wordcount: '2245'
ht-degree: 25%

---

# [!DNL SAP Commerce]-Verbindung

[!DNL SAP Commerce], früher bekannt als [[!DNL Hybris]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), ist eine Cloud-basierte E-Commerce-Plattform-Lösung für B2B- und B2C-Unternehmen und ist als Teil des SAP Customer Experience-Portfolios verfügbar. [[!DNL SAP] Abrechnung von Abonnements](https://www.sap.com/products/financial-management/subscription-billing.html) ist ein Produkt im Portfolio und ermöglicht ein komplettes Abonnement-Lebenszyklusmanagement mit vereinfachten Verkaufs- und Zahlungserlebnissen durch standardisierte Integrationen.

Diese [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) verwendet die [[!DNL SAP Subscription Billing] Kundenmanagement-API](https://api.sap.com/api/BusinessPartner_APIs/path/PUT_customers-customerNumber), um Ihre Kundendetails in zu aktualisieren. [!DNL SAP Commerce] aus einer bestehenden Experience Platform-Audience nach der Aktivierung.

Anweisungen zur Authentifizierung bei Ihrer [!DNL SAP Commerce]-Instanz sehen Sie weiter unten im Abschnitt [Authentifizieren bei Ziel](#authenticate).

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL SAP Commerce]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

[!DNL SAP Commerce] -Kunden speichern Informationen über Einzelpersonen oder Organisationseinheiten, die mit Ihrem Unternehmen interagieren. Ihr Team verwendet die in vorhandenen Kunden [!DNL SAP Commerce] um die Experience Platform-Zielgruppen zu erstellen. Nach dem Senden dieser Zielgruppen an [!DNL SAP Commerce], werden ihre Informationen aktualisiert und jedem Kunden wird eine Eigenschaft mit seinem Wert als Zielgruppenname zugewiesen, der angibt, zu welcher Zielgruppe der Kunde gehört.

## Voraussetzungen {#prerequisites}

In den folgenden Abschnitten finden Sie alle Voraussetzungen, die Sie unter Experience Platform einrichten müssen. [!DNL SAP Commerce] und für Informationen, die Sie vor der Arbeit mit dem [!DNL SAP Commerce] Ziel.

### Voraussetzungen für Experience Platform {#prerequisites-in-experience-platform}

Vor der Aktivierung der Daten für [!DNL SAP Commerce] Ziel, müssen Sie über eine [schema](/help/xdm/schema/composition.md), a [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=de), und [Zielgruppen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) erstellt in [!DNL Experience Platform].

Weitere Informationen finden Sie in der Experience Platform-Dokumentation für [Feldergruppe Zielgruppenzugehörigkeitsdetails](/help/xdm/field-groups/profile/segmentation.md) wenn Sie Anleitungen zum Zielgruppenstatus benötigen.

### Voraussetzungen für die [!DNL SAP Commerce] Ziel {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen, um Daten von Platform in Ihre [!DNL SAP Commerce] Konto:

#### Sie müssen über eine [!DNL SAP Subscription Billing] account {#prerequisites-account}

So exportieren Sie Daten von Platform in Ihre [!DNL SAP Commerce] -Konto, benötigen Sie eine [!DNL SAP Subscription Billing] -Konto. Wenn Sie kein gültiges Abrechnungskonto haben, wenden Sie sich an Ihren [!DNL SAP] Kundenbetreuer. Siehe Abschnitt [[!DNL SAP] Plattformkonfiguration](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) für weitere Details.

#### Generieren eines Dienstschlüssels {#prerequisites-service-key}

* Die [!DNL SAP Commerce] Der Service-Schlüssel ermöglicht Ihnen den Zugriff auf die [!DNL SAP Subscription Billing] API über Experience Platform. Siehe Abschnitt [!DNL SAP Commerce] [Erstellen eines Dienstschlüssels mit Client-ID und Client-Geheimnis](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/87c11a0f5dc3494eaf3baa355925c030.html#create-a-service-key-with-client-id-and-client-secret) , um einen Dienstschlüssel zu erstellen. [!DNL SAP Commerce] erfordert Folgendes:
   * Client-ID
   * Client-Geheimnis
   * URL. Das URL-Muster sieht wie folgt aus: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Dieser Wert wird später zum Abrufen von Werten für `Region` und `Endpoint`.

+++Auswählen , um ein Beispiel des Dienstschlüssels anzuzeigen

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

#### Erstellen Sie benutzerdefinierte Verweise in [!DNL SAP Subscription Billing] {#prerequisites-custom-reference}

So aktualisieren Sie den Experience Platform-Zielgruppenstatus in [!DNL SAP Subscription Billing]benötigen Sie ein benutzerdefiniertes Referenzfeld für jede in Platform ausgewählte Zielgruppe.

Um die benutzerdefinierten Referenzen zu erstellen, melden Sie sich bei Ihrer [!DNL SAP Subscription Billing] -Konto und navigieren Sie zum **[Master-Daten und -Konfiguration]** > **[Benutzerdefinierte Verweise]** Seite. Wählen Sie als Nächstes **[!UICONTROL Erstellen]** , um für jede in Platform ausgewählte Zielgruppe einen neuen Verweis hinzuzufügen. Sie benötigen diese Referenzfeldnamen in den folgenden [Zielgruppenexport und Beispiel planen](#schedule-segment-export-example) Schritt.

Ein Beispiel für die Erstellung eines benutzerdefinierten **[!UICONTROL Referenztyp]** Innerhalb [!DNL SAP Subscription Billing] ist unten dargestellt:
![Bild, das anzeigt, wo eine benutzerdefinierte Referenz in der SAP-Abonnementabrechnung erstellt werden soll.](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

Weitere Hinweise finden Sie im Abschnitt [!DNL SAP Subscription Billing] [benutzerspezifische Verweise](https://help.sap.com/docs/CLOUD_TO_CASH_OD/80d121f216af43648e79664efe5595f7/85696a63c8d8453a934e86c9413a25cf.html?version=2023-11-27) Dokumentation.

### Sammeln erforderlicher Anmeldeinformationen {#gather-credentials}

Verbindung herstellen [!DNL SAP Commerce] zum Experience Platform müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Client-ID | Der Wert von `clientId` aus dem Dienstschlüssel. |
| Client-Geheimnis | Der Wert von `clientSecret` aus dem Dienstschlüssel. |
| Endpunkt | Der Wert von `url` aus dem Dienstschlüssel ist er ähnlich wie `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| Region | Ihr Rechenzentrumsstandort. Die Region ist in der Region `url` und weist einen Wert auf, der `eu10` oder `us10`. Beispiel: `url` is `https://eu10.revenue.cloud.sap/api` benötigen `eu10`. |

## Leitplanken {#guardrails}

API-Anfragen an [!DNL SAP Cloud Management service] unterliegen [Ratenbeschränkungen](https://help.sap.com/docs/btp/sap-business-technology-platform/account-administration-rate-limiting). Bei Überschreitung des Ratenlimits wird ein `HTTP 429 Too Many Requests` Antwortstatus-Code .

## Unterstützte Identitäten {#supported-identities}

[!DNL SAP Commerce] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
| --- | --- | --- |
| `customerNumberSAP` | Eine Kundenkennung des in Ihrer [!DNL SAP Commerce] -Konto. | Obligatorisch |

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt werden alle Zielgruppen beschrieben, die Sie an dieses Ziel exportieren können.

Dieses Ziel unterstützt die Aktivierung aller durch die Experience Platform generierten Zielgruppen über den [Segmentierungsdienst](../../../segmentation/home.md).

Dieses Ziel unterstützt auch die Aktivierung der in der folgenden Tabelle beschriebenen Zielgruppen.

| Zielgruppentyp | Beschreibung |
---------|----------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder einer Zielgruppe zusammen mit den gewünschten Schemafeldern *(z. B. E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Für jede ausgewählte Zielgruppe in Platform wird die entsprechende [!DNL SAP Commerce] wird das zusätzliche Attribut mit dem Zielgruppenstatus von Platform aktualisiert.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | <ul><li>Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Wenn ein Profil auf der Grundlage einer Zielgruppenbewertung im Experience Platform aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Within **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**, suchen Sie nach [!DNL SAP Commerce]. Alternativ können Sie sie unter der **[!UICONTROL eCommerce]** Kategorie.

### Beim Ziel authentifizieren {#authenticate}

Füllen Sie die erforderlichen Felder aus. Siehe Abschnitt [Generieren eines Dienstschlüssels](#prerequisites-service-key) für Hinweise.

| Feld | Beschreibung |
| --- | --- |
| **[!UICONTROL Client ID]** (Client-ID) | Der Wert von `clientId` aus dem Dienstschlüssel. |
| **[!UICONTROL Client-Geheimschlüssel]** | Der Wert von `clientSecret` aus dem Dienstschlüssel. |
| **[!UICONTROL Endpunkt]** | Der Wert von `url` aus dem Dienstschlüssel ist er ähnlich wie `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| **[!UICONTROL Region]** | Ihr Rechenzentrumsstandort. Die Region ist in der Region `url` und weist einen Wert auf, der `eu10` oder `us10`. Beispiel: `url` is `https://eu10.revenue.cloud.sap/api` benötigen `eu10`. |

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Mit Ziel verbinden]**.
![Bild aus der Platform-Benutzeroberfläche, das zeigt, wie eine Authentifizierung für das Ziel durchgeführt werden kann.](../../assets/catalog/ecommerce/sap-commerce/authenticate-destination.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche den Status **[!UICONTROL Verbunden]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
![Bild aus der Platform-Benutzeroberfläche, das die Zieldetails anzeigt, die nach der Authentifizierung ausgefüllt werden sollen.](../../assets/catalog/ecommerce/sap-commerce/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Art des Kunden]**: Wählen Sie entweder ***Individuum*** oder ***Unternehmen*** abhängig von den Entitäten in Ihrer Audience. Die [!DNL SAP Subscription Billing] [schema](https://api.sap.com/api/BusinessPartner_APIs/schema) ändert die Pflichtfelder je nach ausgewählter Option, die der `customerType` -Attribut. Wenn die Auswahl ***Unternehmen***, dann die obligatorischen Zuordnungen wie `firstName` und `lastName` für einen einzelnen Kunden erforderlich sind, werden ignoriert und `company` wird obligatorisch und umgekehrt.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

So senden Sie Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an die [!DNL SAP Commerce] Ziel, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodells (XDM) in Ihrem Platform-Konto und den jeweiligen Entsprechungen vom Ziel zu erstellen. So ordnen Sie Ihre XDM-Felder korrekt der [!DNL SAP Commerce] Gehen Sie wie folgt vor:

#### Ordnen Sie die `customerNumberSAP` identity

Die `customerNumberSAP` identity ist eine obligatorische Zuordnung für dieses Ziel. Gehen Sie wie folgt vor, um sie zuzuordnen:
1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird jetzt eine neue Zuordnungszeile angezeigt.
   ![Screenshot der Platform-Benutzeroberfläche mit hervorgehobener Schaltfläche zum Hinzufügen einer neuen Zuordnung.](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. Im **[!UICONTROL Quellfeld auswählen]** Fenster, wählen Sie die **[!UICONTROL Identitäts-Namespace auswählen]** und wählen `customerNumberSAP`.
   ![Screenshot der Platform-Benutzeroberfläche zur Auswahl von E-Mail als Quellattribut, das als Identität zugeordnet werden soll.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-identity.png)
1. Im **[!UICONTROL Zielgruppenfeld auswählen]** Fenster, wählen Sie die **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie die `customerNumber` Identität.
   ![Screenshot der Platform-Benutzeroberfläche zur Auswahl von E-Mail als Zielattribut, das als Identität zugeordnet werden soll.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-identity.png)

| Quellfeld | Zielfeld | Obligatorisch |
| --- | --- | --- |
| `IdentityMap: customerNumberSAP` | `Identity: customerNumber` | Ja |

Nachfolgend finden Sie ein Beispiel mit der Identitätszuordnung:
![Bild aus der Platform-Benutzeroberfläche, das ein Beispiel für die Zuordnung der customerNumber-Identität zeigt.](../../assets/catalog/ecommerce/sap-commerce/mapping-identities.png)

#### Zuordnen von Attributen

So fügen Sie weitere Attribute hinzu, die Sie zwischen Ihrem XDM-Profilschema und Ihrem [!DNL SAP Subscription Billing] -Konto verwenden, wiederholen Sie die folgenden Schritte:
1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird jetzt eine neue Zuordnungszeile angezeigt.
   ![Screenshot der Platform-Benutzeroberfläche mit hervorgehobener Schaltfläche zum Hinzufügen einer neuen Zuordnung.](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. Im **[!UICONTROL Quellfeld auswählen]** Fenster, wählen Sie die **[!UICONTROL Attribute auswählen]** und wählen Sie das XDM-Attribut aus.
   ![Screenshot der Platform-Benutzeroberfläche zur Auswahl des Nachnamens als Quellattribut.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-attribute.png)
1. Im **[!UICONTROL Zielgruppenfeld auswählen]** auswählen **[!UICONTROL Benutzerdefinierte Attribute auswählen]** und geben Sie den Namen der [!DNL SAP Subscription Billing] -Attribut aus der Kundenliste [schema](https://api.sap.com/api/BusinessPartner_APIs/schema) -Attribute.
   ![Screenshot der Platform-Benutzeroberfläche, in dem lastName als Zielattribut definiert ist.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-attribute.png)

>[!IMPORTANT]
>
> Bei Zielfeldnamen wird zwischen Groß- und Kleinschreibung unterschieden und sollte mit der [!DNL SAP Subscription Billing] Attributnamen. Die einzige Ausnahme dafür ist `country` wo Sie `countryCode` anstatt. [!DNL SAP Subscription Billing] unterstützt Alpha-2 (ISO 3166)-Ländercodes. Beim Wert wird zwischen 0 und 3 Zeichen unterschieden. Stellen Sie daher sicher, dass Sie genau so angeben, wie Sie es definieren, da sonst Fehler auftreten würden: `The country code {} does not exist` oder `size must be between 0 and 3`.

#### Zuordnung `mandatory` Attribute für den ausgewählten Kundentyp

Erforderliche Zuordnungen von Attributen hängen von der **[!UICONTROL Art des Kunden]** die Sie ausgewählt haben. Um die obligatorischen Attribute zuzuordnen, wählen Sie aus den folgenden Optionen aus:

>[!BEGINTABS]

>[!TAB Individueller Kunde]

| Quellfeld | Zielfeld | Obligatorisch |
| --- | --- | --- |
| `xdm: person.lastName` | `Attribute: lastName` | Ja |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | Ja |

>[!TAB Firmenkunden]

| Quellfeld | Zielfeld | Obligatorisch |
| --- | --- | --- |
| `xdm: b2b.companyName` | `Attribute: company` | Ja |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | Ja |

>[!ENDTABS]

#### Zuordnen zusätzlicher Attribute

Sie können dann alle weiteren Zuordnungen zwischen Ihrem XDM-Profilschema und dem [!DNL SAP Subscription Billing] [schema](https://api.sap.com/api/BusinessPartner_APIs/schema) -Attribute für einen Kunden wie unten dargestellt:

>[!BEGINTABS]

>[!TAB Individueller Kunde]

| Quellfeld | Zielfeld | Obligatorisch |
| --- | --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstName` | Nein |
| `xdm: workAddress.street1` | `Attribute: street` | Nein |
| `xdm: workAddress.city` | `Attribute: city` | Nein |

Nachfolgend finden Sie ein Beispiel mit obligatorischen und optionalen Attributzuordnungen, bei denen der Kunde eine Person ist:
![Bild aus der Platform-Benutzeroberfläche, das ein Beispiel mit obligatorischen und optionalen Attributzuordnungen zeigt, bei denen der Kunde ein Kontakt ist.](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-individual.png)

>[!TAB Firmenkunden]

| Quellfeld | Zielfeld | Obligatorisch |
| --- | --- | --- |
| `xdm: workAddress.street1` | `Attribute: street` | Nein |
| `xdm: workAddress.city` | `Attribute: city` | Nein |

Nachfolgend finden Sie ein Beispiel mit obligatorischen und optionalen Attributzuordnungen, bei denen der Kunde ein Unternehmen ist:
![Bild aus der Platform-Benutzeroberfläche mit einem Beispiel mit obligatorischen und optionalen Attributzuordnungen, bei denen der Kunde ein Unternehmen ist.](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-corporate.png)

>[!ENDTABS]

Wenn Sie mit der Bereitstellung der Zuordnungen für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Nächste]**.

### Zielgruppenexport und Beispiel planen {#schedule-segment-export-example}

Bei der Durchführung der [Zielgruppenexport planen](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) Schritt, müssen Sie Platform-Zielgruppen manuell dem [attributes](#prerequisites-attribute) in [!DNL SAP Subscription Billing].

Ein Beispiel für den Schritt Zielgruppenexport planen mit dem Speicherort der [!DNL SAP Commerce] **[!UICONTROL Zuordnungs-ID]** hervorgehoben ist, wird unten gezeigt:
![Bild aus Platform, das den terminierten Zielgruppenexport mit ausgefüllten Zuordnungs-IDs anzeigt.](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export.png)

Wählen Sie dazu jedes Segment aus und geben Sie dann den Namen der benutzerdefinierten Referenz aus [!DNL SAP Subscription Billing] im [!DNL SAP Commerce] **[!UICONTROL Zuordnungs-ID]** Zielverbindungsfeld. Eine Anleitung zum Erstellen benutzerdefinierter Verweise finden Sie im Abschnitt [Erstellen Sie benutzerdefinierte Verweise in [!DNL SAP Subscription Billing]](#prerequisites-custom-reference) Abschnitt.

>[!IMPORTANT]
>
> Verwenden Sie nicht die benutzerdefinierte Referenzbeschriftung als Wert.
>![Bild, das angibt, dass Sie den benutzerdefinierten Referenzbeschriftungswert nicht für die Zuordnung verwenden sollten.](../../assets/catalog/ecommerce/sap-commerce/custom-reference-dont-use-label-for-mapping.png)

Wenn Ihre ausgewählte Experience Platform-Audience beispielsweise `sap_audience1` und Sie möchten, dass sein Status in der Variablen [!DNL SAP Subscription Billing] benutzerspezifischer Verweis `SAP_1`, geben Sie diesen Wert in der [!DNL SAP_Commerce] **[!UICONTROL Zuordnungs-ID]** -Feld.

Beispiel **[!UICONTROL Referenztyp]** von [!DNL SAP Subscription Billing] ist unten dargestellt:
![Bild, das anzeigt, wo eine benutzerdefinierte Referenz in der SAP-Abonnementabrechnung erstellt werden soll.](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

Beispiel für den Schritt Zielgruppenexport planen mit ausgewählter Zielgruppe und der zugehörigen [!DNL SAP Commerce] **[!UICONTROL Zuordnungs-ID]** hervorgehoben ist, wird unten gezeigt:
![Bild aus Platform, das den terminierten Zielgruppenexport mit ausgefüllten Zuordnungs-IDs anzeigt.](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export-example.png)

Wie der Wert im **[!UICONTROL Zuordnungs-ID]** sollte genau mit dem [!DNL SAP Subscription Billing] **[!UICONTROL Referenztyp]** Wert .

Wiederholen Sie diesen Abschnitt für jede aktivierte Platform-Audience.

Basierend auf dem oben gezeigten Bild, in dem Sie zwei Zielgruppen ausgewählt haben, würde das Mapping wie folgt aussehen: | [!DNL SAP Commerce] Zielgruppenname | [!DNL SAP Subscription Billing] **[!UICONTROL Referenztyp]** | [!DNL SAP Commerce] **[!UICONTROL Zuordnungs-ID]** value | | — | — | — | | sap_audience1 | `SAP_1` | `SAP_1` | | SAP Audience2 | `SAP_2` | `SAP_2` |

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

Melden Sie sich bei [!DNL SAP Subscription Billing] -Konto und navigieren Sie dann zum **[!UICONTROL Kontakte]** Seite, um den Audience-Status zu überprüfen. Die Liste kann so konfiguriert werden, dass Spalten für die benutzerdefinierten Verweise angezeigt und die entsprechenden Zielgruppenstatus angezeigt werden.
![Bild der SAP-Abonnement-Abrechnung, auf der die Kundenübersichtsseite mit Spaltenüberschriften angezeigt wird, die den Zielgruppennamen und den Zellenstatus der Zielgruppe anzeigen](../../assets/catalog/ecommerce/sap-commerce/customer-overview.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

Siehe Abschnitt [[!DNL SAP Subscription Billing] Fehlertypen](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/1a6a0dd6129c48e8b235190a1b5409fa.html) Dokumentationsseite mit einer Liste möglicher Fehlertypen und ihren Antwortcodes.

## Zusätzliche Ressourcen {#additional-resources}

Zusätzliche nützliche Informationen aus dem [!DNL SAP] Die Dokumentation finden Sie unten:
* [Integrierte SAP-Abonnement-Abrechnung](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/e4b8badf7d124026991e4ab6b57d2a33.html)

### Änderungsprotokoll

In diesem Abschnitt werden aktualisierte Funktionen und wesentliche Dokumentationsänderungen für diesen Ziel-Connector erfasst.

+++ Änderungsprotokoll anzeigen

| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| Januar 2024 | Erstmalige Veröffentlichung | Erste Zielversion und Veröffentlichung der Dokumentation. |

{style="table-layout:auto"}

+++