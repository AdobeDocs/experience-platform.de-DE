---
keywords: crm;CRM;crm-Ziele;Salesforce crm;Salesforce crm-Ziel
title: Salesforce CRM-Verbindung
description: Mit dem Salesforce CRM-Ziel können Sie Ihre Kontodaten exportieren und im Salesforce CRM für Ihre geschäftlichen Anforderungen aktivieren.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: b243a5f88cadc238ac3edd3bf45a54564598bbf0
workflow-type: tm+mt
source-wordcount: '2256'
ht-degree: 4%

---

# [!DNL Salesforce CRM]-Verbindung

## Übersicht {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) ist eine beliebte CRM-Plattform (Customer Relationship Management) und unterstützt Folgendes:

* [Leads](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) - Ein Lead ist der Name einer Person oder Firma, die an den von Ihnen verkauften Produkten oder Dienstleistungen interessiert sein kann (oder nicht).
* [Kontakte](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) - Ein Kontakt ist eine Person, mit der einer Ihrer Mitarbeiter eine Beziehung aufgebaut und als potenzieller Kunde qualifiziert hat.

Diese [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt die [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm)unterstützt, die beide oben beschriebenen Profiltypen unterstützt.

Wann [Aktivieren von Segmenten](#activate)können Sie zwischen Leads oder Kontakten wählen und Attribute und Segmentdaten in aktualisieren. [!DNL Salesforce CRM].

[!DNL Salesforce CRM] verwendet OAuth 2 mit Password Grant als Authentifizierungsmechanismus für die Kommunikation mit der Salesforce REST API. Anweisungen zur Authentifizierung bei Ihrem [!DNL Salesforce CRM] -Instanz weiter unten im [An Ziel authentifizieren](#authenticate) Abschnitt.

## Anwendungsbeispiele {#use-cases}

Als Marketer können Sie Ihren Benutzern personalisierte Erlebnisse auf der Basis von Attributen aus ihren Adobe Experience Platform-Profilen bereitstellen. Sie können Segmente aus Ihren Offline-Daten erstellen und an Salesforce CRM senden, um sie in den Feeds der Benutzer anzuzeigen, sobald Segmente und Profile in Adobe Experience Platform aktualisiert wurden.

## Voraussetzungen {#prerequisites}

### Voraussetzungen für die Experience Platform {#prerequisites-in-experience-platform}

Bevor Sie Daten für das Salesforce CRM-Ziel aktivieren, benötigen Sie eine [schema](/help/xdm/schema/composition.md), [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) erstellt in [!DNL Experience Platform].

### Voraussetzungen in [!DNL Salesforce CRM] {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen in [!DNL Salesforce CRM], um Daten von Platform in Ihr Salesforce-Konto zu exportieren:

#### Sie benötigen ein Salesforce-Konto {#prerequisites-account}

Gehe zu Salesforce [Testversion](https://www.salesforce.com/in/form/signup/freetrial-sales/) -Seite, um sich zu registrieren und ein Salesforce-Konto zu erstellen, falls noch keines vorhanden ist.

#### Eine verbundene App konfigurieren {#prerequisites-connected-app}

Als Nächstes müssen Sie eine [verbundene App](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) innerhalb Ihres Salesforce-Kontos, falls noch keines vorhanden ist.

Stellen Sie in der verbundenen App sicher, dass [OAuth-Einstellungen](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) aktiviert ist.

Stellen Sie außerdem sicher, dass [Bereiche](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) werden ausgewählt.

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

#### Benutzerdefiniertes Feld in Salesforce erstellen {#prerequisites-custom-field}

Benutzerdefiniertes Feld vom Typ erstellen `Text Area Long`, die Experience Platform verwendet, um den Segmentstatus in [!DNL Salesforce CRM].
Weitere Informationen finden Sie in der Salesforce-Dokumentation unter [Benutzerdefinierte Felder erstellen](https://help.salesforce.com/s/articleView?id=sf.adding_fields.htm&amp;type=5) wenn Sie zusätzliche Anleitungen benötigen.

>[!IMPORTANT]
>
>Stellen Sie sicher, dass der Feldname keine Leerzeichen enthält. Verwenden Sie stattdessen den Unterstrich. `(_)` als Trennzeichen.

>[!NOTE]
>
>* Objekte in Salesforce sind auf 25 externe Felder beschränkt, siehe [Benutzerdefinierte Feldattribute](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
>* Diese Einschränkung bedeutet, dass Sie immer nur maximal 25 Experience Platformen Segmentmitgliedschaften aktiv sein können.
>* Wenn Sie diese Grenze in Salesforce erreicht haben, müssen Sie das benutzerdefinierte Attribut aus Salesforce entfernen, mit dem der Segmentstatus für ältere Segmente in Experience Platform vor einer neuen gespeichert wurde. **[!UICONTROL Zuordnungs-ID]** verwendet werden.


Weitere Informationen finden Sie in der Dokumentation zu Adobe Experience Platform . [Feldergruppe Segmentzugehörigkeitsdetails](/help/xdm/field-groups/profile/segmentation.md) , wenn Sie Anleitungen zum Segmentstatus benötigen.

#### Salesforce-Anmeldeinformationen sammeln {#gather-credentials}

Beachten Sie die folgenden Elemente, bevor Sie sich bei der [!DNL Salesforce CRM] Ziel:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| <ul><li>Salesforce-Domänenpräfix</li></ul> | Siehe [Salesforce-Domänenpräfix](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) für zusätzliche Leitlinien. | <ul><li>Wenn Ihre Domäne wie folgt lautet, benötigen Sie den hervorgehobenen Wert.<br> <i>`d5i000000isb4eak-dev-ed`.my.salesforce.com</i></li></ul> |
| <ul><li>Consumer Key</li><li>Verbrauchergeheimnis</li></ul> | Siehe Abschnitt [Salesforce-Dokumentation](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) wenn Sie zusätzliche Anleitungen benötigen. | <ul><li>r23kxxxxxxxx0z05xxxxxx</code></li><li>ipxxxxxxxxxxT4xxxxxxxxxxxx</code></li></ul> |

### Limits {#guardrails}

Salesforce gleicht Transaktionslasten durch Auferlegung von Anforderungs-, Rate- und Timeout-Beschränkungen aus. Siehe Abschnitt [API-Anforderungsbeschränkungen und -zuordnungen](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) für Details.

>[!IMPORTANT]
>
>Wann [Aktivieren von Segmenten](#activate) Sie müssen zwischen *Kontakt* oder *Lead* Typen. Sie müssen sicherstellen, dass Ihre Segmente entsprechend dem ausgewählten Typ über das entsprechende Daten-Mapping verfügen.

## Unterstützte Identitäten {#supported-identities}

[!DNL Salesforce CRM] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Weitere Informationen [identities](/help/identity-service/namespaces.md).

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| `SalesforceId` | Die [!DNL Salesforce CRM] Kennung für die Kontakt- oder Lead-Identitäten, die Sie über Ihr Segment exportieren oder aktualisieren. | Obligatorisch |

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern *(z. B.: E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Jeder Segmentstatus in [!DNL Salesforce CRM] wird mit dem entsprechenden Segmentstatus von Platform aktualisiert, basierend auf dem **[!UICONTROL Zuordnungs-ID]** Wert, der während der [Segmentplanung](#schedule-segment-export-example) Schritt.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | <ul><li>Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Within **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** Suchen nach [!DNL Salesforce CRM]. Alternativ können Sie sie unter der **[!UICONTROL CRM]** Kategorie.

### An Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**.

![Screenshot der Platform-Benutzeroberfläche, in dem die Authentifizierung gezeigt wird.](../../assets/catalog/crm/salesforce/authenticate-destination.png)

* **[!UICONTROL Passwort]**: Ihr Salesforce-Kontokennwort.
* **[!UICONTROL Benutzerdefinierte Domäne]**: Ihre Salesforce-Domäne.
* **[!UICONTROL Client-ID]**: Kundenschlüssel der mit Salesforce verbundenen App.
* **[!UICONTROL Client Secret]**: Ihre mit Salesforce verbundene App - Kundengeheimnis.
* **[!UICONTROL Benutzername]**: Ihr Salesforce-Konto-Benutzername.

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche eine **[!UICONTROL Verbunden]** Status mit einem grünen Häkchen anzeigen, können Sie mit dem nächsten Schritt fortfahren.

### Zieldetails ausfüllen {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
![Screenshot der Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/crm/salesforce/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Salesforce-ID-Typ]**: Auswählen **[!UICONTROL Kontakt]** ob die Identitäten, die Sie exportieren oder aktualisieren möchten, vom Typ *Kontakt*. Auswählen **[!UICONTROL Lead]** ob die Identitäten, die Sie exportieren oder aktualisieren möchten, vom Typ *Lead*.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen über den Status des Datenflusses an Ihr Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
>
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

So senden Sie Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an die [!DNL Salesforce CRM] Ziel, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodell (XDM) in Ihrem Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen. So ordnen Sie Ihre XDM-Felder korrekt der [!DNL Salesforce CRM] Führen Sie die folgenden Schritte aus:

1. Im **[!UICONTROL Zuordnung]** Schritt auswählen **[!UICONTROL Neues Mapping hinzufügen]**, wird eine neue Zuordnungszeile auf dem Bildschirm angezeigt.
   ![Screenshot der Platform-Benutzeroberfläche zum Hinzufügen einer neuen Zuordnung.](../../assets/catalog/crm/salesforce/add-new-mapping.png)

1. Im **[!UICONTROL Quellfeld auswählen]** Fenster, wählen Sie die **[!UICONTROL Identitäts-Namespace auswählen]** oder **[!UICONTROL Attribute auswählen]** Kategorie und wählen Sie `crmID`.
   ![Screenshot-Beispiel der Platform-Benutzeroberfläche für die Quellzuordnung.](../../assets/catalog/crm/salesforce/source-mapping.png)

1. Im **[!UICONTROL Zielgruppenfeld auswählen]** Fenster, wählen Sie die **[!UICONTROL Identitäts-Namespace auswählen]** Kategorie und wählen Sie `SalesforceId`.
   ![Screenshot der Platform-Benutzeroberfläche mit Target-Zuordnung für SalesforceId.](../../assets/catalog/crm/salesforce/target-mapping-salesforceid.png)

   * Fügen Sie die folgende Zuordnung zwischen Ihrem XDM-Profilschema und Ihrem [!DNL Salesforce CRM] instance:
   | XDM-Profilschema | [!DNL Salesforce CRM] Instanz | Obligatorisch |
   |---|---|---|
   | `crmID` | `SalesforceId` | Ja |

   * **[!UICONTROL Benutzerdefinierte Attribute auswählen]**: Wählen Sie diese Option aus, um Ihr Quellfeld einem benutzerdefinierten Attribut zuzuordnen, das Sie in der Variablen **[!UICONTROL Attributname]** -Feld. Siehe Abschnitt [[!DNL Salesforce CRM] Dokumentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5) für Anleitungen zu unterstützten Attributen.
      ![Screenshot der Platform-Benutzeroberfläche mit Target-Zuordnung für LastName.](../../assets/catalog/crm/salesforce/target-mapping-lastname.png)

   * Wenn Sie mit *Kontakte* in Ihrem Segment finden Sie in der Objektreferenz in Salesforce für [Kontakt](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) , um Zuordnungen für die zu aktualisierenden Felder zu definieren.
   * Sie können Pflichtfelder identifizieren, indem Sie nach dem Wort suchen *Erforderlich*, was in den Feldbeschreibungen im obigen Link erwähnt wird.
   * Fügen Sie je nach den Feldern, die Sie exportieren oder aktualisieren möchten, Zuordnungen zwischen Ihrem XDM-Profilschema und Ihrem [!DNL Salesforce CRM] instance:

   | XDM-Profilschema | [!DNL Salesforce CRM] Instanz | Anmerkungen |
   | --- | --- | --- |
   | `person.name.lastName` | `LastName` | `Required`. Nachname des Kontakts mit bis zu 80 Zeichen. |
   | `person.name.firstName` | `FirstName` | Vorname des Kontakts mit einer Länge von bis zu 40 Zeichen. |
   | `personalEmail.address` | `Email` | Die E-Mail-Adresse des Kontakts. |

   * Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Zuordnungen:
      ![Screenshot der Platform-Benutzeroberfläche mit Target-Zuordnungen.](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   * Wenn Sie mit *Leads* in Ihrem Segment finden Sie in der Objektreferenz in Salesforce für [Lead](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) , um Zuordnungen für die zu aktualisierenden Felder zu definieren.
   * Sie können Pflichtfelder identifizieren, indem Sie nach dem Wort suchen *Erforderlich*, was in den Feldbeschreibungen im obigen Link erwähnt wird.
   * Fügen Sie je nach den Feldern, die Sie exportieren oder aktualisieren möchten, Zuordnungen zwischen Ihrem XDM-Profilschema und Ihrem [!DNL Salesforce CRM] instance:

   | XDM-Profilschema | [!DNL Salesforce CRM] Instanz | Anmerkungen |
   | --- | --- | --- |
   | `person.name.lastName` | `LastName` | `Required`. Nachname des Kontakts mit bis zu 80 Zeichen. |
   | `b2b.companyName` | `Company` | `Required`. Die Führung ist dabei. |
   | `personalEmail.address` | `Email` | Die E-Mail-Adresse des Kontakts. |

   * Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Zuordnungen:
      ![Screenshot der Platform-Benutzeroberfläche mit Target-Zuordnungen.](../../assets/catalog/crm/salesforce/mappings-leads.png)




### Segmentexport planen, Beispiel {#schedule-segment-export-example}

Bei der Durchführung der [Segmentexport planen](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) Schritt müssen Sie Platform-Segmente manuell dem benutzerdefinierten Feldattribut in Salesforce zuordnen.

Wählen Sie dazu jedes Segment aus und geben Sie dann das entsprechende benutzerdefinierte Feldattribut aus Salesforce in das Feld **[!UICONTROL Zuordnungs-ID]** -Feld.

>[!IMPORTANT]
>
>* Der für die **[!UICONTROL Zuordnungs-ID]** sollte genau mit dem Namen des benutzerdefinierten Feldattributs übereinstimmen, das in Salesforce erstellt wurde.
>* Stellen Sie sicher, dass der Name des von Ihnen in Salesforce erstellten benutzerdefinierten Feldattributs nicht das Leerzeichen verwendet.


Nachfolgend finden Sie ein Beispiel:
![Screenshot-Beispiel der Platform-Benutzeroberfläche mit der Option Segmentexport planen .](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

## Datenexport überprüfen {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Auswählen **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** um zur Liste der Ziele zu navigieren.
   ![Screenshot der Platform-Benutzeroberfläche mit den Browse-Zielen.](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. Wählen Sie das Ziel aus und überprüfen Sie, ob der Status **[!UICONTROL enabled]**.
   ![Screenshot der Platform-Benutzeroberfläche mit dem Ziel-Datenfluss.](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. Wechseln Sie zu **[!UICONTROL Aktivierungsdaten]** und wählen Sie einen Segmentnamen aus.
   ![Screenshot-Beispiel der Platform-Benutzeroberfläche mit Zielen-Aktivierungsdaten.](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. Überwachen Sie die Segmentzusammenfassung und stellen Sie sicher, dass die Anzahl der Profile der im Segment erstellten Anzahl entspricht.
   ![Beispiel für einen Screenshot der Platform-Benutzeroberfläche mit Segment.](../../assets/catalog/crm/salesforce/segment.png)

1. Melden Sie sich schließlich bei der Salesforce-Website an und überprüfen Sie, ob die Profile aus dem Segment hinzugefügt oder aktualisiert wurden.
   * Wenn Sie *Kontakte* Navigieren Sie in Ihrem Platform-Segment zu der **[!DNL Apps]** > **[!DNL Contacts]** Seite.
      ![Salesforce CRM-Screenshot mit der Seite Kontakte mit den Profilen aus dem Segment.](../../assets/catalog/crm/salesforce/contacts.png)

   * Wählen Sie eine *Kontakt* und überprüfen Sie, ob die Felder aktualisiert wurden. Sie können sehen, dass jeder Segmentstatus in [!DNL Salesforce CRM] mit dem entsprechenden Segmentstatus von Platform aktualisiert wurde, basierend auf dem **[!UICONTROL Zuordnungs-ID]** Wert, der während der [Segmentplanung](#schedule-segment-export-example).
      ![Salesforce CRM-Screenshot mit der Seite Kontaktdetails mit aktualisiertem Segmentstatus.](../../assets/catalog/crm/salesforce/contact-info.png)

   * Wenn Sie *Leads* in Ihrem Platform-Segment und navigieren Sie dann zum **[!DNL Apps]** > **[!DNL Leads]** Seite.
      ![Salesforce CRM-Screenshot mit der Leads-Seite mit den Profilen aus dem Segment.](../../assets/catalog/crm/salesforce/leads.png)

   * Wählen Sie eine *Lead* und überprüfen Sie, ob die Felder aktualisiert wurden. Sie können sehen, dass jeder Segmentstatus in [!DNL Salesforce CRM] mit dem entsprechenden Segmentstatus von Platform aktualisiert wurde, basierend auf dem **[!UICONTROL Zuordnungs-ID]** Wert, der während der [Segmentplanung](#schedule-segment-export-example).
      ![Salesforce CRM-Screenshot mit der Seite Lead-Details mit aktualisiertem Segmentstatus.](../../assets/catalog/crm/salesforce/lead-info.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

### Unbekannte Fehler beim Senden von Ereignissen an das Ziel {#unknown-errors}

Wenn Sie beim Überprüfen eines Datenflusses die folgende Fehlermeldung erhalten: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

![Screenshot der Platform-Benutzeroberfläche mit Fehlermeldung.](../../assets/catalog/crm/salesforce/error.png)

Um diesen Fehler zu beheben, überprüfen Sie, ob die Variable **[!UICONTROL Zuordnungs-ID]** Sie haben [!DNL Salesforce CRM] für Ihr Platform-Segment gültig ist und in [!DNL Salesforce CRM].

## Weitere Ressourcen {#additional-resources}

Zusätzliche nützliche Informationen aus dem [Salesforce-Entwicklerportal](https://developer.salesforce.com/) unten steht:
* [Schnellstart](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [Datensatz erstellen](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [Benutzerspezifische Empfehlungszielgruppen](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [Verwenden von Composite-Ressourcen](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* Dieses Ziel nutzt die [Mehrere Datensätze aktualisieren](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) API anstelle der [Einzelne Datensätze hochladen](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) API-Aufruf.