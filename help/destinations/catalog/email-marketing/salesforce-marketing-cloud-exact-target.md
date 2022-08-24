---
keywords: E-Mail; E-Mail; E-Mail; E-Mail-Ziele; Salesforce; api Salesforce Marketing Cloud-Ziel
title: (API) Salesforce-Marketing Cloud-Verbindung
description: Mit dem Salesforce-Marketing Cloud (ehemals ExactTarget)-Ziel können Sie Ihre Kontodaten exportieren und im Salesforce-Marketing Cloud für Ihre Geschäftsanforderungen aktivieren.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 2dda77c3d9a02b53a02128e835abf77ab97ad033
workflow-type: tm+mt
source-wordcount: '1906'
ht-degree: 6%

---

# [!DNL (API) Salesforce Marketing Cloud]-Verbindung

## Übersicht {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/overview/) (ehemals ExactTarget) ist eine Digital-Marketing-Suite, mit der Sie Journey für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.

>[!IMPORTANT]
> 
> Beachten Sie den Unterschied zwischen dieser Verbindung und der anderen [Salesforce-Marketing Cloud-Verbindung](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/salesforce-marketing-cloud.html?lang=en) , die im Abschnitt E-Mail-Marketing-Katalog vorhanden ist. Mit der anderen Salesforce-Marketing Cloud-Verbindung können Sie Dateien an einen bestimmten Speicherort exportieren, während es sich hierbei um eine API-basierte Streaming-Verbindung handelt.

