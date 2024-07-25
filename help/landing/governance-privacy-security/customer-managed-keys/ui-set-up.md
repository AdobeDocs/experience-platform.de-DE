---
title: Einrichten und Konfigurieren von kundenverwalteten Schlüsseln über die Platform-Benutzeroberfläche
description: Erfahren Sie, wie Sie Ihre CMK-App mit Ihrem Azure-Mandanten einrichten und Ihre Verschlüsselungsschlüssel-ID an Adobe Experience Platform senden.
exl-id: 5f38997a-66f3-4f9d-9c2f-fb70266ec0a6
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 20%

---

# Einrichten und Konfigurieren von kundenverwalteten Schlüsseln über die Platform-Benutzeroberfläche

In diesem Dokument wird der Prozess zum Aktivieren der Funktion für kundenverwaltete Schlüssel (CMK) in Platform mithilfe der Benutzeroberfläche beschrieben. Anweisungen zum Ausführen dieses Prozesses mithilfe der API finden Sie im Dokument [API CMK setup document](./api-set-up.md) .

## Voraussetzungen

Um den Abschnitt [!UICONTROL Verschlüsselung] in Adobe Experience Platform anzuzeigen und aufzurufen, müssen Sie eine Rolle erstellt und dieser Rolle die Berechtigung [!UICONTROL Kundenverwalteten Schlüssel verwalten] zugewiesen haben. Jeder Benutzer mit der Berechtigung [!UICONTROL Kunden-verwalteten Schlüssel verwalten] kann CMK für seine Organisation aktivieren.

Weiterführende Informationen zum Zuweisen von Rollen und Berechtigungen in Experience Platform finden Sie in der Dokumentation [Berechtigungen konfigurieren](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=de) .

Um CMK zu aktivieren, muss Ihr [[!DNL Azure] Key Vault](./azure-key-vault-config.md) mit den folgenden Einstellungen konfiguriert werden:

* [Bereinigungsschutz aktivieren](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Soft-Delete aktivieren](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Konfigurieren des Zugriffs mithilfe der rollenbasierten Zugriffskontrolle [!DNL Azure] 2}](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Konfigurieren eines [!DNL Azure] Schlüssel-Vault](./azure-key-vault-config.md)

## Einrichten der CMK-App {#register-app}

Nachdem Sie Ihren Key Vault konfiguriert haben, müssen Sie die CMK-Anwendung registrieren, die mit Ihrem [!DNL Azure] -Mandanten verknüpft wird.

### Erste Schritte

Um das Dashboard [!UICONTROL Verschlüsselungskonfigurationen] anzuzeigen, wählen Sie **[!UICONTROL Verschlüsselung]** unter der Überschrift [!UICONTROL Administration] in der linken Navigationsseitenleiste aus.

