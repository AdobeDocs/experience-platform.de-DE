---
title: (API) Oracle Eloqua-Verbindung
description: Mit dem (API) Oracle Eloqua-Ziel können Sie Ihre Kontodaten exportieren und innerhalb von Oracle Eloqua für Ihre Geschäftsanforderungen aktivieren.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '2033'
ht-degree: 30%

---


# [!DNL (API) Oracle Eloqua]-Verbindung

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) ermöglicht es Marketing-Experten, Kampagnen zu planen und auszuführen und gleichzeitig ein personalisiertes Kundenerlebnis für ihre potenziellen Kunden bereitzustellen. Dank integrierter Lead-Verwaltung und einfacher Kampagnenerstellung können Marketingexperten die richtige Zielgruppe zum richtigen Zeitpunkt auf der Journey ansprechen und elegant skalieren, um Zielgruppen kanalübergreifend zu erreichen, einschließlich E-Mail, Display-Suche, Video und Mobil. Vertriebsteams können mehr Angebote schneller schließen und so den Marketing-ROI durch Echtzeiteinblicke steigern.

Dieses [!DNL Adobe Experience Platform] [Ziel](/help/destinations/home.md) nutzt den Vorgang [Kontaktaufnahme aktualisieren](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) der [!DNL Oracle Eloqua] REST-API, mit dem Sie **Identitäten innerhalb einer Audience in [!DNL Oracle Eloqua] aktualisieren können.**

