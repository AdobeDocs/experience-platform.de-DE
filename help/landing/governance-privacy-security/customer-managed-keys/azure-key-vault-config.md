---
title: Konfigurieren eines Azure Key Vault
description: Erfahren Sie, wie Sie mit Azure ein neues Unternehmenskonto erstellen oder ein vorhandenes Unternehmenskonto verwenden und das Key Vault erstellen.
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: 4f08e8fcc8d53b981af60226f1397a1d1ac4d8dc
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 24%

---

# Konfigurieren eines [!DNL Azure]-Schlüsseltresors

Vom Kunden verwaltete Schlüssel (CMK) unterstützen nur Schlüssel aus einem [!DNL Microsoft Azure] Key Vault. Zunächst müssen Sie mit [!DNL Azure] , um ein neues Unternehmenskonto zu erstellen oder ein vorhandenes Unternehmenskonto zu verwenden, und führen Sie die folgenden Schritte aus, um das Key Vault zu erstellen.

>[!IMPORTANT]
>
>Nur die Ebenen Standard, Premium und Managed HSM für [!DNL Azure] Key Vault wird unterstützt. [!DNL Azure Dedicated HSM] und [!DNL Azure Payments HSM] werden nicht unterstützt. Siehe die [[!DNL Azure] Dokumentation](https://learn.microsoft.com/de-de/azure/security/fundamentals/key-management#azure-key-management-services) für weitere Informationen über angebotene Schlüsselverwaltungsdienste.

>[!NOTE]
>
>Die folgende Dokumentation behandelt nur die grundlegenden Schritte zum Erstellen des Key Vault. Außerhalb dieser Anleitung sollten Sie den Key Vault gemäß den Richtlinien Ihres Unternehmens konfigurieren.

Melden Sie sich beim [!DNL Azure]-Portal an und suchen Sie mithilfe der Suchleiste unter der Liste der Dienste nach **[!DNL Key vaults]**.

![Die Suchfunktion in [!DNL Microsoft Azure] mit [!DNL Key vaults] in den Suchergebnissen hervorgehoben werden.](../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

Die **[!DNL Key vaults]**-Seite wird angezeigt, nachdem Sie den Dienst ausgewählt haben. Klicken Sie von hier aus auf **[!DNL Create]**.

![Die [!DNL Key vaults] Dashboard in [!DNL Microsoft Azure] mit [!DNL Create] hervorgehoben.](../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Füllen Sie mithilfe des bereitgestellten Formulars die grundlegenden Details für das Key Vault aus, einschließlich eines Namens und einer zugewiesenen Ressourcengruppe.

>[!WARNING]
>
>Die meisten Optionen können als Standardwerte beibehalten werden. **Stellen Sie sicher, dass Sie die Schutzoptionen für Soft-Löschen und Bereinigen aktivieren**. Wenn Sie diese Funktionen nicht aktivieren, riskieren Sie, den Zugriff auf Ihre Daten zu verlieren, wenn das Key Vault gelöscht wird.
>
>![Die [!DNL Microsoft Azure] [!DNL Create a Key Vault] Workflow mit hervorgehobenem Schutz gegen Softlöschung und Bereinigung.](../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

Fahren Sie von hier aus mit dem Workflow zur Erstellung von Key Vault fort und konfigurieren Sie die verschiedenen Optionen entsprechend den Richtlinien Ihres Unternehmens.

Sobald Sie bei der **[!DNL Review + create]** Schritt, können Sie die Details des Key Vault während der Validierung überprüfen. Nachdem die Validierung erfolgreich abgeschlossen wurde, klicken Sie auf **[!DNL Create]**, um den Prozess abzuschließen.

![Die Microsoft Azure Key-Werte Überprüfen und erstellen Seite mit hervorgehobenem Erstellen.](../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Zugriff konfigurieren {#configure-access}

Aktivieren Sie als Nächstes die rollenbasierte Azure-Zugriffskontrolle für Ihren Key Vault. Auswählen **[!DNL Access configuration]** im [!DNL Settings] im linken Navigationsbereich und wählen Sie **[!DNL Azure role-based access control]** , um die Einstellung zu aktivieren. Dieser Schritt ist unbedingt erforderlich, da die CMK-App später mit einer Azure-Rolle verknüpft werden muss. Das Zuweisen einer Rolle wird in beiden [API](./api-set-up.md#assign-to-role) und [Benutzeroberfläche](./ui-set-up.md#assign-to-role) Workflows.

![Die [!DNL Microsoft Azure] Dashboard mit [!DNL Access configuration] und [!DNL Azure role-based access control] hervorgehoben.](../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## Konfigurieren von Netzwerkoptionen {#configure-network-options}

Wenn Ihr Key Vault so konfiguriert ist, dass der öffentliche Zugriff auf bestimmte virtuelle Netzwerke eingeschränkt oder der öffentliche Zugriff vollständig deaktiviert wird, müssen Sie [!DNL Microsoft] eine Firewall-Ausnahme.

Wählen Sie **[!DNL Networking]** in der linken Navigation aus. Markieren Sie unter **[!DNL Firewalls and virtual networks]** das Kontrollkästchen **[!DNL Allow trusted Microsoft services to bypass this firewall]** und klicken Sie dann auf **[!DNL Apply]**.

![Die [!DNL Networking] Tab von [!DNL Microsoft Azure] mit [!DNL Networking] und [!DNL Allow trusted Microsoft surfaces to bypass this firewall] Ausnahmefehler hervorgehoben.](../../images/governance-privacy-security/customer-managed-keys/networking.png)

### Generieren eines Schlüssels {#generate-a-key}

Nachdem Sie ein Key Vault erstellt haben, können Sie einen neuen Schlüssel generieren. Navigieren Sie zur Registerkarte **[!DNL Keys]** und wählen Sie **[!DNL Generate/Import]** aus.

![Die [!DNL Keys] Tab von [!DNL Azure] mit [!DNL Generate import] hervorgehoben.](../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Verwenden Sie das bereitgestellte Formular, um einen Namen für den Schlüssel anzugeben, und wählen Sie entweder **RSA** oder **RSA-HSM** für den Schlüsseltyp. Mindestens die Variable **[!DNL RSA key size]** darf nicht kleiner sein als **3072** Bits nach Bedarf von [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] ist auch mit RSA 3027 kompatibel.

>[!NOTE]
>
>Merken Sie sich den Namen, den Sie für den Schlüssel angeben, da der Schlüssel an Adobe gesendet werden muss.

Verwenden Sie die restlichen Steuerelemente, um den Schlüssel zu konfigurieren, den Sie erstellen oder importieren möchten. Wenn Sie fertig sind, wählen Sie **[!DNL Create]** aus.

![Die [!DNL Create a key] Dashboard mit [!DNL 3072] hervorgehobene Bit.](../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

Der konfigurierte Schlüssel wird in der Liste der Schlüssel für den Tresor angezeigt.

![Die [!DNL Keys] Arbeitsbereich mit hervorgehobenem Schlüsselnamen.](../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Nächste Schritte

Um den einmaligen Prozess zum Einrichten der Funktion für kundenverwaltete Schlüssel fortzusetzen, fahren Sie mit dem [API](./api-set-up.md) oder [Benutzeroberfläche](./ui-set-up.md) Benutzerhandbücher zur Einrichtung von kundenverwalteten Schlüsseln.
