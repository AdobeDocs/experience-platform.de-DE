---
title: SAP Commerce-Verbindung
description: Verwenden Sie den SAP Commerce Destination Connector, um Kundendatensätze in Ihrem SAP-Konto zu aktualisieren.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 3bd1a2a7-fb56-472d-b9bd-603b94a8937e
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '2246'
ht-degree: 26%

---

# [!DNL SAP Commerce]-Verbindung

[!DNL SAP Commerce], früher als [[!DNL Hybris]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html) bezeichnet, ist eine Cloud-basierte E-Commerce-Plattform-Lösung für B2B- und B2C-Unternehmen und als Teil des SAP Customer Experience-Portfolios verfügbar. [[!DNL SAP] Abonnement-Abrechnung](https://www.sap.com/products/financial-management/subscription-billing.html) ist ein Produkt im Portfolio und ermöglicht ein vollständiges Abonnementlebenszyklusmanagement mit vereinfachten Verkaufs- und Zahlungserlebnissen durch standardisierte Integrationen.

Dieses [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) verwendet die [[!DNL SAP Subscription Billing] Kunden-Management-API](https://api.sap.com/api/BusinessPartner_APIs/path/PUT_customers-customerNumber), um Ihre Kundendetails innerhalb von [!DNL SAP Commerce] von einer bestehenden Experience Platform-Audience nach der Aktivierung zu aktualisieren.

Anweisungen zur Authentifizierung bei Ihrer [!DNL SAP Commerce]-Instanz sehen Sie weiter unten im Abschnitt [Authentifizieren bei Ziel](#authenticate).

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL SAP Commerce]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

[!DNL SAP Commerce] -Kunden speichern Informationen über Einzelpersonen oder Organisationseinheiten, die mit Ihrem Unternehmen interagieren. Ihr Team verwendet die in [!DNL SAP Commerce] vorhandenen Kunden, um die Experience Platform-Zielgruppen zu erstellen. Nachdem diese Zielgruppen an [!DNL SAP Commerce] gesendet wurden, werden ihre Informationen aktualisiert und jedem Kunden wird eine Eigenschaft mit dem Wert als Zielgruppenname zugewiesen, der angibt, zu welcher Zielgruppe der Kunde gehört.

## Voraussetzungen {#prerequisites}

In den folgenden Abschnitten finden Sie alle Voraussetzungen, die Sie unter Experience Platform und [!DNL SAP Commerce] einrichten müssen, sowie Informationen, die Sie vor der Arbeit mit dem [!DNL SAP Commerce]-Ziel erfassen müssen.

### Voraussetzungen für Experience Platform {#prerequisites-in-experience-platform}

Bevor Sie Daten für das Ziel [!DNL SAP Commerce] aktivieren, müssen Sie über ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) und [Zielgruppen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) verfügen, die in [!DNL Experience Platform] erstellt wurden.

Informationen zum Zielgruppenstatus finden Sie in der Experience Platform-Dokumentation für die Schemakonferenz [Zielgruppenzugehörigkeitsdetails](/help/xdm/field-groups/profile/segmentation.md) .

### Voraussetzungen für das [!DNL SAP Commerce]-Ziel {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen, um Daten von Platform in Ihr [!DNL SAP Commerce] -Konto zu exportieren:

#### Sie müssen über ein [!DNL SAP Subscription Billing] -Konto verfügen. {#prerequisites-account}

Um Daten von Platform in Ihr [!DNL SAP Commerce] -Konto zu exportieren, benötigen Sie ein [!DNL SAP Subscription Billing] -Konto. Wenn Sie kein gültiges Abrechnungskonto haben, wenden Sie sich an Ihren [!DNL SAP] -Kundenbetreuer. Weitere Informationen finden Sie im Dokument [[!DNL SAP] Plattformkonfiguration](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) .

#### Generieren eines Dienstschlüssels {#prerequisites-service-key}

* Mit dem Dienstschlüssel [!DNL SAP Commerce] können Sie über Experience Platform auf die [!DNL SAP Subscription Billing] -API zugreifen. Informationen zum Erstellen eines Dienstschlüssels finden Sie unter [!DNL SAP Commerce] [Erstellen eines Dienstschlüssels mit Client-ID und Client-Geheimnis](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/87c11a0f5dc3494eaf3baa355925c030.html#create-a-service-key-with-client-id-and-client-secret) . [!DNL SAP Commerce] erfordert Folgendes:
   * Client-ID
   * Client-Geheimnis
   * URL. Das URL-Muster lautet wie folgt: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Dieser Wert wird später verwendet, um Werte für `Region` und `Endpoint` zu erhalten.

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

#### Erstellen benutzerdefinierter Verweise in [!DNL SAP Subscription Billing] {#prerequisites-custom-reference}

Um den Experience Platform-Zielgruppenstatus in [!DNL SAP Subscription Billing] zu aktualisieren, benötigen Sie ein benutzerdefiniertes Referenzfeld für jede in Platform ausgewählte Zielgruppe.

Um die benutzerdefinierten Verweise zu erstellen, melden Sie sich bei Ihrem [!DNL SAP Subscription Billing] -Konto an und navigieren Sie zur Seite **[Master Data and Configuration]** > **[Custom References]** . Wählen Sie als Nächstes **[!UICONTROL Erstellen]** aus, um eine neue Referenz für jede in Platform ausgewählte Zielgruppe hinzuzufügen. Sie benötigen diese Referenzfeldnamen im nachfolgenden Schritt [Zielgruppenexport planen und Beispiel](#schedule-segment-export-example) .

Nachfolgend finden Sie ein Beispiel für die Erstellung eines benutzerdefinierten **[!UICONTROL Verweistyps]** in [!DNL SAP Subscription Billing]:
![Bild, das anzeigt, wo eine benutzerdefinierte Referenz in der SAP-Abonnementabrechnung erstellt werden soll.](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

Weitere Hinweise finden Sie in der Dokumentation zu [!DNL SAP Subscription Billing] [benutzerdefinierten Verweisen](https://help.sap.com/docs/CLOUD_TO_CASH_OD/80d121f216af43648e79664efe5595f7/85696a63c8d8453a934e86c9413a25cf.html?version=2023-11-27) .

### Sammeln erforderlicher Anmeldeinformationen {#gather-credentials}

Um [!DNL SAP Commerce] mit Experience Platform zu verbinden, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Client-ID | Der Wert von `clientId` aus dem Dienstschlüssel. |
| Client-Geheimnis | Der Wert von `clientSecret` aus dem Dienstschlüssel. |
| Endpunkt | Der Wert von `url` aus dem Dienstschlüssel ist ähnlich wie `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| Region | Ihr Rechenzentrumsstandort. Der Bereich ist im `url` vorhanden und hat einen Wert ähnlich dem Wert `eu10` oder `us10`. Wenn der `url` beispielsweise `https://eu10.revenue.cloud.sap/api` ist, benötigen Sie `eu10`. |

## Leitplanken {#guardrails}

API-Anfragen an die [!DNL SAP Cloud Management service] unterliegen den [Ratenbeschränkungen](https://help.sap.com/docs/btp/sap-business-technology-platform/account-administration-rate-limiting). Wenn das Ratenlimit überschritten wird, wird ein Antwort-Status-Code `HTTP 429 Too Many Requests` ausgegeben.

## Unterstützte Identitäten {#supported-identities}

[!DNL SAP Commerce] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
| --- | --- | --- |
| `customerNumberSAP` | Eine Kundenkennung des Kunden oder Unternehmens-Kunden, der bereits in Ihrem [!DNL SAP Commerce]-Konto vorhanden ist. | Obligatorisch |

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt werden alle Zielgruppen beschrieben, die Sie an dieses Ziel exportieren können.

Dieses Ziel unterstützt die Aktivierung aller durch die Experience Platform generierten Zielgruppen über den [Segmentierungsdienst](../../../segmentation/home.md).

Dieses Ziel unterstützt auch die Aktivierung der in der folgenden Tabelle beschriebenen Zielgruppen.

| Zielgruppentyp | Unterstützt | Beschreibung |
| ------------- | --------- | ----------- |
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die durch den Experience Platform [Segmentierungsdienst](../../../segmentation/home.md) generiert wurden. |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder einer Zielgruppe zusammen mit den gewünschten Schemafeldern *(z. B. E-Mail-Adresse, Telefonnummer, Nachname)* gemäß Ihrer Feldzuordnung.</li><li> Für jede ausgewählte Zielgruppe in Platform wird das entsprechende zusätzliche Attribut [!DNL SAP Commerce] mit dem Zielgruppenstatus von Platform aktualisiert.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | <ul><li>Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Wenn ein Profil auf der Grundlage einer Zielgruppenbewertung im Experience Platform aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** nach [!DNL SAP Commerce]. Alternativ können Sie sie unter der Kategorie **[!UICONTROL eCommerce]** finden.

### Beim Ziel authentifizieren {#authenticate}

Füllen Sie die erforderlichen Felder aus. Eine Anleitung dazu finden Sie im Abschnitt [Einen Dienstschlüssel erstellen](#prerequisites-service-key) .

| Feld | Beschreibung |
| --- | --- |
| **[!UICONTROL Client-ID]** | Der Wert von `clientId` aus dem Dienstschlüssel. |
| **[!UICONTROL Client-Geheimnis]** | Der Wert von `clientSecret` aus dem Dienstschlüssel. |
| **[!UICONTROL Endpunkt]** | Der Wert von `url` aus dem Dienstschlüssel ist ähnlich wie `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| **[!UICONTROL Region]** | Ihr Rechenzentrumsstandort. Der Bereich ist im `url` vorhanden und hat einen Wert ähnlich dem Wert `eu10` oder `us10`. Wenn der `url` beispielsweise `https://eu10.revenue.cloud.sap/api` ist, benötigen Sie `eu10`. |

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Mit Ziel verbinden]**.
![Bild aus der Platform-Benutzeroberfläche, das die Authentifizierung für das Ziel anzeigt.](../../assets/catalog/ecommerce/sap-commerce/authenticate-destination.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche den Status **[!UICONTROL Verbunden]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
![Bild aus der Platform-Benutzeroberfläche, das die Zieldetails anzeigt, die nach der Authentifizierung ausgefüllt werden sollen.](../../assets/catalog/ecommerce/sap-commerce/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Typ des Kunden]**: Wählen Sie je nach den Entitäten in Ihrer Audience entweder ***Individuell*** oder ***Unternehmen*** aus. Das [!DNL SAP Subscription Billing] [schema](https://api.sap.com/api/BusinessPartner_APIs/schema) schaltet die erforderlichen Felder abhängig von dieser Auswahl um, die dem Attribut `customerType` zugeordnet ist. Wenn die Auswahl ***Unternehmen*** ist, werden die obligatorischen Zuordnungen wie `firstName` und `lastName` ignoriert, die für einen einzelnen Kunden erforderlich sind, und `company` wird obligatorisch und umgekehrt.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Um Ihre Zielgruppendaten korrekt von Adobe Experience Platform an das Ziel [!DNL SAP Commerce] zu senden, müssen Sie den Schritt für die Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodells (XDM) in Ihrem Platform-Konto und den jeweiligen Entsprechungen vom Ziel zu erstellen. Gehen Sie wie folgt vor, um Ihre XDM-Felder korrekt den [!DNL SAP Commerce] -Zielfeldern zuzuordnen:

#### `customerNumberSAP`-Identität zuordnen

Die `customerNumberSAP` -Identität ist eine obligatorische Zuordnung für dieses Ziel. Gehen Sie wie folgt vor, um sie zuzuordnen:
1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird jetzt eine neue Zuordnungszeile angezeigt.
   ![Screenshot der Platform-Benutzeroberfläche mit hervorgehobener Schaltfläche zum Hinzufügen einer neuen Zuordnung.](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. Wählen Sie im Fenster **[!UICONTROL Quellfeld auswählen]** den Namen **[!UICONTROL Identitäts-Namespace auswählen]** und danach `customerNumberSAP` aus.
   ![Screenshot der Platform-Benutzeroberfläche, in dem E-Mail als Quellattribut ausgewählt wird, das als Identität zugeordnet werden soll.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-identity.png)
1. Wählen Sie im Fenster **[!UICONTROL Zielfeld auswählen]** den Namen **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie die Identität `customerNumber` aus.
   ![Screenshot der Platform-Benutzeroberfläche, in dem E-Mail als Zielattribut ausgewählt wird, das als Identität zugeordnet werden soll.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-identity.png)

| Quellfeld | Zielfeld | Obligatorisch |
| --- | --- | --- |
| `IdentityMap: customerNumberSAP` | `Identity: customerNumber` | Ja |

Nachfolgend finden Sie ein Beispiel mit der Identitätszuordnung:
![Bild aus der Platform-Benutzeroberfläche, das ein Beispiel für die Zuordnung der customerNumber-Identität zeigt.](../../assets/catalog/ecommerce/sap-commerce/mapping-identities.png)

#### Zuordnen von Attributen

Um weitere Attribute hinzuzufügen, die Sie zwischen Ihrem XDM-Profilschema und Ihrem [!DNL SAP Subscription Billing]-Konto aktualisieren möchten, wiederholen Sie die folgenden Schritte:
1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird jetzt eine neue Zuordnungszeile angezeigt.
   ![Screenshot der Platform-Benutzeroberfläche mit hervorgehobener Schaltfläche zum Hinzufügen einer neuen Zuordnung.](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. Wählen Sie im Fenster **[!UICONTROL Quellfeld auswählen]** die Kategorie **[!UICONTROL Attribute auswählen]** und danach das XDM-Attribut aus.
   ![Screenshot der Platform-Benutzeroberfläche, in dem Nachname als Quellattribut ausgewählt wird.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-attribute.png)
1. Wählen Sie im Fenster **[!UICONTROL Zielfeld auswählen]** die Kategorie **[!UICONTROL Benutzerdefinierte Attribute auswählen]** und geben Sie den Namen des Attributs [!DNL SAP Subscription Billing] aus der Liste der Kundenattribute [schema](https://api.sap.com/api/BusinessPartner_APIs/schema) ein.
   ![Screenshot der Platform-Benutzeroberfläche, in dem lastName als Zielattribut definiert ist.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-attribute.png)

>[!IMPORTANT]
>
> Bei Zielfeldnamen wird zwischen Groß- und Kleinschreibung unterschieden und sollte mit den Attributnamen [!DNL SAP Subscription Billing] übereinstimmen. Die einzige Ausnahme dafür ist `country`, wo Sie stattdessen `countryCode` verwenden sollten. [!DNL SAP Subscription Billing] unterstützt Alpha-2 (ISO 3166)-Ländercodes. Beim Wert wird zwischen 0 und 3 Zeichen unterschieden. Stellen Sie daher sicher, dass Sie genau so angeben, wie Sie es definieren, da sonst Fehler auftreten würden: `The country code {} does not exist` oder `size must be between 0 and 3`.

#### `mandatory` Attribute für den ausgewählten Kundentyp zuordnen

Erforderliche Zuordnungen von Attributen hängen vom ausgewählten **[!UICONTROL Typ des Kunden]** ab. Um die obligatorischen Attribute zuzuordnen, wählen Sie aus den folgenden Optionen aus:

>[!BEGINTABS]

>[!TAB Individueller Kunde]

| Quellfeld | Zielfeld | Obligatorisch |
| --- | --- | --- |
| `xdm: person.lastName` | `Attribute: lastName` | Ja |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | Ja |

>[!TAB Firmenkunde]

| Quellfeld | Zielfeld | Obligatorisch |
| --- | --- | --- |
| `xdm: b2b.companyName` | `Attribute: company` | Ja |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | Ja |

>[!ENDTABS]

#### Zuordnen zusätzlicher Attribute

Sie können dann alle weiteren Zuordnungen zwischen Ihrem XDM-Profilschema und den [!DNL SAP Subscription Billing] [schema](https://api.sap.com/api/BusinessPartner_APIs/schema) -Attributen für einen Kunden hinzufügen, wie unten dargestellt:

>[!BEGINTABS]

>[!TAB Individueller Kunde]

| Quellfeld | Zielfeld | Obligatorisch |
| --- | --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstName` | Nein |
| `xdm: workAddress.street1` | `Attribute: street` | Nein |
| `xdm: workAddress.city` | `Attribute: city` | Nein |

Nachfolgend finden Sie ein Beispiel mit obligatorischen und optionalen Attributzuordnungen, bei denen der Kunde eine Person ist:
![Bild aus der Platform-Benutzeroberfläche, das ein Beispiel mit obligatorischen und optionalen Attributzuordnungen zeigt, bei denen der Kunde ein Kontakt ist.](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-individual.png)

>[!TAB Firmenkunde]

| Quellfeld | Zielfeld | Obligatorisch |
| --- | --- | --- |
| `xdm: workAddress.street1` | `Attribute: street` | Nein |
| `xdm: workAddress.city` | `Attribute: city` | Nein |

Nachfolgend finden Sie ein Beispiel mit obligatorischen und optionalen Attributzuordnungen, bei denen der Kunde ein Unternehmen ist:
![Bild aus der Platform-Benutzeroberfläche, das ein Beispiel mit obligatorischen und optionalen Attributzuordnungen zeigt, bei denen der Kunde ein Unternehmen ist.](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-corporate.png)

>[!ENDTABS]

Wenn Sie die Zuordnungen für Ihre Zielverbindung bereitgestellt haben, wählen Sie **[!UICONTROL Weiter]** aus.

### Zielgruppenexport und Beispiel planen {#schedule-segment-export-example}

Beim Ausführen des Schritts [Zielgruppenexport planen](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) müssen Sie Platform-Zielgruppen den [Attributen](#prerequisites-attribute) in [!DNL SAP Subscription Billing] manuell zuordnen.

Ein Beispiel für den Schritt Zielgruppenexport planen , bei dem der Speicherort der [!DNL SAP Commerce] **[!UICONTROL Zuordnungs-ID]** hervorgehoben ist, ist unten dargestellt:
![Bild aus Platform, das den geplanten Zielgruppenexport mit ausgefüllten Zuordnungs-IDs anzeigt.](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export.png)

Wählen Sie dazu jedes Segment aus und geben Sie dann den Namen des benutzerdefinierten Verweises aus [!DNL SAP Subscription Billing] in das Feld [!DNL SAP Commerce] **[!UICONTROL Zuordnungs-ID]** Ziel-Connector ein. Eine Anleitung zum Erstellen benutzerdefinierter Verweise finden Sie im Abschnitt [Erstellen benutzerdefinierter Verweise in  [!DNL SAP Subscription Billing]](#prerequisites-custom-reference) .

>[!IMPORTANT]
>
> Verwenden Sie nicht die benutzerdefinierte Referenzbeschriftung als Wert.
>![Bild, das angibt, dass Sie den benutzerdefinierten Referenzbeschriftungswert nicht für die Zuordnung verwenden sollten.](../../assets/catalog/ecommerce/sap-commerce/custom-reference-dont-use-label-for-mapping.png)

Wenn Ihre ausgewählte Experience Platform-Audience beispielsweise &quot;`sap_audience1`&quot;lautet und ihr Status in den benutzerdefinierten Verweis [!DNL SAP Subscription Billing] `SAP_1` aktualisiert werden soll, geben Sie diesen Wert im Feld [!DNL SAP_Commerce] **[!UICONTROL Zuordnungs-ID]** an.

Nachfolgend finden Sie ein Beispiel für den **[!UICONTROL Referenztyp]** von [!DNL SAP Subscription Billing]:
![Bild, das anzeigt, wo eine benutzerdefinierte Referenz in der SAP-Abonnementabrechnung erstellt werden soll.](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

Nachfolgend finden Sie ein Beispiel für den Schritt Zielgruppenexport planen , bei dem eine Zielgruppe ausgewählt und die zugehörige [!DNL SAP Commerce] **[!UICONTROL Zuordnungs-ID]** hervorgehoben ist:
![Bild aus Platform, das den geplanten Zielgruppenexport mit ausgefüllten Zuordnungs-IDs anzeigt.](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export-example.png)

Wie gezeigt, sollte der Wert im Feld **[!UICONTROL Zuordnungs-ID]** genau mit dem Wert [!DNL SAP Subscription Billing] **[!UICONTROL Referenztyp]** übereinstimmen.

Wiederholen Sie diesen Abschnitt für jede aktivierte Platform-Audience.

Basierend auf dem oben gezeigten Bild, in dem Sie zwei Zielgruppen ausgewählt haben, würde das Mapping wie folgt aussehen:
| [!DNL SAP Commerce] Zielgruppenname | [!DNL SAP Subscription Billing] **[!UICONTROL Referenztyp]** | [!DNL SAP Commerce] **[!UICONTROL ID-Wert]** zuordnen |
| — | — | — |
| sap_audience1 | `SAP_1` | `SAP_1` |
| SAP Audience2 | `SAP_2` | `SAP_2` |

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

Melden Sie sich beim Konto [!DNL SAP Subscription Billing] an und navigieren Sie dann zur Seite **[!UICONTROL Kontakte]** , um den Zielgruppenstatus zu überprüfen. Die Liste kann so konfiguriert werden, dass Spalten für die benutzerdefinierten Verweise angezeigt und die entsprechenden Zielgruppenstatus angezeigt werden.
![Bild der SAP-Abonnement-Abrechnung mit einer Kundenübersichtsseite mit Spaltenüberschriften, die den Zielgruppennamen und den Zellenstatus der Zielgruppe anzeigen](../../assets/catalog/ecommerce/sap-commerce/customer-overview.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

Eine Liste der möglichen Fehlertypen und ihrer Antwortcodes finden Sie auf der Dokumentationsseite [[!DNL SAP Subscription Billing] Fehlertypen](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/1a6a0dd6129c48e8b235190a1b5409fa.html) .

## Zusätzliche Ressourcen {#additional-resources}

Weitere nützliche Informationen aus der [!DNL SAP] -Dokumentation finden Sie unten:
* [SAP-Abonnementabrechnung an Bord](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/e4b8badf7d124026991e4ab6b57d2a33.html)

### Änderungsprotokoll

In diesem Abschnitt werden aktualisierte Funktionen und wesentliche Dokumentationsänderungen für diesen Ziel-Connector erfasst.

+++ Änderungsprotokoll anzeigen

| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| Januar 2024 | Erstmalige Veröffentlichung | Erste Zielversion und Veröffentlichung der Dokumentation. |

{style="table-layout:auto"}

+++
