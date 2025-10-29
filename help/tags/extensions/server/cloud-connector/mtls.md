---
title: Übersicht über Mutual Transport Layer Security (TLS)
description: Erfahren Sie, wie Sie mit mTLS öffentliche Zertifikate, die von Adobe für die Ereignisweiterleitung ausgestellt wurden, sicher abrufen können.
exl-id: e8ee8655-213d-4d2a-93d4-d62824b53b1d
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 2%

---

# Übersicht über die gegenseitige Transport Layer Security ([!DNL mTLS])

Binden Sie die Zertifikate für die gegenseitige Transport Layer Security ([!DNL mTLS]) in der [!UICONTROL Environments UI], um die Sicherheit Ihrer Erweiterung zu steuern. Das [!DNL mTLS]-Zertifikat ist eine digitale Berechtigung, die die Identität eines Servers oder Clients in sicherer Kommunikation nachweist. Wenn Sie die [!DNL mTLS] Service-API verwenden, helfen Ihnen diese Zertifikate bei der Verifizierung und Verschlüsselung Ihrer Interaktionen mit der Adobe Experience Platform-Ereignisweiterleitung. Dieser Prozess schützt nicht nur Ihre Daten, sondern stellt auch sicher, dass jede Verbindung von einem vertrauenswürdigen Partner stammt.

## Implementieren von [!DNL mTLS] in einer neuen Umgebung {#implement-mtls}

Richten Sie die Ereignisweiterleitungsumgebung ein, um sicherzustellen, dass Ihre Bibliotheks-Builds ordnungsgemäß im Edge-Netzwerk bereitgestellt werden. Während des Setups können Sie die Hosting-Option auswählen, die Ihren Bereitstellungsanforderungen am besten entspricht. Zur sicheren Kommunikation wird Ihrer neuen Umgebung auch automatisch ein [!DNL mTLS]-Zertifikat hinzugefügt.

Um eine neue Umgebung zu erstellen, wählen Sie im linken Bereich der Eigenschaften der Ereignisweiterleitung die Registerkarte **[!UICONTROL Environments]** und dann **[!UICONTROL Add Environment]** aus.

![Eigenschaften der Ereignisweiterleitung, die vorhandene Umgebungen anzeigen, Hervorhebung von [!UICONTROL Add Environment].](../../../images/extensions/server/cloud-connector/add-environment.png)

Wählen Sie auf der nächsten Seite die Umgebung aus, die Sie für dieses Setup verwenden möchten. Es stehen drei Umgebungen zur Verfügung:

>[!NOTE]
>
>Eine Eigenschaft ist auf eine Entwicklungs-, eine Staging- und eine Produktionsumgebung beschränkt.

| Umgebung | Beschreibung |
| --- | --- |
| Entwicklung | Die Entwicklungsumgebung ist für Team-Mitglieder gedacht, um Bibliotheken oder Änderungen an der Ereignisweiterleitung zu testen. |
| Staging | Die Staging-Umgebung ist optional und ermöglicht es genehmigten Team-Mitgliedern, eine Bibliothek zu testen und zu genehmigen, bevor sie veröffentlicht wird. |
| Produktion | Die Produktionsumgebung wird für Live-Produktionsdaten verwendet. |

![Der Auswahlbildschirm für die Umgebung, in dem [!UICONTROL Select] für die Entwicklung hervorgehoben sind.](../../../images/extensions/server/cloud-connector/select-environment.png)

Geben Sie auf der Seite **[!UICONTROL Create Environment]** einen **[!UICONTROL Name]** ein und wählen Sie ***Adobe Managed*** aus dem Dropdown-Menü **[!UICONTROL Select Host]** aus. Die **[!UICONTROL Certificate]** wird ***automatisch hinzugefügt***. Wählen Sie abschließend **[!UICONTROL Save]** aus.

![Die Seite „Entwicklungsumgebung erstellen“, auf der [!UICONTROL Name], [!UICONTROL Select Host] und [!UICONTROL Save] hervorgehoben sind.](../../../images/extensions/server/cloud-connector/create-environment.png)

Die Umgebung wurde erfolgreich erstellt und Sie kehren zur Registerkarte **[!UICONTROL Environments]** zurück, auf der Ihre neue Umgebung angezeigt wird.

