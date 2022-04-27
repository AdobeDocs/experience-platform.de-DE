---
title: HTTP-API-Verbindung
keywords: Streaming;
description: Verwenden Sie das HTTP-API-Ziel in Adobe Experience Platform, um Profildaten an den Drittanbieter-HTTP-Endpunkt zu senden, um Ihre eigenen Analysen auszuführen oder andere Vorgänge durchzuführen, die Sie möglicherweise für aus Experience Platform exportierte Profildaten benötigen.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 30549f31e7ba7f9cfafd2e71fb3ccfb701b9883f
workflow-type: tm+mt
source-wordcount: '2296'
ht-degree: 3%

---

# HTTP-API-Verbindung

## Übersicht {#overview}

>[!IMPORTANT]
>
> Dieses Ziel ist nur für [Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) -Kunden.

Das HTTP-API-Ziel ist ein [!DNL Adobe Experience Platform] Streaming-Ziel, mit dem Sie Profildaten an HTTP-Endpunkte von Drittanbietern senden können.

Um Profildaten an HTTP-Endpunkte zu senden, müssen Sie zunächst [Verbindung zum Ziel herstellen](#connect-destination) in [!DNL Adobe Experience Platform].

## Anwendungsfälle {#use-cases}

Mit dem HTTP-API-Ziel können Sie XDM-Profildaten und Zielgruppensegmente in allgemeine HTTP-Endpunkte exportieren. Dort können Sie Ihre eigenen Analysen durchführen oder beliebige andere Vorgänge ausführen, die Sie für aus der Experience Platform exportierte Profildaten benötigen.

HTTP-Endpunkte können entweder eigene Systeme von Kunden oder Lösungen von Drittanbietern sein.

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Mapping-Bildschirm des [Zielaktivierungs-Workflow](../../ui/activate-segment-streaming-destinations.md#mapping). |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Voraussetzungen {#prerequisites}

Um Daten aus Experience Platform mithilfe des HTTP-API-Ziels zu exportieren, müssen folgende Voraussetzungen erfüllt sein:

* Sie müssen über einen HTTP-Endpunkt verfügen, der die REST-API unterstützt.
* Ihr HTTP-Endpunkt muss das Experience Platform-Profilschema unterstützen. Im HTTP-API-Ziel wird keine Umwandlung in ein Drittanbieter-Payload-Schema unterstützt. Siehe Abschnitt [exportierte Daten](#exported-data) ein Beispiel für das Ausgabeschema der Experience Platform.
* Ihr HTTP-Endpunkt muss Kopfzeilen unterstützen.

>[!TIP]
>
> Sie können auch [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) , um eine Experience Platform einzurichten und Profildaten an einen HTTP-Endpunkt zu senden.

## IP-Adressen-Zulassungsliste {#ip-address-allowlist}

Um die Sicherheits- und Compliance-Anforderungen von Kunden zu erfüllen, stellt Experience Platform eine Liste mit statischen IPs bereit, die Sie für das HTTP-API-Ziel auf die Zulassungsliste gesetzt haben. Siehe [IP-Adressen-Zulassungsliste für Streaming-Ziele](/help/destinations/catalog/streaming/ip-address-allow-list.md) für die vollständige Liste der IP-Adressen in Zulassungsliste.

## Unterstützte Authentifizierungstypen {#supported-authentication-types}

Das HTTP-API-Ziel unterstützt mehrere Authentifizierungstypen für Ihren HTTP-Endpunkt:

* HTTP-Endpunkt ohne Authentifizierung;
* Authentifizierung von Trägertoken;
* [OAuth 2.0-Client-Anmeldeinformationen](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) Authentifizierung mit dem Hauptteilformular, mit [!DNL client ID], [!DNL client secret] und [!DNL grant type] im Hauptteil der HTTP-Anforderung, wie im folgenden Beispiel gezeigt.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [OAuth 2.0-Client-Anmeldeinformationen](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) mit grundlegender Autorisierung, mit einem Autorisierungs-Header, der URL-kodiert enthält [!DNL client ID] und [!DNL client secret].

```shell
curl --location --request POST 'https://some-api.com/token' \
--header 'Authorization: Basic base64(clientId:clientSecret)' \
--header 'Content-type: application/x-www-form-urlencoded; charset=UTF-8' \
--data-urlencode 'grant_type=client_credentials'
```

* [OAuth 2.0-Passwortgewährung](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/).

## Herstellen einer Verbindung mit der Datenbank {#connect-destination}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Beim Herstellen einer Verbindung zu diesem Ziel müssen Sie die folgenden Informationen angeben:

### Authentifizierungsinformationen {#authentication-information}

#### Trägertoken-Authentifizierung {#bearer-token-authentication}

Wenn Sie die **[!UICONTROL Trägertoken]** Authentifizierungstyp zum Herstellen einer Verbindung mit Ihrem HTTP-Endpunkt, Eingabe der folgenden Felder und Auswahl **[!UICONTROL Mit Ziel verbinden]**:

![Bild des UI-Bildschirms, auf dem Sie mithilfe der Authentifizierung des Trägertokens eine Verbindung zum HTTP-API-Ziel herstellen können](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL Trägertoken]**: Fügen Sie das Trägertoken ein, um sich bei Ihrem HTTP-Speicherort zu authentifizieren.

#### Keine Authentifizierung {#no-authentication}

Wenn Sie die **[!UICONTROL Keines]** Authentifizierungstyp zum Herstellen einer Verbindung mit Ihrem HTTP-Endpunkt:

![Bild des UI-Bildschirms, auf dem Sie ohne Authentifizierung eine Verbindung zum HTTP-API-Ziel herstellen können](../../assets/catalog/http/http-api-authentication-none.png)

Wenn Sie diese Authentifizierung öffnen, müssen Sie nur **[!UICONTROL Mit Ziel verbinden]** und die Verbindung zu Ihrem Endpunkt hergestellt wird.

#### OAuth 2 Password Authentication {#oauth-2-password-authentication}

Wenn Sie die **[!UICONTROL OAuth 2 Password]** Authentifizierungstyp zum Herstellen einer Verbindung mit Ihrem HTTP-Endpunkt, Eingabe der folgenden Felder und Auswahl **[!UICONTROL Mit Ziel verbinden]**:

![Bild des UI-Bildschirms, auf dem Sie mithilfe von OAuth 2 mit Passwortauthentifizierung eine Verbindung zum HTTP-API-Ziel herstellen können](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL Zugriffstoken-URL]**: Die URL auf Ihrer Seite, die Zugriffstoken und optional Token aktualisieren ausgibt.
* **[!UICONTROL Client-ID]**: Die [!DNL client ID] , die Ihr System Adobe Experience Platform zuweist.
* **[!UICONTROL Client Secret]**: Die [!DNL client secret] , die Ihr System Adobe Experience Platform zuweist.
* **[!UICONTROL Benutzername]**: Der Benutzername für den Zugriff auf Ihren HTTP-Endpunkt.
* **[!UICONTROL Passwort]**: Das Kennwort für den Zugriff auf Ihren HTTP-Endpunkt.

#### OAuth 2 Client Credentials authentication {#oauth-2-client-credentials-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="Client-Anmeldeinformationen-Typ"
>abstract="Auswählen **Textkörperformular kodiert** , um die Client-ID und das Client-Geheimnis in den Text der Anfrage einzuschließen, oder **Grundlegende Autorisierung** , um die Client-ID und das Client-Geheimnis in einen Autorisierungs-Header aufzunehmen. Anzeigen von Beispielen in der Dokumentation."

Wenn Sie die **[!UICONTROL OAuth 2 Client-Anmeldedaten]** Authentifizierungstyp zum Herstellen einer Verbindung mit Ihrem HTTP-Endpunkt, Eingabe der folgenden Felder und Auswahl **[!UICONTROL Mit Ziel verbinden]**:

![Bild des UI-Bildschirms, auf dem Sie eine Verbindung zum HTTP-API-Ziel herstellen können, indem Sie OAuth 2 mit Client-Anmeldedaten-Authentifizierung verwenden](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

* **[!UICONTROL Zugriffstoken-URL]**: Die URL auf Ihrer Seite, die Zugriffstoken und optional Token aktualisieren ausgibt.
* **[!UICONTROL Client-ID]**: Die [!DNL client ID] , die Ihr System Adobe Experience Platform zuweist.
* **[!UICONTROL Client Secret]**: Die [!DNL client secret] , die Ihr System Adobe Experience Platform zuweist.
* **[!UICONTROL Client Credentials Type]**: Wählen Sie den Typ der von Ihrem Endpunkt unterstützten OAuth2-Client-Anmeldedaten aus:
   * **[!UICONTROL Textkörperformular kodiert]**: In diesem Fall wird die [!DNL client ID] und [!DNL client secret] sind enthalten *im Hauptteil des Antrags* an Ihr Ziel gesendet. Ein Beispiel finden Sie unter [Unterstützte Authentifizierungstypen](#supported-authentication-types) Abschnitt.
   * **[!UICONTROL Grundlegende Autorisierung]**: In diesem Fall wird die [!DNL client ID] und [!DNL client secret] sind enthalten *in einer `Authorization` header* nachdem base64-kodiert und an Ihr Ziel gesendet wurde. Ein Beispiel finden Sie unter [Unterstützte Authentifizierungstypen](#supported-authentication-types) Abschnitt.

### Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="Header"
>abstract="Geben Sie alle benutzerdefinierten Header ein, die in die Ziel-Aufrufe aufgenommen werden sollen. Verwenden Sie dazu folgendes Format: `header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="HTTP-Endpunkt"
>abstract="Die URL des HTTP-Endpunkts, an den Sie die Profildaten senden möchten."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="Segmentnamen einschließen"
>abstract="Schalten Sie ein, wenn der Datenexport die Namen der Segmente enthalten soll, die Sie exportieren. Zeigen Sie die Dokumentation für ein Beispiel für einen Datenexport mit dieser Option an."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="Segmentzeitstempel einschließen"
>abstract="Schalten Sie ein, wenn der Datenexport zum Zeitpunkt der Erstellung und Aktualisierung der Segmente den UNIX-Zeitstempel sowie den UNIX-Zeitstempel enthalten soll, zu dem die Segmente zum Zeitpunkt der Aktivierung dem Ziel zugeordnet wurden. Zeigen Sie die Dokumentation für ein Beispiel für einen Datenexport mit dieser Option an."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="Abfrageparameter"
>abstract="Optional können Sie Abfrageparameter zur HTTP-Endpunkt-URL hinzufügen. Formatieren Sie die verwendeten Abfrageparameter wie folgt: `parameter1=value&parameter2=value`."

Geben Sie nach Einrichtung der Authentifizierungsverbindung zum HTTP-Endpunkt die folgenden Informationen für das Ziel ein:

![Bild des UI-Bildschirms mit ausgefüllten Feldern für die HTTP-Zieldetails](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, mit dem Sie dieses Ziel in Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung ein, mit der Sie dieses Ziel in der Zukunft identifizieren können.
* **[!UICONTROL Kopfzeilen]**: Geben Sie alle benutzerdefinierten Header ein, die in die Ziel-Aufrufe aufgenommen werden sollen. Verwenden Sie dazu folgendes Format: `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL HTTP-Endpunkt]**: Die URL des HTTP-Endpunkts, an den Sie die Profildaten senden möchten.
* **[!UICONTROL Abfrageparameter]**: Optional können Sie Abfrageparameter zur HTTP-Endpunkt-URL hinzufügen. Formatieren Sie die verwendeten Abfrageparameter wie folgt: `parameter1=value&parameter2=value`.
* **[!UICONTROL Segmentnamen einschließen]**: Schalten Sie ein, wenn der Datenexport die Namen der Segmente enthalten soll, die Sie exportieren. Ein Beispiel für einen Datenexport mit aktivierter Option finden Sie im Abschnitt [Exportierte Daten](#exported-data) weiter unten.
* **[!UICONTROL Segmentzeitstempel einschließen]**: Schalten Sie ein, wenn der Datenexport zum Zeitpunkt der Erstellung und Aktualisierung der Segmente den UNIX-Zeitstempel sowie den UNIX-Zeitstempel enthalten soll, zu dem die Segmente zum Zeitpunkt der Aktivierung dem Ziel zugeordnet wurden. Ein Beispiel für einen Datenexport mit aktivierter Option finden Sie im Abschnitt [Exportierte Daten](#exported-data) weiter unten.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Streaming-Profil-Export-Ziele](../../ui/activate-streaming-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

### Zielattribute {#attributes}

Im [[!UICONTROL Attribute auswählen]](../../ui/activate-streaming-profile-destinations.md#select-attributes) in Adobe empfiehlt, eine eindeutige Kennung aus der [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten.

## Profil-Exportverhalten {#profile-export-behavior}

Experience Platform optimiert das Profil-Exportverhalten für Ihr HTTP-API-Ziel, sodass nur Daten an Ihren API-Endpunkt exportiert werden, wenn relevante Profilaktualisierungen nach der Segmentqualifizierung oder anderen wichtigen Ereignissen durchgeführt wurden. Profile werden in den folgenden Situationen an Ihr Ziel exportiert:

* Die Aktualisierung des Profils wurde durch eine Änderung der Segmentzugehörigkeit für mindestens eines der dem Ziel zugeordneten Segmente bestimmt. Beispielsweise hat sich das Profil für eines der Segmente qualifiziert, die dem Ziel zugeordnet sind, oder eines der dem Ziel zugeordneten Segmente verlassen.
* Die Aktualisierung des Profils wurde durch eine Änderung der [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md). Beispielsweise wurde einem Profil, das sich bereits für eines der dem Ziel zugeordneten Segmente qualifiziert hatte, eine neue Identität im Identitätszuordnungsattribut hinzugefügt.
* Die Aktualisierung des Profils wurde durch eine Änderung der Attribute für mindestens eines der dem Ziel zugeordneten Attribute bestimmt. Beispielsweise wird eines der Attribute, die dem Ziel im Zuordnungsschritt zugeordnet sind, einem Profil hinzugefügt.

In allen oben beschriebenen Fällen werden nur die Profile exportiert, in denen relevante Aktualisierungen vorgenommen wurden. Wenn beispielsweise ein Segment, das dem Zielfluss zugeordnet ist, aus hundert Mitgliedern besteht und fünf neue Profile für das Segment qualifiziert sind, ist der Export in Ihr Ziel inkrementell und umfasst nur die fünf neuen Profile.

Beachten Sie, dass alle zugeordneten Attribute unabhängig vom Speicherort der Änderungen für ein Profil exportiert werden. Daher werden im Beispiel vor allem alle zugeordneten Attribute für diese fünf neuen Profile exportiert, selbst wenn sich die Attribute selbst nicht geändert haben.

### Was bestimmt einen Datenexport und was ist im Export enthalten? {#what-determines-export-what-is-included}

Für die Daten, die für ein bestimmtes Profil exportiert werden, ist es wichtig, die beiden verschiedenen Konzepte von *was den Datenexport an Ihr HTTP-API-Ziel bestimmt* und *welche Daten im Export enthalten sind*.

| Was bestimmt den Zielexport? | Im Zielexport enthaltene Informationen |
|---------|----------|
| <ul><li>Zugeordnete Attribute und Segmente dienen als Hinweis für einen Zielexport. Das bedeutet, dass ein Zielexport gestartet wird, wenn zugeordnete Segmente den Status ändern (von null zu realisiert oder von realisiert/existiert zu ausstieg) oder alle zugeordneten Attribute aktualisiert werden.</li><li>Da Identitäten derzeit nicht HTTP-API-Zielen zugeordnet werden können, bestimmen Änderungen an der Identität eines bestimmten Profils auch die Zielexporte.</li><li>Eine Änderung für ein Attribut wird als jede Aktualisierung des Attributs definiert, unabhängig davon, ob es sich um denselben Wert handelt oder nicht. Das bedeutet, dass eine Überschreiben eines Attributs als Änderung gilt, selbst wenn sich der Wert selbst nicht geändert hat.</li></ul> | <ul><li>Alle Segmente (mit dem aktuellen Mitgliedschaftsstatus), unabhängig davon, ob sie im Datenfluss zugeordnet sind oder nicht, werden im `segmentMembership` -Objekt.</li><li>Alle Identitäten in der `identityMap` -Objekt ebenfalls enthalten (Experience Platform unterstützt derzeit keine Identitätszuordnung im HTTP-API-Ziel).</li><li>Nur die zugeordneten Attribute werden in den Zielexport einbezogen.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Betrachten Sie beispielsweise diesen Datenfluss an ein HTTP-Ziel, bei dem drei Segmente im Datenfluss ausgewählt und dem Ziel vier Attribute zugeordnet sind.

![HTTP-API-Ziel-Datenfluss](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Ein Profilexport an das Ziel kann durch ein Profil bestimmt werden, das für eines der *drei zugeordnete Segmente*. Im Datenexport jedoch wird im `segmentMembership` -Objekt (siehe [Exportierte Daten](#exported-data) unten), können weitere nicht zugeordnete Segmente angezeigt werden, wenn dieses bestimmte Profil Mitglied ist. Wenn ein Profil für den Kunden mit dem Segment &quot;DeLorean Cars&quot;qualifiziert ist, aber auch Mitglied der Segmente &quot;Zurück zur Zukunft&quot;für Film- und Science Fiction-Fans ist, sind diese beiden anderen Segmente auch in den Segmenten `segmentMembership` -Objekt des Datenexports, auch wenn diese nicht im Datenfluss zugeordnet sind.

Aus Sicht der Profilattribute bestimmen alle Änderungen an den vier oben zugeordneten Attributen einen Zielexport und eines der vier im Profil vorhandenen zugeordneten Attribute wird im Datenexport vorhanden sein.

## Aufstockung historischer Daten {#historical-data-backfill}

Wenn Sie ein neues Segment zu einem vorhandenen Ziel hinzufügen oder wenn Sie ein neues Ziel erstellen und ihm Segmente zuordnen, exportiert Experience Platform historische Segmentqualifikationsdaten an das Ziel. Profile, die sich für das Segment qualifiziert haben *before* das Segment, das zum Ziel hinzugefügt wurde, innerhalb von etwa einer Stunde an das Ziel exportiert wird.

## Exportierte Daten {#exported-data}

Ihr exportiert [!DNL Experience Platform] Daten landen in Ihrer [!DNL HTTP] Ziel im JSON-Format. Beispielsweise enthält der unten stehende Export ein Profil, das sich für ein bestimmtes Segment qualifiziert hat, Mitglied weiterer zwei Segmente ist und ein weiteres Segment verlassen hat. Der Export umfasst auch das Profilattribut mit Vorname, Nachname, Geburtsdatum und persönlicher E-Mail-Adresse. Die Identitäten für dieses Profil sind ECID und E-Mail.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
      }
   }
},
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

Im Folgenden finden Sie weitere Beispiele für exportierte Daten, abhängig von den Benutzeroberflächeneinstellungen, die Sie im Zielfluss &quot;Verbindung&quot;für die **[!UICONTROL Segmentnamen einschließen]** und **[!UICONTROL Segmentzeitstempel einschließen]** options:

+++ Das folgende Beispiel für den Datenexport enthält Segmentnamen im `segmentMembership` Abschnitt

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ Im folgenden Beispiel für den Datenexport sind Segmentzeitstempel im `segmentMembership` Abschnitt

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## Einschränkungen und Wiederholungsrichtlinien {#limits-retry-policy}

In 95 % der Fälle versucht Experience Platform, eine Durchsatzlatenz von weniger als 10 Minuten für erfolgreich gesendete Nachrichten mit einer Rate von weniger als 10.000 Anfragen pro Sekunde für jeden Datenfluss an ein HTTP-Ziel anzubieten.

Bei fehlgeschlagenen Anfragen an Ihr HTTP-API-Ziel speichert Experience Platform die fehlgeschlagenen Anfragen und versucht es zweimal, die Anfragen an Ihren -Endpunkt zu senden.