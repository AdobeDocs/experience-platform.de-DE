---
title: Einrichten und Konfigurieren von kundenverwalteten Schlüsseln mithilfe der API
description: Erfahren Sie, wie Sie Ihre CMK-App mit Ihrem Azure-Mandanten einrichten und Ihre Verschlüsselungsschlüssel-ID an Adobe Experience Platform senden.
exl-id: c9a1888e-421f-4bb4-b4c7-968fb1d61746
source-git-commit: 4f08e8fcc8d53b981af60226f1397a1d1ac4d8dc
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 49%

---

# Einrichten und Konfigurieren von kundenverwalteten Schlüsseln mithilfe der API

In diesem Dokument wird der Prozess zum Aktivieren der Funktion für kundenverwaltete Schlüssel (CMK) in Adobe Experience Platform mithilfe der API beschrieben. Anweisungen zum Abschließen dieses Prozesses mithilfe der Benutzeroberfläche finden Sie im Dokument [CMK-Setup für die Benutzeroberfläche](./ui-set-up.md).

## Voraussetzungen

Um den Abschnitt [!UICONTROL Verschlüsselung] in Adobe Experience Platform anzuzeigen und aufzurufen, müssen Sie eine Rolle erstellt und dieser Rolle die Berechtigung [!UICONTROL Kundenverwalteten Schlüssel verwalten] zugewiesen haben. Jeder Benutzer mit der Berechtigung [!UICONTROL Kunden-verwalteten Schlüssel verwalten] kann CMK für seine Organisation aktivieren.

Weiterführende Informationen zum Zuweisen von Rollen und Berechtigungen in Experience Platform finden Sie in der Dokumentation [Berechtigungen konfigurieren](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=de) .

Um CMK zu aktivieren, muss Ihr [[!DNL Azure] Key Vault](./azure-key-vault-config.md) mit den folgenden Einstellungen konfiguriert werden:

* [Bereinigungsschutz aktivieren](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Soft-Delete aktivieren](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Konfigurieren des Zugriffs mithilfe der rollenbasierten Zugriffskontrolle [!DNL Azure] 2}](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Konfigurieren eines [!DNL Azure] Schlüssel-Vault](./azure-key-vault-config.md)

## Einrichten der CMK-App {#register-app}

Nachdem Sie Ihren Key Vault konfiguriert haben, müssen Sie sich für die CMK-Anwendung registrieren, die mit Ihrem [!DNL Azure] -Mandanten verknüpft wird.

### Erste Schritte

Zum Registrieren des CMK-Programms müssen Sie Aufrufe an Platform-APIs durchführen. Weitere Informationen dazu, wie Sie die erforderlichen Authentifizierungskopfzeilen für diese Aufrufe erfassen, finden Sie im [Handbuch zur Platform-API-Authentifizierung](../../api-authentication.md).

Während das Authentifizierungshandbuch Anweisungen zum Generieren Ihres eigenen eindeutigen Werts für die erforderliche `x-api-key`-Anfragekopfzeile enthält, verwenden alle API-Vorgänge in diesem Handbuch stattdessen den statischen Wert `acp_provisioning`. Sie müssen allerdings weiterhin eigene Werte für `{ACCESS_TOKEN}` und `{ORG_ID}` angeben.

In allen in diesem Handbuch angezeigten API-Aufrufen wird `platform.adobe.io` als Stammpfad verwendet, der standardmäßig auf den VA7-Bereich verweist. Wenn Ihr Unternehmen eine andere Region verwendet, muss auf `platform` ein Bindestrich und der Ihrer Organisation zugewiesene Regionscode folgen: `nld2` für NLD2 oder `aus5` für AUS5 (z. B. `platform-aus5.adobe.io`). Wenn Sie die Region Ihres Unternehmens nicht kennen, wenden Sie sich an Ihren Systemadministrator.

### Abrufen einer Authentifizierungs-URL {#fetch-authentication-url}

