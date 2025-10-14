---
title: (API) Oracle Eloqua-Verbindung
description: Mit dem (API) Oracle Eloqua -Ziel können Sie Ihre Kontodaten exportieren und in Oracle Eloqua für Ihre Geschäftsanforderungen aktivieren.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2044'
ht-degree: 28%

---


# [!DNL (API) Oracle Eloqua]-Verbindung

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) ermöglicht es Marketing-Experten, Kampagnen zu planen und auszuführen und dabei ein personalisiertes Kundenerlebnis für ihre potenziellen Kunden zu liefern. Dank der integrierten Lead-Verwaltung und der einfachen Kampagnenerstellung können Marketing-Fachleute die richtige Zielgruppe zur richtigen Zeit auf der Journey ihres Käufers ansprechen. Außerdem kann die Lösung elegant skaliert werden, um Zielgruppen über verschiedene Kanäle wie E-Mail, Display-Suche, Video und Mobilgeräte zu erreichen. Vertriebsteams können mehr Angebote schneller abschließen und so den Marketing-ROI durch Echtzeit-insight steigern.

Dieses [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt den Vorgang [Aktualisieren eines &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) aus der [!DNL Oracle Eloqua] REST-API, mit dem Sie **einer Zielgruppe** Identitäten in [!DNL Oracle Eloqua] aktualisieren können.

[!DNL Oracle Eloqua] verwendet [Standardauthentifizierung](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) für die Kommunikation mit der [!DNL Oracle Eloqua] REST-API. Anweisungen zur Authentifizierung bei Ihrer [!DNL Oracle Eloqua]-Instanz sehen Sie weiter unten im Abschnitt [Authentifizieren bei Ziel](#authenticate).

## Anwendungsbeispiele {#use-cases}

Die Marketing-Abteilung einer Online-Plattform möchte eine E-Mail-basierte Marketing-Kampagne an eine kuratierte Audience von Leads senden. Das Marketing-Team der Plattform kann bestehende Lead-Informationen über Adobe Experience Platform aktualisieren, Zielgruppen aus ihren eigenen Offline-Daten erstellen und diese Zielgruppen an [!DNL Oracle Eloqua] senden, die dann zum Senden der E-Mail mit der Marketing-Kampagne verwendet werden können.

## Voraussetzungen {#prerequisites}

### Voraussetzungen für Experience Platform {#prerequisites-in-experience-platform}

Vor der Aktivierung der Daten für das [!DNL Oracle Eloqua]-Ziel müssen Sie über ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=de) und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=de) verfügen, die in [!DNL Experience Platform] erstellt wurden.

Weitere Informationen finden Sie in der Experience Platform[Dokumentation für die Schemafeldgruppe „Details zur Zielgruppenzugehörigkeit](/help/xdm/field-groups/profile/segmentation.md) , wenn Sie Anleitungen zu Zielgruppenstatus benötigen.

### Voraussetzungen für [!DNL Oracle Eloqua] {#prerequisites-destination}

Um Daten aus Experience Platform in Ihr [!DNL Oracle Eloqua]-Konto zu exportieren, benötigen Sie ein [!DNL Oracle Eloqua].

Darüber hinaus benötigen Sie mindestens die *„Erweiterte Benutzer - Marketing-Berechtigungen“* für Ihre [!DNL Oracle Eloqua]. Eine Anleitung finden Sie im Abschnitt *Sicherheitsgruppen* auf der Seite [Gesicherter &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm)&quot;. Der Zugriff ist für das Ziel erforderlich, um beim Aufrufen der [!DNL Oracle Eloqua]-API programmgesteuert [Ihre Basis-](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html) zu bestimmen).

#### Sammeln von [!DNL Oracle Eloqua]-Anmeldedaten {#gather-credentials}

