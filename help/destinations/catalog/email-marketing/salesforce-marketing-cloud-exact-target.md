---
keywords: E-Mail; E-Mail; E-Mail; E-Mail-Ziele; Salesforce; api Salesforce Marketing Cloud-Ziel
title: (API) Salesforce-Marketing Cloud-Verbindung
description: Mit dem Salesforce-Marketing Cloud (ehemals ExactTarget)-Ziel können Sie Ihre Kontodaten exportieren und im Salesforce-Marketing Cloud für Ihre Geschäftsanforderungen aktivieren.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 2c778fe087a04261c79b9daf8579666cd0794eb4
workflow-type: tm+mt
source-wordcount: '1912'
ht-degree: 5%

---

# [!DNL (API) Salesforce Marketing Cloud]-Verbindung

## Übersicht {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/overview/) (früher bekannt als [!DNL ExactTarget]) ist eine Digital Marketing Suite, mit der Sie Journey für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.

>[!IMPORTANT]
>
>Beachten Sie den Unterschied zwischen dieser Verbindung und der anderen [[!DNL Salesforce Marketing Cloud] connection](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) , die im Abschnitt E-Mail-Marketing-Katalog vorhanden ist. Mit der anderen Salesforce-Marketing Cloud-Verbindung können Sie Dateien an einen bestimmten Speicherort exportieren, während es sich hierbei um eine API-basierte Streaming-Verbindung handelt.

