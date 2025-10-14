---
title: Konfigurieren eines Azure-Schlüsseltresors für kundenverwaltete Schlüssel
description: Erfahren Sie, wie Sie mit Azure ein neues Unternehmenskonto erstellen oder ein vorhandenes Unternehmenskonto verwenden und den Schlüsseltresor erstellen.
role: Developer
feature: Privacy
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: c920f78363ee5f040964dbd3a0d0815474094b07
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 19%

---

# Konfigurieren eines [!DNL Azure] Schlüsseltresors für kundenverwaltete Schlüssel

Kundenseitig verwaltete Schlüssel (CMK) unterstützen Schlüssel von [!DNL Microsoft Azure] Key Vaults und AWS [!DNL Key Management Service (KMS)]. Wenn Ihre Implementierung auf [!DNL Azure] gehostet wird, führen Sie die folgenden Schritte aus, um einen Schlüsseltresor zu erstellen. Informationen zu von AWS gehosteten Implementierungen finden Sie im [AWS KMS-Konfigurationshandbuch](../aws/configure-kms.md).

>[!IMPORTANT]
>
>Nur die Ebenen Standard, Premium und Managed HSM für [!DNL Azure] Schlüsseltresor werden unterstützt. [!DNL Azure Dedicated HSM] und [!DNL Azure Payments HSM] werden nicht unterstützt. Siehe die [[!DNL Azure] Dokumentation](https://learn.microsoft.com/de-de/azure/security/fundamentals/key-management#azure-key-management-services) für weitere Informationen über angebotene Schlüsselverwaltungsdienste.

>[!NOTE]
>
>Die folgende Dokumentation behandelt nur die grundlegenden Schritte zum Erstellen des Schlüsseltresors. Außerhalb dieser Anleitung sollten Sie den Schlüsseltresor gemäß den Richtlinien Ihrer Organisation konfigurieren.

Melden Sie sich beim [!DNL Azure]-Portal an und suchen Sie mithilfe der Suchleiste unter der Liste der Dienste nach **[!DNL Key vaults]**.

![Die Suchfunktion in [!DNL Microsoft Azure] mit hervorgehobenen [!DNL Key vaults] in den Suchergebnissen.](../../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

Die **[!DNL Key vaults]**-Seite wird angezeigt, nachdem Sie den Dienst ausgewählt haben. Klicken Sie von hier aus auf **[!DNL Create]**.

![Das [!DNL Key vaults]-Dashboard in [!DNL Microsoft Azure] mit hervorgehobener [!DNL Create].](../../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Füllen Sie mithilfe des bereitgestellten Formulars die grundlegenden Details für den Schlüsseltresor aus, einschließlich eines Namens und einer zugewiesenen Ressourcengruppe.

>[!WARNING]
>
>Die meisten Optionen können als Standardwerte beibehalten werden. **Stellen Sie sicher, dass Sie die Schutzoptionen für Soft-Löschen und Bereinigen aktivieren**. Wenn Sie diese Funktionen nicht aktivieren, riskieren Sie, den Zugriff auf Ihre Daten zu verlieren, wenn der Schlüsseltresor gelöscht wird.
>
>![Der [!DNL Microsoft Azure] [!DNL Create a Key Vault]-Workflow mit hervorgehobenem Schutz für Soft-Löschen und Bereinigen.](../../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

Fahren Sie von hier aus mit dem Workflow zur Erstellung des Schlüsseltresors fort und konfigurieren Sie die verschiedenen Optionen entsprechend den Richtlinien Ihrer Organisation.

Wenn Sie beim **[!DNL Review + create]** Schritt ankommen, können Sie die Details des Schlüsseltresors während der Validierung überprüfen. Nachdem die Validierung erfolgreich abgeschlossen wurde, klicken Sie auf **[!DNL Create]**, um den Prozess abzuschließen.

![Die Microsoft Azure-Schlüsseltresore „Überprüfen und Erstellen“ mit hervorgehobener Option „Erstellen“.](../../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Zugriff konfigurieren {#configure-access}

Aktivieren Sie als Nächstes die rollenbasierte Zugriffssteuerung für Azure für Ihren Schlüsseltresor. Wählen Sie **[!DNL Access configuration]** im [!DNL Settings] Abschnitt des linken Navigationsbereichs und dann **[!DNL Azure role-based access control]** aus, um die Einstellung zu aktivieren. Dieser Schritt ist wichtig, da die CMK-App später mit einer Azure-Rolle verknüpft werden muss. Die Zuweisung einer Rolle ist in den Workflows [API](./api-set-up.md#assign-to-role) und [UI](./ui-set-up.md#assign-to-role) dokumentiert.

![Das [!DNL Microsoft Azure]-Dashboard mit hervorgehobenen [!DNL Access configuration] und [!DNL Azure role-based access control].](../../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## Konfigurieren von Netzwerkoptionen {#configure-network-options}

Wenn Ihr Schlüsseltresor so konfiguriert ist, dass der öffentliche Zugriff auf bestimmte virtuelle Netzwerke eingeschränkt oder der öffentliche Zugriff vollständig deaktiviert wird, müssen Sie [!DNL Microsoft] eine Firewall-Ausnahme gewähren.

Wählen Sie **[!DNL Networking]** in der linken Navigation aus. Markieren Sie unter **[!DNL Firewalls and virtual networks]** das Kontrollkästchen **[!DNL Allow trusted Microsoft services to bypass this firewall]** und klicken Sie dann auf **[!DNL Apply]**.

>[!NOTE]
>
>Wenn Ihr Schlüsseltresor eingeschränkten Netzwerkzugriff verwendet, empfiehlt Adobe, die folgende statische IP-Adresse hinzuzufügen: `20.88.123.53`. Durch Hinzufügen dieser IP-Adresse können Adobe-Services die Konnektivität effektiver überwachen und plattforminterne Warnhinweise bereitstellen, wenn Zugriffsprobleme erkannt werden.
>
>Weitere Informationen dazu, wann die IP-Adresse von Adobe auf die Zulassungsliste gesetzt wird, wie Warnhinweise funktionieren und wie auf Benachrichtigungen zu wichtigen Zugriffsfehlern reagiert werden kann, finden Sie unter [Konfigurieren von Warnhinweisen und IP-Zugriff für Azure CMK](./alerts-and-ip-access.md).
>
>Wenn Ihr Schlüsseltresor bereits so konfiguriert ist, dass er den Zugriff auf ein öffentliches Netzwerk zulässt, sind keine weiteren Maßnahmen erforderlich.

![Die Registerkarte &quot;[!DNL Networking]&quot; von [!DNL Microsoft Azure] mit Hervorhebung von [!DNL Networking] und [!DNL Allow trusted Microsoft surfaces to bypass this firewall] Ausnahme.](../../../images/governance-privacy-security/customer-managed-keys/networking.png)

### Generieren eines Schlüssels {#generate-a-key}

Nachdem Sie einen Schlüsseltresor erstellt haben, können Sie einen neuen Schlüssel generieren. Navigieren Sie zur Registerkarte **[!DNL Keys]** und wählen Sie **[!DNL Generate/Import]** aus.

![Die Registerkarte &quot;[!DNL Keys]&quot; von [!DNL Azure] mit hervorgehobener [!DNL Generate import].](../../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Geben Sie in dem bereitgestellten Formular einen Namen für den Schlüssel ein und wählen Sie entweder **RSA** oder **RSA-HSM** für den Schlüsseltyp aus. Bei [!DNL Azure] gehosteten Implementierungen muss der **[!DNL RSA key size]** mindestens **3072** Bit betragen, wie für [!DNL Azure Cosmos DB] erforderlich. [!DNL Azure Data Lake Storage] ist auch mit RSA 3027 kompatibel.

>[!NOTE]
>
>Merken Sie sich den Namen, den Sie für den Schlüssel angeben, da er erforderlich ist, um den Schlüssel an Adobe zu senden.

Verwenden Sie die restlichen Steuerelemente, um den Schlüssel zu konfigurieren, den Sie erstellen oder importieren möchten. Wenn Sie fertig sind, wählen Sie **[!DNL Create]** aus.

![Das [!DNL Create a key]-Dashboard mit hervorgehobenen [!DNL 3072] Bits.](../../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

Der konfigurierte Schlüssel wird in der Liste der Schlüssel für den Tresor angezeigt.

![Der [!DNL Keys] Arbeitsbereich mit hervorgehobenem Schlüsselnamen.](../../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Nächste Schritte

Um den einmaligen Prozess zum Einrichten der Funktion für kundenseitig verwaltete Schlüssel fortzusetzen, folgen Sie den Einrichtungshandbüchern für die Hosting-Umgebung Ihrer Plattform:

- Verwenden Sie [!DNL Azure] die Einrichtungshandbücher für [API](./api-set-up.md) oder [UI](./ui-set-up.md).
- Informationen zu AWS finden Sie im [Handbuch zur AWS-Konfiguration &#x200B;](../aws/configure-kms.md) KMS und im [Einrichtungshandbuch für die Benutzeroberfläche](../aws/ui-set-up.md).
