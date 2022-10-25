---
title: Vom Kunden verwaltete Schlüssel in Adobe Experience Platform
description: Erfahren Sie, wie Sie eigene Verschlüsselungsschlüssel für in Adobe Experience Platform gespeicherte Daten einrichten.
source-git-commit: f06f00f7581ccd7fe64f5292a53ebb0303c65069
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 2%

---

# Vom Kunden verwaltete Schlüssel in Adobe Experience Platform

Alle in Adobe Experience Platform gespeicherten Daten werden im Ruhezustand mithilfe von Schlüsseln auf Systemebene verschlüsselt. Wenn Sie eine Anwendung verwenden, die auf Platform aufbaut, können Sie stattdessen eigene Verschlüsselungsschlüssel verwenden, um die Datensicherheit zu verbessern.

In diesem Dokument wird der Prozess zum Aktivieren der Funktion für kundenverwaltete Schlüssel (CMK) in Platform beschrieben.

## Prozesszusammenfassung

CMK ist Teil des Gesundheitsschilds und des Datenschutzschilds der Adobe. Nachdem Ihr Unternehmen eines dieser Angebote erworben hat, können Sie einen einmaligen Prozess zur Einrichtung der Funktion starten.

>[!WARNING]
>
>Nach dem Einrichten von CMK können Sie nicht zu systemverwalteten Schlüsseln zurückkehren. Sie sind für die sichere Verwaltung Ihrer Schlüssel und Schlüsselwerte in [!DNL Azure] um zu verhindern, dass der Zugriff auf Ihre Daten verloren geht.

Der Prozess sieht folgendermaßen aus:

