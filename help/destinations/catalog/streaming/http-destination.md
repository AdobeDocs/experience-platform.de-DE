---
keywords: Streaming; HTTP-Ziel
title: HTTP-API-Verbindung
description: Verwenden Sie das HTTP-API-Ziel in Adobe Experience Platform, um Profildaten an Drittanbieter-HTTP-Endpunkte zu senden. Damit können Sie Ihre eigenen Analysen oder andere Vorgänge ausführen, die Sie möglicherweise für Profildaten benötigen, die aus Experience Platform exportiert wurden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: d78b7a06318dabff5dac763068ca7c21a5a86633
workflow-type: tm+mt
source-wordcount: '2692'
ht-degree: 71%

---

# HTTP-API-Verbindung

## Übersicht {#overview}

>[!IMPORTANT]
>
> Dieses Ziel ist nur für Kunden von [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) verfügbar.

Das HTTP-API-Ziel ist ein Streaming-Ziel von [!DNL Adobe Experience Platform], mit dem Sie Profildaten an HTTP-Endpunkte von Drittanbietern senden können.

Um Profildaten an HTTP-Endpunkte zu senden, müssen Sie in [!DNL Adobe Experience Platform] zunächst eine [Verbindung zum Ziel herstellen](#connect-destination).

## Anwendungsbeispiele {#use-cases}

Mit dem HTTP-API-Ziel können Sie XDM-Profildaten und -Zielgruppen in generische HTTP-Endpunkte exportieren. Dort können Sie Ihre eigenen Analysen oder beliebige andere Vorgänge ausführen, die Sie für aus Experience Platform exportierte Profildaten benötigen.

HTTP-Endpunkte können entweder eigene Systeme von Kunden oder Lösungen von Drittanbietern sein.

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (wie etwa E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Zuordnung“ im [Zielaktivierungs-Workflow](../../ui/activate-segment-streaming-destinations.md#mapping) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

Um Daten aus Experience Platform mithilfe des HTTP-API-Ziels zu exportieren, müssen folgende Voraussetzungen erfüllt sein:

* Sie müssen über einen HTTP-Endpunkt verfügen, der die REST-API unterstützt.
* Ihr HTTP-Endpunkt muss das Profilschema von Experience Platform unterstützen. Im HTTP-API-Ziel wird keine Umwandlung in ein Payload-Schema von Drittanbietern unterstützt. Im Abschnitt [exportierte Daten](#exported-data) finden Sie ein Beispiel für das Ausgabeschema von Experience Platform.
* Ihr HTTP-Endpunkt muss Kopfzeilen unterstützen.

>[!TIP]
>
> Sie können auch das [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) verwenden, um eine Integration einzurichten und Profildaten von Experience Platform an einen HTTP-Endpunkt zu senden.

## Unterstützung und Zertifikat des mTLS-Protokolls {#mtls-protocol-support}

Sie können [!DNL Mutual Transport Layer Security] ([!DNL mTLS]) verwenden, um erweiterte Sicherheit bei ausgehenden Verbindungen zu Ihren HTTP-API-Zielverbindungen zu gewährleisten.

[!DNL mTLS] ist eine End-to-End-Sicherheitsmethode für die gegenseitige Authentifizierung, die sicherstellt, dass beide Parteien, die Informationen austauschen, vor der Datenfreigabe diejenigen sind, für die sie sich ausgeben. [!DNL mTLS] umfasst einen zusätzlichen Schritt im Vergleich zu [!DNL TLS], bei dem der Server auch nach dem Zertifikat des Clients fragt und es an seinem Ende überprüft.

Wenn Sie [!DNL mTLS] mit [!DNL HTTP API] Zielen verwenden möchten, müssen für die Server-Adresse, die Sie auf der Seite [Zieldetails](#destination-details) eingeben, [!DNL TLS] Protokolle deaktiviert und nur aktiviert [!DNL mTLS]. Wenn das Protokoll [!DNL TLS] 1.2 noch auf dem Endpunkt aktiviert ist, wird kein Zertifikat für die Client-Authentifizierung gesendet. Das bedeutet, dass Ihr Empfangs-Server-Endpunkt ein [!DNL mTLS]-fähiger Verbindungsendpunkt sein muss, um [!DNL mTLS] mit Ihrem [!DNL HTTP API]-Ziel verwenden zu können.

### Abrufen und Überprüfen von Zertifikatdetails {#certificate}

Wenn Sie Zertifikatdetails wie die [!DNL Common Name] (CN) und [!DNL Subject Alternative Names] (SAN) auf zusätzliche Validierungen durch Dritte überprüfen möchten, verwenden Sie die API, um das Zertifikat abzurufen und diese Felder aus der Antwort zu extrahieren.

Weitere Informationen finden [ in der ](../../../data-governance/mtls-api/public-certificate-endpoint.md) zum öffentlichen Zertifikatendpunkt .

## Zulassungsliste von IP-Adressen {#ip-address-allowlist}

Um die Sicherheits- und Compliance-Anforderungen von Kunden zu erfüllen, stellt Experience Platform eine Liste mit statischen IPs bereit, die Sie für das HTTP-API-Ziel auf die Zulassungsliste setzen können. Siehe [IP-Adressen-Zulassungsliste für Streaming](/help/destinations/catalog/streaming/ip-address-allow-list.md)Ziele, um die vollständige Liste der IPs in der Zulassungsliste aufzurufen.

## Unterstützte Authentifizierungstypen {#supported-authentication-types}

Das HTTP-API-Ziel unterstützt mehrere Authentifizierungstypen für Ihren HTTP-Endpunkt:

* HTTP-Endpunkt ohne Authentifizierung;
* Authentifizierung mit Bearer-Token;
* [Client-Anmeldeinformationen für OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) Authentifizierung mit dem Textkörper-Formular, mit [!DNL client ID], [!DNL client secret] und [!DNL grant type] im Textkörper der HTTP-Anfrage, wie im folgenden Beispiel gezeigt.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [Anmeldedaten für OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) mit einfacher Autorisierung, mit einer Autorisierungskopfzeile, die URL-codierte [!DNL client ID] und [!DNL client secret] enthält.

```shell
curl --location --request POST 'https://some-api.com/token' \
--header 'Authorization: Basic base64(clientId:clientSecret)' \
--header 'Content-type: application/x-www-form-urlencoded; charset=UTF-8' \
--data-urlencode 'grant_type=client_credentials'
```

* [Passwortgewährung für OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/).

## Herstellen einer Verbindung mit dem Ziel {#connect-destination}

>[!IMPORTANT]
> 
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Beim Herstellen einer Verbindung zu diesem Ziel müssen Sie die folgenden Informationen angeben:

### Authentifizierungsinformationen {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="Typ der Client-Anmeldedaten"
>abstract="Wählen Sie **Im Textkörper codiert**, um die Client-ID und das Client-Geheimwort in den Textkörper der Anfrage aufzunehmen, oder **Einfache Autorisierung**, um die Client-ID und das Client-Geheimnis in eine Autorisierungskopfzeile aufzunehmen. Beispiele sind in der Dokumentation zu finden."

#### Authentifizierung über Bearer-Token {#bearer-token-authentication}

Wenn Sie den Authentifizierungstyp **[!UICONTROL Bearer-Token]** für die Verbindung zu Ihrem HTTP-Endpunkt wählen, füllen Sie die Felder unten aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**:

![Abbildung des Bildschirms der Benutzeroberfläche, über den Sie mithilfe der Bearer-Token-Authentifizierung eine Verbindung zum HTTP-API-Ziel herstellen können.](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL Bearer-Token]**: Fügen Sie das Bearer-Token ein, um sich bei Ihrer HTTP-Adresse zu authentifizieren.

#### Keine Authentifizierung {#no-authentication}

Wenn Sie **[!UICONTROL keinen]** Authentifizierungstyp zum Herstellen einer Verbindung mit Ihrem HTTP-Endpunkt auswählen:

![Abbildung des Bildschirms der Benutzeroberfläche, über den Sie ohne Authentifizierung eine Verbindung zum HTTP-API-Ziel herstellen können.](../../assets/catalog/http/http-api-authentication-none.png)

Wenn Sie diese offene Authentifizierung auswählen, brauchen Sie nur auf **[!UICONTROL Mit Ziel verbinden]** zu klicken, und die Verbindung zu Ihrem Endpunkt wird hergestellt.

#### Passwort-Authentifizierung für OAuth 2 {#oauth-2-password-authentication}

Wenn Sie für die Verbindung zu Ihrem HTTP-Endpunkt den Authentifizierungstyp **[!UICONTROL OAuth 2 mit Passwort]** wählen, füllen Sie die unten stehenden Felder aus und klicken Sie auf **[!UICONTROL Mit Ziel verbinden]**:

![Abbildung des Bildschirms der Benutzeroberfläche, über den Sie mithilfe von OAuth 2 mit Passwortauthentifizierung eine Verbindung zum HTTP-API-Ziel herstellen können.](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL Zugriffstoken-URL]**: Die URL auf Ihrer Seite, die Zugriffstoken ausgibt und Token optional aktualisiert.
* **[!UICONTROL Client-ID]**: Die [!DNL client ID], die Ihr System Adobe Experience Platform zuweist.
* **[!UICONTROL Client-Geheimnis]**: Das [!DNL client secret], das Ihr System Adobe Experience Platform zuweist.
* **[!UICONTROL Benutzername]**: Der Benutzername für den Zugriff auf Ihren HTTP-Endpunkt.
* **[!UICONTROL Passwort]**: Das Passwort für den Zugriff auf Ihren HTTP-Endpunkt.

#### Authentifizierung mit Client-Anmeldedaten für OAuth 2 {#oauth-2-client-credentials-authentication}

Wenn Sie den Authentifizierungstyp **[!UICONTROL Client-Anmeldeinformationen für OAuth 2]** wählen, um sich mit Ihrem HTTP-Endpunkt zu verbinden, füllen Sie die unten stehenden Felder aus und klicken Sie auf **[!UICONTROL Mit Ziel verbinden]**:

![Abbildung des Bildschirms der Benutzeroberfläche, über den Sie mithilfe von OAuth 2 mit Authentifizierung über Client-Anmeldeinformationen eine Verbindung zum HTTP-API-Ziel herstellen können.](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

>[!WARNING]
> 
>Bei Verwendung der [!UICONTROL OAuth 2 Client-Anmeldeinformationen] -Authentifizierung kann [!UICONTROL Zugriffstoken-URL] maximal einen Abfrageparameter aufweisen. Das Hinzufügen einer [!UICONTROL Zugriffstoken-URL] mit mehr Abfrageparametern kann zu Problemen beim Herstellen einer Verbindung zu Ihrem Endpunkt führen.

* **[!UICONTROL Zugriffstoken-URL]**: Die URL auf Ihrer Seite, die Zugriffstoken ausgibt und Token optional aktualisiert.
* **[!UICONTROL Client-ID]**: Die [!DNL client ID], die Ihr System Adobe Experience Platform zuweist.
* **[!UICONTROL Client-Geheimwort]**: Das [!DNL client secret], das Ihr System Adobe Experience Platform zuweist.
* **[!UICONTROL Typ der Client-Anmeldedaten]**: Wählen Sie den Typ der von Ihrem Endpunkt unterstützten Client-Anmeldedaten für OAuth2 aus:
   * **[!UICONTROL Im Textkörper codiert]**: In diesem Fall sind [!DNL client ID] und [!DNL client secret] im *Textkörper der Anfrage* enthalten, die an Ihr Ziel gesendet wird.. Ein Beispiel finden Sie im Abschnitt [unterstützte Authentifizierungstypen](#supported-authentication-types).
   * **[!UICONTROL Einfache Autorisierung]**: In diesem Fall werden [!DNL client ID] und [!DNL client secret], nachdem sie mit Base64 codiert wurden, *in eine `Authorization`-Kopfzeile* aufgenommen und an Ihr Ziel gesendet. Ein Beispiel finden Sie im Abschnitt [Unterstützte Authentifizierungstypen](#supported-authentication-types).

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="Kopfzeilen"
>abstract="Geben Sie alle benutzerdefinierten Kopfzeilen ein, die in die Ziel-Aufrufe aufgenommen werden sollen. Verwenden Sie dazu folgendes Format: `header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="HTTP-Endpunkt"
>abstract="Die URL des HTTP-Endpunkts, an den Sie die Profildaten senden möchten."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="Segmentnamen einschließen"
>abstract="Schalten Sie diese Option ein, wenn der Datenexport die Namen der zu exportierenden Zielgruppen enthalten soll. In der Dokumentation finden Sie ein Beispiel für einen Datenexport mit dieser Option."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="Zeitstempel für Segmente einschließen"
>abstract="Schalten Sie diese Option ein, wenn der Datenexport den UNIX-Zeitstempel enthalten soll, an dem die Zielgruppen erstellt und aktualisiert wurden, sowie den UNIX-Zeitstempel, an dem die Zielgruppen dem Ziel für die Aktivierung zugeordnet wurden. In der Dokumentation finden Sie ein Beispiel für einen Datenexport mit dieser Option."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="Abfrageparameter"
>abstract="Optional können Sie Abfrageparameter zur HTTP-Endpunkt-URL hinzufügen. Formatieren Sie die verwendeten Abfrageparameter wie folgt: `parameter1=value&parameter2=value`."

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Abbildung des Bildschirms der Benutzeroberfläche mit ausgefüllten Feldern für die Details zum HTTP-Ziel.](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, um dieses Ziel in Zukunft zu erkennen.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung ein, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Kopfzeilen]**: Geben Sie alle benutzerdefinierten Kopfzeilen ein, die in die Ziel-Aufrufe aufgenommen werden sollen. Verwenden Sie dazu folgendes Format: `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL HTTP-Endpunkt]**: Die URL des HTTP-Endpunkts, an den Sie die Profildaten senden möchten.
* **[!UICONTROL Abfrageparameter]**: Optional können Sie Abfrageparameter zur HTTP-Endpunkt-URL hinzufügen. Formatieren Sie die verwendeten Abfrageparameter wie folgt: `parameter1=value&parameter2=value`.
* **[!UICONTROL Segmentnamen einschließen]**: Schalten Sie diese Option ein, wenn der Datenexport die Namen der zu exportierenden Zielgruppen enthalten soll. Ein Beispiel für einen Datenexport, bei dem diese Option aktiviert ist, finden Sie im Abschnitt [Exportierte Daten](#exported-data) weiter unten.
* **[!UICONTROL Segmentzeitstempel einschließen]**: Schalten Sie diese Option ein, wenn der Datenexport den UNIX-Zeitstempel enthalten soll, an dem die Zielgruppen erstellt und aktualisiert wurden, sowie den UNIX-Zeitstempel, an dem die Zielgruppen dem Ziel für die Aktivierung zugeordnet wurden. Ein Beispiel für einen Datenexport, bei dem diese Option aktiviert ist, finden Sie im Abschnitt [exportierte Daten](#exported-data) weiter unten.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* [Bewertung der Einverständnisrichtlinie](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) wird derzeit nicht in Exporten an das HTTP-API-Ziel unterstützt. [Weitere Informationen](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Anweisungen [ Aktivieren von Zielgruppen für dieses Ziel finden Sie ](../../ui/activate-streaming-profile-destinations.md) „Aktivieren von Zielgruppendaten für Streaming Profilexportziele“.

### Zielattribute {#attributes}

Im Schritt [[!UICONTROL Attribute auswählen]](../../ui/activate-streaming-profile-destinations.md#select-attributes) empfiehlt Adobe, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten.

## Profilexportverhalten {#profile-export-behavior}

Experience Platform optimiert das Verhalten beim Profilexport für Ihr HTTP-API-Ziel, sodass nur Daten an Ihren API-Endpunkt exportiert werden, wenn relevante Profilaktualisierungen nach der Zielgruppen-Qualifizierung oder anderen wichtigen Ereignissen durchgeführt wurden. Profile werden in den folgenden Situationen an Ihr Ziel exportiert:

* Die Aktualisierung des Profils wurde durch eine Änderung der Zielgruppenzugehörigkeit für mindestens eine der dem Ziel zugeordneten Zielgruppen bestimmt. Beispielsweise hat sich das Profil für eine der Zielgruppen qualifiziert, die dem Ziel zugeordnet sind, oder es hat eine der dem Ziel zugeordneten Zielgruppen verlassen.
* Die Aktualisierung des Profils wurde durch eine Änderung der [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md) bestimmt. Beispielsweise wurde einem Profil, das sich bereits für eine der dem Ziel zugeordneten Zielgruppen qualifiziert hatte, eine neue Identität im Identitätszuordnungsattribut hinzugefügt.
* Die Aktualisierung des Profils wurde durch eine Änderung der Attribute für mindestens eines der dem Ziel zugeordneten Attribute bestimmt. Beispielsweise wird eines der Attribute, die dem Ziel im Zuordnungsschritt zugeordnet sind, einem Profil hinzugefügt.

In allen oben beschriebenen Fällen werden nur die Profile exportiert, in denen relevante Aktualisierungen vorgenommen wurden. Wenn beispielsweise eine Zielgruppe, die dem Zielfluss zugeordnet ist, aus hundert Mitgliedern besteht und fünf neue Profile sich für das Segment qualifizieren, ist der Export in Ihr Ziel inkrementell und umfasst nur die fünf neuen Profile.

Beachten Sie, dass alle zugeordneten Attribute unabhängig von der Art der Änderungen für ein Profil exportiert werden. Daher werden im obigen Beispiel alle zugeordneten Attribute für diese fünf neuen Profile exportiert, selbst wenn sich die Attribute selbst nicht geändert haben.

### Was bestimmt einen Datenexport und was ist im Export enthalten? {#what-determines-export-what-is-included}

Was die Daten betrifft, die für ein bestimmtes Profil exportiert werden, ist es wichtig, die beiden verschiedenen Konzepte zu verstehen, nämlich *was den Datenexport an Ihr HTTP-API-Ziel bestimmt* und *welche Daten im Export enthalten sind*.

| Was einen Zielexport bestimmt | Im Zielexport enthaltene Informationen |
|---------|----------|
| <ul><li>Zugeordnete Attribute und Zielgruppen dienen als Hinweis für einen Zielexport. Das bedeutet, dass ein Zielexport ausgelöst wird, wenn sich der Status einer zugeordneten Zielgruppe ändert (von `null` auf `realized` oder von `realized` auf `exiting`) oder wenn zugeordnete Attribute aktualisiert werden.</li><li>Da Identitäten derzeit nicht HTTP-API-Zielen zugeordnet werden können, bestimmen Änderungen an der Identität eines bestimmten Profils auch die Zielexporte.</li><li>Als Änderung für ein Attribut wird jede Aktualisierung des Attributs definiert, unabhängig davon, ob es sich um denselben Wert handelt oder nicht. Das bedeutet, dass das Überschreiben eines Attributs als Änderung gilt, selbst wenn sich der Wert selbst nicht geändert hat.</li></ul> | <ul><li>Das `segmentMembership`-Objekt enthält die Zielgruppe, die im Aktivierungsdatenfluss zugeordnet ist und für die sich der Status des Profils nach einem Qualifikations- oder Zielgruppenaustrittsereignis geändert hat. Beachten Sie, dass andere nicht zugeordnete Zielgruppen, für die sich das Profil qualifiziert hat, Teil des Zielexports sein können, wenn diese Zielgruppen zu derselben [Zusammenführungsrichtlinie](/help/profile/merge-policies/overview.md) gehören wie die im Aktivierungsdatenfluss zugeordnete Zielgruppe. </li><li>Alle Identitäten im `identityMap`-Objekt sind ebenfalls enthalten (Experience Platform unterstützt derzeit keine Identitätszuordnung im HTTP-API-Ziel).</li><li>Nur die zugeordneten Attribute werden in den Zielexport einbezogen.</li></ul> |

{style="table-layout:fixed"}

Betrachten Sie beispielsweise den folgenden Datenfluss an ein HTTP-Ziel, bei dem im Datenfluss drei Zielgruppen ausgewählt und dem Ziel vier Attribute zugeordnet sind.

![Beispiel für einen HTTP-API-Ziel-Datenfluss.](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Ein Profilexport an das Ziel kann durch ein Profil bestimmt werden, das sich für eines der *drei zugeordneten Segmente* qualifiziert. Im Datenexport jedoch können im `segmentMembership` (siehe [Exportierte Daten](#exported-data) Abschnitt unten) weitere nicht zugeordnete Zielgruppen angezeigt werden, wenn dieses bestimmte Profil zu diesen Profil gehört und diese Zielgruppen dieselbe Zusammenführungsrichtlinie verwenden wie die Zielgruppe, die den Export ausgelöst hat. Wenn ein Profil sich für das Segment **Kunde mit DeLorean-Autos** qualifiziert hat, aber auch Mitglied der Segmente **Hat „Zurück in die Zukunft“** und **Science-Fiction-**&quot; ist, sind diese beiden anderen Zielgruppen ebenfalls im `segmentMembership` des Datenexports vorhanden, obwohl diese nicht im Datenfluss zugeordnet sind, falls diese dieselbe Zusammenführungsrichtlinie wie das Segment **Kunde mit DeLorean-Autos** verwenden.

Aus Sicht der Profilattribute bestimmen alle Änderungen an den vier oben zugeordneten Attributen einen Zielexport, und eines der vier im Profil vorhandenen zugeordneten Attribute wird im Datenexport vorhanden sein.

## Aufstockung historischer Daten {#historical-data-backfill}

Wenn Sie eine neue Zielgruppe zu einem vorhandenen Ziel hinzufügen oder wenn Sie ein neues Ziel erstellen und diesem Zielgruppen zuordnen, exportiert Experience Platform historische Zielgruppen-Qualifizierungsdaten an das Ziel. Profile, die sich für die Zielgruppe qualifiziert haben *zuvor* wurde die Zielgruppe zum Ziel hinzugefügt, werden innerhalb von etwa einer Stunde an das Ziel exportiert.

## Exportierte Daten {#exported-data}

Ihre exportierten [!DNL Experience Platform]-Daten landen in Ihrem [!DNL HTTP]-Ziel im JSON-Format. Beispielsweise enthält der folgende Export ein Profil, das sich für ein bestimmtes Segment qualifiziert hat, Mitglied zweier weiterer Segmente ist und ein weiteres Segment verlassen hat. Der Export umfasst außerdem Vorname, Nachname, Geburtsdatum und persönliche E-Mail-Adresse des Profilattributs. Die Identitäten für dieses Profil sind ECID und E-Mail.

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
         "status":"realized"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"realized"
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

Im Folgenden finden Sie weitere Beispiele für exportierte Daten, abhängig von den Benutzeroberflächeneinstellungen, die Sie im Fluss „Ziel verbinden“ für die Optionen **[!UICONTROL Segmentnamen einschließen]** und **[!UICONTROL Zeitstempel für Segmente einschließen]** auswählen.

+++ Das folgende Beispiel für den Datenexport enthält Zielgruppennamen im Abschnitt `segmentMembership` .

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
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

+++ Das folgende Beispiel für den Datenexport enthält Zielgruppen-Zeitstempel im Abschnitt `segmentMembership` .

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## Beschränkungen und Wiederholungsrichtlinien {#limits-retry-policy}

Experience Platform versucht, in 95 Prozent der Fälle eine Durchsatzlatenz von weniger als 10 Minuten für erfolgreich gesendete Nachrichten mit einer Rate von weniger als 10.000 Anfragen pro Sekunde für jeden Datenfluss an ein HTTP-Ziel zu bieten.

Bei fehlgeschlagenen Anfragen an Ihr HTTP-API-Ziel speichert Experience Platform die fehlgeschlagenen Anfragen und versucht es zweimal erneut, die Anfragen an Ihren Endpunkt zu senden.