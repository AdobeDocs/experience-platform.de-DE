---
title: Übersicht über den Salesforce Source Connector
description: Erfahren Sie, wie Sie Salesforce mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: d8d9303e358c66c4cd891d6bf59a801c09a95f8e
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 4%

---

# [!DNL Salesforce]

>[!IMPORTANT]
>
>Sie können jetzt die [!DNL Salesforce]-Quelle verwenden, wenn Sie Adobe Experience Platform auf Amazon Web Services (AWS) ausführen. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../landing/multi-cloud.md).

>[!WARNING]
>
>Die Standardauthentifizierung für die [!DNL Salesforce] wird im Januar 2026 eingestellt. Sie müssen zur Authentifizierung mit Client-Anmeldeinformationen für OAuth 2 wechseln, um weiterhin die -Quelle verwenden und Daten von Ihrem [!DNL Salesforce]-Konto in Experience Platform aufnehmen zu können.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform bietet Unterstützung für die Aufnahme von Daten aus einem CRM-System eines Drittanbieters. Unterstützung für CRM-Anbieter umfasst [!DNL Salesforce].

## Einrichten der [!DNL Salesforce] für Experience Platform auf Azure {#azure}

Gehen Sie wie folgt vor, um zu erfahren, wie Sie Ihr [!DNL Salesforce] für Experience Platform auf Azure einrichten können.

### AUF DIE ZULASSUNGSLISTE SETZEN IP-Adresse für die Verbindung mit Azure

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform auf Azure verbinden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Auf die Zulassungsliste setzen Weitere Informationen finden [ auf der Seite ](../../ip-address-allow-list.md)IP-Adresse“.

>[!BEGINTABS]

>[!TAB VA7]

- `40.70.226.96/28`
- `40.70.226.32/28`
- `52.232.229.255`
- `52.232.229.253`
- `40.70.226.144/28`
- `40.70.226.64/28`
- `40.70.225.240/28`
- `40.70.225.224/28`
- `40.70.224.64/29`
- `40.70.226.80/28`
- `40.70.226.176/28`
- `52.232.229.230`
- `40.70.226.128/28`
- `40.70.226.0/28`
- `40.70.226.16/28`
- `52.138.119.167`
- `40.70.226.160/28`
- `40.70.226.192/28`
- `40.70.226.48/28`
- `20.96.243.176`
- `40.70.226.112/28`
- `40.70.226.208/28`

>[!TAB NLD2]

- `40.74.4.144/28`
- `40.74.3.176/28`
- `40.74.5.128/28`
- `40.74.4.176/28`
- `40.74.6.112/28`
- `40.74.7.128/28`
- `40.74.6.144/28`
- `51.105.144.81`
- `52.142.236.87`
- `40.74.6.80/28`
- `20.101.246.9`
- `40.74.7.208/28`
- `40.74.6.128/28`
- `40.74.7.176/28`
- `51.124.70.4`
- `40.74.7.144/28`
- `108.141.12.47`
- `20.50.23.153`
- `51.144.184.248/29`
- `40.74.7.160/28`
- `40.74.7.192/28`
- `51.105.144.1`
- `40.74.4.160/28`
- `40.74.6.96/28`

>[!TAB AUS5]

- `20.43.111.32/28`
- `20.43.110.144/28`
- `20.53.111.113`
- `20.227.32.175`
- `20.43.110.96/28`
- `20.43.110.64/28`
- `20.193.56.144/28`
- `20.43.110.192/28`
- `20.43.97.95`
- `20.43.111.16/28`
- `20.43.110.128/28`
- `20.40.185.111`
- `20.193.56.160/28`
- `20.43.110.112/28`
- `40.82.220.111`
- `20.43.111.0/28`
- `20.193.38.208/28`
- `20.43.110.80/28`
- `20.43.110.176/28`
- `20.43.110.48/28`
- `20.193.36.37`
- `20.43.110.208/28`
- `20.43.110.224/28`
- `20.43.110.160/28`
- `20.40.185.225`
- `20.43.110.240/28`
- `20.193.56.128/28`
- `20.40.185.185`

>[!TAB CAN2]