Diese [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt die [!DNL Salesforce Marketing Cloud] [Kontakte aktualisieren](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API, mit der Sie Kontakte hinzufügen/Kontaktdaten für Ihre geschäftlichen Anforderungen aktualisieren können, nachdem Sie sie in einer neuen aktiviert haben [!DNL Salesforce Marketing Cloud] Segment.

[!DNL Salesforce Marketing Cloud] verwendet OAuth 2 mit Client-Anmeldeinformationen als Authentifizierungsmechanismus für die Kommunikation mit dem [!DNL Salesforce Marketing Cloud] API. Anweisungen zur Authentifizierung bei Ihrem [!DNL Salesforce Marketing Cloud] -Instanz weiter unten im [An Ziel authentifizieren](#authenticate) Abschnitt.

## Anwendungsbeispiele {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die [!DNL Salesforce Marketing Cloud] Ziel, hier ein Beispielanwendungsfall, den Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Senden von E-Mails an Kontakte für Marketingkampagnen {#use-case-send-emails}

Die Vertriebsabteilung einer Heimmiet-Plattform möchte eine Marketing-E-Mail an eine zielgerichtete Kundenzielgruppe senden. Das Marketing-Team der Plattform kann neue Kontakte hinzufügen/vorhandene Kontakte aktualisieren *(und ihre E-Mail-Adressen)* Erstellen Sie über Adobe Experience Platform Segmente aus eigenen Offline-Daten und senden Sie diese Segmente an [!DNL Salesforce Marketing Cloud], die dann zum Versand der E-Mail-Adresse der Marketing-Kampagne verwendet werden kann.

## Voraussetzungen {#prerequisites}

### Voraussetzungen für die Experience Platform {#prerequisites-in-experience-platform}

Vor der Aktivierung der Daten für [!DNL Salesforce Marketing Cloud] Ziel, müssen Sie über eine [schema](/help/xdm/schema/composition.md), [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) erstellt in [!DNL Experience Platform].

### Voraussetzungen in [!DNL Salesforce Marketing Cloud] {#prerequisites-destination}

Beachten Sie die folgenden Voraussetzungen, um Daten von Platform in Ihre [!DNL Salesforce Marketing Cloud] Konto:

#### Sie benötigen eine [!DNL Salesforce Marketing Cloud] account {#prerequisites-account}

Wenden Sie sich an Ihre [!DNL Salesforce Account Executive] , um sich für die [!DNL Salesforce Marketing Cloud Account Engagement] Produkt, wenn Sie es noch nicht haben.

#### Erstellen Sie ein benutzerdefiniertes Feld in [!DNL Salesforce Marketing Cloud] {#prerequisites-custom-field}

Sie müssen ein benutzerdefiniertes Attribut des Typs `Text Area Long`, die Experience Platform verwendet, um den Segmentstatus in [!DNL Salesforce Marketing Cloud]. Aktivieren Sie im Workflow zum Aktivieren von Segmenten für das Ziel im **[Segmentplan](#schedule-segment-export-example)** Schritt, verwenden Sie das benutzerdefinierte Attribut als **[!UICONTROL Zuordnungs-ID]** für jedes Segment, das Sie aktivieren.

Siehe Abschnitt [!DNL Salesforce Marketing Cloud] Dokumentation zu [Benutzerdefinierte Felder erstellen](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) wenn Sie zusätzliche Anleitungen benötigen.

>[!IMPORTANT]
>
> Stellen Sie sicher, dass Sie das benutzerdefinierte Attribut unter dem `Email Demographics` -Attribut in Ihrer [!DNL Salesforce Marketing Cloud] -Konto.

Weitere Informationen finden Sie in der Dokumentation zu Adobe Experience Platform . [Feldergruppe Segmentzugehörigkeitsdetails](/help/xdm/field-groups/profile/segmentation.md) , wenn Sie Anleitungen zum Segmentstatus benötigen.

#### Salesforce-Anmeldeinformationen sammeln {#gather-credentials}

Beachten Sie die folgenden Elemente, bevor Sie sich bei der [!DNL Salesforce Marketing Cloud] Ziel.

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| <ul><li>[!DNL Salesforce Marketing Cloud] prefix</li></ul> | Siehe [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) für zusätzliche Leitlinien. | <ul><li>Wenn Ihre Domäne wie folgt lautet, benötigen Sie den hervorgehobenen Wert.<br> <i>`mcq4jrssqdlyc4lph19nnqgzzs84`.login.executeTarget.com</i></li></ul> |
| <ul><li>Client-ID</li><li>Client-Geheimnis</li></ul> | Siehe Abschnitt [!DNL Salesforce Marketing Cloud] [Dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) wenn Sie zusätzliche Anleitungen benötigen. | <ul><li>r23kxxxxxxxx0z05xxxxxx</li><li>ipxxxxxxxxxxT4xxxxxxxxxxxx</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Beschränkungen in [!DNL Salesforce Marketing Cloud] {#limits}

* Salesforce setzt bestimmte [Grenzwerte](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * Siehe Abschnitt [!DNL Salesforce Marketing Cloud] [Dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) , um alle möglichen Einschränkungen zu beheben, die bei der Ausführung auftreten könnten, und Fehler zu reduzieren.
   * Siehe Abschnitt [[!DNL Salesforce Marketing Cloud] Interaktionskosten](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) Seite zu *Vollständige Vergleichstabelle herunterladen* als pdf , in dem die durch Ihren Plan festgelegten Grenzen beschrieben werden.
   * Die [API-Übersicht](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) Seite enthält zusätzliche Einschränkungen.
   * Siehe [here](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) für eine Seite, die diese Details sortiert.
* Die Anzahl der *Benutzerdefinierte Felder pro Objekt zulässig* variiert je nach Salesforce Edition.
   * Siehe Abschnitt [!DNL Salesforce] [Dokumentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) für zusätzliche Leitlinien.
   * Wenn Sie die für *Benutzerdefinierte Felder pro Objekt zulässig* Innerhalb [!DNL Salesforce Marketing Cloud] Sie müssen
      * Entfernen Sie ältere benutzerdefinierte Felder, bevor Sie neue benutzerdefinierte Felder in hinzufügen. [!DNL Salesforce Marketing Cloud].
      * Aktualisieren oder entfernen Sie alle Ziele in Platform, die diese älteren benutzerdefinierten Feldnamen als Wert für **[!UICONTROL Zuordnungs-ID]** während der [Segmentplanung](#schedule-segment-export-example) Schritt.

## Unterstützte Identitäten {#supported-identities}

[!DNL Salesforce Marketing Cloud] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Weitere Informationen [identities](/help/identity-service/namespaces.md).

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] Kontaktschlüssel. Siehe Abschnitt [!DNL Salesforce Marketing Cloud] [Dokumentation](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) wenn Sie zusätzliche Anleitungen benötigen. | Obligatorisch |

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern *(z. B.: E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Jeder Segmentstatus in [!DNL Salesforce Marketing Cloud] wird mit dem entsprechenden Segmentstatus von Platform aktualisiert, basierend auf dem **[!UICONTROL Zuordnungs-ID]** Wert, der während der [Segmentplanung](#schedule-segment-export-example) Schritt.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Within **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**, suchen Sie nach [!DNL (API) Salesforce Marketing Cloud]. Alternativ können Sie sie unter der **[!UICONTROL E-Mail-Marketing]** Kategorie.

### An Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**.
![Screenshot der Platform-Benutzeroberfläche, in dem gezeigt wird, wie die Authentifizierung für das Salesforce-Marketing Cloud erfolgt.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

* **[!UICONTROL Subdomain]**: Ihre [!DNL Salesforce Marketing Cloud] Domänen-Präfix. Beispiel: Ihre Domäne *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.executeTarget.com* benötigen Sie den hervorgehobenen Wert.
* **[!UICONTROL Client-ID]**: Ihre [!DNL Salesforce Marketing Cloud] Client-ID.
* **[!UICONTROL Client Secret]**: Ihre [!DNL Salesforce Marketing Cloud] Client Secret.

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche eine **[!UICONTROL Verbunden]** Status mit einem grünen Häkchen anzeigen, können Sie mit dem nächsten Schritt fortfahren.

### Zieldetails ausfüllen {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
![Screenshot der Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen über den Status des Datenflusses an Ihr Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
>
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

So senden Sie Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an die [!DNL Salesforce Marketing Cloud] Ziel, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodell (XDM) in Ihrem Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen. So ordnen Sie Ihre XDM-Felder korrekt der [!DNL Salesforce Marketing Cloud] Gehen Sie wie folgt vor:

>[!IMPORTANT]
>
>Auch wenn Ihre Attributnamen gemäß Ihrer [!DNL Salesforce Marketing Cloud] -Konto, die Zuordnungen für beide `contactKey` und `personalEmail.address` sind zwingend erforderlich.

1. Im **[!UICONTROL Zuordnung]** Schritt auswählen **[!UICONTROL Neues Mapping hinzufügen]**. Auf dem Bildschirm wird eine neue Zuordnungszeile angezeigt.
   ![Screenshot der Platform-Benutzeroberfläche zum Hinzufügen einer neuen Zuordnung.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)

1. Im **[!UICONTROL Quellfeld auswählen]** Fenster, wählen Sie die **[!UICONTROL Attribute auswählen]** Kategorie und wählen Sie `contactKey`.
   ![Screenshot-Beispiel der Platform-Benutzeroberfläche für die Quellzuordnung.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/source-mapping.png)

1. Im **[!UICONTROL Zielgruppenfeld auswählen]** wählen Sie den Typ des Zielfelds aus, dem Sie Ihr Quellfeld zuordnen möchten.
   * **[!UICONTROL Identitäts-Namespace auswählen]**: Wählen Sie diese Option aus, um Ihr Quellfeld einem Identitäts-Namespace aus der Liste zuzuordnen.
      ![Screenshot der Platform-Benutzeroberfläche mit Target-Zuordnung für salesforceContactKey.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping.png)

   * Fügen Sie die folgende Zuordnung zwischen Ihrem XDM-Profilschema und Ihrem [!DNL Salesforce Marketing Cloud] instance: |XDM-Profilschema|[!DNL Salesforce Marketing Cloud] Instanz| Erforderlich| |—|—|—| |`contactKey`|`salesforceContactKey`| Ja |

   * **[!UICONTROL Benutzerdefinierte Attribute auswählen]**: Wählen Sie diese Option aus, um Ihr Quellfeld einem benutzerdefinierten Attribut zuzuordnen, das Sie in der Variablen **[!UICONTROL Attributname]** -Feld. Siehe [!DNL Salesforce Marketing Cloud] [Dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) für eine Liste der unterstützten Attribute. Beachten Sie außerdem, dass das Ziel die [Salesforce Search Attribute-Set Definitions REST API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) um Attribute abzurufen, die in Salesforce für Ihre Kontakte definiert sind und speziell für Ihr Konto gelten.
      ![Screenshot der Platform-Benutzeroberfläche mit Target-Zuordnung.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping-custom.png)

   * Fügen Sie je nach den Werten, die Sie aktualisieren möchten, beispielsweise die folgende Zuordnung zwischen Ihrem XDM-Profilschema und Ihrem [!DNL Salesforce Marketing Cloud] instance: |XDM-Profilschema|[!DNL Salesforce Marketing Cloud] Instanz| |—|—| |`person.name.firstName`|`Email Demographics.First Name`| |`personalEmail.address`|`Email Addresses.Email Address`|

   * Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Zuordnungen:
      ![Screenshot der Platform-Benutzeroberfläche mit Target-Zuordnungen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

### Segmentexport planen, Beispiel {#schedule-segment-export-example}

Bei der Durchführung der [Segmentexport planen](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) Schritt: Sie müssen Platform-Segmente manuell dem [benutzerspezifisches Attribut](#prerequisites-custom-field) in Salesforce.

Wählen Sie dazu jedes Segment aus und geben Sie dann das entsprechende benutzerdefinierte Attribut aus Salesforce in das **[!UICONTROL Zuordnungs-ID]** -Feld.

>[!IMPORTANT]
>
>Der für die Zuordnungs-ID verwendete Wert sollte genau mit dem Namen des benutzerdefinierten Attributs übereinstimmen, das in Salesforce unter dem Attributsatz &quot;E-Mail-Demografie&quot;erstellt wurde.

Nachfolgend finden Sie ein Beispiel:
![Screenshot-Beispiel der Platform-Benutzeroberfläche mit der Option Segmentexport planen .](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

## Datenexport überprüfen {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Auswählen **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** um zur Liste der Ziele zu navigieren.
   ![Screenshot der Platform-Benutzeroberfläche mit den Browse-Zielen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Wählen Sie das Ziel aus und überprüfen Sie, ob der Status **[!UICONTROL enabled]**.
   ![Screenshot der Platform-Benutzeroberfläche mit dem Ziel-Datenfluss.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Wechseln Sie zu **[!DNL Activation data]** und wählen Sie einen Segmentnamen aus.
   ![Screenshot-Beispiel der Platform-Benutzeroberfläche mit Zielen-Aktivierungsdaten.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Überwachen Sie die Segmentzusammenfassung und stellen Sie sicher, dass die Anzahl der Profile der im Segment erstellten Anzahl entspricht.
   ![Beispiel für einen Screenshot der Platform-Benutzeroberfläche mit Segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Melden Sie sich bei der [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/) Website. Navigieren Sie dann zum **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** und überprüfen Sie, ob die Profile aus dem Segment hinzugefügt wurden.
   ![Screenshot der Salesforce Marketing Cloud-Benutzeroberfläche mit der Kontaktseite mit den im Segment verwendeten Profilen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Um zu überprüfen, ob Profile aktualisiert wurden, navigieren Sie zum **[!UICONTROL Email]** und überprüfen Sie, ob die Attributwerte für das Profil aus dem Segment aktualisiert wurden. Bei Erfolg können Sie sehen, dass jeder Segmentstatus in [!DNL Salesforce Marketing Cloud] mit dem entsprechenden Segmentstatus von Platform aktualisiert wurde, basierend auf dem **[!UICONTROL Zuordnungs-ID]** Wert, der im [Segmentplanung](#schedule-segment-export-example) Schritt.
   ![Screenshot der Salesforce Marketing Cloud-Benutzeroberfläche mit der ausgewählten Kontakts-E-Mail-Seite mit aktualisiertem Segmentstatus.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

### Unbekannte Fehler beim Senden von Ereignissen an das Salesforce-Marketing Cloud {#unknown-errors}

Beim Überprüfen eines Datenfluss-Ablaufs wird möglicherweise die folgende Fehlermeldung angezeigt: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

![Screenshot der Platform-Benutzeroberfläche mit Fehlermeldung.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

Um diesen Fehler zu beheben, überprüfen Sie, ob die Variable **[!UICONTROL Zuordnungs-ID]** die Sie in [!DNL Salesforce Marketing Cloud] für Ihr Platform-Segment gültig ist und in [!DNL Salesforce Marketing Cloud].

## Weitere Ressourcen {#additional-resources}

* [[!DNL Salesforce Marketing Cloud] APIs](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