[!DNL Oracle Eloqua] verwendet [Grundlegende Authentifizierung](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) für die Kommunikation mit der [!DNL Oracle Eloqua] REST-API. Anweisungen zur Authentifizierung bei Ihrer [!DNL Oracle Eloqua]-Instanz sehen Sie weiter unten im Abschnitt [Authentifizieren bei Ziel](#authenticate).

## Anwendungsbeispiele {#use-cases}

Die Marketingabteilung einer Online-Plattform möchte eine E-Mail-basierte Marketing-Kampagne an eine kuratierte Zielgruppe von Leads senden. Das Marketing-Team der Plattform kann vorhandene Lead-Informationen über Adobe Experience Platform aktualisieren, Zielgruppen aus eigenen Offline-Daten erstellen und diese Zielgruppen an [!DNL Oracle Eloqua] senden, was dann zum Senden der E-Mail-Adresse der Marketing-Kampagne verwendet werden kann.

## Voraussetzungen {#prerequisites}

### Voraussetzungen für Experience Platform {#prerequisites-in-experience-platform}

Vor der Aktivierung der Daten für das [!DNL Oracle Eloqua]-Ziel müssen Sie über ein [Schema](/help/xdm/schema/composition.md), einen [Datensatz](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) und [Segmente](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) verfügen, die in [!DNL Experience Platform] erstellt wurden.

Informationen zum Zielgruppenstatus finden Sie in der Experience Platform-Dokumentation für die Schemafeldergruppe [Zielgruppenzugehörigkeitsdetails](/help/xdm/field-groups/profile/segmentation.md) .

### Voraussetzungen für [!DNL Oracle Eloqua] {#prerequisites-destination}

Um Daten von Platform in Ihr [!DNL Oracle Eloqua] -Konto zu exportieren, benötigen Sie ein [!DNL Oracle Eloqua] -Konto.

Zusätzlich benötigen Sie mindestens die *&quot;Erweiterte Benutzer - Marketing-Berechtigungen&quot;* für Ihre [!DNL Oracle Eloqua] -Instanz. Eine Anleitung dazu finden Sie im Abschnitt *&quot;Sicherheitsgruppen&quot;* auf der Seite [Sicherer Benutzerzugriff](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm) . Der Zugriff ist für das Ziel erforderlich, um beim Aufrufen der [!DNL Oracle Eloqua] -API programmgesteuert [Ihre Basis-URL](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html) zu bestimmen.

#### Sammeln von [!DNL Oracle Eloqua]-Anmeldedaten {#gather-credentials}

Beachten Sie die folgenden Elemente, bevor Sie sich beim [!DNL Oracle Eloqua]-Ziel authentifizieren:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `Company Name` | Der mit Ihrem [!DNL Oracle Eloqua]-Konto verknüpfte Unternehmensname. <br>Sie verwenden später die `Company Name` und [!DNL Oracle Eloqua] `Username` als verkettete Zeichenfolge, die als **[!UICONTROL Benutzername]** verwendet werden soll, wenn [sich beim Ziel authentifizieren](#authenticate). |
| `Username` | Der Benutzername Ihres [!DNL Oracle Eloqua]-Kontos. |
| `Password` | Das Kennwort Ihres [!DNL Oracle Eloqua]-Kontos. |
| `Pod` | [!DNL Oracle Eloqua] unterstützt mehrere Rechenzentren mit jeweils einem eindeutigen Domänennamen. [!DNL Oracle Eloqua] bezeichnet diese als &quot;Pods&quot;, derzeit sind es insgesamt sieben - p01, p02, p03, p04, p06, p07 und p08. Um den POD abzurufen, melden Sie sich bei [!DNL Oracle Eloqua] an und notieren Sie sich die URL in Ihrem Browser, nachdem Sie sich erfolgreich angemeldet haben. Wenn Ihre Browser-URL beispielsweise &quot;`secure.p01.eloqua.com`&quot; lautet, lautet Ihr `pod` &quot;`p01`&quot;. Weitere Anleitungen finden Sie auf der Seite [Bestimmen Ihres POD](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua) . |

Eine Anleitung dazu finden Sie unter [Anmelden bei  [!DNL Oracle Eloqua]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing) .

## Leitplanken {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] benutzerdefinierte Kontaktfelder werden automatisch unter Verwendung der Namen der Zielgruppen erstellt, die im Schritt **[!UICONTROL Segmente auswählen]** ausgewählt wurden.

* [!DNL Oracle Eloqua] erlaubt maximal 250 benutzerdefinierte Kontaktfelder.
* Stellen Sie vor dem Export neuer Zielgruppen sicher, dass die Anzahl der Platform-Zielgruppen und die Anzahl der vorhandenen Zielgruppen innerhalb von [!DNL Oracle Eloqua] diese Grenze nicht überschreiten.
* Wenn diese Grenze überschritten wird, tritt beim Experience Platform ein Fehler auf. Der Grund dafür ist, dass die [!DNL Oracle Eloqua] -API die Anfrage nicht validieren kann und mit einer Fehlermeldung - *400: Es gab einen Validierungsfehler* - antwortet, die das Problem beschreibt.
* Wenn Sie die oben angegebene Grenze erreicht haben, müssen Sie vorhandene Zuordnungen aus Ihrem Ziel entfernen und die entsprechenden benutzerdefinierten Kontaktfelder in Ihrem [!DNL Oracle Eloqua] -Konto löschen, bevor Sie weitere Segmente exportieren können.

* Weitere Informationen zu zusätzlichen Beschränkungen finden Sie auf der Seite [[!DNL Oracle Eloqua] Erstellen von Kontaktfeldern](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) .

## Unterstützte Identitäten {#supported-identities}

[!DNL Oracle Eloqua] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Obligatorisch |
|---|---|---|
| `EloquaId` | Eindeutige Kennung des Kontakts. | Ja |

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | <ul><li>Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern *(z. B.: E-Mail-Adresse, Telefonnummer, Nachname)*, entsprechend Ihrer Feldzuordnung.</li><li> Für jede ausgewählte Zielgruppe in Platform wird der entsprechende Segmentstatus [!DNL Oracle Eloqua] mit dem Zielgruppenstatus von Platform aktualisiert.</li></ul> |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | <ul><li>Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

Suchen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** nach [!DNL (API) Oracle Eloqua]. Alternativ können Sie ihn unter der Kategorie **[!UICONTROL E-Mail-Marketing]** finden.

### Beim Ziel authentifizieren {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="Firmenname\Benutzername"
>abstract="Füllen Sie dieses Feld mit Ihrem Firmennamen und dem Benutzernamen von Oracle Eloqua aus `{COMPANY_NAME}\{USERNAME}`"

Füllen Sie die erforderlichen Felder aus. Eine Anleitung finden Sie im Abschnitt [Anmeldedaten sammeln [!DNL Oracle Eloqua] 2} .](#gather-credentials)
* **[!UICONTROL Kennwort]**: Das Kennwort Ihres [!DNL Oracle Eloqua]-Kontos.
* **[!UICONTROL Benutzername]**: Eine verkettete Zeichenfolge, die aus Ihrem [!DNL Oracle Eloqua] Firmennamen und dem [!DNL Oracle Eloqua] Benutzernamen besteht.<br>Der verkettete Wert hat die Form &quot;`{COMPANY_NAME}\{USERNAME}`&quot;.<br> Beachten Sie, dass Sie keine geschweiften Klammern oder Leerzeichen verwenden und die `\` beibehalten. <br>Wenn Ihr [!DNL Oracle Eloqua] Firmenname beispielsweise `MyCompany` und [!DNL Oracle Eloqua] Benutzername `Username` ist, lautet der verkettete Wert, den Sie im Feld **[!UICONTROL Benutzername]** verwenden, `MyCompany\Username`.

Um sich beim Ziel zu authentifizieren, wählen Sie **[!UICONTROL Mit Ziel verbinden]**.
![Screenshot der Platform-Benutzeroberfläche, auf dem die Authentifizierung gezeigt wird.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Wenn die angegebenen Details gültig sind, zeigt die Benutzeroberfläche den Status **[!UICONTROL Verbunden]** mit einem grünen Häkchen an. Sie können dann mit dem nächsten Schritt fortfahren.

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="Um Ihre Pod-Nummer zu finden, melden Sie sich bei Oracle Eloqua an. Notieren Sie die URL in Ihrem Browser, nachdem Sie sich erfolgreich angemeldet haben. "

<!-- >additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Oracle Knowledge base - find out your Pod number" -->

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.
![Screenshot der Platform-Benutzeroberfläche mit den Zieldetails.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Werbeunterbrechung]**: Um den `pod` zu erhalten, auf dem Sie sich befinden, melden Sie sich bei [!DNL Oracle Eloqua] an und notieren Sie sich die URL in Ihrem Browser, nachdem Sie sich erfolgreich angemeldet haben. Wenn Ihre Browser-URL beispielsweise `secure.p01.eloqua.com` ist, müssen Sie den Wert `pod` als `p01` auswählen. Weitere Hinweise finden Sie im Abschnitt [Anmeldedaten sammeln [!DNL Oracle Eloqua] 2} .](#gather-credentials)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnungsüberlegungen und Beispiel {#mapping-considerations-example}

Um Ihre Zielgruppendaten ordnungsgemäß von Adobe Experience Platform an das [!DNL Oracle Eloqua]-Ziel zu senden, müssen Sie den Schritt zur Feldzuordnung durchlaufen. Die Zuordnung besteht darin, eine Verknüpfung zwischen den Schemafeldern Ihres Experience-Datenmodell (XDM) in Ihrem Platform-Konto und den entsprechenden Entsprechungen vom Ziel zu erstellen.

Gehen Sie wie folgt vor, um Ihre XDM-Felder den [!DNL Oracle Eloqua] -Zielfeldern zuzuordnen:

1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird eine neue Zuordnungszeile angezeigt.
1. Wählen Sie im Fenster **[!UICONTROL Quellfeld auswählen]** die Kategorie **[!UICONTROL Attribute auswählen]** aus, wählen Sie das XDM-Attribut aus oder wählen Sie den Eintrag **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie eine Identität aus.
1. Wählen Sie im Fenster **[!UICONTROL Zielfeld auswählen]** die Option **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie eine Identität aus oder wählen Sie **[!UICONTROL Benutzerdefinierte Attribute auswählen]** und geben Sie den gewünschten Attributnamen in das Feld **[!UICONTROL Attributname]** ein. Der von Ihnen angegebene Attributname sollte mit dem in [!DNL Oracle Eloqua] vorhandenen Kontaktattribut übereinstimmen. Unter [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) finden Sie die genauen Attributnamen, die Sie in [!DNL Oracle Eloqua] verwenden können.

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

   * Nachfolgend finden Sie ein Beispiel mit den oben aufgeführten Zuordnungen:
     ![Screenshot der Platform-Benutzeroberfläche mit Attributzuordnungen.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* Die im Feld **[!UICONTROL Ziel]** angegebenen Attribute müssen genau so benannt sein, wie in [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) angegeben, da diese Attribute den Anfrageinhalt bilden.
>* Im Feld **[!UICONTROL Source]** angegebene Attribute unterliegen keiner solchen Einschränkung. Sie können sie nach Bedarf zuordnen. Wenn das Datenformat jedoch beim Pushen auf [!DNL Oracle Eloqua] nicht korrekt ist, wird ein Fehler ausgegeben. Sie können beispielsweise den Identitäts-Namespace **[!UICONTROL Source field]** `contact key`, `ABC ID` usw. zuordnen. auf **[!UICONTROL Zielfeld]** : `EloquaId` , nachdem sichergestellt wurde, dass die ID-Werte mit dem Format übereinstimmen, das von [!DNL Oracle Eloqua] akzeptiert wird.
>* Die Zuordnung `EloquaID` ist erforderlich, um Attribute zu aktualisieren, die der Identität entsprechen.
>* Die `emailAddress` -Zuordnung ist erforderlich. Andernfalls gibt die API einen Fehler aus, wie unten dargestellt:
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

Wenn Sie die Zuordnungen für Ihre Zielverbindung bereitgestellt haben, wählen Sie **[!UICONTROL Weiter]** aus.

>[!NOTE]
>
>Das Ziel fügt bei jeder Ausführung beim Senden der Kontaktinformationen an [!DNL Oracle Eloqua] automatisch eine eindeutige Kennung den ausgewählten Zielgruppennamen hinzu. Dadurch wird sichergestellt, dass sich die Kontaktfeldnamen, die Ihren Zielgruppennamen entsprechen, nicht überschneiden. Siehe Screenshot des Abschnitts [Datenexport überprüfen](#exported-data) einer Seite mit [!DNL Oracle Eloqua] Kontaktdetails mit benutzerdefinierten Kontaktfeldern, die mit den Zielgruppennamen erstellt wurden.

## Überprüfen des Datenexports {#exported-data}

Gehen Sie wie folgt vor, um zu überprüfen, ob Sie das Ziel korrekt eingerichtet haben:

1. Wählen Sie **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** aus und navigieren Sie zur Liste der Ziele.
1. Wählen Sie anschließend das Ziel aus und wechseln Sie zur Registerkarte **[!UICONTROL Aktivierungsdaten]** und wählen Sie dann einen Zielgruppennamen aus.
   ![Beispiel-Screenshot der Platform-Benutzeroberfläche mit Daten zur Aktivierung von Zielen.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Überwachen Sie die Zielgruppenzusammenfassung und stellen Sie sicher, dass die Anzahl der Profile der Anzahl innerhalb des Segments entspricht.
   ![Beispiel-Screenshot der Platform-Benutzeroberfläche mit Segment.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Melden Sie sich bei der [!DNL Oracle Eloqua] -Website an und navigieren Sie dann zur Seite **[!UICONTROL Kontaktübersicht]** , um zu überprüfen, ob die Profile aus der Zielgruppe hinzugefügt wurden. Um den Zielgruppenstatus anzuzeigen, führen Sie einen Drilldown zur Seite **[!UICONTROL Kontaktdetails]** durch und überprüfen Sie, ob das Kontaktfeld mit dem ausgewählten Zielgruppennamen als Präfix erstellt wurde.

![Oracle Eloqua UI-Screenshot mit der Seite &quot;Kontaktdetails&quot;mit dem benutzerdefinierten Kontaktfeld, das mit dem Zielgruppennamen erstellt wurde.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

Beim Erstellen des Ziels erhalten Sie möglicherweise eine der folgenden Fehlermeldungen: `400: There was a validation error` oder `400 BAD_REQUEST`. Dies geschieht, wenn Sie die Beschränkung von 250 benutzerdefinierten Kontaktfeldern überschreiten, wie im Abschnitt [Limits](#guardrails) beschrieben. Um diesen Fehler zu beheben, stellen Sie sicher, dass Sie die Grenze für benutzerdefinierte Kontaktfelder in [!DNL Oracle Eloqua] nicht überschreiten.
![Screenshot der Platform-Benutzeroberfläche mit Fehler.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Eine umfassende Liste der Status- und Fehlercodes mit Erklärungen finden Sie auf den Seiten [[!DNL Oracle Eloqua] HTTP-Status-Codes](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) und [[!DNL Oracle Eloqua] Validierungsfehler](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) .

## Zusätzliche Ressourcen {#additional-resources}

Weitere Informationen finden Sie in der Dokumentation zu [!DNL Oracle Eloqua]:

* [Oracle Eloqua Marketing Automation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [REST-API für Oracle Eloqua Marketing Cloud Service](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### Änderungsprotokoll

In diesem Abschnitt werden aktualisierte Funktionen und wesentliche Dokumentationsänderungen für diesen Ziel-Connector erfasst.

+++ Änderungsprotokoll anzeigen

| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| April 2023 | Aktualisierung der Dokumentation | <ul><li>Wir haben den Abschnitt [Anwendungsfälle](#use-cases) mit einem klareren Beispiel aktualisiert, wann Kunden von der Verwendung dieses Ziels profitieren würden.</li> <li>Wir haben den Abschnitt [Zuordnen](#mapping-considerations-example) mit klaren Beispielen für obligatorische und optionale Zuordnungen aktualisiert.</li> <li>Wir haben den Abschnitt [Verbindung zum Ziel herstellen](#connect) mit einem Beispiel aktualisiert, in dem erläutert wird, wie der verkettete Wert für das Feld **[!UICONTROL Benutzername]** unter Verwendung von [!DNL Oracle Eloqua] Firmenname und [!DNL Oracle Eloqua] Benutzername erstellt werden kann. (PLATIR-28343)</li><li>Wir haben die Abschnitte [Gather [!DNL Oracle Eloqua] credentials](#gather-credentials) und [Fill in Zieldetails](#destination-details) mit Anleitungen zur Auswahl [!DNL Oracle Eloqua] **[!UICONTROL Pod]** aktualisiert. Der Wert *&quot;Pod&quot;* wird vom Ziel verwendet, um die Basis-URL für die API-Aufrufe zu erstellen. Der Abschnitt [[!DNL Oracle Eloqua] Voraussetzungen](#prerequisites-destination) wurde ebenfalls mit Anleitungen zum Zuweisen von *&quot;Erweiterte Benutzer - Marketing-Berechtigungen&quot;* als erforderlichen *&quot;Sicherheitsgruppen&quot;* für Ihre [!DNL Oracle Eloqua]-Instanz aktualisiert.</li></ul> |
| März 2023 | Erstmalige Veröffentlichung | Erste Zielversion und Veröffentlichung der Dokumentation. |

{style="table-layout:auto"}

+++