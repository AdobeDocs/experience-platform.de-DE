---
title: Übersicht über Mutual Transport Layer Security (TLS)
description: Erfahren Sie, wie Sie mit mTLS öffentliche Zertifikate, die von Adobe für die Ereignisweiterleitung ausgestellt wurden, sicher abrufen können.
exl-id: e8ee8655-213d-4d2a-93d4-d62824b53b1d
source-git-commit: ab16cc3f70ec54460c7c4834e665c828d75d4d9e
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 2%

---

# Übersicht über die gegenseitige Transport Layer Security ([!DNL mTLS])

Binden Sie in der [!UICONTROL Umgebungen-Benutzeroberfläche) gegenseitige Transport Layer Security ([!DNL mTLS])-], um die Sicherheit Ihrer Erweiterung zu steuern. Das [!DNL mTLS]-Zertifikat ist eine digitale Berechtigung, die die Identität eines Servers oder Clients in sicherer Kommunikation nachweist. Wenn Sie die [!DNL mTLS] Service-API verwenden, helfen Ihnen diese Zertifikate bei der Verifizierung und Verschlüsselung Ihrer Interaktionen mit der Adobe Experience Platform-Ereignisweiterleitung. Dieser Prozess schützt nicht nur Ihre Daten, sondern stellt auch sicher, dass jede Verbindung von einem vertrauenswürdigen Partner stammt.

## Implementieren von [!DNL mTLS] in einer neuen Umgebung {#implement-mtls}

Richten Sie die Ereignisweiterleitungsumgebung ein, um sicherzustellen, dass Ihre Bibliotheks-Builds ordnungsgemäß im Edge-Netzwerk bereitgestellt werden. Während des Setups können Sie die Hosting-Option auswählen, die Ihren Bereitstellungsanforderungen am besten entspricht. Zur sicheren Kommunikation wird Ihrer neuen Umgebung auch automatisch ein [!DNL mTLS]-Zertifikat hinzugefügt.

Um eine neue Umgebung zu erstellen, wählen Sie **[!UICONTROL Registerkarte]** Umgebungen“ im linken Bereich Ihrer Properties der Ereignisweiterleitung aus und klicken Sie auf **[!UICONTROL Umgebung hinzufügen]**.

![Properties der Ereignisweiterleitung, in denen vorhandene Umgebungen angezeigt werden, hervorgehoben [!UICONTROL Umgebung hinzufügen].](../../../images/extensions/server/cloud-connector/add-environment.png)

Wählen Sie auf der nächsten Seite die Umgebung aus, die Sie für dieses Setup verwenden möchten. Es stehen drei Umgebungen zur Verfügung:

>[!NOTE]
>
>Eine Eigenschaft ist auf eine Entwicklungs-, eine Staging- und eine Produktionsumgebung beschränkt.

| Umgebung | Beschreibung |
| --- | --- |
| Entwicklung | Die Entwicklungsumgebung ist für Team-Mitglieder gedacht, um Bibliotheken oder Änderungen an der Ereignisweiterleitung zu testen. |
| Staging | Die Staging-Umgebung ist optional und ermöglicht es genehmigten Team-Mitgliedern, eine Bibliothek zu testen und zu genehmigen, bevor sie veröffentlicht wird. |
| Produktion | Die Produktionsumgebung wird für Live-Produktionsdaten verwendet. |

![Der Bildschirm „Umgebungsauswahl“ mit hervorgehobener Option [!UICONTROL Auswählen] für Entwicklung.](../../../images/extensions/server/cloud-connector/select-environment.png)

Geben Sie auf der **[!UICONTROL Umgebung erstellen]** einen **[!UICONTROL Namen]** ein und wählen Sie ***Adobe Managed*** aus dem Dropdown-Menü **[!UICONTROL Host auswählen]**. Das **[!UICONTROL Zertifikat]** wird ***automatisch hinzugefügt***. Wählen Sie abschließend **[!UICONTROL Speichern]** aus.

![Die Seite „Entwicklungsumgebung erstellen“, auf der [!UICONTROL Name], [!UICONTROL Host auswählen] und [!UICONTROL Speichern] hervorgehoben ist.](../../../images/extensions/server/cloud-connector/create-environment.png)

Die Umgebung wurde erfolgreich erstellt und Sie kehren zur Registerkarte **[!UICONTROL Umgebungen]** zurück, auf der Ihre neue Umgebung angezeigt wird.