1. [Erstellen Sie eine [!DNL Microsoft Azure] Key Vault](#create-key-vault), dann [einen Verschlüsselungsschlüssel generieren](#generate-a-key) (basierend auf den Richtlinien Ihres Unternehmens), die letztendlich für die Adobe freigegeben werden.
1. Verwenden Sie API-Aufrufe für [die CMK-App registrieren](#register-app) mit [!DNL Azure] Mandanten.
1. [Dienstprinzipal für die CMK-App zuweisen](#assign-to-role) auf eine geeignete Rolle für den Schlüsselgewölbe.
1. Verwenden Sie API-Aufrufe für [Ihre Verschlüsselungsschlüssel-ID an Adobe senden](#send-to-adobe).

Sobald der Einrichtungsprozess abgeschlossen ist, werden alle Daten, die über alle Sandboxes in Platform integriert werden, mit Ihrer [!DNL Azure] Schlüsseleinrichtung, die für Ihre [[!DNL Cosmos DB]](https://docs.microsoft.com/de-de/azure/cosmos-db/) und [[!DNL Data Lake Storage]](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) Ressourcen. CMK nutzt [!DNL Azure]s [öffentliches Vorschaufenster](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/) um dies zu ermöglichen.

## Erstellen Sie eine [!DNL Azure] Key Vault {#create-key-vault}

CMK unterstützt nur Schlüssel aus einem [!DNL Microsoft Azure] Key Vault. Zunächst müssen Sie mit [!DNL Azure] , um ein neues Unternehmenskonto zu erstellen oder ein vorhandenes Unternehmenskonto zu verwenden, und führen Sie die folgenden Schritte aus, um das Key Vault zu erstellen.

>[!IMPORTANT]
>
>Nur die Service-Ebenen Premium und Standard für [!DNL Azure] Key Vault wird unterstützt. [!DNL Azure Managed HSM], [!DNL Azure Dedicated HSM] und [!DNL Azure Payments HSM] werden nicht unterstützt. Siehe Abschnitt [[!DNL Azure] Dokumentation](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) für weitere Informationen über angebotene Schlüsselverwaltungsdienste.

>[!NOTE]
>
>Die folgende Dokumentation behandelt nur die grundlegenden Schritte zum Erstellen des SchlüsselVault. Außerhalb dieser Anleitung sollten Sie den Schlüsselwert gemäß den Richtlinien Ihres Unternehmens konfigurieren.

Melden Sie sich bei der [!DNL Azure] Portal und suchen Sie mithilfe der Suchleiste nach **[!DNL Key vaults]** unter der Liste der Dienste.

![Suchen und Auswählen von Schlüsselwerten](../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

Die **[!DNL Key vaults]** angezeigt, nachdem Sie den Dienst ausgewählt haben. Wählen Sie von hier aus **[!DNL Create]**.

![Erstellen von Schlüsselwerten](../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Füllen Sie mithilfe des bereitgestellten Formulars die grundlegenden Details für den Schlüsselgewölbe aus, einschließlich eines Namens und einer zugewiesenen Ressourcengruppe.

>[!WARNING]
>
>Die meisten Optionen können als Standardwerte beibehalten werden. **Stellen Sie sicher, dass Sie die Schutzoptionen für Soft-Löschen und Bereinigen aktivieren**. Wenn Sie diese Funktionen nicht aktivieren, riskieren Sie, den Zugriff auf Ihre Daten zu verlieren, wenn der Schlüsselwert gelöscht wird.
>
>![Bereinigungsschutz aktivieren](../images/governance-privacy-security/customer-managed-keys/basic-config.png)

Fahren Sie von hier aus mit dem Workflow zur Erstellung von SchlüsselVault fort und konfigurieren Sie die verschiedenen Optionen entsprechend den Richtlinien Ihres Unternehmens.

Sobald Sie bei der **[!DNL Review + create]** Schritt, können Sie die Details des SchlüsselVault während der Validierung überprüfen. Nachdem die Validierung erfolgreich abgeschlossen wurde, wählen Sie **[!DNL Create]** , um den Prozess abzuschließen.

![Grundlegende Konfiguration für den Key Vault](../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Microsoft eine Firewall-Ausnahme gewähren

Wenn Ihr Key Vault so konfiguriert ist, dass der öffentliche Zugriff auf bestimmte virtuelle Netzwerke eingeschränkt oder der öffentliche Zugriff vollständig deaktiviert wird, müssen Sie Microsoft eine Firewall-Ausnahme gewähren.

Auswählen **[!DNL Networking]** in der linken Navigation. under **[!DNL Firewalls and virtual networks]**, aktivieren Sie das Kontrollkästchen **[!DNL Allow trusted Microsoft services to bypass this firewall]**, wählen Sie **[!DNL Apply]**.

![Grundlegende Konfiguration für den Key Vault](../images/governance-privacy-security/customer-managed-keys/networking.png)

## Schlüssel generieren {#generate-a-key}

Nachdem Sie einen Schlüssel erstellt haben, können Sie einen neuen Schlüssel generieren. Navigieren Sie zum **[!DNL Keys]** Registerkarte und wählen Sie **[!DNL Generate/Import]**.

![Schlüssel generieren](../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Verwenden Sie das bereitgestellte Formular, um einen Namen für den Schlüssel anzugeben, und wählen Sie **RSA** für den Schlüsseltyp. Die Variable **[!DNL RSA key size]** darf nicht kleiner sein als **3072** Bit nach [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] ist auch mit RSA 3027 vereinbar.

>[!NOTE]
>
>Merken Sie sich den Namen, den Sie für den Schlüssel angeben, da er in einem späteren Schritt verwendet wird, wenn [Senden des Schlüssels an Adobe](#send-to-adobe).

Verwenden Sie die restlichen Steuerelemente, um den Schlüssel zu konfigurieren, den Sie erstellen oder importieren möchten. Wenn Sie fertig sind, wählen Sie **[!DNL Create]**.

![Schlüssel konfigurieren](../images/governance-privacy-security/customer-managed-keys/configure-key.png)

Der konfigurierte Schlüssel wird in der Liste der Schlüssel für den Vault angezeigt.

![Schlüssel hinzugefügt](../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Registrieren der CMK-App {#register-app}

Nachdem Sie Ihren KeyVault konfiguriert haben, müssen Sie sich für die CMK-Anwendung registrieren, die mit Ihrer [!DNL Azure] Mandanten.

>[!NOTE]
>
>Zum Registrieren der CMK-App müssen Sie Aufrufe an Platform-APIs durchführen. Weitere Informationen dazu, wie Sie die erforderlichen Authentifizierungskopfzeilen für diese Aufrufe erfassen, finden Sie unter [Authentifizierungshandbuch zur Platform-API](../../landing/api-authentication.md).
>
>Das Authentifizierungshandbuch enthält Anweisungen zum Generieren Ihres eigenen eindeutigen Werts für die erforderlichen `x-api-key` Anfragekopfzeile verwenden alle API-Vorgänge in diesem Handbuch den statischen Wert `acp_provisioning` anstatt. Sie müssen weiterhin eigene Werte für `{ACCESS_TOKEN}` und `{ORG_ID}`jedoch.

### Abrufen einer Authentifizierungs-URL

Um den Registrierungsprozess zu starten, stellen Sie eine GET-Anfrage an den App-Registrierungsendpunkt, um die erforderliche Authentifizierungs-URL für Ihr Unternehmen abzurufen.

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/byok/app-registration \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine `applicationRedirectUrl` -Eigenschaft, die die Authentifizierungs-URL enthält.

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

Kopieren und einfügen Sie die `applicationRedirectUrl` Adresse in einen Browser eingeben, um ein Authentifizierungsdialogfeld zu öffnen. Auswählen **[!DNL Accept]** , um den Prinzipal des CMK-App-Dienstes zu Ihrem [!DNL Azure] Mandanten.

![Genehmigungsanfrage](../images/governance-privacy-security/customer-managed-keys/app-permission.png)

## Zuweisen der CMK-App zu einer Rolle {#assign-to-role}

Navigieren Sie nach Abschluss des Authentifizierungsprozesses zu Ihrer [!DNL Azure] Key Vault und Auswahl **[!DNL Access control]** in der linken Navigation. Wählen Sie von hier aus **[!DNL Add]** gefolgt von **[!DNL Add role assignment]**.

![Rollenzuweisung hinzufügen](../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

Im nächsten Bildschirm werden Sie aufgefordert, eine Rolle für diese Zuweisung auszuwählen. Auswählen **[!DNL Key Vault Crypto Service Encryption User]** vor der Auswahl **[!DNL Next]** , um fortzufahren.

![Rolle auswählen](../images/governance-privacy-security/customer-managed-keys/select-role.png)

Wählen Sie auf dem nächsten Bildschirm **[!DNL Select members]** , um ein Dialogfeld in der rechten Leiste zu öffnen. Verwenden Sie die Suchleiste, um den Dienstprinzipal für die CMK-Anwendung zu suchen und ihn aus der Liste auszuwählen. Wenn Sie fertig sind, wählen Sie **[!DNL Save]**.

>[!NOTE]
>
>Wenn Sie Ihre Anwendung nicht in der Liste finden, wurde Ihr Dienstprinzipal nicht in Ihrem Mandanten akzeptiert. Arbeiten Sie bitte mit Ihrem [!DNL Azure] Administrator oder Support-Mitarbeiter, um sicherzustellen, dass Sie über die richtigen Berechtigungen verfügen.

## Senden des Schlüssel-URI an Adobe {#send-to-adobe}

Nach der Installation der CMK-App auf [!DNL Azure]können Sie Ihre Verschlüsselungsschlüsselkennung an Adobe senden. Auswählen **[!DNL Keys]** in der linken Navigation gefolgt vom Namen des Schlüssels, den Sie senden möchten.

![Schlüssel auswählen](../images/governance-privacy-security/customer-managed-keys/select-key.png)

Wählen Sie die neueste Version des Schlüssels aus und die Detailseite wird angezeigt. Von hier aus können Sie optional die zulässigen Vorgänge für den Schlüssel konfigurieren. Der Schlüssel muss mindestens dem **[!DNL Wrap Key]** und **[!DNL Unwrap Key]** Berechtigungen.

Die **[!UICONTROL Schlüsselkennung]** zeigt die URI-Kennung für den Schlüssel an. Kopieren Sie diesen URI-Wert zur Verwendung im nächsten Schritt.

![Schlüssel-URL kopieren](../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Nachdem Sie den Schlüssel-Vault-URI erhalten haben, können Sie ihn mit einer POST-Anfrage an den CMK-Konfigurations-Endpunkt senden.

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/infrastructure/manager/customer/config \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "name": "Config1",
        "type": "BYOK_CONFIG",
        "imsOrgId": "{ORG_ID}",
        "configData": {
          "providerType": "AZURE_KEYVAULT",
          "keyVaultIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Ein Name für die Konfiguration. Stellen Sie sicher, dass Sie sich diesen Wert merken, da er erforderlich ist, um den Konfigurationsstatus in einem [Späterschritt](#check-status). Beim Wert wird zwischen Groß- und Kleinschreibung unterschieden. |
| `type` | Der Konfigurationstyp. Muss auf `BYOK_CONFIG` festgelegt werden. |
| `imsOrgId` | Die Kennung Ihrer IMS-Organisation. Dieser Wert muss mit dem Wert übereinstimmen, der unter `x-gw-ims-org-id` -Kopfzeile. |
| `configData` | Enthält die folgenden Details zur Konfiguration:<ul><li>`providerType`: Muss auf `AZURE_KEYVAULT` festgelegt werden.</li><li>`keyVaultIdentifier`: Der URI für den Schlüsselwert, den Sie kopiert haben [früher](#send-to-adobe).</li></ul> |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Konfigurationsauftrags zurück.

```json
{
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "config": {
    "configData": {
      "keyVaultUri": "https://adobecmkexample.vault.azure.net",
      "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
      "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
      "keyName": "Config1",
      "providerType": "AZURE_KEYVAULT"
    },
    "name": "acpcf978863Aaepcmkmultitenantapp",
    "type": "BYOK_CONFIG",
    "imsOrgId": "{IMS_ORG}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

Der Auftrag sollte die Verarbeitung innerhalb weniger Minuten abschließen.

### Überprüfen des Konfigurationsstatus {#check-status}

Um den Status der Konfigurationsanfrage zu überprüfen, können Sie eine GET-Anfrage stellen.

**Anfrage**

Sie müssen die `name` der Konfiguration, die Sie zum Pfad (`config1` im Beispiel unten) und fügen Sie eine `configType` Abfrageparameter festgelegt auf `BYOK_CONFIG`.

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den Status des Auftrags zurück.

```json
{
  "name": "acpcf978863Aaepcmkmultitenantapp",
  "type": "BYOK_CONFIG",
  "status": "COMPLETED",
  "configData": {
    "keyVaultUri": "https://adobecmkexample.vault.azure.net",
    "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
    "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
    "keyName": "Config1",
    "providerType": "AZURE_KEYVAULT"
  },
  "imsOrgId": "{IMS_ORG}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

Die `status` -Attribut kann einen von vier Werten mit der folgenden Bedeutung haben:

1. `RUNNING`: Überprüft, ob Platform Zugriff auf den Schlüssel und den Schlüssel-Vault hat.
1. `UPDATE_EXISTING_RESOURCES`: Das System fügt den Schlüsselwert und den Schlüsselnamen zu den Datenspeichern in allen Sandboxes in Ihrer Organisation hinzu.
1. `COMPLETED`: Der Schlüssel und der Schlüsselname wurden den Datenspeichern hinzugefügt.
1. `FAILED`: Es ist ein Problem aufgetreten, das in erster Linie mit dem Schlüssel-, Schlüssel- oder Multi-Mandanten-App-Setup zusammenhängt.

## Nächste Schritte

Durch Ausführung der oben genannten Schritte haben Sie CMK für Ihr Unternehmen erfolgreich aktiviert. Alle Daten, die in Platform erfasst werden, werden jetzt mit den Schlüsseln in Ihrer [!DNL Azure] Key Vault. Wenn Sie den Platform-Zugriff auf Ihre Daten sperren möchten, können Sie die mit der Anwendung verknüpfte Benutzerrolle aus dem Schlüsselwert in [!DNL Azure].

Nach der Deaktivierung des Zugriffs auf die Anwendung dauert es zwischen zwei und 24 Stunden, bis Daten nicht mehr in Platform verfügbar sind. Der gleiche Zeitraum gilt für Daten, die erneut verfügbar werden, wenn der Zugriff auf die Anwendung erneut aktiviert wird.
