---
title: (API) Oracle Eloqua-Verbindung
description: Mit dem (API) Oracle Eloqua-Ziel können Sie Ihre Kontodaten exportieren und innerhalb von Oracle Eloqua für Ihre Geschäftsanforderungen aktivieren.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2156'
ht-degree: 32%

---


# [!DNL (API) Oracle Eloqua]-Verbindung

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) ermöglicht es Marketing-Experten, Kampagnen zu planen und auszuführen und gleichzeitig ein personalisiertes Kundenerlebnis für ihre potenziellen Kunden bereitzustellen. Dank integrierter Lead-Verwaltung und einfacher Kampagnenerstellung können Marketingexperten die richtige Zielgruppe zum richtigen Zeitpunkt auf der Journey ansprechen und elegant skalieren, um Zielgruppen kanalübergreifend zu erreichen, einschließlich E-Mail, Display-Suche, Video und Mobil. Vertriebsteams können mehr Angebote schneller schließen und so den Marketing-ROI durch Echtzeiteinblicke steigern.

Diese [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt die [Kontakt aktualisieren](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) Vorgang von [!DNL Oracle Eloqua] REST-API, mit der Sie **Identitäten aktualisieren** innerhalb einer Zielgruppe in [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] uses [Grundlegende Authentifizierung](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) zur Kommunikation mit dem [!DNL Oracle Eloqua] REST-API. Anweisungen zur Authentifizierung bei Ihrer [!DNL Oracle Eloqua]-Instanz sehen Sie weiter unten im Abschnitt [Authentifizieren bei Ziel](#authenticate).

## Anwendungsbeispiele {#use-cases}

Die Marketingabteilung einer Online-Plattform möchte eine E-Mail-basierte Marketing-Kampagne an eine kuratierte Zielgruppe von Leads senden. Das Marketing-Team der Plattform kann vorhandene Lead-Informationen über Adobe Experience Platform aktualisieren, Zielgruppen aus eigenen Offline-Daten erstellen und diese Zielgruppen an senden [!DNL Oracle Eloqua], die dann zum Versand der E-Mail-Adresse der Marketing-Kampagne verwendet werden kann.

## Voraussetzungen {#prerequisites}

### Voraussetzungen für Experience Platform {#prerequisites-in-experience-platform}

Vor der Aktivierung der Daten für das [!DNL Oracle Eloqua]-Ziel müssen Sie über ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=de) und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) verfügen, die in [!DNL Experience Platform] erstellt wurden.

Weitere Informationen finden Sie in der Experience Platform-Dokumentation für [Feldergruppe Zielgruppenzugehörigkeitsdetails](/help/xdm/field-groups/profile/segmentation.md) wenn Sie Anleitungen zum Zielgruppenstatus benötigen.

### Voraussetzungen für [!DNL Oracle Eloqua] {#prerequisites-destination}

So exportieren Sie Daten von Platform in Ihre [!DNL Oracle Eloqua] -Konto, für das Sie eine [!DNL Oracle Eloqua] -Konto.

Darüber hinaus benötigen Sie mindestens die Variable *&quot;Erweiterte Benutzer - Marketing-Berechtigungen&quot;* für Ihre [!DNL Oracle Eloqua] -Instanz. Siehe Abschnitt *&quot;Sicherheitsgruppen&quot;* im Abschnitt [Sicherer Benutzerzugriff](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm) -Seite für Anleitungen. Der Zugriff ist für das Ziel erforderlich, um programmgesteuert [die Basis-URL bestimmen](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html) beim Aufrufen der [!DNL Oracle Eloqua] API.

#### Sammeln von [!DNL Oracle Eloqua]-Anmeldeinformationen {#gather-credentials}