![Die Registerkarte &quot;[!UICONTROL Environments]&quot;, auf der die Entwicklungsumgebung hervorgehoben ist.](../../../images/extensions/server/cloud-connector/new-environment-created.png)

## Anzeigen von Details zum Umgebungszertifikat {#view-certificate}

Um die Zertifikatdetails für eine Umgebung anzuzeigen, wählen Sie die Registerkarte **[!UICONTROL Environments]** im linken Bereich Ihrer Properties der Ereignisweiterleitung und dann die Umgebung aus, um die Details anzuzeigen.

Die folgenden Zertifikatdetails werden angezeigt:

| Feldname | Beschreibung |
| --- | --- |
| Zertifikat | Einzelheiten der Bescheinigung, darunter:<ul><li>**Name**: Der Name des Zertifikats.</li><li>**Erstellungsdatum**: Das Datum, an dem das Zertifikat erstellt wurde.</li><li>**Status**: Der aktuelle Status des Zertifikats:<ul><li>**Aktuell**: Das Zertifikat wird aktiv verwendet.</li><li>**Veraltet**: Das Zertifikat wird nicht verwendet, ist aber noch nicht abgelaufen. Es kann weiterhin zur Verwendung ausgewählt werden.</li><li>**Abgelaufen**: Das Zertifikat ist abgelaufen, ausgegraut und nicht mehr verfügbar.</li></ul></ul> |
| Expires | Datum, an dem das Zertifikat abläuft. |
| Variable Name | Der Variablenname des Zertifikats. |
| Status | Der aktuelle Status des Zertifikats:<ul><li>**bereitgestellt**: Das Zertifikat wurde erfolgreich bereitgestellt und ist aktiv.</li><li>**Wird**: Das Zertifikat wird gerade bereitgestellt.</li><li>**Bereitstellung erforderlich**: Dieser Status wird angezeigt, wenn ein veraltetes Zertifikat ausgewählt wurde.</li></ul> |

![Die Seite „Entwicklungsumgebung bearbeiten“, auf der [!UICONTROL Certificate] Details hervorgehoben sind.](../../../images/extensions/server/cloud-connector/certificate-details.png)

### Auswählen und Bereitstellen eines veralteten Zertifikats {#deploy-obsolete-certificate}

Um ein veraltetes Zertifikat zu verwenden, navigieren Sie zur Registerkarte **[!UICONTROL Environments]** im linken Bereich Ihrer Ereignisweiterleitungs-Eigenschaften und wählen Sie dann die Umgebung aus, um ihre Details anzuzeigen.

![Die Registerkarte &quot;[!UICONTROL Environments]&quot;, auf der die Entwicklungsumgebung hervorgehoben ist.](../../../images/extensions/server/cloud-connector/new-environment-created.png)

Wählen Sie aus der Dropdown-Liste **[!UICONTROL Certificate]** ein veraltetes Zertifikat aus und klicken Sie dann auf **[!UICONTROL Save]**.

![Die Seite „Entwicklungsumgebung bearbeiten“, auf der [!UICONTROL Certificate] Dropdown-Menü mit veraltetem Zertifikat und „Speichern“ hervorgehoben ist.](../../../images/extensions/server/cloud-connector/obsolete-certificate.png)

Um das Zertifikat bereitzustellen, wählen Sie **[!UICONTROL Save and deploy]** im Dialogfeld **[!UICONTROL Deploy Certificate]** aus.

![Dialogfeld „Zertifikat bereitstellen“ mit hervorgehobener Option „Speichern und Bereitstellen“.](../../../images/extensions/server/cloud-connector/obsolete-certificate-deploy.png)


## Nächste Schritte {#next-steps}

In diesem Dokument wurde gezeigt, wie Sie eine Umgebung für Ihre Ereignisweiterleitungseigenschaft erstellen, ein Zertifikat hinzufügen und ein veraltetes Zertifikat verwenden. Weitere Informationen zu den [!DNL mTLS] Zertifikaten finden Sie unter [[!DNL mTLS] Service-API - Übersicht](../../../../data-governance/mtls-api/overview.md)

Informationen zur Verwendung von [!DNL mTLS]-Zertifikaten in Ereignisweiterleitungsregeln finden Sie im Abschnitt [Übersicht über die Cloud Connector-Erweiterung](../cloud-connector/overview.md#mtls-rules).