![Registerkarte [!UICONTROL Umgebungen], auf der die Entwicklungsumgebung hervorgehoben ist.](../../../images/extensions/server/cloud-connector/new-environment-created.png)

## Anzeigen von Details zum Umgebungszertifikat {#view-certificate}

Um die Zertifikatdetails für eine Umgebung anzuzeigen, wählen Sie **[!UICONTROL Registerkarte]** Umgebungen“ im linken Bereich Ihrer Ereignisweiterleitungs-Eigenschaften aus und wählen Sie dann die Umgebung aus, um die Details anzuzeigen.

Die folgenden Zertifikatdetails werden angezeigt:

| Feldname | Beschreibung |
| --- | --- |
| Zertifikat | Einzelheiten der Bescheinigung, darunter:<ul><li>**Name**: Der Name des Zertifikats.</li><li>**Erstellungsdatum**: Das Datum, an dem das Zertifikat erstellt wurde.</li><li>**Status**: Der aktuelle Status des Zertifikats:<ul><li>**Aktuell**: Das Zertifikat wird aktiv verwendet.</li><li>**Veraltet**: Das Zertifikat wird nicht verwendet, ist aber noch nicht abgelaufen. Es kann weiterhin zur Verwendung ausgewählt werden.</li><li>**Abgelaufen**: Das Zertifikat ist abgelaufen, ausgegraut und nicht mehr verfügbar.</li></ul></ul> |
| Expires | Datum, an dem das Zertifikat abläuft. |
| Variable Name | Der Variablenname des Zertifikats. |
| Status | Der aktuelle Status des Zertifikats:<ul><li>**bereitgestellt**: Das Zertifikat wurde erfolgreich bereitgestellt und ist aktiv.</li><li>**Wird**: Das Zertifikat wird gerade bereitgestellt.</li><li>**Bereitstellung erforderlich**: Dieser Status wird angezeigt, wenn ein veraltetes Zertifikat ausgewählt wurde.</li></ul> |

![Die Seite „Entwicklungsumgebung bearbeiten“, auf der [!UICONTROL Zertifikat] Details hervorgehoben sind.](../../../images/extensions/server/cloud-connector/certificate-details.png)

### Auswählen und Bereitstellen eines veralteten Zertifikats {#deploy-obsolete-certificate}

Um ein veraltetes Zertifikat zu verwenden, navigieren Sie zur Registerkarte **[!UICONTROL Umgebungen]** im linken Bereich Ihrer Ereignisweiterleitungs-Eigenschaften und wählen Sie dann die Umgebung aus, um ihre Details anzuzeigen.

![Registerkarte [!UICONTROL Umgebungen], auf der die Entwicklungsumgebung hervorgehoben ist.](../../../images/extensions/server/cloud-connector/new-environment-created.png)

Wählen Sie aus **[!UICONTROL Dropdown-]** „Zertifikat“ ein veraltetes Zertifikat aus und klicken Sie dann auf **[!UICONTROL Speichern]**.

![Die Seite „Entwicklungsumgebung bearbeiten“, auf der das Dropdown[!UICONTROL Zertifikat] mit veraltetem Zertifikat und hervorgehobener Option „Speichern“ hervorgehoben ist.](../../../images/extensions/server/cloud-connector/obsolete-certificate.png)

Um das Zertifikat bereitzustellen, wählen Sie **[!UICONTROL Speichern und]**) im Dialogfeld **[!UICONTROL Zertifikat]**.

![Dialogfeld „Zertifikat bereitstellen“ mit hervorgehobener Option „Speichern und Bereitstellen“.](../../../images/extensions/server/cloud-connector/obsolete-certificate-deploy.png)


## Nächste Schritte {#next-steps}

In diesem Dokument wurde gezeigt, wie Sie eine Umgebung für Ihre Ereignisweiterleitungseigenschaft erstellen, ein Zertifikat hinzufügen und ein veraltetes Zertifikat verwenden. Weitere Informationen zu den [!DNL mTLS] Zertifikaten finden Sie unter [[!DNL mTLS] Service-API - Übersicht](../../../../data-governance/mtls-api/overview.md)

Informationen zur Verwendung von [!DNL mTLS]-Zertifikaten in Ereignisweiterleitungsregeln finden Sie im Abschnitt [Übersicht über die Cloud Connector-Erweiterung](../cloud-connector/overview.md/#mtls-rules).
