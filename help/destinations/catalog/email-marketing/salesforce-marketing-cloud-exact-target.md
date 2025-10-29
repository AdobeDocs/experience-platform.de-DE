---
title: (API) Salesforce Marketing Cloud-Verbindung
description: Mit dem Ziel Salesforce Marketing Cloud (ehemals ExactTarget) können Sie Ihre Kontodaten exportieren und in Salesforce Marketing Cloud für Ihre Geschäftsanforderungen aktivieren.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '2823'
ht-degree: 18%

---

# [!DNL (API) Salesforce Marketing Cloud]-Verbindung

## Übersicht {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/engagement/) (früher als [!DNL ExactTarget] bezeichnet) ist eine Digital Marketing-Suite, mit der Sie Journey erstellen und anpassen können, damit Besuchende und Kunden ihr Erlebnis personalisieren können.

>[!IMPORTANT]
>
> Beachten Sie den Unterschied zwischen dieser Verbindung und der anderen [[!DNL Salesforce Marketing Cloud] Verbindung](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) die im Abschnitt E-Mail-Marketing-Katalog vorhanden ist. Die andere Salesforce Marketing Cloud-Verbindung ermöglicht den Export von Dateien an einen bestimmten Speicherort, während es sich hierbei um eine API-basierte Streaming-Verbindung handelt.

Im Vergleich zu [!DNL Salesforce Marketing Cloud Account Engagement], das stärker auf **B2B**-Marketing ausgerichtet ist, ist das [!DNL (API) Salesforce Marketing Cloud]-Ziel ideal für **B2C**-Anwendungsfälle mit kürzeren Entscheidungszyklen bei Transaktionen. Sie können größere Datensätze konsolidieren, die das Verhalten Ihrer Zielgruppe widerspiegeln, um Marketing-Kampagnen anzupassen und zu verbessern, indem Sie Kontakte priorisieren und segmentieren, insbesondere aus Datensätzen außerhalb von [!DNL Salesforce]. *Beachten Sie, dass Experience Platform auch über eine Verbindung für die [[!DNL Salesforce Marketing Cloud Account Engagement]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) verfügt.*

Dieses [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) verwendet die [!DNL Salesforce Marketing Cloud] [Kontakte aktualisieren](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html)-API, mit der Sie **Kontakte hinzufügen und Kontaktdaten aktualisieren** für Ihre Geschäftsanforderungen können, nachdem Sie sie in einem neuen [!DNL Salesforce Marketing Cloud]-Segment aktiviert haben.

[!DNL Salesforce Marketing Cloud] verwendet OAuth 2 mit Client-Anmeldeinformationen als Authentifizierungsmechanismus für die Kommunikation mit der [!DNL Salesforce Marketing Cloud]-API. Anweisungen zur Authentifizierung bei Ihrer [!DNL Salesforce Marketing Cloud]-Instanz sehen Sie weiter unten im Abschnitt [Authentifizieren bei Ziel](#authenticate).

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL (API) Salesforce Marketing Cloud]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

### Senden von E-Mails an Kontakte für Marketing-Kampagnen {#use-case-send-emails}

Die Verkaufsabteilung einer Wohnungsvermietungsplattform möchte eine Marketing-E-Mail an eine Zielgruppe senden. Das Marketing-Team der Plattform kann über Adobe Experience Platform neue Kontakte hinzufügen/bestehende *(und ihre E-Mail-Adressen)*, Zielgruppen aus eigenen Offline-Daten erstellen und diese Zielgruppen an [!DNL Salesforce Marketing Cloud] senden, die dann zum Senden der E-Mail-Adresse der Marketing-Kampagne verwendet werden können.

## Voraussetzungen {#prerequisites}

### Voraussetzungen in Experience Platform {#prerequisites-in-experience-platform}

Vor der Aktivierung der Daten für das [!DNL (API) Salesforce Marketing Cloud]-Ziel müssen Sie über ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) verfügen, die in [!DNL Experience Platform] erstellt wurden.

### Voraussetzungen in [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen, um Daten aus Experience Platform in Ihr [!DNL Salesforce Marketing Cloud]-Konto zu exportieren:

#### Sie benötigen ein [!DNL Salesforce Marketing Cloud]-Konto {#prerequisites-account}

