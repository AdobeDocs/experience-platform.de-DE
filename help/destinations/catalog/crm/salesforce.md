---
keywords: crm;CRM;crm-Ziele;Salesforce crm;Salesforce crm-Ziel
title: Salesforce-CRM-Verbindung
description: Mit dem Salesforce CRM-Ziel können Sie Ihre Kontodaten exportieren und im Salesforce CRM für Ihre geschäftlichen Anforderungen aktivieren.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '2821'
ht-degree: 20%

---

# [!DNL Salesforce CRM]-Verbindung

## Übersicht {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) ist eine beliebte CRM-Plattform (Customer Relationship Management) und unterstützt die unten beschriebenen Profiltypen:

* [Leads](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) - Ein Lead ist der Name einer Person oder Firma, die an den von Ihnen verkauften Produkten oder Dienstleistungen interessiert sein kann (oder nicht).
* [Kontakte](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) - Ein Kontakt ist eine Person, mit der einer Ihrer Mitarbeiter eine Beziehung aufgebaut hat und die als potenzieller Kunde qualifiziert wurde.

Diese [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt die [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm)unterstützt, die beide oben beschriebenen Profiltypen unterstützt.

Wann [Segmente aktivieren](#activate)können Sie zwischen Leads oder Kontakten wählen und Attribute und Zielgruppendaten in [!DNL Salesforce CRM].

[!DNL Salesforce CRM] verwendet OAuth 2 mit Password Grant als Authentifizierungsmechanismus für die Kommunikation mit der Salesforce REST API. Anweisungen zur Authentifizierung bei Ihrer [!DNL Salesforce CRM]-Instanz sehen Sie weiter unten im Abschnitt [Authentifizieren bei Ziel](#authenticate).

## Anwendungsbeispiele {#use-cases}

Als Marketing-Experte können Sie Ihren Benutzern personalisierte Erlebnisse auf der Basis von Attributen aus ihren Adobe Experience Platform-Profilen bereitstellen. Sie können Zielgruppen aus Ihren Offline-Daten erstellen und an Salesforce CRM senden, um die CRM-Mitgliedschaft zu aktualisieren, sobald Audiences und Profile in Adobe Experience Platform aktualisiert wurden.

## Voraussetzungen {#prerequisites}

### Voraussetzungen für Experience Platform {#prerequisites-in-experience-platform}

Bevor Sie Daten für das Salesforce CRM-Ziel aktivieren, benötigen Sie eine [schema](/help/xdm/schema/composition.md), a [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=de), und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) erstellt in [!DNL Experience Platform].

### Voraussetzungen in [!DNL Salesforce CRM] {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen in [!DNL Salesforce CRM], um Daten von Platform in Ihr Salesforce-Konto zu exportieren:

#### Sie benötigen ein [!DNL Salesforce]-Konto {#prerequisites-account}

Navigieren Sie zu [!DNL Salesforce] [Testversion](https://www.salesforce.com/in/form/signup/freetrial-sales/) zu registrieren und zu erstellen [!DNL Salesforce] , wenn Sie noch keinen haben.

#### Eine verbundene App in konfigurieren [!DNL Salesforce] {#prerequisites-connected-app}

Zunächst müssen Sie eine [[!DNL Salesforce] vernetzte App](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) in [!DNL Salesforce] , wenn Sie noch keinen haben. [!DNL Salesforce CRM] nutzt die verbundene App für die Verbindung mit [!DNL Salesforce].

Aktivieren Sie als Nächstes [!DNL OAuth Settings for API Integration] für die [!DNL Salesforce connected app]. Siehe Abschnitt [[!DNL Salesforce]](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) Dokumentation für Anleitungen.

Stellen Sie außerdem sicher, dass die Variable [Bereiche](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) die unten aufgeführten Kriterien für die [!DNL Salesforce connected app].

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

Stellen Sie schließlich sicher, dass die Variable `password` -Zuschuss in Ihrer [!DNL Salesforce] -Konto. Siehe Abschnitt [!DNL Salesforce] [OAuth 2.0 Username-Password Flow für spezielle Szenarien](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_username_password_flow.htm&amp;type=5) Dokumentation, wenn Sie Anleitungen benötigen.

>[!IMPORTANT]
>
>Wenn [!DNL Salesforce] Kontoadministrator hat eingeschränkten Zugriff auf vertrauenswürdige IP-Bereiche, müssen Sie sie kontaktieren, um [Experience Platform-IPs](/help/destinations/catalog/streaming/ip-address-allow-list.md) auf die Zulassungsliste gesetzt. Siehe Abschnitt [!DNL Salesforce] [Einschränken des Zugriffs auf vertrauenswürdige IP-Bereiche für eine verbundene App](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) Dokumentation, wenn Sie zusätzliche Anleitungen benötigen.

#### Erstellen Sie benutzerdefinierte Felder in [!DNL Salesforce] {#prerequisites-custom-field}

Beim Aktivieren von Zielgruppen für die [!DNL Salesforce CRM] Ziel, müssen Sie einen Wert in die **[!UICONTROL Zuordnungs-ID]** -Feld für jede aktivierte Zielgruppe im **[Zielgruppenplanung](#schedule-segment-export-example)** Schritt.

[!DNL Salesforce CRM] benötigt diesen Wert, um Zielgruppen aus Experience Platform richtig zu lesen und zu interpretieren und ihren Zielgruppenstatus in [!DNL Salesforce]. Weitere Informationen finden Sie in der Experience Platform-Dokumentation für [Feldergruppe Zielgruppenzugehörigkeitsdetails](/help/xdm/field-groups/profile/segmentation.md) wenn Sie Anleitungen zum Zielgruppenstatus benötigen.

Für jede Zielgruppe, die Sie von Platform zu aktivieren [!DNL Salesforce CRM], müssen Sie ein benutzerdefiniertes Feld des Typs `Text Area (Long)` Innerhalb [!DNL Salesforce]. Sie können die Länge von Feldzeichen zwischen 256 und 131.072 Zeichen entsprechend Ihren Geschäftsanforderungen definieren. Siehe [!DNL Salesforce] [Benutzerdefinierte Feldtypen](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&amp;type=5) Dokumentationsseite für weitere Informationen zu benutzerdefinierten Feldtypen. Weitere Informationen finden Sie unter [!DNL Salesforce] Dokumentation zu [Benutzerdefinierte Felder erstellen](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) wenn Sie Hilfe bei der Felderstellung benötigen.

>[!IMPORTANT]
>
>Fügen Sie keine Leerzeichen in den Feldnamen ein. Verwenden Sie stattdessen den Unterstrich. `(_)` als Trennzeichen.
>Within [!DNL Salesforce] Sie müssen benutzerdefinierte Felder mit einer **[!UICONTROL Feldname]** genau mit dem Wert übereinstimmt, der in **[!UICONTROL Zuordnungs-ID]** für jedes aktivierte Platform-Segment. Der folgende Screenshot zeigt beispielsweise ein benutzerdefiniertes Feld mit dem Namen `crm_2_seg`. Fügen Sie beim Aktivieren einer Zielgruppe für dieses Ziel hinzu `crm_2_seg` as **[!UICONTROL Zuordnungs-ID]** , um Zielgruppen aus der Experience Platform in dieses benutzerdefinierte Feld zu füllen.

Ein Beispiel für die Erstellung eines benutzerdefinierten Felds in [!DNL Salesforce], *1. Schritt - Datentyp auswählen*, wie unten gezeigt:
![Salesforce-UI-Screenshot mit der Erstellung benutzerdefinierter Felder, Schritt 1: Auswählen des Datentyps.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-1.png)

Ein Beispiel für die Erstellung eines benutzerdefinierten Felds in [!DNL Salesforce], *Schritt 2: Eingabe der Details für das benutzerdefinierte Feld*, wie unten gezeigt:
![Salesforce UI-Screenshot mit der Erstellung benutzerdefinierter Felder, Schritt 2 - Geben Sie die Details für das benutzerdefinierte Feld ein.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-2.png)

>[!TIP]
>
>* So unterscheiden Sie zwischen benutzerdefinierten Feldern, die für Platform-Zielgruppen verwendet werden, und anderen benutzerdefinierten Feldern in [!DNL Salesforce] können Sie beim Erstellen des benutzerdefinierten Felds ein erkennbares Präfix oder Suffix einfügen. Beispiel: anstelle von `test_segment`, verwenden `Adobe_test_segment` oder `test_segment_Adobe`
>* Wenn bereits andere benutzerdefinierte Felder in erstellt wurden [!DNL Salesforce]können Sie denselben Namen wie das Platform-Segment verwenden, um die Zielgruppe in [!DNL Salesforce].

>[!NOTE]
>
>* Objekte in Salesforce sind auf 25 externe Felder beschränkt, siehe [Benutzerdefinierte Feldattribute](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
>* Diese Einschränkung bedeutet, dass Sie immer nur maximal 25 Experience Platform-Zielgruppenmitgliedschaften aktiv sein können.
>* Wenn Sie diese Grenze in Salesforce erreicht haben, müssen Sie die benutzerdefinierten Attribute aus Salesforce entfernen, die zum Speichern des Zielgruppenstatus für ältere Zielgruppen innerhalb von Experience Platform verwendet wurden, bevor eine neue **[!UICONTROL Zuordnungs-ID]** verwendet werden.

#### Sammeln von [!DNL Salesforce CRM]-Anmeldeinformationen {#gather-credentials}

Beachten Sie die folgenden Elemente, bevor Sie sich bei der [!DNL Salesforce CRM] Ziel:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| `Username` | Ihre [!DNL Salesforce] Benutzername des Kontos. | |
| `Password` | Ihre [!DNL Salesforce] Kontokennwort. | |
| `Security Token` | Ihre [!DNL Salesforce] Sicherheits-Token, das Sie später an das Ende Ihrer [!DNL Salesforce] Kennwort zum Erstellen einer verketteten Zeichenfolge, die als **[!UICONTROL Passwort]** when [beim Ziel authentifizieren](#authenticate).<br> Siehe Abschnitt [!DNL Salesforce] Dokumentation zu [Setzen des Sicherheits-Tokens](https://help.salesforce.com/s/articleView?id=sf.user_security_token.htm&amp;type=5) , um zu erfahren, wie Sie es mithilfe der [!DNL Salesforce] -Schnittstelle, wenn Sie nicht über das Sicherheits-Token verfügen. |  |
| `Custom Domain` | Ihre [!DNL Salesforce] Domänen-Präfix. <br> Siehe [[!DNL Salesforce] Dokumentation](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) , um zu erfahren, wie Sie diesen Wert aus dem [!DNL Salesforce] -Schnittstelle. | Wenn [!DNL Salesforce] Domäne ist<br> *`d5i000000isb4eak-dev-ed`.my.salesforce.com*,<br> benötigen Sie `d5i000000isb4eak-dev-ed` als Wert. |
| `Client ID` | Ihre Salesforce `Consumer Key`. <br> Siehe Abschnitt [[!DNL Salesforce] Dokumentation](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) , um zu erfahren, wie Sie diesen Wert aus dem [!DNL Salesforce] -Schnittstelle. | |
| `Client Secret` | Ihre Salesforce `Consumer Secret`. <br> Siehe Abschnitt [[!DNL Salesforce] Dokumentation](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) , um zu erfahren, wie Sie diesen Wert aus dem [!DNL Salesforce] -Schnittstelle. | |

### Leitplanken {#guardrails}

[!DNL Salesforce] gleicht Transaktionslasten durch Auferlegung von Anforderungs-, Rate- und Timeout-Beschränkungen aus. Siehe Abschnitt [API-Anforderungsbeschränkungen und -zuordnungen](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) für Details.

Wenn [!DNL Salesforce] Kontoadministrator hat IP-Einschränkungen erzwungen. Sie müssen [Experience Platform-IP-Adressen](/help/destinations/catalog/streaming/ip-address-allow-list.md) auf [!DNL Salesforce] Vertrauenswürdige IP-Bereiche der Konten. Siehe Abschnitt [!DNL Salesforce] [Einschränken des Zugriffs auf vertrauenswürdige IP-Bereiche für eine verbundene App](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) Dokumentation, wenn Sie zusätzliche Anleitungen benötigen.

>[!IMPORTANT]
>
>Wann [Segmente aktivieren](#activate) Sie müssen zwischen *Kontakt* oder *Lead* Typen. Sie müssen sicherstellen, dass Ihre Zielgruppen entsprechend dem ausgewählten Typ über das entsprechende Daten-Mapping verfügen.

## Unterstützte Identitäten {#supported-identities}

[!DNL Salesforce CRM] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| `SalesforceId` | Die [!DNL Salesforce CRM] Kennung für die Kontakt- oder Lead-Identitäten, die Sie über Ihr Segment exportieren oder aktualisieren. | Obligatorisch |

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern *(z. B.: E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Jeder Zielgruppenstatus in [!DNL Salesforce CRM] wird mit dem entsprechenden Zielgruppenstatus von Platform aktualisiert, basierend auf dem **[!UICONTROL Zuordnungs-ID]** Wert, der während der [Zielgruppenplanung](#schedule-segment-export-example) Schritt.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | <ul><li>Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** nach [!DNL Salesforce CRM]. Alternativ können Sie es unter der **[!UICONTROL CRM]**-Kategorie finden.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder unten aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**. Siehe Abschnitt [Gather [!DNL Salesforce CRM] Anmeldeinformationen](#gather-credentials) für Hinweise.
| Berechtigung | Beschreibung | | — | — | | **[!UICONTROL Benutzername]** | Ihre [!DNL Salesforce] Benutzername des Kontos. | | **[!UICONTROL Passwort]** | Eine verkettete Zeichenfolge, die aus [!DNL Salesforce] Passwort des Kontos angehängt mit Ihrem [!DNL Salesforce] Sicherheitstoken.<br>Der verkettete Wert hat die Form `{PASSWORD}{TOKEN}`.<br> Beachten Sie, dass Sie keine geschweiften Klammern oder Leerzeichen verwenden.<br>Beispiel: Wenn [!DNL Salesforce] Kennwort ist `MyPa$$w0rd123` und [!DNL Salesforce] Sicherheits-Token `TOKEN12345....0000`, der verkettete Wert, den Sie im **[!UICONTROL Passwort]** Feld ist `MyPa$$w0rd123TOKEN12345....0000`. | | **[!UICONTROL Benutzerdefinierte Domäne]** | Ihre [!DNL Salesforce] Domänen-Präfix. <br>Beispiel: Ihre Domäne *`d5i000000isb4eak-dev-ed`.my.salesforce.com*, müssen Sie `d5i000000isb4eak-dev-ed` als Wert. | | **[!UICONTROL Client-ID]** | Ihre [!DNL Salesforce] vernetzte App `Consumer Key`. | | **[!UICONTROL Client Secret]** | Ihre [!DNL Salesforce] vernetzte App `Consumer Secret`. |

![Screenshot der Platform-Benutzeroberfläche, auf dem die Authentifizierung gezeigt wird.](../../assets/catalog/crm/salesforce/authenticate-destination.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche eine **[!UICONTROL Verbunden]** Status mit einem grünen Häkchen angezeigt wird, können Sie dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Salesforce-ID-Typ]**:
   * Auswählen **[!UICONTROL Kontakt]** ob die Identitäten, die Sie exportieren oder aktualisieren möchten, vom Typ *Kontakt*.
   * Auswählen **[!UICONTROL Lead]** ob die Identitäten, die Sie exportieren oder aktualisieren möchten, vom Typ *Lead*.

![Screenshot der Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/crm/salesforce/destination-details.png)

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

Um Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an das [!DNL Salesforce CRM]-Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodell (XDM) in Ihrem Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen.

In der Variablen **[!UICONTROL Zielfeld]** sollte genau wie in der Tabelle der Attributzuordnungen beschrieben benannt werden, da diese Attribute den Anfragetext bilden.

In der Variablen **[!UICONTROL Quellfeld]** keine solchen Einschränkungen befolgen. Sie können sie nach Bedarf zuordnen. Stellen Sie jedoch sicher, dass das Format der Eingabedaten entsprechend der Variablen [[!DNL Salesforce] Dokumentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5). Wenn die Eingabedaten nicht gültig sind, wird der Aktualisierungsaufruf an [!DNL Salesforce] schlägt fehl und Ihre Kontakte/Leads werden nicht aktualisiert.

Um Ihre XDM-Felder den [!DNL (API) Salesforce CRM]-Zielfeldern korrekt zuzuordnen, führen Sie die folgenden Schritte aus:

1. Im **[!UICONTROL Zuordnung]** Schritt auswählen **[!UICONTROL Neues Mapping hinzufügen]**, wird eine neue Zuordnungszeile auf dem Bildschirm angezeigt.
   ![Beispiel-Screenshot der Platform-Benutzeroberfläche für „Neue Zuordnung hinzufügen“.](../../assets/catalog/crm/salesforce/add-new-mapping.png)
1. Im **[!UICONTROL Quellfeld auswählen]** Fenster, wählen Sie die **[!UICONTROL Attribute auswählen]** und wählen Sie das XDM-Attribut oder die **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie eine Identität.
1. Im **[!UICONTROL Zielgruppenfeld auswählen]** Fenster, wählen Sie die **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie eine Identität oder **[!UICONTROL Benutzerdefinierte Attribute auswählen]** und wählen Sie ein Attribut aus oder definieren Sie eines mithilfe der **[!UICONTROL Attributname]** nach Bedarf. Siehe Abschnitt [[!DNL Salesforce CRM] Dokumentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5) für Anleitungen zu unterstützten Attributen.
   * Wiederholen Sie diese Schritte, um die folgenden Zuordnungen zwischen Ihrem XDM-Profilschema und [!DNL (API) Salesforce CRM]:

   **Arbeiten mit Kontakten**

   * Wenn Sie mit *Kontakte* in Ihrem Segment finden Sie in der Objektreferenz in Salesforce für [Kontakt](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) , um Zuordnungen für die zu aktualisierenden Felder zu definieren.
   * Sie können Pflichtfelder identifizieren, indem Sie nach dem Wort suchen *Erforderlich*, was in den Feldbeschreibungen im obigen Link erwähnt wird.
   * Fügen Sie je nach den Feldern, die Sie exportieren oder aktualisieren möchten, Zuordnungen zwischen Ihrem XDM-Profilschema und [!DNL (API) Salesforce CRM]: |Quellfeld|Zielfeld| Hinweise | | — | — | — | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. Nachname des Kontakts mit bis zu 80 Zeichen. |\
     |`xdm: person.name.firstName`|`Attribute: FirstName`| Vorname des Kontakts mit bis zu 40 Zeichen. | |`xdm: personalEmail.address`|`Attribute: Email`| Die E-Mail-Adresse des Kontakts. |

   * Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Zuordnungen:
     ![Beispiel-Screenshot der Platform-Benutzeroberfläche mit Ziel-Zuordnungen.](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   **Arbeiten mit Leads**

   * Wenn Sie mit *Leads* in Ihrem Segment finden Sie in der Objektreferenz in Salesforce für [Lead](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) , um Zuordnungen für die zu aktualisierenden Felder zu definieren.
   * Sie können Pflichtfelder identifizieren, indem Sie nach dem Wort suchen *Erforderlich*, was in den Feldbeschreibungen im obigen Link erwähnt wird.
   * Fügen Sie je nach den Feldern, die Sie exportieren oder aktualisieren möchten, Zuordnungen zwischen Ihrem XDM-Profilschema und [!DNL (API) Salesforce CRM]: |Quellfeld|Zielfeld| Hinweise | | — | — | — | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. Nachname des Leads mit bis zu 80 Zeichen. |\
     |`xdm: b2b.companyName`|`Attribute: Company`| `Mandatory`. Die Führung ist dabei. | |`xdm: personalEmail.address`|`Attribute: Email`| Die E-Mail-Adresse des Leads. |

   * Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Zuordnungen:
     ![Beispiel-Screenshot der Platform-Benutzeroberfläche mit Ziel-Zuordnungen.](../../assets/catalog/crm/salesforce/mappings-leads.png)

Wenn Sie die Zuordnungen für Ihre Zielverbindung bereitgestellt haben, wählen Sie **[!UICONTROL Nächste]**.

### Zielgruppenexport und Beispiel planen {#schedule-segment-export-example}

Bei der Durchführung der [Zielgruppenexport planen](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) Schritt: Sie müssen Zielgruppen, die von Platform aktiviert werden, manuell dem entsprechenden benutzerdefinierten Feld in [!DNL Salesforce].

Wählen Sie dazu jedes Segment aus und geben Sie dann den benutzerdefinierten Feldnamen aus [!DNL Salesforce] im [!DNL Salesforce CRM] **[!UICONTROL Zuordnungs-ID]** -Feld. Siehe Abschnitt [Erstellen Sie benutzerdefinierte Felder in [!DNL Salesforce]](#prerequisites-custom-field) Abschnitt mit Anleitungen und Best Practices zum Erstellen benutzerdefinierter Felder in [!DNL Salesforce].

Wenn beispielsweise Ihre [!DNL Salesforce] benutzerdefiniertes Feld ist `crm_2_seg`, geben Sie diesen Wert in der [!DNL Salesforce CRM] **[!UICONTROL Zuordnungs-ID]** , um Zielgruppen aus der Experience Platform in dieses benutzerdefinierte Feld zu füllen.

Ein Beispiel für ein benutzerdefiniertes Feld aus [!DNL Salesforce] ist unten dargestellt:
![[!DNL Salesforce] UI-Screenshot mit benutzerdefiniertem Feld.](../../assets/catalog/crm/salesforce/salesforce-custom-field.png)

Ein Beispiel, das die Position der [!DNL Salesforce CRM] **[!UICONTROL Zuordnungs-ID]** ist unten dargestellt:
![Screenshot-Beispiel der Platform-Benutzeroberfläche mit der Option Zielgruppenexport planen](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

Wie oben gezeigt, [!DNL Salesforce] **[!UICONTROL Feldname]** exakt mit dem Wert übereinstimmt, der in [!DNL Salesforce CRM] **[!UICONTROL Zuordnungs-ID]**.

Je nach Anwendungsfall können alle aktivierten Zielgruppen demselben [!DNL Salesforce] benutzerdefiniertes Feld oder anders **[!UICONTROL Feldname]** in [!DNL Salesforce CRM]. Ein typisches Beispiel, das auf dem oben gezeigten Bild basiert, könnte sein.
| [!DNL Salesforce CRM] Segmentname | [!DNL Salesforce] **[!UICONTROL Feldname]** | [!DNL Salesforce CRM] **[!UICONTROL Zuordnungs-ID]** | | — | — | — | | crm_1_seg | `crm_1_seg` | `crm_1_seg` | | crm_2_seg | `crm_2_seg` | `crm_2_seg` |

Wiederholen Sie diesen Abschnitt für jedes aktivierte Platform-Segment.

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Wählen Sie **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** aus, um zur Liste der Ziele zu navigieren.
   ![Screenshot der Platform-Benutzeroberfläche mit den Durchsuchen-Zielen.](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. Wählen Sie das Ziel aus und überprüfen Sie, ob der Status **[!UICONTROL aktiviert]** ist.
   ![Screenshot der Platform-Benutzeroberfläche mit Zielen der Datenflussausführung.](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. Wechseln Sie zu **[!UICONTROL Aktivierungsdaten]** und wählen Sie einen Zielgruppennamen aus.
   ![Beispiel-Screenshot der Platform-Benutzeroberfläche mit Daten zur Aktivierung von Zielen.](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. Überwachen Sie die Zielgruppenzusammenfassung und stellen Sie sicher, dass die Anzahl der Profile der im Segment erstellten Anzahl entspricht.
   ![Beispiel-Screenshot der Platform-Benutzeroberfläche mit Segment.](../../assets/catalog/crm/salesforce/segment.png)

1. Melden Sie sich schließlich bei der Salesforce-Website an und überprüfen Sie, ob die Profile der Audience hinzugefügt oder aktualisiert wurden.

   **Arbeiten mit Kontakten**

   * Wenn Sie *Kontakte* Navigieren Sie in Ihrem Platform-Segment zu der **[!DNL Apps]** > **[!DNL Contacts]** Seite.
     ![Salesforce CRM-Screenshot mit der Seite Kontakte mit den Profilen aus dem Segment.](../../assets/catalog/crm/salesforce/contacts.png)

   * Wählen Sie eine *Kontakt* und überprüfen Sie, ob die Felder aktualisiert wurden. Sie können sehen, dass jeder Zielgruppenstatus in [!DNL Salesforce CRM] mit dem entsprechenden Zielgruppenstatus von Platform aktualisiert wurde, basierend auf dem **[!UICONTROL Zuordnungs-ID]** Wert, der während der [Zielgruppenplanung](#schedule-segment-export-example).
     ![Salesforce CRM-Screenshot mit der Seite Kontaktdetails mit aktualisiertem Zielgruppenstatus.](../../assets/catalog/crm/salesforce/contact-info.png)

   **Arbeiten mit Leads**

   * Wenn Sie *Leads* in Ihrem Platform-Segment und navigieren Sie dann zum **[!DNL Apps]** > **[!DNL Leads]** Seite.
     ![Salesforce CRM-Screenshot mit der Leads-Seite mit den Profilen aus dem Segment.](../../assets/catalog/crm/salesforce/leads.png)

   * Wählen Sie eine *Lead* und überprüfen Sie, ob die Felder aktualisiert wurden. Sie können sehen, dass jeder Zielgruppenstatus in [!DNL Salesforce CRM] mit dem entsprechenden Zielgruppenstatus von Platform aktualisiert wurde, basierend auf dem **[!UICONTROL Zuordnungs-ID]** Wert, der während der [Zielgruppenplanung](#schedule-segment-export-example).
     ![Salesforce CRM-Screenshot mit der Seite Lead-Details mit aktualisiertem Zielgruppenstatus.](../../assets/catalog/crm/salesforce/lead-info.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

### Unbekannte Fehler beim Senden von Ereignissen an das Ziel {#unknown-errors}

* Beim Überprüfen eines Datenfluss-Ablaufs wird möglicherweise die folgende Fehlermeldung angezeigt: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![Screenshot der Platform-Benutzeroberfläche mit Fehlermeldung.](../../assets/catalog/crm/salesforce/error.png)

   * Um diesen Fehler zu beheben, überprüfen Sie, ob die Variable **[!UICONTROL Zuordnungs-ID]** die Sie im Aktivierungs-Workflow für das [!DNL Salesforce CRM] Das Ziel stimmt genau mit dem Wert des benutzerdefinierten Feldtyps überein, den Sie in [!DNL Salesforce]. Siehe Abschnitt [Erstellen Sie benutzerdefinierte Felder in [!DNL Salesforce]](#prerequisites-custom-field) für Hinweise.

* Beim Aktivieren eines Segments erhalten Sie möglicherweise eine Fehlermeldung: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Wenden Sie sich zur Behebung dieses Fehlers an Ihren [!DNL Salesforce] Kontoadministrator zum Hinzufügen [Experience Platform-IP-Adressen](/help/destinations/catalog/streaming/ip-address-allow-list.md) auf [!DNL Salesforce] Vertrauenswürdige IP-Bereiche der Konten. Siehe Abschnitt [!DNL Salesforce] [Einschränken des Zugriffs auf vertrauenswürdige IP-Bereiche für eine verbundene App](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) Dokumentation, wenn Sie zusätzliche Anleitungen benötigen.

## Zusätzliche Ressourcen {#additional-resources}

Zusätzliche nützliche Informationen aus dem [Salesforce-Entwicklerportal](https://developer.salesforce.com/) unten steht:
* [Schnellstart](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [Datensatz erstellen](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [Benutzerspezifische Empfehlungszielgruppen](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [Verwenden von Composite-Ressourcen](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* Dieses Ziel nutzt die [Mehrere Datensätze aktualisieren](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) API anstelle der [Einzelne Datensätze hochladen](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) API-Aufruf.