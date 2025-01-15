---
title: Einrichten und Konfigurieren von kundenverwalteten Schlüsseln für Azure mithilfe der Platform-Benutzeroberfläche
description: Erfahren Sie, wie Sie Ihre CMK-App mit Ihrem Azure-Mandanten einrichten und Ihre Verschlüsselungsschlüssel-ID an Adobe Experience Platform senden.
role: Developer
feature: Privacy
exl-id: 5f38997a-66f3-4f9d-9c2f-fb70266ec0a6
source-git-commit: 58bc7a650ff58f877550fa8838c6f8e2908f0090
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 18%

---

# Einrichten und Konfigurieren von kundenverwalteten Schlüsseln für Azure mithilfe der Platform-Benutzeroberfläche

In diesem Dokument werden die Azure-spezifischen Anweisungen zum Aktivieren der CMK-Funktion (Customer Managed Keys) in Platform mithilfe der Benutzeroberfläche behandelt. Spezifische Anweisungen für AWS finden Sie im [AWS-Setup-Handbuch](../aws/ui-set-up.md).

Anweisungen, wie Sie diesen Prozess für von Azure gehostete Platform-Instanzen mithilfe der API abschließen, finden Sie im Dokument [API CMK-Einrichtung](./api-set-up.md).

## Voraussetzungen

Um den Abschnitt [!UICONTROL Verschlüsselung] in Adobe Experience Platform anzuzeigen, müssen Sie eine Rolle erstellt und dieser Rolle die Berechtigung [!UICONTROL Kundenverwalteten Schlüssel verwalten] zugewiesen haben. Jeder Benutzer, der über die Berechtigung [!UICONTROL Kundenverwalteten Schlüssel verwalten] verfügt, kann für seine Organisation CMK aktivieren.

Weitere Informationen zur Zuweisung von Rollen und Berechtigungen in Experience Platform finden Sie in der [Dokumentation zu Berechtigungen konfigurieren](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=de).

Um CMK zu aktivieren[[!DNL Azure]  muss Ihr Schlüsseltresor mit ](./azure-key-vault-config.md) Einstellungen konfiguriert werden:

* [Bereinigungsschutz aktivieren](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Soft-Delete aktivieren](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Konfigurieren des Zugriffs mithilfe  [!DNL Azure]  rollenbasierten Zugriffssteuerung](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Konfigurieren  [!DNL Azure]  Schlüsseltresors](./azure-key-vault-config.md)

## Einrichten der CMK-App {#register-app}

Nachdem Sie Ihren Schlüsseltresor konfiguriert haben, müssen Sie das CMK-Programm registrieren, das sich mit Ihrem [!DNL Azure]-Mandanten verbindet.

### Erste Schritte

Um das Dashboard [!UICONTROL Verschlüsselungskonfigurationen] anzuzeigen, wählen Sie **[!UICONTROL Verschlüsselung]** unter der Überschrift [!UICONTROL Administration] in der linken Navigationsseitenleiste aus.