Beachten Sie die folgenden Punkte, bevor Sie sich beim [!DNL Oracle Eloqua]-Ziel authentifizieren:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `Company Name` | Der mit Ihrem [!DNL Oracle Eloqua]-Konto verknüpfte Firmenname. <br>Sie verwenden die `Username` `Company Name` und [!DNL Oracle Eloqua] später als verkettete Zeichenfolge, die beim [&#x200B; der Authentifizierung beim Ziel als **[!UICONTROL Benutzername]** verwendet wird](#authenticate). |
| `Username` | Der Benutzername Ihres [!DNL Oracle Eloqua]. |
| `Password` | Das Kennwort Ihres [!DNL Oracle Eloqua] Kontos. |
| `Pod` | [!DNL Oracle Eloqua] unterstützt mehrere Rechenzentren mit jeweils einem eindeutigen Domain-Namen. [!DNL Oracle Eloqua] bezeichnet diese als „Pods“, es gibt derzeit insgesamt sieben - P01, P02, P03, P04, P06, P07 und P08. Um zu erfahren, in welchem POD Sie sich befinden, melden Sie sich bei [!DNL Oracle Eloqua] an und notieren Sie sich die URL in Ihrem Browser, nachdem Sie sich erfolgreich angemeldet haben. Wenn Ihre Browser-URL beispielsweise `secure.p01.eloqua.com` lautet, wird Ihr `pod` `p01`. Weitere Anleitungen finden Sie auf [&#x200B; Seite Bestimmen &#x200B;](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua) POD . |

Eine Anleitung finden Sie [&#x200B; Abschnitt „Anmelden  [!DNL Oracle Eloqua]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing)&quot;.

## Leitlinien {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] benutzerdefinierten Kontaktfelder werden automatisch mit den Namen der Zielgruppen erstellt, die im Schritt **[!UICONTROL Segmente auswählen]** ausgewählt wurden.

* [!DNL Oracle Eloqua] ist auf maximal 250 benutzerdefinierte Kontaktfelder beschränkt.
* Stellen Sie vor dem Exportieren neuer Zielgruppen sicher, dass diese Grenze nicht überschritten wird, sowohl von Experience Platform als auch von der Anzahl vorhandener Zielgruppen in [!DNL Oracle Eloqua].
* Wenn diese Grenze überschritten wird, tritt in Experience Platform ein Fehler auf. Der Grund dafür ist, dass die [!DNL Oracle Eloqua]-API die Anfrage nicht validieren kann und mit der Fehlermeldung - *400: Es gab einen Validierungsfehler* - , der das Problem beschreibt.
* Wenn Sie das oben angegebene Limit erreicht haben, müssen Sie vorhandene Zuordnungen aus Ihrem Ziel entfernen und die entsprechenden benutzerdefinierten Kontaktfelder in Ihrem [!DNL Oracle Eloqua]-Konto löschen, bevor Sie weitere Segmente exportieren können.

* Weitere Informationen zu zusätzlichen [[!DNL Oracle Eloqua]  finden Sie auf &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) Seite „Kontaktfelder erstellen“.

## Unterstützte Identitäten {#supported-identities}

[!DNL Oracle Eloqua] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Obligatorisch |
|---|---|---|
| `EloquaId` | Eindeutige Kennung des Kontakts. | Ja |

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern *(z. B.: E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Für jede ausgewählte Zielgruppe in Experience Platform wird der entsprechende [!DNL Oracle Eloqua] Segmentstatus mit dem Zielgruppenstatus aus Experience Platform aktualisiert.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | <ul><li>Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** nach [!DNL (API) Oracle Eloqua]. Alternativ können Sie es unter der Kategorie **[!UICONTROL E-Mail-Marketing]** finden.

### Beim Ziel authentifizieren {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="Firmenname\Benutzername"
>abstract="Füllen Sie dieses Feld mit Ihrem Firmennamen und dem Benutzernamen von Oracle Eloqua aus `{COMPANY_NAME}\{USERNAME}`"

Füllen Sie die erforderlichen Felder aus. Eine Anleitung dazu finden [&#x200B; im Abschnitt  [!DNL Oracle Eloqua] Sammeln](#gather-credentials)Anmeldeinformationen“.
* **[!UICONTROL Kennwort]**: Das Kennwort Ihres [!DNL Oracle Eloqua] Kontos.
* **[!UICONTROL Benutzername]**: Eine verkettete Zeichenfolge, die aus dem Namen Ihres [!DNL Oracle Eloqua] Unternehmens und dem [!DNL Oracle Eloqua] Benutzernamen besteht.<br>Der verkettete Wert hat die Form von `{COMPANY_NAME}\{USERNAME}`.<br> Hinweis: Verwenden Sie keine Klammern oder Leerzeichen und behalten Sie die `\` bei. <br>Wenn Ihr [!DNL Oracle Eloqua] Firmenname beispielsweise `MyCompany` und [!DNL Oracle Eloqua] Benutzername `Username` ist, wird der verkettete Wert, den Sie im Feld **[!UICONTROL Benutzername]** verwenden, `MyCompany\Username`.

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Mit Ziel verbinden]**.
Screenshot der ![Experience Platform-Benutzeroberfläche, auf dem die Authentifizierung gezeigt wird.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche den Status **[!UICONTROL Verbunden]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="Um Ihre Pod-Nummer zu finden, melden Sie sich bei Oracle Eloqua an. Notieren Sie die URL in Ihrem Browser, nachdem Sie sich erfolgreich angemeldet haben. "

<!-- >additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Oracle Knowledge base - find out your Pod number" -->

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
Screenshot der ![Experience Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Pod]**: Um zu erfahren, in welchem `pod` Sie sich befinden, melden Sie sich bei [!DNL Oracle Eloqua] an und notieren Sie sich die URL in Ihrem Browser, nachdem Sie sich erfolgreich angemeldet haben. Wenn Ihre Browser-URL beispielsweise `secure.p01.eloqua.com` ist, müssen Sie den `pod` Wert `p01` auswählen. Weitere Anleitungen finden [&#x200B; im Abschnitt  [!DNL Oracle Eloqua] Sammeln](#gather-credentials)Anmeldeinformationen“.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

Um Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an das [!DNL Oracle Eloqua]-Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodells (XDM) in Ihrem Experience Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen.

Gehen Sie wie folgt vor, um Ihre XDM-Felder den [!DNL Oracle Eloqua]-Zielfeldern zuzuordnen:

1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird eine neue Zuordnungszeile angezeigt.
1. Wählen Sie im Fenster **[!UICONTROL Quellfeld auswählen]** die Kategorie **[!UICONTROL Attribute auswählen]** und wählen Sie das XDM-Attribut oder den **[!UICONTROL Identity-Namespace auswählen]** und wählen Sie eine Identität aus.
1. Wählen Sie im Fenster **[!UICONTROL Zielfeld auswählen]** die Option **[!UICONTROL Identity-Namespace]** und wählen Sie eine Identität aus, oder wählen Sie **[!UICONTROL Benutzerdefinierte Attribute auswählen]** und geben Sie den gewünschten Attributnamen in das Feld **[!UICONTROL Attributname]** ein. Der von Ihnen angegebene Attributname sollte mit einem vorhandenen Kontaktattribut in [!DNL Oracle Eloqua] übereinstimmen. Unter [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) finden Sie die genauen Attributnamen, die Sie in [!DNL Oracle Eloqua] verwenden können.

   * Wiederholen Sie diese Schritte, um sowohl die erforderlichen als auch alle gewünschten Attributzuordnungen zwischen Ihrem XDM-Profilschema und [!DNL Oracle Eloqua] hinzuzufügen:

     | Quellfeld | Zielfeld | Obligatorisch |
     |---|---|---|
     | `IdentityMap: Eid` | `Identity: EloquaId` | Ja |
     | `xdm: personalEmail.address` | `Attribute: emailAddress` | Ja |
     | `xdm: personName.firstName` | `Attribute: firstName` | |
     | `xdm: personName.lastName` | `Attribute: lastName` | |
     | `xdm: workAddress.street1` | `Attribute: address1` | |
     | `xdm: workAddress.street2` | `Attribute: address2` | |
     | `xdm: workAddress.street3` | `Attribute: address3` | |
     | `xdm: workAddress.postalCode` | `Attribute: postalCode` | |
     | `xdm: workAddress.country` | `Attribute: country` | |
     | `xdm: workAddress.city` | `Attribute: city` | |

   * Nachfolgend finden Sie ein Beispiel mit den oben genannten Zuordnungen:

     Beispiel-Screenshot der ![Experience Platform-Benutzeroberfläche mit Attributzuordnungen.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* Die im Feld &quot;**[!UICONTROL &quot; angegebenen Attribute]** genau so benannt werden, wie sie im [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) angegeben sind, da diese Attribute den Anfragetext bilden.
>* Im Feld **[!UICONTROL Source angegebene Attribute]** folgen keiner dieser Einschränkungen. Sie können sie nach Bedarf zuordnen. Wenn das Datenformat jedoch beim Pushen in [!DNL Oracle Eloqua] nicht korrekt ist, führt dies zu einem Fehler. Sie können beispielsweise das Feld **[!UICONTROL Source,]** Namespace-`contact key`, `ABC ID` usw. zuordnen. nach **[!UICONTROL Zielfeld]** : `EloquaId`, nachdem sichergestellt wurde, dass die ID-Werte dem Format entsprechen, das von [!DNL Oracle Eloqua] akzeptiert wird.
>* Die `EloquaID` Zuordnung ist obligatorisch, um Attribute zu aktualisieren, die der Identität entsprechen.
>* Die `emailAddress` Zuordnung ist erforderlich. Ohne sie gibt die API einen Fehler aus, wie unten dargestellt:
>
>```json
>{
>     "type":"ObjectValidationError",
>     "container":{
>           "type":"ObjectKey",
>           "objectType":"Contact"
>     },
>     "property":"emailAddress",
>     "requirement":{
>           "type":"EmailAddressRequirement"
>     },
>     "value":"<null>"
>}
>```

Wenn Sie mit dem Eingeben der Zuordnungen für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

>[!NOTE]
>
>Das Ziel fügt bei jeder Ausführung automatisch eine eindeutige Kennung zu den ausgewählten Zielgruppennamen hinzu, wenn die Kontaktfeldinformationen an [!DNL Oracle Eloqua] gesendet werden. Dadurch wird sichergestellt, dass sich die Namen der Kontaktfelder, die Ihren Zielgruppennamen entsprechen, nicht überschneiden. Siehe den [Datenexport validieren](#exported-data) Abschnitt Screenshot-Beispiel einer Seite mit [!DNL Oracle Eloqua] Kontaktdetails, auf der ein benutzerdefiniertes Kontaktfeld mithilfe der Zielgruppennamen erstellt wurde.

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Wählen Sie **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** aus und navigieren Sie zur Liste der Ziele.
1. Wählen Sie als Nächstes das Ziel aus, wechseln Sie zur Registerkarte **[!UICONTROL Aktivierungsdaten]** und wählen Sie dann einen Zielgruppennamen aus.
   Beispiel-Screenshot der Experience Platform-Benutzeroberfläche mit Daten zur Aktivierung von Zielen.![&#128279;](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Überwachen Sie die Zielgruppenzusammenfassung und stellen Sie sicher, dass die Anzahl der Profile der Anzahl innerhalb des Segments entspricht.
   Beispiel-Screenshot der Experience Platform-Benutzeroberfläche mit Segment.![&#128279;](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Melden Sie sich bei der [!DNL Oracle Eloqua]-Website an und navigieren Sie dann zur Seite **[!UICONTROL Kontaktübersicht]**, um zu überprüfen, ob die Profile aus der Audience hinzugefügt wurden. Um den Zielgruppenstatus anzuzeigen, gehen Sie zu einer Seite **[!UICONTROL Kontaktdetails]** und überprüfen Sie, ob das Kontaktfeld mit dem ausgewählten Zielgruppennamen als Präfix erstellt wurde.

Screenshot der Benutzeroberfläche von Oracle Eloqua ![mit der Kontaktdetailseite mit einem benutzerdefinierten Kontaktfeld, das mit dem Zielgruppennamen erstellt wurde.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

Beim Erstellen des Ziels erhalten Sie möglicherweise eine der folgenden Fehlermeldungen: `400: There was a validation error` oder `400 BAD_REQUEST`. Dies geschieht, wenn Sie das Limit von 250 benutzerdefinierten Kontaktfeldern überschreiten, wie im Abschnitt [Leitplanken](#guardrails) beschrieben. Um diesen Fehler zu beheben, stellen Sie sicher, dass Sie das Limit für benutzerdefinierte Kontaktfelder in [!DNL Oracle Eloqua] nicht überschreiten.
Screenshot der ![Experience Platform-Benutzeroberfläche mit Fehlermeldung.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Auf den Seiten [[!DNL Oracle Eloqua] HTTP-Status](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html)Codes und [[!DNL Oracle Eloqua] Validierungsfehler](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) finden Sie eine umfassende Liste von Status- und Fehler-Codes mit Erläuterungen.

## Zusätzliche Ressourcen {#additional-resources}

Weitere Informationen finden Sie in der [!DNL Oracle Eloqua]:

* [Oracle Eloqua Marketing Automation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [REST-API für Oracle Eloqua Marketing Cloud Service](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### Änderungsprotokoll

In diesem Abschnitt werden aktualisierte Funktionen und wesentliche Dokumentationsänderungen für diesen Ziel-Connector erfasst.

+++ Änderungsprotokoll anzeigen

| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| April 2023 | Dokumentation aktualisieren | <ul><li>Wir haben den Abschnitt [Anwendungsfälle](#use-cases) mit einem klareren Beispiel dafür aktualisiert, wann Kundinnen und Kunden von der Verwendung dieses Ziels profitieren würden.</li> <li>Der Abschnitt [Zuordnung](#mapping-considerations-example) wurde mit klaren Beispielen für obligatorische und optionale Zuordnungen aktualisiert.</li> <li>Der Abschnitt [Verbindung zum Ziel herstellen](#connect) wurde mit einem Beispiel für die Erstellung des verketteten Werts für das Feld **[!UICONTROL Benutzername]** unter Verwendung des [!DNL Oracle Eloqua] Unternehmensnamens und des [!DNL Oracle Eloqua] Benutzernamens aktualisiert. (PLATIR-28343)</li><li>Die Abschnitte [Sammeln [!DNL Oracle Eloqua] Anmeldeinformationen](#gather-credentials) und [Ausfüllen der Zieldetails](#destination-details) wurden mit Anleitungen zur Auswahl [!DNL Oracle Eloqua] **[!UICONTROL Pod]** aktualisiert. Der *Pod“*-Wert wird vom Ziel verwendet, um die Basis-URL für die API-Aufrufe zu erstellen. Der Abschnitt [[!DNL Oracle Eloqua] Voraussetzungen](#prerequisites-destination) wurde auch mit Anleitungen zum Zuweisen von *„Erweiterte Benutzer - Marketing-Berechtigungen“* als erforderliches *„Sicherheitsgruppen“* für Ihre [!DNL Oracle Eloqua]-Instanz aktualisiert.</li></ul> |
| März 2023 | Erstmalige Veröffentlichung | Erstmalige Zielveröffentlichung und Dokumentation. |

{style="table-layout:auto"}

+++