- `20.116.159.48/28`
- `20.116.159.144/28`
- `20.116.159.96/28`
- `20.220.243.238`
- `20.116.159.80/28`
- `20.116.159.32/28`
- `20.151.241.138`
- `4.172.28.20`
- `20.151.241.124`
- `20.116.248.0/28`
- `20.116.155.128/28`
- `20.116.159.64/28`
- `20.116.159.192/28`
- `20.116.159.176/28`
- `20.116.175.240/28`
- `20.116.248.16/28`
- `20.116.158.240/28`
- `20.116.159.112/28`
- `20.151.240.247`
- `20.151.241.173`
- `20.116.159.128/28`
- `20.116.159.160/28`
- `20.116.159.0/28`
- `20.104.5.248`
- `20.116.175.224/28`
- `20.116.159.208/28`
- `20.116.159.224/28`

>[!TAB GBR9]

- `20.162.155.16/28`
- `20.162.154.96/28`
- `20.26.64.0/28`
- `20.26.64.96/28`
- `20.162.154.64/28`
- `20.108.200.27`
- `20.162.154.80/28`
- `20.162.153.192/28`
- `20.108.200.61`
- `20.162.154.48/28`
- `20.162.154.192/28`
- `20.162.154.0/28`
- `20.26.64.16/28`
- `20.162.154.112/28`
- `20.162.153.32/28`
- `20.254.80.141`
- `20.162.153.208/28`
- `20.108.203.20`
- `20.26.64.48/28`
- `20.162.154.240/28`
- `20.162.154.208/28`
- `20.162.154.160/28`
- `20.108.205.182`
- `20.108.202.198`
- `20.162.154.32/28`
- `20.162.153.16/28`

>[!TAB IND2]

- `4.188.92.84`
- `4.224.5.224/28`
- `4.224.7.32/28`
- `4.188.92.87`
- `4.188.89.92`
- `4.224.5.112/28`
- `4.224.6.80/28`
- `4.224.144.224/28`
- `4.224.144.240/28`
- `4.224.6.96/28`
- `4.188.89.255`
- `4.188.94.32/28`
- `4.224.5.96/28`
- `4.224.6.64/28`
- `4.224.7.48/28`
- `4.224.5.208/28`
- `4.188.90.65`
- `4.224.6.16/28`
- `4.224.6.0/28`
- `4.224.5.192/28`
- `4.224.7.16/28`
- `4.188.90.67`
- `4.188.90.17`
- `4.188.94.48/28`
- `4.224.6.112/28`
- `4.224.5.240/28`
- `4.224.7.0/28`

>[!ENDTABS]

### Feldzuordnung von [!DNL Salesforce] zu XDM

Um eine Quellverbindung zwischen [!DNL Salesforce] und Experience Platform herzustellen, müssen die [!DNL Salesforce] Quelldatenfelder den entsprechenden XDM-Zielfeldern zugeordnet werden, bevor sie in Experience Platform aufgenommen werden können.

Ausführliche Informationen zu den Regeln für die Feldzuordnung zwischen [!DNL Salesforce] Datensätzen und Experience Platform finden Sie unten:

