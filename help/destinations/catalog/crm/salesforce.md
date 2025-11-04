---
keywords: crm;CRM;CRM-Ziele;Salesforce CRM;Salesforce CRM-Ziel
title: Salesforce-CRM-Verbindung
description: Mit dem Salesforce CRM-Ziel können Sie Ihre Kontodaten exportieren und in Salesforce CRM für Ihre Geschäftsanforderungen aktivieren.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: 27f2b28d924fbd85eefbea5a65d1ee9249bafa87
workflow-type: tm+mt
source-wordcount: '2734'
ht-degree: 16%

---

# [!DNL Salesforce CRM]-Verbindung

## Übersicht {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) ist eine beliebte CRM-Plattform (Customer Relationship Management) und unterstützt die unten beschriebenen Profiltypen:

* [Leads](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) - Ein Lead ist der Name einer Person oder eines Unternehmens, die bzw. das möglicherweise nicht an den von Ihnen verkauften Produkten oder Services interessiert ist.
* [Kontakte](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) - Ein Kontakt ist eine Person, mit der einer Ihrer Mitarbeiter eine Beziehung aufgebaut hat und die als potenzieller Kunde qualifiziert wurde.

Dieses [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt die [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm), die beide oben beschriebenen Profiltypen unterstützt.

Beim [Aktivieren von Segmenten](#activate) können Sie entweder zwischen Leads oder Kontakten wählen und Attribute und Zielgruppendaten in [!DNL Salesforce CRM] aktualisieren.

[!DNL Salesforce CRM] verwendet OAuth 2 mit Passwortgewährung als Authentifizierungsmechanismus für die Kommunikation mit der Salesforce REST-API. Anweisungen zur Authentifizierung bei Ihrer [!DNL Salesforce CRM]-Instanz sehen Sie weiter unten im Abschnitt [Authentifizieren bei Ziel](#authenticate).

## Anwendungsbeispiele {#use-cases}

Als Marketing-Experte können Sie Ihren Benutzern personalisierte Erlebnisse auf der Basis von Attributen aus ihren Adobe Experience Platform-Profilen bereitstellen. Sie können Zielgruppen aus Ihren Offline-Daten erstellen und diese Zielgruppen an Salesforce CRM senden, um die CRM-Mitgliedschaft zu aktualisieren, sobald Zielgruppen und Profile in Adobe Experience Platform aktualisiert werden.

## Voraussetzungen {#prerequisites}

### Voraussetzungen in Experience Platform {#prerequisites-in-experience-platform}

Bevor Sie Daten für das Salesforce CRM-Ziel aktivieren, müssen Sie ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) in [!DNL Experience Platform] erstellt haben.

### Voraussetzungen in [!DNL Salesforce CRM] {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen in [!DNL Salesforce CRM], um Daten aus Experience Platform in Ihr Salesforce-Konto zu exportieren:

#### Sie benötigen ein [!DNL Salesforce]-Konto {#prerequisites-account}

Navigieren Sie zur [!DNL Salesforce] [Testversion](https://www.salesforce.com/in/form/signup/freetrial-sales/)-Seite, um sich zu registrieren und ein [!DNL Salesforce] Konto zu erstellen, falls Sie noch keines haben.

#### Konfigurieren einer verbundenen App in [!DNL Salesforce] {#prerequisites-connected-app}

Zunächst müssen Sie eine [[!DNL Salesforce] verbundene App](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&language=en_US&r=https%3A%2F%2Fhelp.salesforce.com%2F&type=5) in Ihrem [!DNL Salesforce]-Konto konfigurieren, falls Sie noch keine haben. [!DNL Salesforce CRM] nutzt die verbundene App, um eine Verbindung zu [!DNL Salesforce] herzustellen.

Aktivieren Sie als Nächstes [!DNL OAuth Settings for API Integration] für die [!DNL Salesforce connected app]. Eine Anleitung dazu finden Sie in der [[!DNL Salesforce]](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&type=5&language=en_US) Dokumentation .

Stellen Sie außerdem sicher[ dass die unten ](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&type=5&language=en_US)Bereiche“ für die [!DNL Salesforce connected app] ausgewählt sind.

* ``chatter_api``
* ``lightning``
* ``visualforce``
* ``content``
* ``openid``
* ``full``
* ``api``
* ``web``
* ``refresh_token``
* ``offline_access``

Stellen Sie abschließend sicher, dass die `password` in Ihrem [!DNL Salesforce]-Konto aktiviert ist. Weitere Informationen finden Sie in der [!DNL Salesforce] [OAuth 2.0 Benutzername-Kennwort-Fluss für ](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_username_password_flow.htm&type=5)-Szenarien“.

>[!IMPORTANT]
>
>Wenn Ihr [!DNL Salesforce]-Kontoadministrator den Zugriff auf vertrauenswürdige IP-Bereiche beschränkt hat, müssen Sie sich an ihn wenden, um [Experience Platform auf die Zulassungsliste setzen IPs](/help/destinations/catalog/streaming/ip-address-allow-list.md) zu erhalten. Weitere Anleitungen finden Sie in der [!DNL Salesforce] [Zugriff auf vertrauenswürdige IP-Bereiche für eine ](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&type=5) App beschränken“.

#### Erstellen benutzerdefinierter Felder in [!DNL Salesforce] {#prerequisites-custom-field}

Beim Aktivieren von Zielgruppen für das [!DNL Salesforce CRM]-Ziel müssen Sie im Schritt **[!UICONTROL Mapping ID]** Zielgruppen-Zeitplan“ für jede aktivierte Zielgruppe einen Wert in **[Feld](#schedule-segment-export-example)** eingeben.

[!DNL Salesforce CRM] erfordert diesen Wert, um Zielgruppen aus Experience Platform korrekt zu lesen und zu interpretieren und ihren Zielgruppenstatus in [!DNL Salesforce] zu aktualisieren. Weitere Informationen finden Sie in der Experience Platform[Dokumentation für die Schemafeldgruppe „Details zur Zielgruppenzugehörigkeit](/help/xdm/field-groups/profile/segmentation.md) , wenn Sie Anleitungen zu Zielgruppenstatus benötigen.

Für jede Zielgruppe, die Sie von Experience Platform in [!DNL Salesforce CRM] aktivieren, müssen Sie ein benutzerdefiniertes Feld des Typs `Text Area (Long)` in [!DNL Salesforce] erstellen. Sie können die Feldzeichenlänge beliebiger Größe zwischen 256 und 131.072 Zeichen entsprechend Ihren Geschäftsanforderungen definieren. Weitere Informationen zu benutzerdefinierten Feldtypen finden [!DNL Salesforce] auf [ Dokumentationsseite ](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&type=5)Benutzerdefinierte Feldtypen“. Weitere Informationen finden Sie auch in der [!DNL Salesforce]-Dokumentation [Erstellen benutzerdefinierter Felder](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&type=5&language=en_US) , wenn Sie Hilfe bei der Felderstellung benötigen.

>[!IMPORTANT]
>
>Verwenden Sie keine Leerzeichen im Feldnamen. Verwenden Sie stattdessen den Unterstrich `(_)` als Trennzeichen.
>In [!DNL Salesforce] müssen Sie benutzerdefinierte Felder mit einem **[!UICONTROL Field Name]** erstellen, der genau mit dem Wert übereinstimmt, der in **[!UICONTROL Mapping ID]** für jedes aktivierte Experience Platform-Segment angegeben ist. Der folgende Screenshot zeigt beispielsweise ein benutzerdefiniertes Feld mit dem Namen `crm_2_seg`. Fügen Sie beim Aktivieren einer Zielgruppe für dieses Ziel `crm_2_seg` als **[!UICONTROL Mapping ID]** hinzu, um Zielgruppen aus Experience Platform in dieses benutzerdefinierte Feld einzufügen.

Ein Beispiel für die Erstellung benutzerdefinierter Felder in [!DNL Salesforce], *Schritt 1 - Wählen Sie den Datentyp aus*, wird unten angezeigt:
![Screenshot der Salesforce-Benutzeroberfläche mit der Erstellung benutzerdefinierter Felder, Schritt 1: Wählen Sie den Datentyp aus.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-1.png)

Ein Beispiel für die Erstellung benutzerdefinierter Felder in [!DNL Salesforce], *Schritt 2: Geben Sie die Details für das benutzerdefinierte Feld ein*, wird unten angezeigt:
![Screenshot der Salesforce-Benutzeroberfläche mit der Erstellung benutzerdefinierter Felder, Schritt 2: Geben Sie die Details für das benutzerdefinierte Feld ein.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-2.png)

>[!TIP]
>
>* Um zwischen benutzerdefinierten Feldern, die für Experience Platform-Zielgruppen verwendet werden, und anderen benutzerdefinierten Feldern in [!DNL Salesforce] zu unterscheiden, können Sie beim Erstellen des benutzerdefinierten Felds ein erkennbares Präfix oder Suffix einfügen. Verwenden Sie beispielsweise anstelle von `test_segment` `Adobe_test_segment` oder `test_segment_Adobe`
>* Wenn Sie bereits andere benutzerdefinierte Felder in [!DNL Salesforce] erstellt haben, können Sie denselben Namen wie das Experience Platform-Segment verwenden, um die Zielgruppe in [!DNL Salesforce] einfach zu identifizieren.

>[!NOTE]
>
>* Objekte in Salesforce sind auf 25 externe Felder beschränkt. Siehe [Benutzerdefinierte Feldattribute](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&type=5).
>* Diese Einschränkung bedeutet, dass Sie immer nur maximal 25 Zielgruppenmitgliedschaften für Experience Platform aktiv haben können.
>* Wenn Sie dieses Limit in Salesforce erreicht haben, müssen Sie die benutzerdefinierten Attribute aus Salesforce entfernen, die zum Speichern des Zielgruppenstatus in älteren Zielgruppen in Experience Platform verwendet wurden, bevor ein neues **[!UICONTROL Mapping ID]** verwendet werden kann.

#### Sammeln von [!DNL Salesforce CRM]-Anmeldedaten {#gather-credentials}

Beachten Sie die folgenden Punkte, bevor Sie sich beim [!DNL Salesforce CRM]-Ziel authentifizieren:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| `Username` | Benutzername Ihres [!DNL Salesforce]. | |
| `Password` | Ihr [!DNL Salesforce]-Passwort. | |
| `Security Token` | Ihr [!DNL Salesforce]-Sicherheits-Token, das Sie später an das Ende Ihres [!DNL Salesforce]-Kennworts anhängen, um eine verkettete Zeichenfolge zu erstellen, die als **[!UICONTROL Password]** bei der ([ beim Ziel) ](#authenticate) wird.<br> Informationen zum Zurücksetzen Ihres Sicherheits-Tokens finden [!DNL Salesforce] in der [-Dokumentation](https://help.salesforce.com/s/articleView?id=sf.user_security_token.htm&type=5) um zu erfahren, wie Sie es über die [!DNL Salesforce]-Oberfläche neu generieren, wenn Sie das Sicherheits-Token nicht haben. |  |
| `Custom Domain` | Ihr [!DNL Salesforce] Domain-Präfix. <br> Informationen zum Abrufen dieses Werts aus der [[!DNL Salesforce] -](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&type=5) finden Sie in der [!DNL Salesforce]Dokumentation. | Wenn Ihre [!DNL Salesforce] Domain ist<br> *`d5i000000isb4eak-dev-ed`.my.salesforce.com*, <br> Sie `d5i000000isb4eak-dev-ed` als Wert benötigen. |
| `Client ID` | Ihr Salesforce-`Consumer Key`. <br> Informationen zum Abrufen dieses Werts aus der [[!DNL Salesforce] -](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&type=5) finden Sie in der [!DNL Salesforce]Dokumentation. | |
| `Client Secret` | Ihr Salesforce-`Consumer Secret`. <br> Informationen zum Abrufen dieses Werts aus der [[!DNL Salesforce] -](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&type=5) finden Sie in der [!DNL Salesforce]Dokumentation. | |

### Leitlinien {#guardrails}

[!DNL Salesforce] gleicht Transaktionslasten ab, indem Sie Limits für Anfragen, Raten und Zeitüberschreitungen festlegen. Weitere Informationen finden Sie unter [API-Anfrage-Limits und ](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm)&quot;.

Wenn der Administrator Ihres [!DNL Salesforce]-Kontos IP-Einschränkungen durchgesetzt hat, müssen Sie [Experience Platform-IP-](/help/destinations/catalog/streaming/ip-address-allow-list.md)Adressen) zu den vertrauenswürdigen IP-Bereichen Ihrer [!DNL Salesforce]-Konten hinzufügen. Weitere Anleitungen finden Sie in der [!DNL Salesforce] [Zugriff auf vertrauenswürdige IP-Bereiche für eine ](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&type=5) App beschränken“.

>[!IMPORTANT]
>
>Beim [Aktivieren ](#activate) Segmente müssen Sie entweder zwischen dem Typ *Kontakt* oder *Lead* wählen. Sie müssen sicherstellen, dass Ihre Zielgruppen über die entsprechende Datenzuordnung entsprechend dem ausgewählten Typ verfügen.

## Unterstützte Identitäten {#supported-identities}

[!DNL Salesforce CRM] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| `SalesforceId` | Die [!DNL Salesforce CRM] Kennung für die Kontakt- oder Lead-Identitäten, die Sie über Ihr Segment exportieren oder aktualisieren. | Obligatorisch |

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern *(z. B.: E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Jeder Zielgruppenstatus in [!DNL Salesforce CRM] wird mit dem entsprechenden Zielgruppenstatus von Experience Platform aktualisiert, basierend auf dem **[!UICONTROL Mapping ID]** Wert, der im Schritt [Zielgruppen-Planung](#schedule-segment-export-example) angegeben wurde.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | <ul><li>Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** nach [!DNL Salesforce CRM]. Alternativ können Sie es unter der Kategorie **[!UICONTROL CRM]** finden.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder unten aus und wählen Sie **[!UICONTROL Connect to destination]** aus. Eine Anleitung dazu finden [ im Abschnitt  [!DNL Salesforce CRM] Sammeln](#gather-credentials)Anmeldeinformationen“.

| Anmeldedaten | Beschreibung |
| --- | --- |
| **[!UICONTROL Username]** | Benutzername Ihres [!DNL Salesforce]. |
| **[!UICONTROL Password]** | Eine verkettete Zeichenfolge, die aus dem Kennwort Ihres [!DNL Salesforce]-Kontos besteht, das an Ihr [!DNL Salesforce]-Sicherheits-Token angehängt wird.<br>Der verkettete Wert hat die Form von `{PASSWORD}{TOKEN}`.<br> Hinweis: Verwenden Sie keine Klammern oder Leerzeichen.<br>Wenn Ihr [!DNL Salesforce]-Kennwort beispielsweise `MyPa$$w0rd123` und [!DNL Salesforce] Sicherheits-Token `TOKEN12345....0000` ist, wird der verkettete Wert, den Sie im **[!UICONTROL Password]** Feld verwenden, `MyPa$$w0rd123TOKEN12345....0000`. |
| **[!UICONTROL Custom Domain]** | Ihr [!DNL Salesforce] Domain-Präfix. <br>Wenn Ihre Domain beispielsweise *`d5i000000isb4eak-dev-ed`.my.salesforce.com lautet* müssen Sie `d5i000000isb4eak-dev-ed` als Wert angeben. |
| **[!UICONTROL Client ID]** | Ihre [!DNL Salesforce] verbundene App `Consumer Key`. |
| **[!UICONTROL Client Secret]** | Ihre [!DNL Salesforce] verbundene App `Consumer Secret`. |

Screenshot der ![Experience Platform-Benutzeroberfläche, auf dem die Authentifizierung gezeigt wird.](../../assets/catalog/crm/salesforce/authenticate-destination.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche einen **[!UICONTROL Connected]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Salesforce ID Type]**

   * Wählen Sie **[!UICONTROL Contact]** aus, wenn die Identitäten, die Sie exportieren oder aktualisieren möchten, vom Typ *Kontakt* sind.
   * Wählen Sie **[!UICONTROL Lead]** aus, wenn die Identitäten, die exportiert oder aktualisiert werden sollen, vom Typ *Lead* sind.

Screenshot der ![Experience Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/crm/salesforce/destination-details.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

Um Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an das [!DNL Salesforce CRM]-Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodells (XDM) in Ihrem Experience Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen.

Die in der **[!UICONTROL Target field]** angegebenen Attribute sollten genau wie in der Tabelle der Attributzuordnungen beschrieben benannt werden, da diese Attribute den Anfragetext bilden.

Die in der **[!UICONTROL Source field]** angegebenen Attribute entsprechen keiner dieser Einschränkungen. Sie können sie nach Bedarf zuordnen, stellen jedoch sicher, dass das Format der Eingabedaten gemäß der [[!DNL Salesforce] Dokumentation) gültig ](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&type=5). Wenn die Eingabedaten ungültig sind, schlägt der Aktualisierungsaufruf an [!DNL Salesforce] fehl und Ihre Kontakte/Leads werden nicht aktualisiert.

Um Ihre XDM-Felder den [!DNL (API) Salesforce CRM]-Zielfeldern korrekt zuzuordnen, führen Sie die folgenden Schritte aus:

1. Wenn Sie im **[!UICONTROL Mapping]** Schritt **[!UICONTROL Add new mapping]** auswählen, wird eine neue Zuordnungszeile auf dem Bildschirm angezeigt.
   Beispiel-Screenshot der Experience Platform-Benutzeroberfläche für „Neue Zuordnung hinzufügen“.![](../../assets/catalog/crm/salesforce/add-new-mapping.png)
1. Wählen Sie im **[!UICONTROL Select source field]** die Kategorie **[!UICONTROL Select attributes]** und dann das XDM-Attribut aus, oder wählen Sie die **[!UICONTROL Select identity namespace]** und dann eine Identität aus.
1. Wählen Sie im **[!UICONTROL Select target field]**-Fenster den **[!UICONTROL Select identity namespace]** und dann eine Identität aus, oder wählen Sie **[!UICONTROL Select custom attributes]** Kategorie aus und wählen Sie ein Attribut aus, oder definieren Sie eines mithilfe des **[!UICONTROL Attribute name]**. Anleitungen zu unterstützten Attributen finden [[!DNL Salesforce CRM]  in der ](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&type=5)Dokumentation).
   * Wiederholen Sie diese Schritte, um die folgenden Zuordnungen zwischen Ihrem XDM-Profilschema und [!DNL (API) Salesforce CRM] hinzuzufügen:

   **Arbeiten mit Kontakten**

   * Wenn Sie in Ihrem Segment mit *Kontakte* arbeiten, definieren Sie in der Objektreferenz in Salesforce für [Kontakt](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) Zuordnungen für die zu aktualisierenden Felder.
   * Sie können Pflichtfelder identifizieren, indem Sie nach dem Wort *Erforderlich* suchen, das in den Feldbeschreibungen im obigen Link erwähnt wird.
   * Fügen Sie je nach den Feldern, die Sie exportieren oder aktualisieren möchten, Zuordnungen zwischen Ihrem XDM-Profilschema und [!DNL (API) Salesforce CRM] hinzu:

     | Quellfeld | Zielfeld | Anmerkungen |
     | --- | --- | --- |
     | `IdentityMap: crmID` | `Identity: SalesforceId` | `Mandatory` |
     | `xdm: person.name.lastName` | `Attribute: LastName` | `Mandatory`. Nachname des Kontakts mit bis zu 80 Zeichen. |
     | `xdm: person.name.firstName` | `Attribute: FirstName` | Der Vorname des Kontakts kann bis zu 40 Zeichen lang sein. |
     | `xdm: personalEmail.address` | `Attribute: Email` | Die E-Mail-Adresse des Kontakts. |

   * Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Zuordnungen:
     Beispiel-Screenshot der Experience Platform-Benutzeroberfläche mit Ziel-Zuordnungen.![](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   **Arbeiten mit Leads**

   * Wenn Sie in Ihrem Segment mit *Leads* arbeiten, definieren Sie in der Objektreferenz in Salesforce für [Lead](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) Zuordnungen für die zu aktualisierenden Felder.
   * Sie können Pflichtfelder identifizieren, indem Sie nach dem Wort *Erforderlich* suchen, das in den Feldbeschreibungen im obigen Link erwähnt wird.
   * Fügen Sie je nach den Feldern, die Sie exportieren oder aktualisieren möchten, Zuordnungen zwischen Ihrem XDM-Profilschema und [!DNL (API) Salesforce CRM] hinzu:

     | Quellfeld | Zielfeld | Anmerkungen |
     | --- | --- | --- |
     | `IdentityMap: crmID` | `Identity: SalesforceId` | `Mandatory` |
     | `xdm: person.name.lastName` | `Attribute: LastName` | `Mandatory`. Nachname des Leads mit bis zu 80 Zeichen. |
     | `xdm: b2b.companyName` | `Attribute: Company` | `Mandatory`. Die Firma des Leads. |
     | `xdm: personalEmail.address` | `Attribute: Email` | Die E-Mail-Adresse des Leads. |

   * Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Zuordnungen:
     Beispiel-Screenshot der Experience Platform-Benutzeroberfläche mit Ziel-Zuordnungen.![](../../assets/catalog/crm/salesforce/mappings-leads.png)

Wenn Sie mit dem Eingeben der Zuordnungen für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

### Planen des Zielgruppenexports und Beispiel {#schedule-segment-export-example}

Bei der Durchführung des [Exportierens von Zielgruppen planen](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) müssen Sie die in Experience Platform aktivierten Zielgruppen manuell dem entsprechenden benutzerdefinierten Feld in [!DNL Salesforce] zuordnen.

Wählen Sie dazu jedes Segment aus und geben Sie dann den benutzerdefinierten Feldnamen aus [!DNL Salesforce] in das Feld [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** ein. Anleitungen und Best Practices [ Erstellen benutzerdefinierter Felder in  [!DNL Salesforce]](#prerequisites-custom-field) finden Sie im Abschnitt zum Erstellen benutzerdefinierter Felder in [!DNL Salesforce].

Wenn Ihr [!DNL Salesforce] benutzerdefiniertes Feld beispielsweise `crm_2_seg` ist, geben Sie diesen Wert im [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** an, um Zielgruppen aus Experience Platform in dieses benutzerdefinierte Feld einzufügen.

Ein Beispiel für ein benutzerdefiniertes Feld aus [!DNL Salesforce] sehen Sie unten:
Screenshot der ![[!DNL Salesforce]-Benutzeroberfläche mit benutzerdefiniertem Feld.](../../assets/catalog/crm/salesforce/salesforce-custom-field.png)

Nachfolgend finden Sie ein Beispiel für den Speicherort des [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]**:
Beispiel-Screenshot der ![Experience Platform-Benutzeroberfläche mit der Option „Zielgruppenexport planen“.](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

Wie oben gezeigt, stimmt der [!DNL Salesforce] **[!UICONTROL Field Name]** genau mit dem in [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** angegebenen Wert überein.

Je nach Anwendungsfall können alle aktivierten Zielgruppen demselben [!DNL Salesforce] benutzerdefinierten Feld oder verschiedenen **[!UICONTROL Field Name]** in [!DNL Salesforce CRM] zugeordnet werden. Ein typisches Beispiel auf der Grundlage des oben gezeigten Bildes könnte wie folgt aussehen.

| [!DNL Salesforce CRM] Segmentname | [!DNL Salesforce] **[!UICONTROL Field Name]** | [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** |
| --- | --- | --- |
| crm_1_seg | `crm_1_seg` | `crm_1_seg` |
| crm_2_seg | `crm_2_seg` | `crm_2_seg` |

Wiederholen Sie diesen Abschnitt für jedes aktivierte Experience Platform-Segment.

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Wählen Sie **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** aus, um zur Liste der Ziele zu navigieren.
   Screenshot der ![Experience Platform-Benutzeroberfläche mit den Durchsuchen-Zielen.](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. Wählen Sie das Ziel aus und überprüfen Sie, ob der Status **[!UICONTROL enabled]** ist.
   Screenshot der ![Experience Platform-Benutzeroberfläche mit Zielen der Datenflussausführung.](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. Wechseln Sie zur Registerkarte **[!UICONTROL Activation data]** und wählen Sie einen Zielgruppennamen aus.
   Beispiel-Screenshot der Experience Platform-Benutzeroberfläche mit Daten zur Aktivierung von Zielen.![](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. Überwachen Sie die Zielgruppenzusammenfassung und stellen Sie sicher, dass die Anzahl der Profile der im Segment erstellten Anzahl entspricht.
   Beispiel-Screenshot der Experience Platform-Benutzeroberfläche mit Segment.![](../../assets/catalog/crm/salesforce/segment.png)

1. Melden Sie sich abschließend bei der Salesforce-Website an und überprüfen Sie, ob die Profile aus der Zielgruppe aktualisiert wurden.

   **Arbeiten mit Kontakten**

   * Wenn Sie in *Experience Platform-* „Kontakte“ ausgewählt haben, navigieren Sie zur Seite **[!DNL Apps]** > **[!DNL Contacts]** .
     ![Screenshot von Salesforce CRM mit der Seite „Kontakte“ und den Profilen aus dem Segment.](../../assets/catalog/crm/salesforce/contacts.png)

   * Wählen Sie einen *Kontakt* aus und überprüfen Sie, ob die Felder aktualisiert wurden. Sie können sehen, dass jeder Zielgruppenstatus in [!DNL Salesforce CRM] mit dem entsprechenden Zielgruppenstatus von Experience Platform aktualisiert wurde, basierend auf dem **[!UICONTROL Mapping ID]** Wert, der während der Zielgruppenplanung [ wurde](#schedule-segment-export-example).
     ![Screenshot von Salesforce CRM mit der Seite „Kontaktdetails“ und aktualisierten Zielgruppenstatus.](../../assets/catalog/crm/salesforce/contact-info.png)

   **Arbeiten mit Leads**

   * Wenn Sie *Leads* innerhalb Ihres Experience Platform-Segments ausgewählt haben, navigieren Sie zur Seite **[!DNL Apps]** > **[!DNL Leads]** .
     ![Screenshot von Salesforce CRM mit der Seite „Leads“ und den Profilen aus dem Segment.](../../assets/catalog/crm/salesforce/leads.png)

   * Wählen Sie einen *Lead* aus und überprüfen Sie, ob die Felder aktualisiert wurden. Sie können sehen, dass jeder Zielgruppenstatus in [!DNL Salesforce CRM] mit dem entsprechenden Zielgruppenstatus von Experience Platform aktualisiert wurde, basierend auf dem **[!UICONTROL Mapping ID]** Wert, der während der Zielgruppenplanung [ wurde](#schedule-segment-export-example).
     ![Screenshot des Salesforce CRM mit der Seite „Lead-Details“ und aktualisierten Zielgruppenstatus.](../../assets/catalog/crm/salesforce/lead-info.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

### Beim Pushen von Ereignissen an das Ziel sind unbekannte Fehler aufgetreten {#unknown-errors}

* Beim Überprüfen einer Datenflussausführung kann die folgende Fehlermeldung auftreten: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  Screenshot der ![Experience Platform-Benutzeroberfläche mit Fehlermeldung.](../../assets/catalog/crm/salesforce/error.png)

   * Um diesen Fehler zu beheben, überprüfen Sie, ob der **[!UICONTROL Mapping ID]**, den Sie im Aktivierungs-Workflow für das [!DNL Salesforce CRM]-Ziel angegeben haben, genau mit dem Wert des benutzerdefinierten Feldtyps übereinstimmt, den Sie in [!DNL Salesforce] erstellt haben. Eine Anleitung finden [ im Abschnitt Erstellen  [!DNL Salesforce]](#prerequisites-custom-field) benutzerdefinierten Feldern in .

* Beim Aktivieren eines Segments erhalten Sie möglicherweise eine Fehlermeldung: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Wenden Sie sich zur Behebung dieses Fehlers an Ihren [!DNL Salesforce]-Kontoadministrator, um [Experience Platform-IP](/help/destinations/catalog/streaming/ip-address-allow-list.md)Adressen) zu den vertrauenswürdigen IP-Bereichen Ihrer [!DNL Salesforce] hinzuzufügen. Weitere Anleitungen finden Sie in der [!DNL Salesforce] [Zugriff auf vertrauenswürdige IP-Bereiche für eine ](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&type=5) App beschränken“.

## Weitere Ressourcen {#additional-resources}

Weitere nützliche Informationen vom [Salesforce-Entwicklerportal](https://developer.salesforce.com/) finden Sie unten:

* [Schnellstart](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [Datensatz erstellen](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [Benutzerdefinierte Recommendations-Zielgruppen](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [Verwenden von zusammengesetzten Ressourcen](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* Dieses Ziel nutzt die API [Upsert Multiple Records](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) anstelle des API-Aufrufs [Upsert Single Record](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts).