Ein [!DNL Salesforce Marketing Cloud] mit einem Abonnement für das [[!DNL Marketing Cloud Engagement]](https://www.salesforce.com/products/marketing-cloud/engagement/) Produkt ist erforderlich, um fortzufahren.

Wenden Sie sich an [[!DNL Salesforce] Support](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10), wenn Sie kein [!DNL Salesforce Marketing Cloud] haben oder Ihrem Konto das [!DNL Marketing Cloud Engagement] Produktabonnement fehlt.

#### Erstellen von Attributen in [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

Beim Aktivieren von Zielgruppen für das [!DNL (API) Salesforce Marketing Cloud]-Ziel müssen Sie im Schritt **[!UICONTROL Mapping ID]** Zielgruppen-Zeitplan“ für jede aktivierte Zielgruppe einen Wert in **[Feld](#schedule-segment-export-example)** eingeben.

[!DNL Salesforce] erfordert diesen Wert, um Zielgruppen aus Experience Platform korrekt zu lesen und zu interpretieren und ihren Zielgruppenstatus in [!DNL Salesforce Marketing Cloud] zu aktualisieren. Weitere Informationen finden Sie in der Experience Platform[Dokumentation für die Schemafeldgruppe „Details zur Zielgruppenzugehörigkeit](/help/xdm/field-groups/profile/segmentation.md) , wenn Sie Anleitungen zu Zielgruppenstatus benötigen.

Für jede Zielgruppe, die Sie von Experience Platform für [!DNL Salesforce] aktivieren, muss ein Attribut des Typs `Text` mit der [!DNL Email Demographics] in [!DNL Salesforce Marketing Cloud] verknüpft sein. Verwenden Sie die [!DNL Salesforce Marketing Cloud]-[!DNL Contact Builder], um Attribute zu erstellen. Weitere Informationen zum Erstellen von Attributen finden [!DNL Salesforce Marketing Cloud] in der [-](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&type=5&language=en_US) unter „Attribute erstellen“.

Die Attributfeldnamen werden für das [!DNL (API) Salesforce Marketing Cloud] Zielfeld während des **[!UICONTROL Mapping]** verwendet. Sie können das Feldzeichen entsprechend Ihren Geschäftsanforderungen mit maximal 4.000 Zeichen definieren. Weitere Informationen zu Attributtypen finden [!DNL Salesforce Marketing Cloud] auf der Dokumentationsseite [Datenerweiterungen](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&type=5) .

Nachfolgend finden Sie ein Beispiel für den Bildschirm „Daten-Designer“ in [!DNL Salesforce Marketing Cloud], dem Sie das Attribut hinzufügen:
![Daten-Designer der Salesforce Marketing Cloud-Benutzeroberfläche.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

Nachfolgend finden Sie eine Ansicht einer [!DNL Salesforce Marketing Cloud] [!DNL Email Data] Attributgruppe mit Attributen, die dem Zielgruppenstatus in der [!DNL Email Demographics] entsprechen:
![E-Mail-Datenattributgruppe der Salesforce Marketing Cloud-Benutzeroberfläche.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demographics-fields.png)

Das [!DNL (API) Salesforce Marketing Cloud]-Ziel verwendet die [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html), um die in [!DNL Salesforce Marketing Cloud] definierten Datenerweiterungen und deren verknüpfte Attribute dynamisch abzurufen.

Diese werden im **[!UICONTROL Target field]** angezeigt, wenn Sie im Workflow [Zuordnung](#mapping-considerations-example) einrichten, um Zielgruppen für [&#x200B; Ziel zu aktivieren](#activate).

>[!IMPORTANT]
>
> In [!DNL Salesforce Marketing Cloud] müssen Sie Attribute mit einem **[!UICONTROL FIELD NAME]** erstellen, der genau mit dem in **[!UICONTROL Mapping ID]** für jedes aktivierte Experience Platform-Segment angegebenen Wert übereinstimmt. Der folgende Screenshot zeigt beispielsweise ein Attribut mit dem Namen `salesforce_mc_segment_1`. Fügen Sie beim Aktivieren einer Zielgruppe für dieses Ziel `salesforce_mc_segment_1` als **[!UICONTROL Mapping ID]** hinzu, um Zielgruppen aus Experience Platform in dieses Attribut einzufügen.

Ein Beispiel für die Erstellung von Attributen in [!DNL Salesforce Marketing Cloud] finden Sie unten:
![Screenshot der Salesforce Marketing Cloud-Benutzeroberfläche mit einem Attribut.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
> * Fügen Sie beim Erstellen des Attributs keine Leerzeichen in den Feldnamen ein. Verwenden Sie stattdessen den Unterstrich `(_)` als Trennzeichen.
> * Um zwischen Attributen zu unterscheiden, die für Experience Platform-Zielgruppen verwendet werden, und anderen Attributen in [!DNL Salesforce Marketing Cloud] zu unterscheiden, können Sie ein erkennbares Präfix oder Suffix für die Attribute einfügen, die für Adobe-Segmente verwendet werden. Verwenden Sie beispielsweise anstelle von `test_segment` `Adobe_test_segment` oder `test_segment_Adobe`.
> * Wenn Sie bereits andere Attribute in [!DNL Salesforce Marketing Cloud] erstellt haben, können Sie denselben Namen wie das Experience Platform-Segment verwenden, um die Zielgruppe in [!DNL Salesforce Marketing Cloud] einfach zu identifizieren.

#### Zuweisen von Benutzerrollen und Berechtigungen in [!DNL Salesforce Marketing Cloud] {#prerequisites-roles-permissions}

Da [!DNL Salesforce Marketing Cloud] benutzerdefinierte Rollen je nach Anwendungsfall unterstützt, sollten Ihrem Benutzer die entsprechenden Rollen zugewiesen werden, um Ihre Attribute in [!DNL Salesforce Marketing Cloud] zu aktualisieren. Ein Beispiel für einem Benutzer zugewiesene Rollen finden Sie unten:
![Salesforce Marketing Cloud-Benutzeroberfläche für einen ausgewählten Benutzer, die die ihm zugewiesenen Rollen anzeigt.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-edit-roles.png)

Je nachdem, welche Rollen Ihrem [!DNL Salesforce Marketing Cloud] Benutzer zugewiesen wurden, müssen Sie auch der [!DNL Salesforce Marketing Cloud]-Datenerweiterung Berechtigungen zuweisen, die mit den Feldern verknüpft sind, die Sie aktualisieren möchten.

Da dieses Ziel Zugriff auf die `[!DNL data extension]` erfordert, müssen Sie es zulassen. Für die `Email` [!DNL data extension] müssen Sie beispielsweise Folgendes zulassen:

![Benutzeroberfläche von Salesforce Marketing Cloud, die die E-Mail-Datenerweiterung mit zulässigen Berechtigungen anzeigt.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-permisions-list.png)

Um die Zugriffsebene einzuschränken, können Sie auch den individuellen Zugriff mithilfe von granularen Berechtigungen überschreiben.
![Benutzeroberfläche von Salesforce Marketing Cloud, die die E-Mail-Datenerweiterung mit granularen Berechtigungen anzeigt.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/sales-email-attribute-set-permission.png)

Ausführliche Anleitungen finden Sie auf den Seiten [[!DNL Marketing Cloud Roles]](https://help.salesforce.com/s/articleView?language=en_US&id=sf.mc_overview_marketing_cloud_roles.htm&type=5) und [[!DNL Marketing Cloud Roles and Permissions]](https://help.salesforce.com/s/articleView?language=en_US&id=sf.mc_overview_roles.htm&type=5) .

#### Sammeln von [!DNL Salesforce Marketing Cloud]-Anmeldedaten {#gather-credentials}

Beachten Sie die folgenden Punkte, bevor Sie sich beim [!DNL (API) Salesforce Marketing Cloud]-Ziel authentifizieren.

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Subdomain | Siehe [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html), um zu erfahren, wie Sie diesen Wert aus der [!DNL Salesforce Marketing Cloud]-Schnittstelle erhalten. | Wenn Ihre [!DNL Salesforce Marketing Cloud] Domain ist<br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.*, <br>Sie müssen `mcq4jrssqdlyc4lph19nnqgzzs84` als Wert angeben. |
| Client-ID | In der [!DNL Salesforce Marketing Cloud] [Dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) erfahren Sie, wie Sie diesen Wert aus der [!DNL Salesforce Marketing Cloud] abrufen. | R23KXXXXXXXX0Z05XXXXXX |
| Client-Geheimnis | In der [!DNL Salesforce Marketing Cloud] [Dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) erfahren Sie, wie Sie diesen Wert aus der [!DNL Salesforce Marketing Cloud] abrufen. | ipxxxxxxxxxxT4xxxxxxxxxxxx |

{style="table-layout:auto"}

### Leitlinien {#guardrails}

* Salesforce setzt bestimmte [Sätze](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * Informationen zu möglichen Beschränkungen[!DNL Salesforce Marketing Cloud] auf die Sie stoßen könnten[&#x200B; und &#x200B;](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) Sie Fehler bei der Ausführung verringern, finden Sie in der Dokumentation.
   * Konsultieren Sie die Seite [[!DNL Salesforce Marketing Cloud] Interaktionspreise](https://www.salesforce.com/editions-pricing/marketing-cloud/email/), um die *Vergleichstabelle für die vollständige Ausgabe herunterzuladen* als PDF, die die von Ihrem Plan auferlegten Beschränkungen detailliert beschreibt.
   * Auf der [API-Übersicht](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) finden Sie zusätzliche Beschränkungen.
   * Siehe [hier](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) für eine Seite, die diese Details sortiert.
* Die Anzahl der *benutzerdefinierten Felder, die pro Objekt zulässig sind* variiert je nach Salesforce Edition.
   * Weitere Anleitungen finden Sie in der [!DNL Salesforce] [Dokumentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&type=5) .
   * Wenn Sie das für (benutzerdefinierte Felder pro *) definierte Limit innerhalb* [!DNL Salesforce Marketing Cloud] erreicht haben, müssen Sie Folgendes tun
      * Entfernen Sie ältere Attribute, bevor Sie neue Attribute in [!DNL Salesforce Marketing Cloud] hinzufügen.
      * Aktualisieren oder entfernen Sie alle aktivierten Zielgruppen in Experience Platform-Zielen, die diese älteren Attributnamen als den Wert verwenden, der während des Schritts „Zielgruppen **[!UICONTROL Mapping ID]** Planung für [&#x200B; bereitgestellt &#x200B;](#schedule-segment-export-example).

## Unterstützte Identitäten {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud]-Kontaktschlüssel. Siehe die [!DNL Salesforce Marketing Cloud] [Dokumentation](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&type=5), wenn Sie zusätzliche Anleitungen benötigen. | Obligatorisch |

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | X | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern *(z. B.: E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Jeder Segmentstatus in [!DNL Salesforce Marketing Cloud] wird mit dem entsprechenden Zielgruppenstatus von Experience Platform aktualisiert, basierend auf dem **[!UICONTROL Mapping ID]** Wert, der im Schritt [Zielgruppen-Planung](#schedule-segment-export-example) angegeben wurde.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
> Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Manage Destinations]** [Zugriffssteuerungsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** nach [!DNL (API) Salesforce Marketing Cloud]. Alternativ können Sie es unter der Kategorie **[!UICONTROL Email marketing]** finden.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder unten aus und wählen Sie **[!UICONTROL Connect to destination]** aus. Eine Anleitung dazu finden [&#x200B; im Abschnitt  [!DNL Salesforce Marketing Cloud] Sammeln](#gather-credentials)Anmeldeinformationen“.

| [!DNL (API) Salesforce Marketing Cloud] | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Subdomain]** | Ihr [!DNL Salesforce Marketing Cloud] Domain-Präfix. <br>Wenn Ihre Domain beispielsweise <br> ist *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.ExactTarget.* com), <br> Sie `mcq4jrssqdlyc4lph19nnqgzzs84` als Wert angeben müssen. |
| **[!UICONTROL Client ID]** | Ihre [!DNL Salesforce Marketing Cloud] `Client ID`. |
| **[!UICONTROL Client Secret]** | Ihre [!DNL Salesforce Marketing Cloud] `Client Secret`. |

Screenshot der ![Experience Platform-Benutzeroberfläche mit Informationen zur Authentifizierung bei Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche einen **[!UICONTROL Connected]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
Screenshot der ![Experience Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
> * Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
> * Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[&#x200B; &#x200B;](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

Um Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an das [!DNL (API) Salesforce Marketing Cloud]-Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodells (XDM) in Ihrem Experience Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen.

Gehen Sie wie folgt vor, um Ihre XDM-Felder den [!DNL (API) Salesforce Marketing Cloud]-Zielfeldern korrekt zuzuordnen.

>[!IMPORTANT]
>
> * Obwohl Ihre Attributnamen Ihrem [!DNL Salesforce Marketing Cloud]-Konto entsprechen, sind die Zuordnungen für `contactKey` und `personalEmail.address` obligatorisch.
>
> * Die Integration mit der [!DNL Salesforce Marketing Cloud]-API unterliegt einem Paginierungslimit für die Anzahl der Attribute, die Experience Platform von Salesforce abrufen kann. Das bedeutet, dass das Zielfeldschema im **[!UICONTROL Mapping]** maximal 2.000 Attribute aus Ihrem Salesforce-Konto anzeigen kann.

1. Wählen Sie im **[!UICONTROL Mapping]** Schritt **[!UICONTROL Add new mapping]** aus. Auf dem Bildschirm wird eine neue Zuordnungszeile angezeigt.
   Beispiel-Screenshot der Experience Platform-Benutzeroberfläche für „Neue Zuordnung hinzufügen“.![](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. Wählen Sie im **[!UICONTROL Select source field]** die Kategorie **[!UICONTROL Select attributes]** und dann das XDM-Attribut aus, oder wählen Sie die **[!UICONTROL Select identity namespace]** und dann eine Identität aus.
1. Wählen Sie im **[!UICONTROL Select target field]** die **[!UICONTROL Select identity namespace]** und dann eine Identität aus, oder wählen Sie **[!UICONTROL Select attributes]** Kategorie und dann ein Attribut aus den angezeigten Datenerweiterungen aus. Das [!DNL (API) Salesforce Marketing Cloud]-Ziel verwendet die [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html), um die in [!DNL Salesforce Marketing Cloud] definierten Datenerweiterungen und deren verknüpfte Attribute dynamisch abzurufen. Diese werden im Popup **[!UICONTROL Target field]** angezeigt, wenn Sie die [Zuordnung](#mapping-considerations-example) im Workflow [Zielgruppen aktivieren](#activate) einrichten.

   * Wiederholen Sie diese Schritte, um die folgenden Zuordnungen zwischen Ihrem XDM-Profilschema und [!DNL (API) Salesforce Marketing Cloud] hinzuzufügen:

     | Quellfeld | Zielfeld | Obligatorisch |
     |---|---|---|
     | `IdentityMap: contactKey` | `Identity: salesforceContactKey` | `Mandatory` |
     | `xdm: personalEmail.address` | `Attribute: Email Address` aus der [!DNL Salesforce Marketing Cloud] [!DNL Email Addresses]. | `Mandatory` beim Hinzufügen neuer Kontakte. |
     | `xdm: person.name.firstName` | `Attribute: First Name` aus der gewünschten [!DNL Salesforce Marketing Cloud]. | – |

   * Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Zuordnungen:
     Beispiel-Screenshot der Experience Platform-Benutzeroberfläche mit Ziel-Zuordnungen.![](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

Wenn Sie mit dem Eingeben der Zuordnungen für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

### Planen des Zielgruppenexports und Beispiel {#schedule-segment-export-example}

Bei der Durchführung des Schritts [Planen des &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling)-Exports) müssen Sie Experience Platform-Zielgruppen manuell den [Attributen](#prerequisites-attribute) in [!DNL Salesforce Marketing Cloud] zuordnen.

Wählen Sie dazu jedes Segment aus und geben Sie dann den Namen des Attributs aus [!DNL Salesforce Marketing Cloud] in das Feld [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** ein. Anleitungen und Best [&#x200B; zum Erstellen von Attributen in  [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) finden Sie im Abschnitt zum Erstellen von Attributen in [!DNL Salesforce Marketing Cloud].

Wenn Ihr [!DNL Salesforce Marketing Cloud] beispielsweise `salesforce_mc_segment_1` ist, geben Sie diesen Wert im [!DNL (API) Salesforce Marketing Cloud]-**[!UICONTROL Mapping ID]** an, um Zielgruppen aus Experience Platform in dieses Attribut einzufügen.

Ein Beispielattribut aus [!DNL Salesforce Marketing Cloud] wird unten angezeigt:
![Screenshot der Salesforce Marketing Cloud-Benutzeroberfläche mit einem Attribut.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

Nachfolgend finden Sie ein Beispiel für den Speicherort des [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]**:

Beispiel-Screenshot der Experience Platform-Benutzeroberfläche mit der Option „Zielgruppenexport planen“.![](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

Wie gezeigt, sollte der [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** genau mit dem in [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]** angegebenen Wert übereinstimmen.

Wiederholen Sie diesen Abschnitt für jedes aktivierte Experience Platform-Segment.

Ein typisches Beispiel auf der Grundlage des oben gezeigten Bildes könnte wie folgt aussehen.

| [!DNL (API) Salesforce Marketing Cloud] Segmentname | [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** |
| --- | --- | --- |
| Salesforce MC Audience 1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` |
| Salesforce MC Audience 2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Wählen Sie **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** aus, um zur Liste der Ziele zu navigieren.
   Screenshot der ![Experience Platform-Benutzeroberfläche mit den Durchsuchen-Zielen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Wählen Sie das Ziel aus und überprüfen Sie, ob der Status **[!UICONTROL enabled]** ist.
   Screenshot der ![Experience Platform-Benutzeroberfläche mit Zielen der Datenflussausführung.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Wechseln Sie zur Registerkarte **[!DNL Activation data]** und wählen Sie einen Zielgruppennamen aus.
   Beispiel-Screenshot der Experience Platform-Benutzeroberfläche mit Daten zur Aktivierung von Zielen.![](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Überwachen Sie die Zielgruppenzusammenfassung und stellen Sie sicher, dass die Anzahl der Profile der im Segment erstellten Anzahl entspricht.
   Beispiel-Screenshot der Experience Platform-Benutzeroberfläche mit Segment.![](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Melden Sie sich bei der [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/)-Website an. Navigieren Sie dann zur Seite **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** und überprüfen Sie, ob die Profile aus der Audience hinzugefügt wurden.
   ![Screenshot der Benutzeroberfläche von Salesforce Marketing Cloud mit der Seite „Kontakte“ und den im Segment verwendeten Profilen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Um festzustellen, ob Profile aktualisiert wurden, navigieren Sie zur Seite **[!UICONTROL Email]** und überprüfen Sie, ob die Attributwerte für das Profil aus der Audience aktualisiert wurden. Bei erfolgreicher Ausführung können Sie sehen, dass jeder Zielgruppenstatus in [!DNL Salesforce Marketing Cloud] mit dem entsprechenden Zielgruppenstatus von Experience Platform aktualisiert wurde, basierend auf dem **[!UICONTROL Mapping ID]** Wert, der im Schritt [Zielgruppen-Planung](#schedule-segment-export-example) angegeben wurde.
   ![Screenshot der Benutzeroberfläche von Salesforce Marketing Cloud mit der E-Mail-Seite „Ausgewählte Kontakte“ mit aktualisierten Zielgruppenstatus.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

### Unbekannte Fehler beim Pushen von Ereignissen an Salesforce Marketing Cloud {#unknown-errors}

* Beim Überprüfen einer Datenflussausführung kann die folgende Fehlermeldung auftreten: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  Screenshot der ![Experience Platform-Benutzeroberfläche mit Fehlermeldung.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * Um diesen Fehler zu beheben, überprüfen Sie, ob die **[!UICONTROL Mapping ID]**, die Sie im Aktivierungs-Workflow für das [!DNL (API) Salesforce Marketing Cloud]-Ziel angegeben haben, genau mit dem Namen des Attributs übereinstimmt, das Sie in [!DNL Salesforce Marketing Cloud] erstellt haben. Eine Anleitung finden [&#x200B; im Abschnitt  [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field)Attribut erstellen in“.

* Beim Aktivieren eines Segments erhalten Sie möglicherweise eine Fehlermeldung: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Wenden Sie sich zur Behebung dieses Fehlers an Ihren [!DNL Salesforce Marketing Cloud]-Kontoadministrator, um [Experience Platform-IP](/help/destinations/catalog/streaming/ip-address-allow-list.md)Adressen) zu den vertrauenswürdigen IP-Bereichen Ihrer [!DNL Salesforce Marketing Cloud] hinzuzufügen. Auf die Zulassungsliste setzen Weitere Anleitungen finden Sie in der [!DNL Salesforce Marketing Cloud] [IP-Adressen für die Aufnahme &#x200B;](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&type=5) Marketing Clouds&quot;.

## Weitere Ressourcen {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [Dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) Erläuterung, wie Kontakte mit den angegebenen Informationen aktualisiert werden.

### Änderungsprotokoll {#changelog}

In diesem Abschnitt werden aktualisierte Funktionen und wesentliche Dokumentationsänderungen für diesen Ziel-Connector erfasst.

+++ Änderungsprotokoll anzeigen

| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| Oktober 2023 | Dokumentation aktualisieren | <ul><li>Der Abschnitt [Voraussetzungen in (API) Salesforce Marketing Cloud](#prerequisites-destination) wurde aktualisiert und im Allgemeinen wurden unnötige Verweise auf Attributgruppen im gesamten Dokument entfernt.</li> <li>Die Dokumentation wurde aktualisiert, um darauf hinzuweisen, dass Attribute für die Zielgruppenstatus nur innerhalb von [!DNL Salesforce Marketing Cloud] innerhalb der [!DNL Email Demographics]-Datenerweiterung erstellt werden sollten.</li> <li>Die Zuordnungstabelle wurde im Abschnitt [Zuordnungsüberlegungen und Beispiel](#mapping-considerations-example) aktualisiert. Die Zuordnung für `Email Address` Attribut innerhalb der `Email Addresses`-Datenerweiterung ist als obligatorisch gekennzeichnet. Diese Anforderung wurde im Legende mit der Kennzeichnung WICHTIG erwähnt, wurde jedoch in der Tabelle weggelassen.</li></ul> |
| April 2023 | Dokumentation aktualisieren | <ul><li>Wir haben eine Erklärung und einen Referenz-Link im Abschnitt [Voraussetzungen in (API) Salesforce Marketing Cloud](#prerequisites-destination) korrigiert, um darauf hinzuweisen, dass [!DNL Salesforce Marketing Cloud Engagement] für die Verwendung dieses Ziels ein Pflichtabonnement ist. Im vorherigen Abschnitt wurde fälschlicherweise darauf hingewiesen, dass Benutzende ein Abonnement für die Marketing Cloud-Interaktion **Account** benötigen, um fortzufahren.</li> <li>Wir haben einen Abschnitt unter [Voraussetzungen](#prerequisites) hinzugefügt, damit [Rollen und Berechtigungen](#prerequisites-roles-permissions) dem [!DNL Salesforce] Benutzer zugewiesen werden können, damit dieses Ziel funktioniert. (PLATIR-26299)</li></ul> |
| Februar 2023 | Dokumentation aktualisieren | Der Abschnitt [Voraussetzungen in (API) Salesforce Marketing Cloud](#prerequisites-destination) wurde aktualisiert und enthält jetzt einen Referenzlink, der darauf verweist, dass [!DNL Salesforce Marketing Cloud Engagement] für die Verwendung dieses Ziels ein Pflichtabonnement ist. |
| Februar 2023 | Funktionsaktualisierung | Es wurde ein Problem behoben, bei dem eine falsche Konfiguration im Ziel dazu führte, dass eine falsch formatierte JSON an Salesforce gesendet wurde. Dies führte dazu, dass einige Benutzende feststellten, dass bei der Aktivierung eine hohe Anzahl von Identitäten fehlgeschlagen war. (PLATIR-26299) |
| Januar 2023 | Dokumentation aktualisieren | <ul><li>Der Abschnitt [Voraussetzungen“  [!DNL Salesforce]](#prerequisites-destination) wurde aktualisiert, um darauf hinzuweisen, dass Attribute auf der [!DNL Salesforce] Seite erstellt werden müssen. Dieser Abschnitt enthält jetzt detaillierte Anweisungen, wie Sie dies tun, und Best Practices für die Benennung der Attribute in [!DNL Salesforce]. (PLATIR-25602)</li><li>Im Schritt „Zielgruppen-Planung“ wurden klare Anweisungen zur Verwendung der Zuordnungs-ID [&#x200B; jede aktivierte Zielgruppe &#x200B;](#schedule-segment-export-example). (PLATIR-25602)</li></ul> |
| Oktober 2022 | Erstmalige Veröffentlichung | Erstmalige Zielveröffentlichung und Dokumentation. |

{style="table-layout:auto"}

+++