Um den Registrierungsprozess zu starten, stellen Sie eine GET-Anfrage an den App-Registrierungsendpunkt, um die erforderliche Authentifizierungs-URL für Ihre Organisation abzurufen.

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/byok/app-registration \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine `applicationRedirectUrl`-Eigenschaft zurück, die die Authentifizierungs-URL enthält.

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

Kopieren Sie die `applicationRedirectUrl`-Adresse und fügen Sie sie in einen Browser ein, um ein Authentifizierungsdialogfeld zu öffnen. Wählen Sie **[!DNL Accept]** aus, um den Service-Prinzipal der CMK-App zu Ihrem [!DNL Azure]-Mandanten hinzuzufügen.

![Ein Dialogfeld mit einer Microsoft-Berechtigungsanfrage, in dem [!UICONTROL Accept] hervorgehoben ist.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### Zuweisen der CMK-App zu einer Rolle {#assign-to-role}

Navigieren Sie nach Abschluss des Authentifizierungsprozesses zu Ihrem [!DNL Azure]-Schlüsseltresor und wählen Sie **[!DNL Access control]** in der linken Navigation aus. Wählen Sie von hier aus **[!DNL Add]** gefolgt von **[!DNL Add role assignment]** aus.

![Das Microsoft Azure-Dashboard mit [!DNL Add] und [!DNL Add role assignment] hervorgehoben.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

Im nächsten Bildschirm werden Sie aufgefordert, eine Rolle für diese Zuweisung auszuwählen. Wählen Sie **[!DNL Key Vault Crypto Service Encryption User]** aus, bevor Sie auf **[!DNL Next]** klicken, um fortzufahren.

>[!NOTE]
>
>Wenn Sie über die [!DNL Managed-HSM Key Vault]-Ebene verfügen, müssen Sie die **[!DNL Managed HSM Crypto Service Encryption User]**-Benutzerrolle auswählen.

![Das Microsoft Azure-Dashboard mit dem hervorgehobenen [!DNL Key Vault Crypto Service Encryption User].](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Wählen Sie auf dem nächsten Bildschirm **[!DNL Select members]** aus, um ein Dialogfeld in der rechten Leiste zu öffnen. Verwenden Sie die Suchleiste, um den Service-Prinzipal für das CMK-Programm zu suchen und ihn aus der Liste auszuwählen. Wenn Sie fertig sind, klicken Sie auf **[!DNL Save]**.

>[!NOTE]
>
>Wenn Sie Ihr Programm in der Liste nicht finden, wurde Ihr Service-Prinzipal in Ihrem Mandanten nicht akzeptiert. Wenden Sie sich an Ihren [!DNL Azure] -Administrator oder -Support-Mitarbeiter, um sicherzustellen, dass Sie über die richtigen Berechtigungen verfügen.

## Aktivieren der Konfiguration des Verschlüsselungsschlüssels auf Experience Platform {#send-to-adobe}

Nach der Installation der CMK-App in [!DNL Azure] können Sie Ihre Verschlüsselungsschlüssel-ID an Adobe senden. Wählen Sie in der linken Navigation **[!DNL Keys]** aus, gefolgt vom Namen des Schlüssels, den Sie senden möchten.

![Das Microsoft Azure-Dashboard mit dem Objekt [!DNL Keys] und dem Schlüsselnamen hervorgehoben.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Wählen Sie die neueste Version des Schlüssels aus, und seine Detailseite wird angezeigt. Von hier aus können Sie optional die zulässigen Vorgänge für den Schlüssel konfigurieren.

>[!IMPORTANT]
>
>Die für den Schlüssel mindestens erforderlichen Vorgänge sind die Berechtigungen **[!DNL Wrap Key]** und **[!DNL Unwrap Key]**. Sie können [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign] und [!DNL Verify] einbeziehen, falls Sie möchten.

Das Feld **[!UICONTROL Schlüsselkennung]** zeigt die URI-Kennung für den Schlüssel an. Kopieren Sie diesen URI-Wert zur Verwendung im nächsten Schritt.

![Die Schlüsseldetails des Microsoft Azure-Dashboards mit den Abschnitten [!DNL Permitted operations] und der URL-Schlüssel zum Kopieren wurden hervorgehoben.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Nachdem Sie den Schlüsseltresor-URI erhalten haben, können Sie ihn mit einer POST-Anfrage an den CMK-Konfigurations-Endpunkt senden.

>[!NOTE]
>
>Nur der Schlüssel und der Schlüsselname werden bei Adobe gespeichert, nicht die Schlüsselversion.

**Anfrage**

+++ Eine Beispielanfrage zum Senden des Schlüssel-Vault-URI an den CMK-Konfigurationsendpunkt.

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
          "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Ein Name für die Konfiguration. Stellen Sie sicher, dass Sie sich diesen Wert merken, da der Konfigurationsstatus in einem [späteren Schritt](#check-status) überprüft werden muss. Bei dem Wert ist die Groß-/Kleinschreibung zu beachten. |
| `type` | Der Konfigurationstyp. Muss auf `BYOK_CONFIG` festgelegt werden. |
| `imsOrgId` | Ihre Organisations-ID. Diese ID muss mit dem unter der Kopfzeile `x-gw-ims-org-id` angegebenen Wert übereinstimmen. |
| `configData` | Diese Eigenschaft enthält die folgenden Details zur Konfiguration:<ul><li>`providerType`: Muss auf `AZURE_KEYVAULT` festgelegt werden.</li><li>`keyVaultKeyIdentifier`: Der URI für den Schlüsseltresor, den Sie [zuvor](#send-to-adobe) kopiert haben.</li></ul> |

+++

**Antwort**

+++ Die erfolgreiche Antwort gibt die Details des Konfigurationsauftrags zurück.

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
    "imsOrgId": "{ORG_ID}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

+++

Der Auftrag sollte die Verarbeitung innerhalb weniger Minuten abschließen.

## Überprüfen des Konfigurationsstatus {#check-status}

Um den Status der Konfigurationsanfrage zu überprüfen, können Sie eine GET-Anfrage stellen.

**Anfrage**

Sie müssen den `name` der Konfiguration, die Sie überprüfen möchten, an den Pfad (`config1` im Beispiel unten) anhängen und einen `configType`-Abfrageparameter, der auf `BYOK_CONFIG` gesetzt ist, einfügen.

+++ Eine Beispielanfrage zur Überprüfung des Status der Konfigurationsanfrage.

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

+++

**Antwort**

+++ Die erfolgreiche Antwort gibt den Status des Auftrags zurück.

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
  "imsOrgId": "{ORG_ID}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

+++

Das `status`-Attribut kann einen von vier Werten mit folgenden Bedeutungen haben:

1. `RUNNING`: Prüft, ob Platform auf den Schlüssel und den Schlüssel-Vault zugreifen kann.
1. `UPDATE_EXISTING_RESOURCES`: Das System fügt den Schlüsseltresor und den Schlüsselnamen zu den Datenspeichern in allen Sandboxes in Ihrer Organisation hinzu.
1. `COMPLETED`: Der Schlüssel und der Schlüsselname wurden den Datenspeichern erfolgreich hinzugefügt.
1. `FAILED`: Es ist ein Problem aufgetreten, das in erster Linie mit dem Schlüssel, dem Schlüsseltresor oder der Einrichtung der Multi-Mandanten-App-zusammenhängt.

## Nächste Schritte

Durch Ausführung der oben genannten Schritte haben Sie CMK für Ihre Organisation erfolgreich aktiviert. Daten, die in Primärdatenspeicher erfasst werden, werden jetzt mit den Schlüsseln in Ihrem [!DNL Azure] Key Vault verschlüsselt und entschlüsselt. Weitere Informationen zur Datenverschlüsselung in Adobe Experience Platform finden Sie in der [Verschlüsselungsdokumentation](../encryption.md).
