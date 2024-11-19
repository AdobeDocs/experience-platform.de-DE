---
title: Konfigurieren eines Azure Key Vault
description: Erfahren Sie, wie Sie mit Azure ein neues Unternehmenskonto erstellen oder ein vorhandenes Unternehmenskonto verwenden und das Key Vault erstellen.
role: Developer
feature: Privacy
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 24%

---

# Konfigurieren eines [!DNL Azure]-Schlüsseltresors

Vom Kunden verwaltete Schlüssel (CMK) unterstützen nur Schlüssel aus einem [!DNL Microsoft Azure] Key Vault. Zunächst müssen Sie mit [!DNL Azure] arbeiten, um ein neues Unternehmenskonto zu erstellen, oder Sie müssen ein vorhandenes Unternehmenskonto verwenden und die folgenden Schritte ausführen, um das Key Vault zu erstellen.

>[!IMPORTANT]
>
>Es werden nur die Ebenen Standard, Premium und Managed HSM für [!DNL Azure] Key Vault unterstützt. [!DNL Azure Dedicated HSM] und [!DNL Azure Payments HSM] werden nicht unterstützt. Siehe die [[!DNL Azure] Dokumentation](https://learn.microsoft.com/de-de/azure/security/fundamentals/key-management#azure-key-management-services) für weitere Informationen über angebotene Schlüsselverwaltungsdienste.

>[!NOTE]
>
>Die folgende Dokumentation behandelt nur die grundlegenden Schritte zum Erstellen des Key Vault. Außerhalb dieser Anleitung sollten Sie den Key Vault gemäß den Richtlinien Ihres Unternehmens konfigurieren.

Melden Sie sich beim [!DNL Azure]-Portal an und suchen Sie mithilfe der Suchleiste unter der Liste der Dienste nach **[!DNL Key vaults]**.

![Die Suchfunktion in [!DNL Microsoft Azure], wobei [!DNL Key vaults] in den Suchergebnissen hervorgehoben ist.](../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

Die **[!DNL Key vaults]**-Seite wird angezeigt, nachdem Sie den Dienst ausgewählt haben. Klicken Sie von hier aus auf **[!DNL Create]**.

![ Das Dashboard [!DNL Key vaults] in [!DNL Microsoft Azure] mit hervorgehobenem [!DNL Create] Dashboard.](../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Füllen Sie mithilfe des bereitgestellten Formulars die grundlegenden Details für das Key Vault aus, einschließlich eines Namens und einer zugewiesenen Ressourcengruppe.

>[!WARNING]
>
>Die meisten Optionen können als Standardwerte beibehalten werden. **Stellen Sie sicher, dass Sie die Schutzoptionen für Soft-Löschen und Bereinigen aktivieren**. Wenn Sie diese Funktionen nicht aktivieren, riskieren Sie, den Zugriff auf Ihre Daten zu verlieren, wenn das Key Vault gelöscht wird.
>
>![Der Workflow [!DNL Microsoft Azure] [!DNL Create a Key Vault] mit hervorgehobenem Schutz zum weichen Löschen und Löschen.](../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

Fahren Sie von hier aus mit dem Workflow zur Erstellung von Key Vault fort und konfigurieren Sie die verschiedenen Optionen entsprechend den Richtlinien Ihres Unternehmens.

Sobald Sie den Schritt &quot;**[!DNL Review + create]**&quot;erreicht haben, können Sie die Details des Key Vault überprüfen, während er die Validierung durchläuft. Nachdem die Validierung erfolgreich abgeschlossen wurde, klicken Sie auf **[!DNL Create]**, um den Prozess abzuschließen.

![Die Microsoft Azure Key-Werte Überprüfen und erstellen Sie eine Seite mit hervorgehobenem Erstellen.](../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Zugriff konfigurieren {#configure-access}

Aktivieren Sie als Nächstes die rollenbasierte Azure-Zugriffskontrolle für Ihren Key Vault. Wählen Sie **[!DNL Access configuration]** im Abschnitt [!DNL Settings] der linken Navigation und dann **[!DNL Azure role-based access control]** aus, um die Einstellung zu aktivieren. Dieser Schritt ist unbedingt erforderlich, da die CMK-App später mit einer Azure-Rolle verknüpft werden muss. Das Zuweisen einer Rolle wird sowohl in den Workflows [API](./api-set-up.md#assign-to-role) als auch [UI](./ui-set-up.md#assign-to-role) dokumentiert.

![ Das [!DNL Microsoft Azure] Dashboard mit [!DNL Access configuration] und [!DNL Azure role-based access control] hervorgehoben.](../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## Konfigurieren von Netzwerkoptionen {#configure-network-options}

Wenn Ihr Key Vault so konfiguriert ist, dass der öffentliche Zugriff auf bestimmte virtuelle Netzwerke eingeschränkt oder der öffentliche Zugriff vollständig deaktiviert wird, müssen Sie [!DNL Microsoft] eine Firewall-Ausnahme gewähren.

Wählen Sie **[!DNL Networking]** in der linken Navigation aus. Markieren Sie unter **[!DNL Firewalls and virtual networks]** das Kontrollkästchen **[!DNL Allow trusted Microsoft services to bypass this firewall]** und klicken Sie dann auf **[!DNL Apply]**.

![Die Registerkarte [!DNL Networking] von [!DNL Microsoft Azure] mit der Ausnahme [!DNL Networking] und [!DNL Allow trusted Microsoft surfaces to bypass this firewall], die hervorgehoben sind.](../../images/governance-privacy-security/customer-managed-keys/networking.png)

### Generieren eines Schlüssels {#generate-a-key}

Nachdem Sie ein Key Vault erstellt haben, können Sie einen neuen Schlüssel generieren. Navigieren Sie zur Registerkarte **[!DNL Keys]** und wählen Sie **[!DNL Generate/Import]** aus.

![ Die Registerkarte [!DNL Keys] von [!DNL Azure] mit der Markierung [!DNL Generate import].](../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Verwenden Sie das bereitgestellte Formular, um einen Namen für den Schlüssel anzugeben, und wählen Sie für den Schlüsseltyp entweder **RSA** oder **RSA-HSM** aus. Mindestens der **[!DNL RSA key size]** muss mindestens **3072** Bit betragen, wie es für [!DNL Cosmos DB] erforderlich ist. [!DNL Azure Data Lake Storage] ist auch mit RSA 3027 kompatibel.

>[!NOTE]
>
>Merken Sie sich den Namen, den Sie für den Schlüssel angeben, da der Schlüssel an Adobe gesendet werden muss.

Verwenden Sie die restlichen Steuerelemente, um den Schlüssel zu konfigurieren, den Sie erstellen oder importieren möchten. Wenn Sie fertig sind, wählen Sie **[!DNL Create]** aus.

![ Das Dashboard [!DNL Create a key] mit [!DNL 3072] Bit hervorgehoben.](../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

Der konfigurierte Schlüssel wird in der Liste der Schlüssel für den Tresor angezeigt.

![ Der Arbeitsbereich [!DNL Keys] mit hervorgehobenem Schlüsselnamen.](../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Nächste Schritte

Um den einmaligen Prozess zum Einrichten der Funktion für kundenverwaltete Schlüssel fortzusetzen, fahren Sie entweder mit den Handbüchern zur Einrichtung von [API](./api-set-up.md) oder [UI](./ui-set-up.md) kundenverwalteten Schlüsseln fort.