Beachten Sie die folgenden Elemente, bevor Sie sich bei der [!DNL Oracle Eloqua] Ziel:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `Company Name` | Der mit Ihrer [!DNL Oracle Eloqua] -Konto. <br>Sie verwenden später die `Company Name` und [!DNL Oracle Eloqua] `Username` als verkettete Zeichenfolge, die als **[!UICONTROL Benutzername]** when [beim Ziel authentifizieren](#authenticate). |
| `Username` | Der Benutzername Ihres [!DNL Oracle Eloqua] -Konto. |
| `Password` | Das Kennwort Ihres [!DNL Oracle Eloqua] -Konto. |
| `Pod` | [!DNL Oracle Eloqua] unterstützt mehrere Rechenzentren mit jeweils einem eindeutigen Domänennamen. [!DNL Oracle Eloqua] bezeichnet diese als &quot;Pods&quot;, es gibt derzeit insgesamt sieben - p01, p02, p03, p04, p06, p07 und p08. Um zu erfahren, welchen POD Sie verwenden, melden Sie sich bei an. [!DNL Oracle Eloqua] und beachten Sie die URL in Ihrem Browser, nachdem Sie sich erfolgreich angemeldet haben. Wenn Ihre Browser-URL beispielsweise `secure.p01.eloqua.com` Ihre `pod` is `p01`. Siehe Abschnitt [Bestimmen Ihres POD](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua) für zusätzliche Anleitungen. |

Siehe Abschnitt [Anmelden bei [!DNL Oracle Eloqua]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing) für Leitlinien.

## Leitplanken {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] Benutzerdefinierte Kontaktfelder werden automatisch unter Verwendung der Namen der Zielgruppen erstellt, die während der **[!UICONTROL Segmente auswählen]** Schritt.

* [!DNL Oracle Eloqua] hat eine maximale Anzahl von 250 benutzerdefinierten Kontaktfeldern.
* Stellen Sie vor dem Export neuer Zielgruppen sicher, dass die Anzahl der Platform-Zielgruppen und die Anzahl der vorhandenen Zielgruppen in [!DNL Oracle Eloqua] diese Grenze nicht überschreiten.
* Wenn diese Grenze überschritten wird, tritt beim Experience Platform ein Fehler auf. Dies liegt daran, dass die Variable [!DNL Oracle Eloqua] Die API kann die Anfrage nicht validieren und antwortet mit einem - *400: Validierungsfehler* - Fehlermeldung, die das Problem beschreibt.
* Wenn Sie die oben angegebene Grenze erreicht haben, müssen Sie vorhandene Zuordnungen aus Ihrem Ziel entfernen und die entsprechenden benutzerdefinierten Kontaktfelder in Ihrem [!DNL Oracle Eloqua] , bevor Sie weitere Segmente exportieren können.

* Siehe Abschnitt [[!DNL Oracle Eloqua] Erstellen von Kontaktfeldern](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) Seite mit Informationen zu zusätzlichen Beschränkungen.

## Unterstützte Identitäten {#supported-identities}

[!DNL Oracle Eloqua] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/namespaces.md).