- [Kontakte](../adobe-applications/mapping/salesforce.md#contact)
- [Leads](../adobe-applications/mapping/salesforce.md#lead)
- [Konten](../adobe-applications/mapping/salesforce.md#account)
- [Opportunities](../adobe-applications/mapping/salesforce.md#opportunity)
- [Rollen von Kontakten bei Opportunities](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Kampagnen](../adobe-applications/mapping/salesforce.md#campaign)
- [Kampagnenmitglieder](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Account-Kontaktbeziehung](../adobe-applications/mapping/salesforce.md#account-contact-relation)

### Einrichten des [!DNL Salesforce] Namespace und des Dienstprogramms zur automatischen Schemaerstellung

Um die [!DNL Salesforce] als Teil von [!DNL B2B-CDP] zu verwenden, müssen Sie zunächst ein [!DNL Postman]-Dienstprogramm einrichten, um Ihre [!DNL Salesforce] Namespaces und Schemata automatisch zu generieren. Die folgende Dokumentation enthält zusätzliche Informationen zum Einrichten des [!DNL Postman]:

- Sie können den Namespace und die Dienstprogrammsammlung zur automatischen Schemaerstellung sowie die Umgebung aus diesem GitHub[Repository ](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Informationen zur Verwendung von Experience Platform-APIs, einschließlich Details zum Erfassen von Werten für erforderliche Kopfzeilen und zum Lesen von Beispiel-API-Aufrufen, finden Sie im Handbuch [Erste Schritte mit Experience Platform-APIs](../../../landing/api-guide.md).
- Informationen zum Generieren Ihrer Anmeldeinformationen für Experience Platform-APIs finden Sie im Tutorial zum [Authentifizieren und Zugreifen auf Experience Platform-APIs](../../../landing/api-authentication.md).
- Informationen zum Einrichten von [!DNL Postman] für Experience Platform-APIs finden Sie im Tutorial zum [ von Entwicklerkonsole und  [!DNL Postman]](../../../landing/postman.md).

Wenn eine Experience Platform-Entwicklerkonsole und [!DNL Postman] eingerichtet sind, können Sie jetzt damit beginnen, die entsprechenden Umgebungswerte auf Ihre [!DNL Postman] anzuwenden.

+++Handbuch zur Variablentabelle anzeigen

Die folgende Tabelle enthält Beispielwerte sowie zusätzliche Informationen zum Ausfüllen Ihrer [!DNL Postman]:

| Variable | Beschreibung | Beispiel |
| --- | --- | --- |
| `CLIENT_SECRET` | Eine eindeutige Kennung, die zum Generieren Ihres `{ACCESS_TOKEN}` verwendet wird. Informationen zum Abrufen Ihrer `{CLIENT_SECRET}` finden [ im Tutorial zum ](../../../landing/api-authentication.md) und Zugreifen auf Experience Platform-APIs . | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Das JSON Web Token (JWT) ist eine Authentifizierungsberechtigung, die zum Generieren Ihres {ACCESS_TOKEN} verwendet wird. Weitere Informationen zum Generieren [ Experience Platform-APIs finden Sie ](../../../landing/api-authentication.md) Tutorial zum Authentifizieren und Zugreifen auf `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Eine eindeutige Kennung, die zum Authentifizieren von Aufrufen an Experience Platform-APIs verwendet wird. Informationen zum Abrufen Ihrer `{API_KEY}` finden [ im Tutorial zum ](../../../landing/api-authentication.md) und Zugreifen auf Experience Platform-APIs . | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Das Autorisierungs-Token, das zum Abschließen von Aufrufen an Experience Platform-APIs erforderlich ist. Informationen zum Abrufen Ihrer `{ACCESS_TOKEN}` finden [ im Tutorial zum ](../../../landing/api-authentication.md) und Zugreifen auf Experience Platform-APIs . | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | In Bezug auf [!DNL Marketo] ist dieser Wert fest und wird immer auf `ent_dataservices_sdk` festgelegt. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Der `global`-Container enthält alle standardmäßigen von Adobe und Experience Platform bereitgestellten Partnerklassen, Schemafeldgruppen, Datentypen und Schemata. In Bezug auf [!DNL Marketo] ist dieser Wert fest und wird immer auf `global` festgelegt. | `global` |
| `PRIVATE_KEY` | Eine Berechtigung, die zum Authentifizieren Ihrer [!DNL Postman] bei Experience Platform-APIs verwendet wird. Anweisungen zum Abrufen Ihrer {PRIVATE_KEY} finden Sie im Tutorial zum Einrichten [ Entwicklerkonsole und  [!DNL Postman]](../../../landing/postman.md)Einrichten der Entwicklerkonsole und . | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Eine Berechtigung, die zur Integration mit Adobe I/O verwendet wird. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Das Identity Management-System (IMS) stellt das Framework für die Authentifizierung für Adobe-Services bereit. In Bezug auf [!DNL Marketo] ist dieser Wert fest und wird immer auf `ims-na1.adobelogin.com` festgelegt. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Eine Unternehmenseinheit, die Produkte und Dienstleistungen besitzen oder lizenzieren und ihren Mitgliedern Zugang gewähren kann. Anweisungen zum Abrufen Ihrer `{ORG_ID}` finden [ im Tutorial zum Einrichten  [!DNL Postman]](../../../landing/postman.md) Entwicklerkonsole und . | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Der Name der virtuellen Sandbox-Partition, die Sie verwenden. | `prod` |
| `TENANT_ID` | Eine ID, mit der sichergestellt wird, dass die von Ihnen erstellten Ressourcen über den richtigen Namespace verfügen und in Ihrer Organisation enthalten sind. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Der URL-Endpunkt, an den Sie API-Aufrufe durchführen. Dieser Wert ist fest und immer auf `http://platform.adobe.io/` festgelegt. | `http://platform.adobe.io/` |
| `munchkinId` | Die eindeutige ID für Ihr [!DNL Marketo]. Informationen zum Abrufen Ihrer `munchkinId` finden [ im Tutorial  [!DNL Marketo] Authentifizieren ](../adobe-applications/marketo/marketo-auth.md)Instanz) . | `123-ABC-456` |
| `sfdc_org_id` | Die Organisations-ID für Ihr [!DNL Salesforce]. Weiterführende Informationen dazu, [[!DNL Salesforce]  Sie Ihre [!DNL Salesforce]-Organisations-ID erhalten, finden Sie im folgenden Handbuch](https://help.salesforce.com/articleView?id=000325251&type=1&mode=1) . | `00D4W000000FgYJUA0` |
| `has_abm` | Ein boolescher Wert, der angibt, ob Sie [!DNL Marketo Account-Based Marketing] abonniert haben. | `false` |
| `has_msi` | Ein boolescher Wert, der angibt, ob Sie [!DNL Marketo Sales Insight] abonniert haben. | `false` |

{style="table-layout:auto"}

+++

### Skripte ausführen

Nachdem Sie Ihre [!DNL Postman] und Umgebung eingerichtet haben, können Sie das Skript jetzt über die [!DNL Postman] ausführen.

Wählen Sie in der [!DNL Postman] den Stammordner des Dienstprogramms zur automatischen Generierung und dann **[!DNL Run]** aus der oberen Kopfzeile aus.

![root-folder](../../images/tutorials/create/salesforce/root-folder.png)

Die [!DNL Runner] wird angezeigt. Stellen Sie von hier aus sicher, dass alle Kontrollkästchen aktiviert sind, und wählen Sie dann **[!DNL Run Namespaces and Schemas Autogeneration Utility]** aus.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

Bei einer erfolgreichen Anfrage werden die B2B-Namespaces und -Schemas gemäß den Beta-Spezifikationen erstellt.

## Einrichten der [!DNL Salesforce] für Experience Platform auf Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../landing/multi-cloud.md).

Gehen Sie wie folgt vor, um zu erfahren, wie Sie Ihr [!DNL Salesforce] für Experience Platform auf Amazon Web Services (AWS) einrichten können.

### Voraussetzungen

Um in einer AWS-Region Ihr [!DNL Salesforce]-Konto mit Experience Platform zu verbinden, benötigen Sie Folgendes:

- Ein [!DNL Salesforce] Konto mit API-Zugriff.
- Ein [!DNL Salesforce Connected App], mit dem Sie dann den OAuth-Fluss JWT_BEARER aktivieren können.
- Die erforderlichen Berechtigungen in [!DNL Salesforce] für den Zugriff auf Daten.

### AUF DIE ZULASSUNGSLISTE SETZEN IP-Adresse für die Verbindung mit AWS

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform in AWS verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform auf AWS](../../ip-address-allow-list.md) .

### Erstellen eines [!DNL Salesforce Connected App]

Verwenden Sie zunächst Folgendes, um Zertifikate/Schlüsselpaare von PEM-Dateien zu erstellen.

```shell
openssl req -newkey rsa:4096 -new -nodes -x509 -days 3650 -keyout key.pem -out cert.pem  
```

1. Wählen Sie im [!DNL Salesforce]-Dashboard Einstellungen aus ![Das Einstellungssymbol.](/help/images/icons/settings.png)) und wählen Sie dann **[!DNL Setup]** aus.
2. Navigieren Sie zu [!DNL App Manager] und wählen Sie **[!DNL New Connection App]** aus.
3. Geben Sie einen Namen für Ihre App an und lassen Sie zu, dass der Rest der Felder automatisch ausgefüllt wird.
4. Aktivieren Sie das Kästchen für [!DNL Enable OAuth Settings].
5. Festlegen einer Callback-URL. Da dies nicht für JWT verwendet wird, können Sie `https://localhost` verwenden.
6. Aktivieren Sie das Kästchen für [!DNL Use Digital Signatures].
7. Laden Sie die zuvor erstellte Datei cert.pem hoch.

#### Erforderliche Berechtigungen hinzufügen

Fügen Sie die folgenden Berechtigungen hinzu:

1. Benutzerdaten über APIs verwalten (API)
2. Zugriff auf benutzerdefinierte Berechtigungen (custom_permissions)
3. Zugriff auf den Identity URL-Service (ID, Profil, E-Mail, Adresse, Telefon)
4. Zugriff auf eindeutige Kennungen (openid)
5. Jederzeit Anfragen ausführen (refresh_token, offline_access)

Nachdem Sie Ihre Berechtigungen hinzugefügt haben, stellen Sie sicher, dass Sie das Feld für **[!DNL Issue JSON Web Token (JWT)-based access tokens for named user]** aktivieren.

Wählen Sie als Nächstes **[!DNL Save]**, **[!DNL Continue]** und dann **[!DNL Manage Customer Details]** aus. Verwenden Sie das Bedienfeld Verbraucherdetails , um Folgendes abzurufen:

- **Kundenschlüssel**: Dieser Kundenschlüssel wird später bei der Authentifizierung Ihres [!DNL Salesforce] bei Experience Platform als Ihre Client-ID verwendet.
- **Consumer Secret**: Dieses Consumer Secret wird später bei der Authentifizierung Ihres [!DNL Salesforce]-Kontos bei Experience Platform als Client-ID verwendet.

### Autorisieren des [!DNL Salesforce] Benutzers für die verbundene App

Gehen Sie wie folgt vor, um eine Autorisierung zur Verwendung der verbundenen App zu erhalten:

1. Navigieren Sie zu **[!DNL Manage Connected Apps]**.
2. Wählen Sie **[!DNL Edit]** aus.
3. Konfigurieren Sie **[!DNL Permitted Users]** als **[!DNL Admin approved users are pre-authorized]** und wählen Sie dann **[!DNL Save]** aus.
4. Navigieren Sie zu **[!DNL Settings]> [!DNL Manage Users] >[!DNL Profiles]**.
5. Bearbeiten Sie das mit Ihrem Benutzer verknüpfte Profil.
6. Navigieren Sie zu **[!DNL Connected App Access]** und wählen Sie die App aus, die Sie in einem früheren Schritt erstellt haben.

### JWT-Bearer-Token generieren

Gehen Sie wie folgt vor, um Ihr JWT-Bearer-Token zu generieren.

#### Schlüsselpaar in pkcs12 konvertieren

Um Ihr JWT-Bearer-Token zu generieren, müssen Sie zunächst den folgenden Befehl verwenden, um Ihr Zertifikat/Schlüsselpaar in das pkcs12-Format zu konvertieren. In diesem Schritt müssen Sie auch **Exportkennwort festlegen** wenn Sie dazu aufgefordert werden.

```shell
openssl pkcs12 -export -in cert.pem -inkey key.pem -name jwtcert >jwtcert.p12
```

#### Java-Keystore basierend auf pkcs12 erstellen

Verwenden Sie als Nächstes den folgenden Befehl, um einen Java-Keystore auf der Grundlage des soeben generierten pkcs12 zu erstellen. In diesem Schritt müssen Sie bei Aufforderung auch **Ziel-Keystore-Kennwort festlegen** festlegen. Darüber hinaus müssen Sie das vorherige Exportkennwort als Quell-Keystore-Kennwort angeben.

```shell
keytool -importkeystore -srckeystore jwtcert.p12 -destkeystore keystore.jks -srcstoretype pkcs12 -alias jwtcert
```

#### Vergewissern Sie sich, dass Ihre Datei keystroke.jks den Alias jwtcert enthält

Verwenden Sie als Nächstes den folgenden Befehl, um zu bestätigen, dass Ihr `keystroke.jks` einen `jwtcert` Alias enthält. In diesem Schritt werden Sie aufgefordert, das Ziel-Keystore-Kennwort anzugeben, das im vorherigen Schritt generiert wurde.

```shell
keytool -keystore keystore.jks -list
```

#### Signiertes Token generieren

Verwenden Sie abschließend das folgende JWTE-Beispiel der Java-Klasse, um Ihr signiertes Token zu generieren.

```java
package org.example;
 
import org.apache.commons.codec.binary.Base64;
 
import java.io.*;
import java.security.*;
import java.text.MessageFormat;
 
public class Main {
 
    public static void main(String[] args) {
 
        String header = "{\"alg\":\"RS256\"}";
        String claimTemplate = "'{'\"iss\": \"{0}\", \"sub\": \"{1}\", \"aud\": \"{2}\", \"exp\": \"{3}\"'}'";
 
        try {
            StringBuffer token = new StringBuffer();
 
            //Encode the JWT Header and add it to our string to sign
            token.append(Base64.encodeBase64URLSafeString(header.getBytes("UTF-8")));
 
            //Separate with a period
            token.append(".");
 
            //Create the JWT Claims Object
            String[] claimArray = new String[5];
            claimArray[0] = "{CLIENT_ID}";
            claimArray[1] = "{AUTHORIZED_SALESFORCE_USERNAME}";
            claimArray[2] = "{SALESFORCE_LOGIN_URL}";
            claimArray[3] = Long.toString((System.currentTimeMillis() / 1000) + 2629746*4);
            MessageFormat claims;
            claims = new MessageFormat(claimTemplate);
            String payload = claims.format(claimArray);
 
            //Add the encoded claims object
            token.append(Base64.encodeBase64URLSafeString(payload.getBytes("UTF-8")));
 
            //Load the private key from a keystore
            KeyStore keystore = KeyStore.getInstance("JKS");
            keystore.load(new FileInputStream("path/to/keystore"), "keystorepassword".toCharArray());
            PrivateKey privateKey = (PrivateKey) keystore.getKey("jwtcert", "privatekeypassword".toCharArray());
 
            //Sign the JWT Header + "." + JWT Claims Object
            Signature signature = Signature.getInstance("SHA256withRSA");
            signature.initSign(privateKey);
            signature.update(token.toString().getBytes("UTF-8"));
            String signedPayload = Base64.encodeBase64URLSafeString(signature.sign());
 
            //Separate with a period
            token.append(".");
 
            //Add the encoded signature
            token.append(signedPayload);
 
            System.out.println(token.toString());
 
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

| Eigenschaft | Konfigurationen  |
| --- | --- |
| `claimArray[0]` | Aktualisieren Sie `claimArray[0]` mit Ihrer Client-ID. |
| `claimArray[1]` | Aktualisieren Sie `claimArray[1]` mit dem [!DNL Salesforce] Benutzernamen, der für die App autorisiert ist. |
| `claimArray[2]` | Aktualisieren Sie `claimArray[2]` mit Ihrer [!DNL Salesforce] Anmelde-URL. |
| `claimArray[3]` | Aktualisieren Sie `claimArray[3]` mit einem Ablaufdatum, das seit der Epochenzeit in Millisekunden formatiert ist. Beispielsweise ist `3660624000000` 12-31-2085. |
| `/path/to/keystore` | Ersetzen Sie `/path/to/keystore` durch den richtigen Pfad zu Ihrem Keystore.jks |
| `keystorepassword` | Ersetzen Sie `keystorepassword` durch Ihr Ziel-Keystore-Kennwort. |
| `privatekeypassword` | Ersetzen Sie `privatekeypassword` durch Ihr Quell-Keystore-Kennwort. |

## Nächste Schritte

Nachdem Sie die Voraussetzungen für Ihr [!DNL Salesforce]-Konto eingerichtet haben, können Sie mit dem Verbinden Ihres [!DNL Salesforce]-Kontos mit Experience Platform fortfahren und Ihre CRM-Daten aufnehmen. Weitere Informationen finden Sie in der folgenden Dokumentation:

### Verbinden von [!DNL Salesforce] mit Experience Platform mithilfe von APIs

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Salesforce] mit Experience Platform mithilfe von APIs oder der Benutzeroberfläche:

- [Verbinden von Salesforce mit Experience Platform mithilfe der Flow Service-API](../../tutorials/api/create/crm/salesforce.md)
- [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine CRM-Quelle mithilfe der Flow Service-API](../../tutorials/api/collect/crm.md)

### Verbinden von [!DNL Salesforce] mit Experience Platform über die Benutzeroberfläche

- [Erstellen einer Salesforce-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/crm/salesforce.md)
- [Erstellen eines Datenflusses für eine CRM-Verbindung über die Benutzeroberfläche](../../tutorials/ui/dataflow/crm.md)