Diese [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt die [Salesforce-Update kontaktiert REST-API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html), mit dem Sie Kontakte hinzufügen/Kontaktdaten für Ihre geschäftlichen Anforderungen aktualisieren können, nachdem Sie diese in einem neuen Salesforce-Segment aktiviert haben.

Salesforce Marketing Cloud verwendet OAuth 2 mit Client-Anmeldeinformationen als Authentifizierungsmechanismus für die Kommunikation mit der Salesforce REST API. Anweisungen zur Authentifizierung für Ihre Salesforce-Instanz finden Sie weiter unten im Abschnitt [An Ziel authentifizieren](#authenticate) Abschnitt.

## Anwendungsbeispiele {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das Salesforce-Marketing Cloud-Ziel verwenden sollten, finden Sie hier ein Beispielanwendungsbeispiel, das Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Senden von E-Mails an Kontakte für Marketingkampagnen {#use-case-send-emails}

Die Vertriebsabteilung einer Heimmiet-Plattform möchte eine Marketing-E-Mail an eine zielgerichtete Kundenzielgruppe senden. Das Marketing-Team der Plattform kann neue Kontakte hinzufügen/vorhandene Kontakte aktualisieren *(und ihre E-Mail-Adressen)* Erstellen Sie über Adobe Experience Platform Segmente aus eigenen Offline-Daten und senden Sie diese Segmente an Salesforce Marketing Cloud, das dann zum Senden der E-Mail-Adresse der Marketingkampagne verwendet werden kann.

## Voraussetzungen {#prerequisites}

### Voraussetzungen für die Experience Platform {#prerequisites-in-experience-platform}

Bevor Sie Daten für das Salesforce-Marketing Cloud-Ziel aktivieren, müssen Sie über eine [schema](/help/xdm/schema/composition.md), [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) erstellt in [!DNL Experience Platform].

### Voraussetzungen in Salesforce CRM {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen in Salesforce, um Daten von Platform in Ihr Salesforce-Marketing Cloud-Konto zu exportieren:

#### Sie benötigen ein Salesforce-Konto {#prerequisites-account}

Gehe zu Salesforce [Testversion](https://www.salesforce.com/in/form/signup/freetrial-sales/) -Seite, um sich zu registrieren und ein Salesforce-Konto zu erstellen, falls noch keines vorhanden ist.

#### Benutzerdefiniertes Feld in Salesforce erstellen {#prerequisites-custom-field}

Sie müssen ein benutzerdefiniertes Attribut des Typs `Text Area Long`, die Experience Platform verwendet, um den Segmentstatus im Salesforce-Marketing Cloud zu aktualisieren. Aktivieren Sie im Workflow zum Aktivieren von Segmenten für das Ziel im **[Segmentplan](#schedule-segment-export-example)** Schritt, verwenden Sie das benutzerdefinierte Attribut als Zuordnungs-ID für jedes Segment, das Sie aktivieren.

Weitere Informationen finden Sie in der Salesforce-Marketing Cloud-Dokumentation unter [Benutzerdefinierte Felder erstellen](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) wenn Sie zusätzliche Anleitungen benötigen.

>[!IMPORTANT]
>
> Stellen Sie sicher, dass Sie das benutzerdefinierte Attribut unter dem Attributsatz &quot;E-Mail-Demografie&quot;in Ihrem Salesforce-Marketing Cloud-Konto erstellen.

>[!NOTE]
>
> * Die Anzahl der pro Objekt zulässigen benutzerdefinierten Attribute variiert je nach Salesforce Edition. Weitere Informationen finden Sie in der Salesforce-Dokumentation für [Benutzerdefinierte Felder pro Objekt zulässig](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) wenn Sie zusätzliche Anleitungen benötigen.
> * Wenn Sie diese Grenze in Salesforce erreicht haben, müssen Sie das benutzerdefinierte Attribut aus Salesforce entfernen, das zum Speichern des Segmentstatus für ältere Segmente in Experience Platform verwendet wurde, bevor eine neue mappingId verwendet werden kann.


Weitere Informationen finden Sie in der Dokumentation zu Adobe Experience Platform . [Feldergruppe Segmentzugehörigkeitsdetails](/help/xdm/field-groups/profile/segmentation.md) , wenn Sie Anleitungen zum Segmentstatus benötigen.

#### Salesforce-Anmeldeinformationen sammeln {#gather-credentials}

Beachten Sie die folgenden Elemente, bevor Sie sich beim Salesforce-Marketing Cloud-Ziel authentifizieren.

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| <ul><li>Salesforce-Marketing Cloud-Präfix</li></ul> | Siehe [Salesforce-Marketing Cloud-Domänenpräfix](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) für zusätzliche Leitlinien. | <ul><li>Wenn Ihre Domäne wie folgt lautet, benötigen Sie den hervorgehobenen Wert.<br> <i>`mcq4jrssqdlyc4lph19nnqgzzs84`.login.executeTarget.com</i></li></ul> |
| <ul><li>Client-ID</li><li>Client-Geheimnis</li></ul> | Siehe Abschnitt [Salesforce-Dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) wenn Sie zusätzliche Anleitungen benötigen. | <ul><li>r23kxxxxxxxx0z05xxxxxx</li><li>ipxxxxxxxxxxT4xxxxxxxxxxxx</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Unterstützte Identitäten {#supported-identities}

Salesforce Marketing Cloud unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Weitere Informationen [identities](/help/identity-service/namespaces.md).

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| contactKey | Salesforce-Kontaktschlüssel. Siehe Abschnitt [Salesforce-Dokumentation](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) wenn Sie zusätzliche Anleitungen benötigen. | Obligatorisch |

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm Profilattribute im [Zielaktivierungs-Workflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

![Katalog](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/catalog.png)

### An Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**.

![Beispiel-Screenshot mit der Authentifizierung beim Salesforce-Marketing Cloud](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

* **[!UICONTROL Subdomain]**: Ihr Salesforce-Marketing Cloud-Domänenpräfix. Beispiel: Ihre Domäne *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.executeTarget.com* benötigen Sie den hervorgehobenen Wert.
* **[!UICONTROL Client-ID]**: Ihre Salesforce-Client-ID.
* **[!UICONTROL Client Secret]**: Ihr Salesforce-Client-Geheimnis.

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche eine **Verbunden** Status mit einem grünen Häkchen anzeigen, können Sie mit dem nächsten Schritt fortfahren.

### Zieldetails ausfüllen {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Beispiel-Screenshot zum Ausfüllen von Details für Salesforce-Marketing Cloud](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Kundenname]**: Dies kann ein beliebiger Wert sein, ein Wert ist jedoch obligatorisch. Andernfalls schlägt die Zielaktivierung fehl.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen über den Status des Datenflusses an Ihr Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

Um Ihre Zielgruppendaten korrekt von Adobe Experience Platform an das Salesforce Marketing Cloud-Ziel zu senden, müssen Sie den Feldzuordnungsschritt durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodell (XDM) in Ihrem Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen. Gehen Sie wie folgt vor, um Ihre XDM-Felder korrekt den Salesforce-Marketing Cloud-Zielfeldern zuzuordnen.

Die Liste der Attribut-Mappings, die für die [Salesforce REST API](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) ist unten angegeben. Das Ziel verwendet die [Salesforce Search Attribute-Set Definitions REST API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) um Attribute abzurufen, die in Salesforce für Ihre Kontakte definiert sind und speziell für Ihr Konto gelten.

>[!IMPORTANT]
> 
> Obwohl Ihre Attributnamen gemäß Ihrem Salesforce-Konto übereinstimmen, werden die Zuordnungen für `contactKey` und `personalEmail.address` sind zwingend erforderlich.

1. Klicken Sie im Schritt &quot;Zuordnung&quot;auf **[!UICONTROL Neues Mapping hinzufügen]**. Auf dem Bildschirm wird jetzt eine neue Zuordnungszeile angezeigt.
   ![Neue Zuordnung hinzufügen](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)

1. Wählen Sie im Fenster Quellfeld auswählen bei der Auswahl des Quellfelds die **[!UICONTROL Attribute auswählen]** und fügen Sie die gewünschten Zuordnungen hinzu.
   ![Quellzuordnung](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/source-mapping.png)

1. Wählen Sie im Fenster Zielfeld auswählen das Zielfeld aus und wählen Sie die **[!UICONTROL Identitäts-Namespace auswählen]** und fügen Sie die gewünschten Zuordnungen hinzu.
   ![Zielgruppenzuordnung](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping.png)

1. Um benutzerdefinierte Attribute zuzuordnen, wählen Sie das Zielfeld-Fenster aus, wählen Sie das Zielfeld aus und wählen Sie die **[!UICONTROL Attribute auswählen]** > **Email Demographic** Kategorie. Geben Sie als Nächstes den gewünschten Zielattribut-Namen ein und fügen Sie die gewünschten Zuordnungen hinzu.
   ![Zielgruppenzuordnung](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping-custom.png)

1. Sie können beispielsweise die folgende Zuordnung zwischen Ihrem XDM-Profilschema und Ihrem [!DNL Salesforce Marketing Cloud] instance:

   |  | XDM-Profilschema | [!DNL Salesforce Marketing Cloud] Instanz | Obligatorisch |
   |---|---|---|---|
   | Attribute | <ul><li>person.name.firstName</code></li><li>personalEmail.address</code></li></ul> | <ul><li>Email Demography.First Name</code></li><li>E-Mail-Adressen.E-Mail-Adresse</code></li></ul> | <ul><li>–</li><li>Ja</code></li></ul> |
   | Identitäten | <ul><li>contactKey</code></li></ul> | <ul><li>salesforceContactKey</code></li></ul> | Ja |

1. Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Zuordnungen:
   ![Target-Zuordnung - Nachname](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

### Segmentexport planen, Beispiel {#schedule-segment-export-example}

Bei der Durchführung der [Segmentexport planen](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) Schritt, müssen Sie Platform-Segmente manuell dem benutzerdefinierten Attribut in Salesforce zuordnen.

Wählen Sie dazu jedes Segment aus und geben Sie dann das entsprechende benutzerdefinierte Attribut aus Salesforce in das **[!UICONTROL Zuordnungs-ID]** -Feld.

>[!IMPORTANT]
>
> Der für die Zuordnungs-ID verwendete Wert sollte genau mit dem Namen des benutzerdefinierten Attributs übereinstimmen, das in Salesforce unter dem Attributsatz &quot;E-Mail-Demografie&quot;erstellt wurde.

Nachfolgend finden Sie ein Beispiel:
![Segmentexport planen](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

## Datenexport überprüfen {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Auswählen **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** um zur Liste der Ziele zu navigieren.

   ![Ziele durchsuchen](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Wählen Sie das Ziel aus und überprüfen Sie, ob der Status **[!UICONTROL enabled]**.

   ![Ziel-Datenfluss](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Wechseln Sie zu **[!DNL Activation data]** und wählen Sie einen Segmentnamen aus.

   ![Zielaktivierungsdaten](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Überwachen Sie die Segmentzusammenfassung und stellen Sie sicher, dass die Anzahl der Profile der im Segment erstellten Anzahl entspricht.

   ![Segment](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Melden Sie sich bei der Salesforce Marketing Cloud-Website an. Navigieren Sie dann zum **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** und überprüfen Sie, ob die Profile aus dem Segment hinzugefügt wurden.

   ![Salesforce-Kontakte](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Um zu überprüfen, ob Profile aktualisiert wurden, navigieren Sie zum **[!DNL Email]** Seitenüberprüfung, ob die Attributwerte für das Profil aus dem Segment aktualisiert wurden.

   ![Salesforce-Kontakte](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

### Unbekannte Fehler beim Senden von Ereignissen an das Salesforce-Marketing Cloud {#unknown-errors}

Wenn Sie die Ausführung eines Datenflusses überprüfen, überprüfen Sie, ob die von Ihnen unter [!DNL Salesforce CRM] für Ihr Platform-Segment gültig ist und in [!DNL Salesforce CRM].
![Fehler](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

## Weitere Ressourcen {#additional-resources}

* [Salesforce-Entwicklerportal](https://developer.salesforce.com/)

### Beschränkungen {#limits}

* Salesforce setzt bestimmte [Grenzwerte](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
* Siehe Abschnitt [Ratenbeschränkungen-Fehler](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) , um eventuelle Fehler zu überprüfen.
* Siehe Abschnitt [Salesforce Marketing Cloud Interaktionspreise](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) Seite zu *Vollständige Vergleichstabelle herunterladen* als pdf , in dem die durch Ihren Plan festgelegten Grenzen beschrieben werden.
* Die [API-Übersicht](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) Seite enthält zusätzliche Einschränkungen.
* Ein KB-Element, das diese Details sortiert, ist verfügbar [here](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits#:~:text=Day%2FHour%2FMinute%20Limit&amp;text=We%20recommend%20a%20limit%20of,per%20minute%20for%20SOAP%20calls.&amp;text=As%20has%20been%20added%20in,interagieren%20with%20the%20REST%2DAPI).