| Ziel-Identität | Beschreibung | Obligatorisch |
|---|---|---|
| `EloquaId` | Eindeutige Kennung des Kontakts. | Ja |

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern *(z. B.: E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Für jede ausgewählte Zielgruppe in Platform wird die entsprechende [!DNL Oracle Eloqua] Der Segmentstatus wird mit dem Zielgruppenstatus von Platform aktualisiert.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | <ul><li>Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** nach [!DNL (API) Oracle Eloqua]. Alternativ können Sie sie unter der **[!UICONTROL E-Mail-Marketing]** Kategorie.

### Beim Ziel authentifizieren {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="Firmenname\Benutzername"
>abstract="Füllen Sie dieses Feld mit Ihrem Firmennamen und dem Benutzernamen von Oracle Eloqua aus `{COMPANY_NAME}\{USERNAME}`"

Füllen Sie die erforderlichen Felder aus. Eine Anleitung dazu finden Sie im Abschnitt [ [!DNL Oracle Eloqua] Sammeln von -Anmeldeinformationen](#gather-credentials).
* **[!UICONTROL Passwort]**: Das Kennwort Ihres [!DNL Oracle Eloqua] -Konto.
* **[!UICONTROL Benutzername]**: Eine verkettete Zeichenfolge aus Ihrem [!DNL Oracle Eloqua] Firmenname und [!DNL Oracle Eloqua] Benutzername.<br>Der verkettete Wert hat die Form `{COMPANY_NAME}\{USERNAME}`.<br> Beachten Sie, dass Sie keine Leerzeichen oder Leerzeichen verwenden und die `\`. <br>Beispiel: Wenn [!DNL Oracle Eloqua] Firmenname ist `MyCompany` und [!DNL Oracle Eloqua] Benutzername ist `Username`, der verkettete Wert, den Sie im **[!UICONTROL Benutzername]** Feld ist `MyCompany\Username`.

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Mit Ziel verbinden]**.
![Screenshot der Platform-Benutzeroberfläche, auf dem die Authentifizierung gezeigt wird.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche den Status **[!UICONTROL Verbunden]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="Um Ihre Pod-Nummer zu finden, melden Sie sich bei Oracle Eloqua an. Notieren Sie die URL in Ihrem Browser, nachdem Sie sich erfolgreich angemeldet haben. "
>additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Oracle-Wissensdatenbank – Erfahren Sie mehr über Ihre Pod-Nummer"

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
![Screenshot der Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Pod]**: So erhalten Sie welche `pod` Sie sind auf, melden Sie sich bei [!DNL Oracle Eloqua] und beachten Sie die URL in Ihrem Browser, nachdem Sie sich erfolgreich angemeldet haben. Wenn Ihre Browser-URL beispielsweise `secure.p01.eloqua.com` die `pod` Wert, den Sie auswählen müssen, ist `p01`. Siehe Abschnitt [Gather [!DNL Oracle Eloqua] Anmeldeinformationen](#gather-credentials) für zusätzliche Anleitungen.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

Um Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an das [!DNL Oracle Eloqua]-Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodells (XDM) in Ihrem Platform-Konto und den jeweiligen Entsprechungen vom Ziel zu erstellen.

So ordnen Sie Ihre XDM-Felder dem [!DNL Oracle Eloqua] Führen Sie die folgenden Schritte aus:

1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird eine neue Zuordnungszeile angezeigt.
1. Im **[!UICONTROL Quellfeld auswählen]** Fenster, wählen Sie die **[!UICONTROL Attribute auswählen]** und wählen Sie das XDM-Attribut oder die **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie eine Identität.
1. Im **[!UICONTROL Zielgruppenfeld auswählen]** auswählen **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie eine Identität aus oder wählen Sie **[!UICONTROL Benutzerdefinierte Attribute auswählen]** und geben Sie den gewünschten Attributnamen in die **[!UICONTROL Attributname]** -Feld. Der Attributname, den Sie angeben, sollte mit dem vorhandenen Kontaktattribut in [!DNL Oracle Eloqua]. Siehe [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) für die genauen Attributnamen, die Sie in [!DNL Oracle Eloqua].
   * Wiederholen Sie diese Schritte, um sowohl die erforderlichen als auch alle gewünschten Attributzuordnungen zwischen Ihrem XDM-Profilschema und [!DNL Oracle Eloqua]: | Quellfeld | Zielfeld | Erforderlich | |—|—|—| |`IdentityMap: Eid`|`Identity: EloquaId`| Ja | |`xdm: personalEmail.address`|`Attribute: emailAddress`| Ja | |`xdm: personName.firstName`|`Attribute: firstName`| | |`xdm: personName.lastName`|`Attribute: lastName`| | |`xdm: workAddress.street1`|`Attribute: address1`| | |`xdm: workAddress.street2`|`Attribute: address2`| | |`xdm: workAddress.street3`|`Attribute: address3`| | |`xdm: workAddress.postalCode`|`Attribute: postalCode`| | |`xdm: workAddress.country`|`Attribute: country`| | |`xdm: workAddress.city`|`Attribute: city`| |

   * Nachfolgend finden Sie ein Beispiel mit den oben aufgeführten Zuordnungen:
     ![Screenshot der Platform-Benutzeroberfläche mit Attributzuordnungen.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* In der Variablen **[!UICONTROL Zielfeld]** sollte genau wie in der Variablen [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) da diese Attribute den Anfrageinhalt bilden.
>* In der Variablen **[!UICONTROL Quellfeld]** keine solchen Einschränkungen befolgen. Sie können sie jedoch nach Bedarf zuordnen, wenn das Datenformat beim Senden an [!DNL Oracle Eloqua] wird ein Fehler ausgegeben. Sie können beispielsweise die **[!UICONTROL Quellfeld]** Identitäts-Namespace `contact key`, `ABC ID` usw. nach **[!UICONTROL Zielfeld]** : `EloquaId` nachdem sichergestellt wurde, dass die ID-Werte mit dem Format übereinstimmen, das von [!DNL Oracle Eloqua].
>* Die `EloquaID` -Zuordnung ist erforderlich, um Attribute zu aktualisieren, die der Identität entsprechen.
>* Die `emailAddress` -Zuordnung erforderlich. Andernfalls gibt die API einen Fehler aus, wie unten dargestellt:
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

Wenn Sie mit der Bereitstellung der Zuordnungen für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Nächste]**.

>[!NOTE]
>
>Bei jeder Ausführung fügt das Ziel den ausgewählten Zielgruppennamen automatisch eine eindeutige Kennung hinzu, wenn die Kontaktinformationen an [!DNL Oracle Eloqua]. Dadurch wird sichergestellt, dass sich die Kontaktfeldnamen, die Ihren Zielgruppennamen entsprechen, nicht überschneiden. Siehe Abschnitt [Datenexport überprüfen](#exported-data) Screenshot-Beispiel eines Abschnitts [!DNL Oracle Eloqua] Kontaktinformationen-Seite mit benutzerdefiniertem Kontaktfeld, das mithilfe der Zielgruppennamen erstellt wurde.

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Auswählen **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** und navigieren Sie zur Liste der Ziele.
1. Wählen Sie als Nächstes das Ziel aus und wechseln Sie zur **[!UICONTROL Aktivierungsdaten]** und wählen Sie einen Zielgruppennamen aus.
   ![Beispiel-Screenshot der Platform-Benutzeroberfläche mit Daten zur Aktivierung von Zielen.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Überwachen Sie die Zielgruppenzusammenfassung und stellen Sie sicher, dass die Anzahl der Profile der Anzahl innerhalb des Segments entspricht.
   ![Beispiel-Screenshot der Platform-Benutzeroberfläche mit Segment.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Melden Sie sich bei [!DNL Oracle Eloqua] Website und navigieren Sie dann zur **[!UICONTROL Kontaktübersicht]** -Seite, um zu überprüfen, ob die Profile aus der Audience hinzugefügt wurden. Um den Zielgruppenstatus anzuzeigen, führen Sie einen Drilldown in eine **[!UICONTROL Kontaktdetails]** und überprüfen Sie, ob das Kontaktfeld mit dem ausgewählten Zielgruppennamen als Präfix erstellt wurde.

![Oracle Eloqua UI-Screenshot mit der Seite &quot;Kontaktdetails&quot;mit dem benutzerdefinierten Kontaktfeld, das mit dem Zielgruppennamen erstellt wurde.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

Beim Erstellen des Ziels erhalten Sie möglicherweise eine der folgenden Fehlermeldungen: `400: There was a validation error` oder `400 BAD_REQUEST`. Dies geschieht, wenn Sie die Beschränkung von 250 benutzerdefinierten Kontaktfeldern überschreiten, wie im Abschnitt [Limits](#guardrails) Abschnitt. Um diesen Fehler zu beheben, dürfen Sie die benutzerdefinierte Feldbegrenzung in [!DNL Oracle Eloqua].
![Screenshot der Platform-Benutzeroberfläche mit Fehlermeldung.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Siehe Abschnitt [[!DNL Oracle Eloqua] HTTP-Statuscodes](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) und [[!DNL Oracle Eloqua] Validierungsfehler](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) Seiten für eine umfassende Liste von Status- und Fehlercodes mit Erklärungen.

## Zusätzliche Ressourcen {#additional-resources}

Weitere Informationen finden Sie im Abschnitt [!DNL Oracle Eloqua] Dokumentation:

* [Oracle Eloqua Marketing Automation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [REST-API für Oracle Eloqua Marketing Cloud Service](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### Änderungsprotokoll

In diesem Abschnitt werden aktualisierte Funktionen und wesentliche Dokumentationsänderungen für diesen Ziel-Connector erfasst.

+++ Änderungsprotokoll anzeigen

| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| April 2023 | Aktualisierung der Dokumentation | <ul><li>Wir haben die [Anwendungsfälle](#use-cases) mit einem klareren Beispiel dafür, wann Kunden von der Verwendung dieses Ziels profitieren würden.</li> <li>Wir haben die [Mapping](#mapping-considerations-example) mit klaren Beispielen für obligatorische und optionale Zuordnungen.</li> <li>Wir haben die [Mit Ziel verbinden](#connect) -Abschnitt mit einem Beispiel zum Erstellen des verketteten Werts für die **[!UICONTROL Benutzername]** -Feld mithilfe des [!DNL Oracle Eloqua] Firmenname und [!DNL Oracle Eloqua] Benutzername. (PLATIR-28343)</li><li>Wir haben die [Gather [!DNL Oracle Eloqua] Anmeldeinformationen](#gather-credentials) und [Zieldetails ausfüllen](#destination-details) Abschnitte mit Anleitungen [!DNL Oracle Eloqua] **[!UICONTROL Pod]** auswählen. Die *&quot;Pod&quot;* -Wert wird vom Ziel verwendet, um die Basis-URL für die API-Aufrufe zu erstellen. Die [[!DNL Oracle Eloqua] Voraussetzungen](#prerequisites-destination) wurde auch mit Anleitungen zum Zuweisen von *&quot;Erweiterte Benutzer - Marketing-Berechtigungen&quot;* als erforderlich *&quot;Sicherheitsgruppen&quot;* für Ihre [!DNL Oracle Eloqua] -Instanz.</li></ul> |
| März 2023 | Erstmalige Veröffentlichung | Erste Zielversion und Veröffentlichung der Dokumentation. |

{style="table-layout:auto"}

+++