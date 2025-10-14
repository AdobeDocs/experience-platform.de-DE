---
title: Einrichten und Konfigurieren von kundenverwalteten Schlüsseln für Azure mithilfe der API
description: Erfahren Sie, wie Sie Ihre CMK-App mit Ihrem Azure-Mandanten einrichten und Ihre Verschlüsselungsschlüssel-ID an Adobe Experience Platform senden.
role: Developer
feature: API, Privacy
exl-id: c9a1888e-421f-4bb4-b4c7-968fb1d61746
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 44%

---

# Einrichten und Konfigurieren von kundenverwalteten Schlüsseln für Azure mithilfe der API

In diesem Dokument werden die Azure-spezifischen Anweisungen zum Aktivieren von kundenverwalteten Schlüsseln (CMK) in Adobe Experience Platform mithilfe der -API behandelt. Anweisungen zum Abschließen dieses Prozesses mithilfe der Benutzeroberfläche für von Azure gehostete Experience Platform-Instanzen finden Sie im Dokument [UI CMK Setup](./ui-set-up.md).

Spezifische Anweisungen für AWS finden Sie im [AWS-Setup-Handbuch](../aws/ui-set-up.md).

## Voraussetzungen

Um den Abschnitt [!UICONTROL Verschlüsselung] in Adobe Experience Platform anzuzeigen, müssen Sie eine Rolle erstellt und dieser Rolle die Berechtigung [!UICONTROL Kundenverwalteten Schlüssel verwalten] zugewiesen haben. Jeder Benutzer, der über die Berechtigung [!UICONTROL Kundenverwalteten Schlüssel verwalten] verfügt, kann für seine Organisation CMK aktivieren.

Weitere Informationen zur Zuweisung von Rollen und Berechtigungen in Experience Platform finden Sie in der [Dokumentation zu Berechtigungen konfigurieren](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=de).

