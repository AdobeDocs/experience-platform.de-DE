---
keywords: crm;CRM;crm-Ziele;Salesforce crm;Salesforce crm-Ziel
title: Salesforce CRM-Verbindung
description: Mit dem Salesforce CRM-Ziel können Sie Ihre Kontodaten exportieren und im Salesforce CRM für Ihre geschäftlichen Anforderungen aktivieren.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: 7d8b25b25b53edd7de836fc508de15cfa2a5a3a2
workflow-type: tm+mt
source-wordcount: '1730'
ht-degree: 6%

---

# [!DNL Salesforce CRM]-Verbindung

## Übersicht {#overview}

[Salesforce CRM](https://www.salesforce.com/) ist eine beliebte CRM-Plattform (Customer Relationship Management).

Diese [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt die [Salesforce REST API](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts), mit dem Sie Identitäten innerhalb eines Segments in Salesforce CRM aktualisieren können.

Salesforce CRM verwendet OAuth 2 mit Password Grant als Authentifizierungsmechanismus für die Kommunikation mit der Salesforce REST API. Anweisungen zur Authentifizierung für Ihre Salesforce CRM-Instanz finden Sie weiter unten im Abschnitt [An Ziel authentifizieren](#authenticate) Abschnitt.

## Anwendungsbeispiele {#use-cases}

Als Marketer können Sie Ihren Benutzern personalisierte Erlebnisse auf der Basis von Attributen aus ihren Adobe Experience Platform-Profilen bereitstellen. Sie können Segmente aus Ihren Offline-Daten erstellen und an Salesforce CRM senden, um sie in den Feeds der Benutzer anzuzeigen, sobald Segmente und Profile in Adobe Experience Platform aktualisiert wurden.

## Voraussetzungen {#prerequisites}

### Voraussetzungen für die Experience Platform {#prerequisites-in-experience-platform}

Bevor Sie Daten für das Salesforce CRM-Ziel aktivieren, benötigen Sie eine [schema](/help/xdm/schema/composition.md), [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) erstellt in [!DNL Experience Platform].

### Voraussetzungen in Salesforce CRM {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen in Salesforce, um Daten von Platform in Ihr Salesforce-Konto zu exportieren:

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

Benutzerdefiniertes Feld vom Typ erstellen `Text Area Long` welche Experience Platform verwendet, um den Segmentstatus im Salesforce CRM zu aktualisieren.
Weitere Informationen finden Sie in der Salesforce-Dokumentation unter [Benutzerdefinierte Felder erstellen](https://help.salesforce.com/s/articleView?id=sf.adding_fields.htm&amp;type=5) wenn Sie zusätzliche Anleitungen benötigen.

>[!IMPORTANT]
>
> Stellen Sie sicher, dass der Feldname keine Leerzeichen enthält. Verwenden Sie stattdessen den Unterstrich. `(_)` als Trennzeichen.

>[!NOTE]
>
> * Objekte in Salesforce sind auf 25 externe Felder beschränkt, siehe [Benutzerdefinierte Feldattribute](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
> * Diese Einschränkung bedeutet, dass Sie immer nur maximal 25 Experience Platformen Segmentmitgliedschaften haben können.
> * Wenn Sie diese Grenze in Salesforce erreicht haben, müssen Sie das benutzerdefinierte Attribut aus Salesforce entfernen, das zum Speichern des Segmentstatus für ältere Segmente in Experience Platform verwendet wurde, bevor eine neue mappingId verwendet werden kann.


Weitere Informationen finden Sie in der Dokumentation zu Adobe Experience Platform . [Feldergruppe Segmentzugehörigkeitsdetails](/help/xdm/field-groups/profile/segmentation.md) , wenn Sie Anleitungen zum Segmentstatus benötigen.

#### Salesforce-Anmeldeinformationen sammeln {#gather-credentials}

Beachten Sie die folgenden Elemente, bevor Sie sich beim Salesforce CRM-Ziel authentifizieren:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| <ul><li>Salesforce-Domänenpräfix</li></ul> | Siehe [Salesforce-Domänenpräfix](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) für zusätzliche Leitlinien. | <ul><li>Wenn Ihre Domäne wie folgt lautet, benötigen Sie den hervorgehobenen Wert.<br> <i>`d5i000000isb4eak-dev-ed`.my.salesforce.com</i></li></ul> |
| <ul><li>Consumer Key</li><li>Verbrauchergeheimnis</li></ul> | Siehe Abschnitt [Salesforce-Dokumentation](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) wenn Sie zusätzliche Anleitungen benötigen. | <ul><li>r23kxxxxxxxx0z05xxxxxx</li><li>ipxxxxxxxxxxT4xxxxxxxxxxxx</li></ul> |

## Unterstützte Identitäten {#supported-identities}

Salesforce CRM unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Weitere Informationen [identities](/help/identity-service/namespaces.md).

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| SalesforceId | Benutzerdefinierte Salesforce CRM-ID, die die Zuordnung einer beliebigen Identität unterstützt. | Obligatorisch. Sie können [identity](../../../identity-service/namespaces.md) der [!DNL Salesforce CRM] Ziel, solange Sie es dem `SalesforceId`. |

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern *(z. B.: E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Status von Platform-Segmenten werden nach exportiert [!DNL Salesforce CRM] durch Angabe des entsprechenden benutzerdefinierten Feldattributs in [!DNL Salesforce CRM] im **[!UICONTROL Ziel aktivieren]** > **[!UICONTROL Segmentexport planen]** > **[!UICONTROL Zuordnungs-ID]** -Feld.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | <ul><li>Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

![Katalog](../../assets/catalog/crm/salesforce/catalog.png)

### An Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**.

![Beispiel-Screenshot, der zeigt, wie eine Authentifizierung bei Salesforce CRM erfolgt](../../assets/catalog/crm/salesforce/authenticate-destination.png)

* **[!UICONTROL Passwort]**: Ihr Salesforce-Kontokennwort.
* **[!UICONTROL Client-ID]**: Kundenschlüssel der mit Salesforce verbundenen App.
* **[!UICONTROL Client Secret]**: Ihre mit Salesforce verbundene App - Kundengeheimnis.
* **[!UICONTROL Benutzername]**: Ihr Salesforce-Konto-Benutzername.

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche eine **Verbunden** Status mit einem grünen Häkchen anzeigen, können Sie mit dem nächsten Schritt fortfahren.

### Zieldetails ausfüllen {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
![Beispiel-Screenshot zum Ausfüllen von Details für Salesforce CRM](../../assets/catalog/crm/salesforce/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Benutzerdefinierte Domäne]**: Ihre Salesforce-Domäne.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen über den Status des Datenflusses an Ihr Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

Um Ihre Zielgruppendaten korrekt von Adobe Experience Platform an das Salesforce CRM-Ziel zu senden, müssen Sie den Feldzuordnungsschritt durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodell (XDM) in Ihrem Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen. Gehen Sie wie folgt vor, um Ihre XDM-Felder korrekt den Salesforce CRM-Zielfeldern zuzuordnen:

1. Klicken Sie im Schritt &quot;Zuordnung&quot;auf **[!UICONTROL Neues Mapping hinzufügen]**, wird eine neue Zuordnungszeile auf dem Bildschirm angezeigt.

   ![Neue Zuordnung hinzufügen](../../assets/catalog/crm/salesforce/add-new-mapping.png)

1. Wählen Sie im Fenster Quellfeld auswählen die Option **[!UICONTROL Attribute auswählen]** und fügen Sie die gewünschten Zuordnungen hinzu.

   ![Quellzuordnung](../../assets/catalog/crm/salesforce/source-mapping.png)

1. Wählen Sie im Fenster Zielfeld auswählen das Zielfeld aus und wählen Sie die **[!UICONTROL Identitäts-Namespace auswählen]** und fügen Sie die gewünschten Zuordnungen hinzu.

   ![Zielgruppen-Mapping mit SalesforceId](../../assets/catalog/crm/salesforce/target-mapping-salesforceid.png)

1. Wählen Sie für benutzerdefinierte Attribute im Fenster Zielfeld auswählen das Zielfeld aus und wählen Sie die **[!UICONTROL Benutzerdefinierte Attribute auswählen]** -Kategorie, geben Sie als Nächstes den gewünschten Zielattribut-Namen an und fügen Sie die gewünschten Zuordnungen hinzu.

   ![Zielgruppen-Mapping mit LastName](../../assets/catalog/crm/salesforce/target-mapping-lastname.png)

1. Sie können beispielsweise die folgende Zuordnung zwischen Ihrem XDM-Profilschema und Ihrem [!DNL Salesforce CRM] instance:

   |  | XDM-Profilschema | [!DNL Salesforce CRM] Instanz | Obligatorisch |
   |---|---|---|---|
   | Attribute | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>personalEmail.address</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>E-Mail</code></li></ul> |
   | Identitäten | <ul><li>crmID</code></li></ul> | <ul><li>SalesforceId</code></li></ul> | Ja |

1. Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Zuordnungen:

   ![Zielgruppenzuordnung](../../assets/catalog/crm/salesforce/mappings.png)

### Segmentexport planen, Beispiel {#schedule-segment-export-example}

Bei der Durchführung der [Segmentexport planen](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) Schritt müssen Sie Platform-Segmente manuell dem benutzerdefinierten Feldattribut in Salesforce zuordnen.

Wählen Sie dazu jedes Segment aus und geben Sie dann das entsprechende benutzerdefinierte Feldattribut aus Salesforce in das Feld **[!UICONTROL Zuordnungs-ID]** -Feld.

>[!IMPORTANT]
>
>* Der für die **[!UICONTROL Zuordnungs-ID]** sollte genau mit dem Namen des benutzerdefinierten Feldattributs übereinstimmen, das in Salesforce erstellt wurde.
>* Stellen Sie sicher, dass der Name des von Ihnen in Salesforce erstellten benutzerdefinierten Feldattributs nicht das Leerzeichen verwendet.


Nachfolgend finden Sie ein Beispiel:
![Segmentexport planen](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

## Datenexport überprüfen {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Auswählen **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** um zur Liste der Ziele zu navigieren.
   ![Ziele durchsuchen](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. Wählen Sie das Ziel aus und überprüfen Sie, ob der Status **[!UICONTROL enabled]**.
   ![Ziel-Datenfluss](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. Wechseln Sie zu **[!DNL Activation data]** und wählen Sie einen Segmentnamen aus.
   ![Zielaktivierungsdaten](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. Überwachen Sie die Segmentzusammenfassung und stellen Sie sicher, dass die Anzahl der Profile der im Segment erstellten Anzahl entspricht.
   ![Segment](../../assets/catalog/crm/salesforce/segment.png)

1. Melden Sie sich bei der Salesforce-Website an und navigieren Sie dann zur **[!DNL Apps]** > **[!DNL Contacts]** und überprüfen Sie, ob die Profile aus dem Segment hinzugefügt wurden.
   ![Salesforce-Kontakte](../../assets/catalog/crm/salesforce/contacts.png)

1. Klicken Sie auf einen Kontakt und prüfen Sie, ob die Felder aktualisiert wurden. Sie werden feststellen, dass der Segmentstatus aus der Experience Platform mit dem entsprechenden benutzerdefinierten Feldattribut aktualisiert wurde, das im **Zuordnungs-ID** -Feld während der **[!UICONTROL Ziel aktivieren]** > **[!UICONTROL Segmentexport planen]** Schritt.
   ![Salesforce-Kontakte](../../assets/catalog/crm/salesforce/contact-info.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

### Unbekannte Fehler beim Senden von Ereignissen an das Ziel {#unknown-errors}

Wenn Sie die Ausführung eines Datenflusses überprüfen, überprüfen Sie, ob die von Ihnen unter [!DNL Salesforce CRM] für Ihr Platform-Segment gültig ist und in [!DNL Salesforce CRM].
![Fehler](../../assets/catalog/crm/salesforce/error.png)

## Weitere Ressourcen {#additional-resources}

Zusätzliche nützliche Informationen aus dem [Salesforce-Entwicklerportal](https://developer.salesforce.com/) unten steht:
* [Datensatz erstellen](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [Benutzerspezifische Empfehlungszielgruppen](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [Verwenden von Composite-Ressourcen](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* [Schnellstart](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)

### Beschränkungen {#limits}

Salesforce gleicht Transaktionslasten durch Auferlegung von Anforderungs-, Rate- und Timeout-Beschränkungen aus. Siehe Abschnitt [API-Anforderungsbeschränkungen und -zuordnungen](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) für Details.