![Das Dashboard für die Verschlüsselungskonfiguration mit Verschlüsselung und die Karte vom Typ &quot;Kundenverwaltete Schlüssel&quot;sind hervorgehoben.](../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

Wählen Sie **[!UICONTROL Konfigurieren]** aus, um die Ansicht [!UICONTROL Konfiguration der vom Kunden verwalteten Schlüssel] zu öffnen. Dieser Arbeitsbereich enthält alle erforderlichen Werte, um die unten beschriebenen Schritte durchzuführen und die Integration mit Ihrem Azure Key-Vault durchzuführen.

### Authentifizierungs-URL kopieren {#copy-authentication-url}

Um den Registrierungsprozess zu starten, kopieren Sie die Authentifizierungs-URL der Anwendung für Ihr Unternehmen aus der Ansicht [!UICONTROL Konfiguration der kundenverwalteten Schlüssel] und fügen Sie sie in Ihre [!DNL Azure] Umgebung **[!DNL Key Vault Crypto Service Encryption User]** ein. Einzelheiten dazu, wie Sie [eine Rolle zuweisen](#assign-to-role), finden Sie im nächsten Abschnitt.

Wählen Sie das Kopiersymbol (![Kopiersymbol) aus.](/help/images/icons/copy.png)) durch die [!UICONTROL Anwendungsauthentifizierungsurl].

![ Die Ansicht [!UICONTROL Konfiguration der vom Kunden verwalteten Schlüssel] mit hervorgehobenem Abschnitt zur Anwendungsauthentifizierungsurl.](../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

Kopieren Sie die [!UICONTROL Application authentication url]-URL und fügen Sie sie in einen Browser ein, um ein Authentifizierungsdialogfeld zu öffnen. Wählen Sie **[!DNL Accept]** aus, um den Prinzipal des CMK-App-Service zu Ihrem [!DNL Azure] -Mandanten hinzuzufügen. Durch Bestätigung der Authentifizierung gelangen Sie zur Landingpage der Experience Cloud.

![Ein Dialogfeld mit einer Microsoft-Berechtigungsanfrage, in dem [!UICONTROL Accept] hervorgehoben ist.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>Wenn Sie mehrere [!DNL Microsoft Azure]-Abonnements haben, können Sie Ihre Platform-Instanz möglicherweise mit dem falschen Schlüsselwert verbinden. In diesem Fall müssen Sie den Abschnitt &quot;`common`&quot; des URL-Namens für die Anwendungsauthentifizierung gegen die Kennung des CMK-Ordners tauschen.<br>Kopieren Sie die Kennung des CMK-Ordners von der Seite &quot;Portal-Einstellungen, Verzeichnisse und Abonnements&quot;der Seite [!DNL Microsoft Azure] application<br>![ Die Seite &quot;[!DNL Microsoft Azure] Einstellungen, Verzeichnisse und Abonnements&quot;mit hervorgehobener Verzeichniskennung.](../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br>Fügen Sie ihn als Nächstes in Ihre Browser-Adressleiste ein.<br>![Eine Google-Browser-Seite mit dem Abschnitt &quot;common&quot;der Anwendungsauthentifizierungsurl ist hervorgehoben.](../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### Zuweisen der CMK-App zu einer Rolle {#assign-to-role}

Navigieren Sie nach Abschluss des Authentifizierungsprozesses zu Ihrem [!DNL Azure]-Schlüsseltresor und wählen Sie **[!DNL Access control]** in der linken Navigation aus. Wählen Sie von hier aus **[!DNL Add]** gefolgt von **[!DNL Add role assignment]** aus.

![ Das [!DNL Microsoft Azure] Dashboard mit [!DNL Add] und [!DNL Add role assignment] hervorgehoben.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

Im nächsten Bildschirm werden Sie aufgefordert, eine Rolle für diese Zuweisung auszuwählen. Wählen Sie **[!DNL Key Vault Crypto Service Encryption User]** aus, bevor Sie auf **[!DNL Next]** klicken, um fortzufahren.

>[!NOTE]
>
>Wenn Sie über die [!DNL Managed-HSM Key Vault]-Ebene verfügen, müssen Sie die **[!DNL Managed HSM Crypto Service Encryption User]**-Benutzerrolle auswählen.

![ Das Dashboard [!DNL Microsoft Azure] mit dem hervorgehobenen [!DNL Key Vault Crypto Service Encryption User].](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Wählen Sie auf dem nächsten Bildschirm **[!DNL Select members]** aus, um ein Dialogfeld in der rechten Leiste zu öffnen. Verwenden Sie die Suchleiste, um den Service-Prinzipal für das CMK-Programm zu suchen und ihn aus der Liste auszuwählen. Wenn Sie fertig sind, klicken Sie auf **[!DNL Save]**.

>[!NOTE]
>
>Wenn Sie Ihr Programm in der Liste nicht finden, wurde Ihr Service-Prinzipal in Ihrem Mandanten nicht akzeptiert. Wenden Sie sich an Ihren [!DNL Azure] -Administrator oder -Support-Mitarbeiter, um sicherzustellen, dass Sie über die richtigen Berechtigungen verfügen.

Sie können die Anwendung überprüfen, indem Sie die [!UICONTROL Anwendungs-ID] in der Ansicht [!UICONTROL Kundenverwaltete Schlüssel-Konfiguration] mit der in der Anwendungsübersicht [!DNL Microsoft Azure] angegebenen [!DNL Application ID] vergleichen.

![Die Ansicht [!UICONTROL Konfiguration der vom Kunden verwalteten Schlüssel] mit hervorgehobener [!UICONTROL Anwendungs-ID].](../../images/governance-privacy-security/customer-managed-keys/application-id.png)

Alle Details, die zur Überprüfung der Azure-Tools erforderlich sind, sind in der Benutzeroberfläche von Platform enthalten. Diese Granularität wird bereitgestellt, da viele Benutzer andere Azure-Tools verwenden möchten, um ihre Fähigkeit zur Überwachung und Protokollierung des Zugriffs auf diese Anwendungen auf ihre SchlüsselVault zu verbessern. Das Verständnis dieser Kennungen ist für diesen Zweck und die Unterstützung der Adobe-Dienste beim Zugriff auf den Schlüssel von entscheidender Bedeutung.

## Aktivieren der Konfiguration des Verschlüsselungsschlüssels auf Experience Platform {#send-to-adobe}

Nach der Installation der CMK-App in [!DNL Azure] können Sie Ihre Verschlüsselungsschlüssel-ID an Adobe senden. Wählen Sie in der linken Navigation **[!DNL Keys]** aus, gefolgt vom Namen des Schlüssels, den Sie senden möchten.

![Das Microsoft Azure-Dashboard mit dem Objekt [!DNL Keys] und dem Schlüsselnamen hervorgehoben.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Wählen Sie die neueste Version des Schlüssels aus, und seine Detailseite wird angezeigt. Von hier aus können Sie optional die zulässigen Vorgänge für den Schlüssel konfigurieren.

>[!IMPORTANT]
>
>Die für den Schlüssel mindestens erforderlichen Vorgänge sind die Berechtigungen **[!DNL Wrap Key]** und **[!DNL Unwrap Key]**. Sie können [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign] und [!DNL Verify] einbeziehen, falls Sie möchten.

Das Feld **[!UICONTROL Schlüsselkennung]** zeigt die URI-Kennung für den Schlüssel an. Kopieren Sie diesen URI-Wert zur Verwendung im nächsten Schritt.

![Die Schlüsseldetails des Microsoft Azure-Dashboards mit den Abschnitten [!DNL Permitted operations] und der URL-Schlüssel zum Kopieren wurden hervorgehoben.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Nachdem Sie den [!DNL Key vault URI] erhalten haben, kehren Sie zur Ansicht [!UICONTROL Konfiguration der vom Kunden verwalteten Schlüssel] zurück und geben Sie einen beschreibenden **[!UICONTROL Konfigurationsnamen]** ein. Fügen Sie als Nächstes die [!DNL Key Identifier] aus der Azure Key-Detailseite in die **[!UICONTROL Key vault key key identifier]** ein und wählen Sie **[!UICONTROL Save]**.

![ Die Ansicht [!UICONTROL Konfiguration der vom Kunden verwalteten Schlüssel] mit dem Abschnitt [!UICONTROL Konfigurationsname] und dem Abschnitt [!UICONTROL Schlüsselkennung der Vault-Schlüssel] wurde hervorgehoben.](../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

Sie werden zum Dashboard [!UICONTROL Verschlüsselungskonfigurationen] zurückgeleitet. Der Status der Konfiguration [!UICONTROL Vom Kunden verwaltete Schlüssel] wird als [!UICONTROL Verarbeitung] angezeigt.

![ Das Dashboard [!UICONTROL Verschlüsselungskonfigurationen] mit [!UICONTROL Verarbeitung], das auf der Karte [!UICONTROL Vom Kunden verwaltete Schlüssel] hervorgehoben ist.](../../images/governance-privacy-security/customer-managed-keys/processing.png)

## Überprüfen des Konfigurationsstatus {#check-status}

Warten Sie eine beträchtliche Zeit für die Verarbeitung. Um den Status der Konfiguration zu überprüfen, kehren Sie zur Ansicht [!UICONTROL Konfiguration der vom Kunden verwalteten Schlüssel] zurück und scrollen Sie nach unten zum Konfigurationsstatus [!UICONTROL 3}. ] Die Fortschrittsleiste wurde in Schritt 1 von drei überarbeitet und erklärt, dass das System prüft, ob Platform Zugriff auf den Schlüssel und den Schlüsselwert hat.

Es gibt vier potenzielle Status der CMK-Konfiguration. Diese sind wie folgt:

* Schritt 1: Validiert, dass Platform auf den Schlüssel und den Schlüssel zugreifen kann.
* Schritt 2: Der Schlüssel und der Schlüsselname werden derzeit allen Datenspeichern in Ihrer Organisation hinzugefügt.
* Schritt 3: Der Schlüssel und der Schlüsselname wurden den Datenspeichern erfolgreich hinzugefügt.
* `FAILED`: Es ist ein Problem aufgetreten, das in erster Linie mit dem Schlüssel, dem Schlüsseltresor oder der Einrichtung der Multi-Mandanten-App-zusammenhängt.

## Nächste Schritte

Durch Ausführung der oben genannten Schritte haben Sie CMK für Ihre Organisation erfolgreich aktiviert. Daten, die in Primärdatenspeicher erfasst werden, werden jetzt mit den Schlüsseln in Ihrem [!DNL Azure] Key Vault verschlüsselt und entschlüsselt.