Um CMK für Azure-gehostete Experience Platform-Instanzen zu aktivieren[[!DNL Azure]  muss Ihr -Schlüsseltresor mit &#x200B;](./azure-key-vault-config.md) Einstellungen konfiguriert werden:

* [Bereinigungsschutz aktivieren](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Soft-Delete aktivieren](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Konfigurieren des Zugriffs mithilfe  [!DNL Azure]  rollenbasierten Zugriffssteuerung](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Konfigurieren  [!DNL Azure]  Schlüsseltresors](./azure-key-vault-config.md)

## Einrichten der CMK-App {#register-app}

Nachdem Sie Ihren Schlüsseltresor konfiguriert haben, müssen Sie sich für das CMK-Programm registrieren, das sich mit Ihrem [!DNL Azure] verknüpft.

### Erste Schritte

Zum Registrieren der CMK-App müssen Sie Aufrufe an Experience Platform-APIs durchführen. Weitere Informationen dazu, wie Sie die erforderlichen Authentifizierungskopfzeilen für diese Aufrufe erfassen, finden Sie im Authentifizierungshandbuch für die [Experience Platform-API](../../../api-authentication.md).

Während das Authentifizierungshandbuch Anweisungen zum Generieren Ihres eigenen eindeutigen Werts für die erforderliche `x-api-key`-Anfragekopfzeile enthält, verwenden alle API-Vorgänge in diesem Handbuch stattdessen den statischen Wert `acp_provisioning`. Sie müssen allerdings weiterhin eigene Werte für `{ACCESS_TOKEN}` und `{ORG_ID}` angeben.

In allen in diesem Handbuch gezeigten API-Aufrufen wird `platform.adobe.io` als Stammpfad verwendet, der standardmäßig auf die VA7-Region verweist. Wenn Ihr Unternehmen eine andere Region verwendet, muss auf `platform` ein Bindestrich und der Ihrer Organisation zugewiesene Regionscode folgen: `nld2` für NLD2 oder `aus5` für AUS5 (z. B.: `platform-aus5.adobe.io`). Wenn Sie die Region Ihres Unternehmens nicht kennen, wenden Sie sich an Ihren Systemadministrator.

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

![Dialogfeld für Microsoft-Berechtigungsanfragen mit hervorgehobener [!UICONTROL Akzeptieren]-Option.](../../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### Zuweisen der CMK-App zu einer Rolle {#assign-to-role}

Navigieren Sie nach Abschluss des Authentifizierungsprozesses zu Ihrem [!DNL Azure]-Schlüsseltresor und wählen Sie **[!DNL Access control]** in der linken Navigation aus. Wählen Sie von hier aus **[!DNL Add]** gefolgt von **[!DNL Add role assignment]** aus.

![Das Microsoft Azure-Dashboard mit hervorgehobenen [!DNL Add] und [!DNL Add role assignment].](../../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

Im nächsten Bildschirm werden Sie aufgefordert, eine Rolle für diese Zuweisung auszuwählen. Wählen Sie **[!DNL Key Vault Crypto Service Encryption User]** aus, bevor Sie auf **[!DNL Next]** klicken, um fortzufahren.

>[!NOTE]
>
>Wenn Sie über die [!DNL Managed-HSM Key Vault] verfügen, müssen Sie die **[!DNL Managed HSM Crypto Service Encryption User]** Benutzerrolle auswählen.

![Das Microsoft Azure-Dashboard mit hervorgehobenem [!DNL Key Vault Crypto Service Encryption User].](../../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Wählen Sie auf dem nächsten Bildschirm **[!DNL Select members]** aus, um ein Dialogfeld in der rechten Leiste zu öffnen. Verwenden Sie die Suchleiste, um den Service-Prinzipal für das CMK-Programm zu suchen und ihn aus der Liste auszuwählen. Wenn Sie fertig sind, klicken Sie auf **[!DNL Save]**.

>[!NOTE]
>
>Wenn Sie Ihr Programm in der Liste nicht finden, wurde Ihr Service-Prinzipal in Ihrem Mandanten nicht akzeptiert. Um sicherzustellen, dass Sie über die richtigen Berechtigungen verfügen, wenden Sie sich an Ihren [!DNL Azure] oder Vertreter.

## Aktivieren der Konfiguration des Verschlüsselungsschlüssels auf Experience Platform {#send-to-adobe}

Nach der Installation der CMK-App in [!DNL Azure] können Sie Ihre Verschlüsselungsschlüssel-ID an Adobe senden. Wählen Sie in der linken Navigation **[!DNL Keys]** aus, gefolgt vom Namen des Schlüssels, den Sie senden möchten.

![Das Microsoft Azure-Dashboard mit dem hervorgehobenen [!DNL Keys] und dem hervorgehobenen Schlüsselnamen.](../../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Wählen Sie die neueste Version des Schlüssels aus, und seine Detailseite wird angezeigt. Von hier aus können Sie optional die zulässigen Vorgänge für den Schlüssel konfigurieren.

>[!IMPORTANT]
>
>Die minimal zulässigen Vorgänge für den Schlüssel sind die Berechtigungen **[!DNL Wrap Key]** und **[!DNL Unwrap Key]** . Sie können bei Bedarf [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign] und [!DNL Verify] einbeziehen.

Das Feld **[!UICONTROL Schlüsselkennung]** zeigt die URI-Kennung für den Schlüssel an. Kopieren Sie diesen URI-Wert zur Verwendung im nächsten Schritt.

![Die Details zum Microsoft Azure-Dashboard-Schlüssel mit den hervorgehobenen Abschnitten &quot;[!DNL Permitted operations]&quot; und „URL des Kopierschlüssels“.](../../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Nachdem Sie den Schlüsseltresor-URI erhalten haben, können Sie ihn mit einer POST-Anfrage an den CMK-Konfigurations-Endpunkt senden.

>[!NOTE]
>
>Nur der Schlüssel und der Schlüsselname werden bei Adobe gespeichert, nicht die Schlüsselversion.

**Anfrage**

+++ Eine Beispielanfrage zum Senden des Schlüsseltresor-URI an den CMK-Konfigurationsendpunkt.

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
| `name` | Ein Name für die Konfiguration. Stellen Sie sicher, dass Sie sich diesen Wert merken, da er erforderlich ist, um den Konfigurationsstatus in einem [&#x200B; Schritt zu überprüfen](#check-status). Bei dem Wert ist die Groß-/Kleinschreibung zu beachten. |
| `type` | Der Konfigurationstyp. Muss auf `BYOK_CONFIG` festgelegt werden. |
| `imsOrgId` | Ihre Organisations-ID. Diese ID muss mit dem Wert übereinstimmen, der unter der `x-gw-ims-org-id`-Kopfzeile angegeben wird. |
| `configData` | Diese Eigenschaft enthält die folgenden Details zur Konfiguration:<ul><li>`providerType`: Muss auf `AZURE_KEYVAULT` festgelegt werden.</li><li>`keyVaultKeyIdentifier`: Der URI für den Schlüsseltresor, den Sie [zuvor](#send-to-adobe) kopiert haben.</li></ul> |

+++

**Antwort**

+++ Die erfolgreiche Antwort gibt die Details des Konfigurationsvorgangs zurück.

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

Der Vorgang sollte die Verarbeitung innerhalb weniger Minuten abschließen.

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

1. `RUNNING`: Überprüft, ob Experience Platform auf den Schlüssel und den Schlüsseltresor zugreifen kann.
1. `UPDATE_EXISTING_RESOURCES`: Das System fügt den Schlüsseltresor und den Schlüsselnamen zu den Datenspeichern in allen Sandboxes in Ihrer Organisation hinzu.
1. `COMPLETED`: Der Schlüsseltresor und der Schlüsselname wurden erfolgreich zu den Datenspeichern hinzugefügt.
1. `FAILED`: Es ist ein Problem aufgetreten, das in erster Linie mit dem Schlüssel, dem Schlüsseltresor oder der Einrichtung der Multi-Mandanten-App-zusammenhängt.

## Nächste Schritte

Durch Ausführung der oben genannten Schritte haben Sie CMK für Ihre Organisation erfolgreich aktiviert. Bei von Azure gehosteten Experience Platform-Instanzen werden Daten, die in primäre Datenspeicher aufgenommen werden, jetzt mit dem oder den Schlüssel(n) in Ihrem [!DNL Azure]-Schlüsseltresor ver- und entschlüsselt.

Weitere Informationen zur Datenverschlüsselung in Adobe Experience Platform finden Sie unter [Verschlüsselungsdokumentation](../../encryption.md).