![Das Dashboard für die Verschlüsselungskonfiguration mit hervorgehobener Karte „Verschlüsselung“ und „Kundenseitig verwaltete Schlüssel“.](../../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

Wählen Sie **[!UICONTROL Konfigurieren]** aus, um die Ansicht [!UICONTROL Konfiguration kundenverwalteter Schlüssel] zu öffnen. Dieser Arbeitsbereich enthält alle erforderlichen Werte, um die unten beschriebenen Schritte auszuführen und die Integration mit Ihrem Azure-Schlüsseltresor durchzuführen.

### Authentifizierungs-URL kopieren {#copy-authentication-url}

Um den Registrierungsprozess zu starten, kopieren Sie die Anwendungsauthentifizierungs-URL für Ihre Organisation aus der Konfiguration [!UICONTROL Kundenseitig verwaltete Schlüssel] und fügen Sie sie in die **[!DNL Key Vault Crypto Service Encryption User]** Ihrer [!DNL Azure] ein. Details zum [Zuweisen einer Rolle](#assign-to-role) finden Sie im nächsten Abschnitt.

Wählen Sie das Kopiersymbol (![Das Kopiersymbol.](../../../../images/icons/copy.png)) durch die [!UICONTROL Anwendungsauthentifizierungs-URL].

![Die Ansicht [!UICONTROL Konfiguration von kundenseitig verwalteten Schlüsseln] mit hervorgehobenem Abschnitt „URL für die Anwendungsauthentifizierung“](../../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

Kopieren Sie die [!UICONTROL Anwendungsauthentifizierungs-URL] und fügen Sie sie in einen Browser ein, um ein Authentifizierungsdialogfeld zu öffnen. Wählen Sie **[!DNL Accept]** aus, um den Service-Prinzipal der CMK-App zu Ihrem [!DNL Azure] hinzuzufügen. Durch Bestätigen der Authentifizierung werden Sie zur Experience Cloud-Landingpage weitergeleitet.

![Dialogfeld für Microsoft-Berechtigungsanfragen mit hervorgehobener [!UICONTROL Akzeptieren]-Option.](../../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>Wenn Sie über mehrere [!DNL Microsoft Azure]-Abonnements verfügen, können Sie Ihre Platform-Instanz möglicherweise mit dem falschen Schlüsseltresor verbinden. In diesem Fall müssen Sie den `common` Abschnitt des URL-Namens für die Anwendungsauthentifizierung durch die CMK-Verzeichnis-ID ersetzen.<br>Kopieren Sie die CMK-Verzeichnis-ID aus der Seite „Portaleinstellungen“, „Verzeichnisse“ und „Abonnements“ der [!DNL Microsoft Azure]-Anwendung<br>![ Die Seite &quot;[!DNL Microsoft Azure]-Anwendungsportaleinstellungen“, „Verzeichnisse und Abonnements“ mit hervorgehobener Verzeichnis-ID.](../../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br>Fügen Sie es als Nächstes in die Adressleiste Ihres Browsers ein.<br>![Eine Google-Browser-Seite mit hervorgehobenem Abschnitt „Allgemein“ der Anwendungsauthentifizierungs-URL.](../../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### Zuweisen der CMK-App zu einer Rolle {#assign-to-role}

Navigieren Sie nach Abschluss des Authentifizierungsprozesses zu Ihrem [!DNL Azure]-Schlüsseltresor und wählen Sie **[!DNL Access control]** in der linken Navigation aus. Wählen Sie von hier aus **[!DNL Add]** gefolgt von **[!DNL Add role assignment]** aus.

![Das [!DNL Microsoft Azure]-Dashboard mit hervorgehobenen [!DNL Add] und [!DNL Add role assignment].](../../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

Im nächsten Bildschirm werden Sie aufgefordert, eine Rolle für diese Zuweisung auszuwählen. Wählen Sie **[!DNL Key Vault Crypto Service Encryption User]** aus, bevor Sie auf **[!DNL Next]** klicken, um fortzufahren.

>[!NOTE]
>
>Wenn Sie über die [!DNL Managed-HSM Key Vault] verfügen, müssen Sie die **[!DNL Managed HSM Crypto Service Encryption User]** Benutzerrolle auswählen.

![Das [!DNL Microsoft Azure]-Dashboard mit hervorgehobenem [!DNL Key Vault Crypto Service Encryption User].](../../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Wählen Sie auf dem nächsten Bildschirm **[!DNL Select members]** aus, um ein Dialogfeld in der rechten Leiste zu öffnen. Verwenden Sie die Suchleiste, um den Service-Prinzipal für das CMK-Programm zu suchen und ihn aus der Liste auszuwählen. Wenn Sie fertig sind, klicken Sie auf **[!DNL Save]**.

>[!NOTE]
>
>Wenn Sie Ihr Programm in der Liste nicht finden, wurde Ihr Service-Prinzipal in Ihrem Mandanten nicht akzeptiert. Um sicherzustellen, dass Sie über die richtigen Berechtigungen verfügen, wenden Sie sich an Ihren [!DNL Azure] oder Vertreter.

Sie können die Anwendung überprüfen, indem Sie die [!UICONTROL Anwendungs-ID] in der Ansicht [!UICONTROL Konfiguration von kundenseitig verwalteten Schlüsseln] mit den [!DNL Application ID] in der [!DNL Microsoft Azure] Anwendungsübersicht vergleichen.

![Die [!UICONTROL Konfiguration für kundenseitig verwaltete Schlüssel] mit der hervorgehobenen [!UICONTROL Anwendungs-ID].](../../../images/governance-privacy-security/customer-managed-keys/application-id.png)

Alle Details, die zur Überprüfung der Azure-Tools erforderlich sind, sind in der Platform-Benutzeroberfläche enthalten. Diese Granularität wird bereitgestellt, da viele Benutzer andere Azure-Tools verwenden möchten, um ihre Fähigkeit zu verbessern, diese Anwendungen beim Zugriff auf ihren Schlüsseltresor zu überwachen und zu protokollieren. Das Verständnis dieser Kennungen ist für diesen Zweck und für den Zugriff der Adobe-Services auf den Schlüssel von entscheidender Bedeutung.

## Aktivieren der Konfiguration des Verschlüsselungsschlüssels auf Experience Platform {#send-to-adobe}

Nach der Installation der CMK-App in [!DNL Azure] können Sie Ihre Verschlüsselungsschlüssel-ID an Adobe senden. Wählen Sie in der linken Navigation **[!DNL Keys]** aus, gefolgt vom Namen des Schlüssels, den Sie senden möchten.

![Das Microsoft Azure-Dashboard mit dem hervorgehobenen [!DNL Keys] und dem hervorgehobenen Schlüsselnamen.](../../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Wählen Sie die neueste Version des Schlüssels aus, und seine Detailseite wird angezeigt. Von hier aus können Sie optional die zulässigen Vorgänge für den Schlüssel konfigurieren.

>[!IMPORTANT]
>
>Die minimal zulässigen Vorgänge für den Schlüssel sind die Berechtigungen **[!DNL Wrap Key]** und **[!DNL Unwrap Key]** . Sie können bei Bedarf [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign] und [!DNL Verify] einbeziehen.

Das Feld **[!UICONTROL Schlüsselkennung]** zeigt die URI-Kennung für den Schlüssel an. Kopieren Sie diesen URI-Wert zur Verwendung im nächsten Schritt.

![Die Details zum Microsoft Azure-Dashboard-Schlüssel mit den hervorgehobenen Abschnitten &quot;[!DNL Permitted operations]&quot; und „URL des Kopierschlüssels“.](../../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Nachdem Sie die [!DNL Key vault URI] erhalten haben, kehren Sie zur Ansicht [!UICONTROL Konfiguration von kundenseitig verwalteten Schlüsseln] zurück und geben Sie einen beschreibenden **[!UICONTROL Konfigurationsnamen]** ein. Fügen Sie als Nächstes die [!DNL Key Identifier] aus der Detailseite Azure-Schlüssel zur **[!UICONTROL Schlüsseltresorschlüsselkennung“ hinzu]** wählen Sie **[!UICONTROL Speichern]**.

![Die [!UICONTROL Konfiguration für kundenseitig verwaltete Schlüssel] mit den hervorgehobenen Abschnitten [!UICONTROL Konfigurationsname] und [!UICONTROL Schlüsseltresorschlüsselkennung].](../../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

Sie gelangen zurück zum [!UICONTROL Dashboard der Verschlüsselungskonfigurationen]. Der Status der Konfiguration [!UICONTROL Kundenseitig verwaltete Schlüssel] wird als &quot;[!UICONTROL &quot; ].

![Das Dashboard [!UICONTROL Verschlüsselungskonfigurationen] mit hervorgehobener [!UICONTROL Verarbeitung] auf der Karte [!UICONTROL Kundenseitig verwaltete Schlüssel].](../../../images/governance-privacy-security/customer-managed-keys/processing.png)

## Überprüfen des Konfigurationsstatus {#check-status}

Lassen Sie der Verarbeitung viel Zeit. Um den Status der Konfiguration zu überprüfen, kehren Sie zur Konfiguration [!UICONTROL Kundenseitig verwaltete Schlüssel] zurück und scrollen Sie nach unten zum [!UICONTROL Konfigurationsstatus]. Die Fortschrittsleiste wurde auf Schritt eins von drei erweitert und erklärt, dass das System überprüft, ob Platform Zugriff auf den Schlüssel und den Schlüsseltresor hat.

Es gibt vier potenzielle Status der CMK-Konfiguration. Diese sind wie folgt:

* Schritt 1: Überprüft, ob Platform Zugriff auf den Schlüssel und den Schlüsseltresor hat.
* Schritt 2: Der Schlüsseltresor und der Schlüsselname werden derzeit zu allen Datenspeichern in Ihrer Organisation hinzugefügt.
* Schritt 3: Der Schlüsseltresor und der Schlüsselname wurden erfolgreich zu den Datenspeichern hinzugefügt.
* `FAILED`: Es ist ein Problem aufgetreten, das in erster Linie mit dem Schlüssel, dem Schlüsseltresor oder der Einrichtung der Multi-Mandanten-App-zusammenhängt.

## Nächste Schritte

Durch Abschluss der oben genannten Schritte haben Sie CMK für Ihre von Azure gehostete Organisation erfolgreich aktiviert. Daten, die in primäre Datenspeicher aufgenommen werden, werden jetzt mit dem oder den Schlüssel(n) in Ihrem [!DNL Azure]-Schlüsseltresor ver- und entschlüsselt.

Nachdem Sie CMK für Ihre von Azure gehostete Organisation aktiviert haben, überwachen Sie die Schlüsselverwendung, implementieren Sie eine Schlüsselrotationsrichtlinie für erhöhte Sicherheit und stellen Sie die Einhaltung der Richtlinien Ihrer Organisation sicher.
