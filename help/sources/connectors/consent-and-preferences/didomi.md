---
title: Übersicht über Didomi Source
description: Erfahren Sie, wie Sie Didomi über die Benutzeroberfläche mit Adobe Experience Platform verbinden.
last-substantial-update: 2025-07-29T00:00:00Z
badge: Beta
exl-id: c59bcfb8-e831-4a13-8b0e-4c6d538f1059
source-git-commit: b0c2d5535bb4cdf7d00eaca43d65f744276494f3
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 2%

---

# [!DNL Didomi]

>[!AVAILABILITY]
>
>Die [!DNL Didomi]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie &#x200B;](../../home.md#terms-and-conditions) den „Nutzungsbedingungen“ in der Quellenübersicht .

[!DNL Didomi] ist eine Plattform zur Einverständnis- und Präferenzverwaltung, die Unternehmen dabei hilft, Benutzerentscheidungen in Bezug auf personenbezogene Daten auf Websites, in Apps und internen Tools zu erfassen, zu verwalten und durchzusetzen.

Adobe Experience Platform unterstützt die Aufnahme von Daten aus einer Vielzahl externer Systeme, einschließlich Cloud-Speicher, Datenbanken und Anwendungen wie [!DNL Didomi], über ein System von Quell-Connectoren. Verwenden Sie Quellen, um externe Systeme zu authentifizieren, den Datenfluss in Experience Platform zu verwalten und eine konsistente und strukturierte Aufnahme Ihrer Kundendaten sicherzustellen.

Verwenden Sie die [!DNL Didomi], um Daten zum Benutzereinverständnis und zu Voreinstellungen in Echtzeit von der [!DNL Didomi] Einverständnis- und Voreinstellungsverwaltungsplattform in Experience Platform zu streamen. Über die [!DNL Didomi] können Sie Einverständnisdaten in Experience Platform zentralisieren und bearbeiten, sodass Ihre Kundenprofile und nachgelagerten Workflows konform und auf dem neuesten Stand sind.

![Die „Didomi“-Datenverarbeitungsarchitektur.](../../images/tutorials/create/didomi/flux.jpeg)

## Voraussetzungen

Führen Sie die unten beschriebenen Schritte aus, um Ihr [!DNL Didomi]-Konto erfolgreich mit Experience Platform zu verbinden.

### Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform](../../ip-address-allow-list.md) .

### Konfigurieren von Berechtigungen für Experience Platform

Sie müssen sowohl **[!UICONTROL Quellen anzeigen]** als auch **[!UICONTROL Quellen verwalten]** für Ihr Konto aktiviert haben, um Ihr [!DNL Didomi]-Konto mit Experience Platform zu verbinden. Wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten. Weitere Informationen finden Sie im [Handbuch zur Benutzeroberfläche der Zugriffssteuerung](../../../access-control/ui/overview.md).

### Sammeln von Adobe-API-Anmeldeinformationen

Um [!DNL Didomi] sicher mit Experience Platform zu verbinden, müssen Sie sich mit Ihren Adobe-API-Anmeldeinformationen authentifizieren. Diese Anmeldeinformationen sind für die Einrichtung des Webhooks und die Konfiguration der Datenaufnahme unerlässlich.

Lesen Sie das Handbuch [Erste Schritte mit Experience Platform-APIs](../../../landing/api-authentication.md) um Informationen darüber zu erhalten, wie Sie Experience Platform-APIs erfolgreich aufrufen können.

### Erstellen eines Experience Platform-Schemas

>[!TIP]
>
>Sie können diesen Schritt überspringen, wenn Sie bereits über ein vorhandenes XDM-Schema verfügen.

Ein **Experience-Datenmodell (XDM)-** definiert die Struktur der Daten, die Sie von [!DNL Didomi] (z. B. Benutzer-IDs, Einverständniszwecke) an Experience Platform senden.

Um ein Schema zu erstellen, wählen Sie [!UICONTROL Schemata] im linken Navigationsbereich der Experience Platform-Benutzeroberfläche aus und klicken Sie auf **[!UICONTROL Schema erstellen]**. Wählen Sie als Nächstes **[!UICONTROL Standard]** als Schematyp aus und wählen Sie dann **[!UICONTROL Manuell]**, um Ihre Felder manuell zu erstellen. Wählen Sie eine Basisklasse für Ihr Schema aus und geben Sie einen Namen für Ihr Schema an.

Aktualisieren Sie das Schema nach der Erstellung, indem Sie eines der erforderlichen Felder hinzufügen. Stellen Sie sicher, dass mindestens ein Feld ein [!UICONTROL Identitätsfeld] ist, um Experience Platform über Ihre primären Identitätswerte zu informieren. Stellen Sie abschließend sicher, dass Sie den Umschalter [!UICONTROL Profil] aktivieren, um Ihre Daten erfolgreich zu speichern.

![create-schema](../../images/tutorials/create/didomi/create-schema.png)

Weitere Informationen finden Sie im Handbuch unter [Erstellen von Schemata in der Benutzeroberfläche](../../../xdm/tutorials/create-schema-ui.md).

### Erstellen eines Datensatzes

>[!TIP]
>
>Sie können diesen Schritt überspringen, wenn Sie bereits über einen vorhandenen Datensatz verfügen.

Ein **Datensatz** in Experience Platform wird verwendet, um eingehende Daten basierend auf dem von Ihnen definierten Schema zu speichern.

Um einen Datensatz zu erstellen, wählen Sie [!UICONTROL Datensätze] im linken Navigationsbereich der Experience Platform-Benutzeroberfläche aus und klicken Sie dann auf **[!UICONTROL Datensatz erstellen]**. Wählen Sie als Nächstes **[!UICONTROL Datensatz aus Schema erstellen]** und wählen Sie dann Ihr Schema aus, das mit Ihrem neuen Datensatz verknüpft werden soll.

![create-dataset](../../images/tutorials/create/didomi/create-dataset.png)

## Konfigurieren des HTTP-Webhooks auf der [!DNL Didomi] Console

[!DNL Webhooks] können Sie Ereignisse abonnieren, die auf der [!DNL Didomi]-Plattform ausgelöst werden, wenn Benutzer mit ihren Einverständnisvoreinstellungen interagieren. Wenn ein relevantes Ereignis auftritt - z. B. wenn ein Benutzer sein Einverständnis erteilt oder widerruft -, sendet [!DNL Didomi] eine Echtzeit-HTTP-POST-Anfrage mit einer JSON-Payload an Ihren konfigurierten [!DNL webhook]-Endpunkt.

![didomi-console](../../images/tutorials/create/didomi/didomi-console.png)

Um die Kompatibilität mit Experience Platform sicherzustellen, muss Ihr Webhook die folgenden Anforderungen erfüllen.

| Feld | Beschreibung | Beispiel |
| --- | --- | --- | 
| Client-Geheimnis | Der mit Ihren Adobe-API-Anmeldeinformationen verknüpfte geheime Schlüssel. | `d8f3b2e1-4c9a-4a7f-9b2e-8f1c3d2a1b6e` |
| API-Schlüssel | Der öffentliche API-Schlüssel, der zum Authentifizieren von Anfragen an Adobe-Services verwendet wird. |
| Gewährungstyp | Die Methode, mit der eine Anwendung ein Zugriffstoken vom Autorisierungs-Server erhält. Legen Sie diesen Wert auf `client_credentials` fest. | `client_credentials` |
| Anwendungsbereich | Die Autorisierungsumfänge definieren die spezifischen Berechtigungen oder Zugriffsebenen, die eine Anwendung vom API-Anbieter anfordert. | `openid,AdobeID,read_organizations,additional_info.projectedProductContext,session` |
| Authentifizierungs-Header | Die zusätzlichen Kopfzeilen, die für die Adobe-Token-Anfrage erforderlich sind. | `{"Content-type": "application/x-www-form-urlencoded"}` |
| Token-URL | Ihr Adobe-Token-Endpunkt. | `https://ims-na1.adobelogin.com/ims/token/v3` |
| Endpunkt-URL | Die endgültige Adobe-Connector-URL (am Ende der Einrichtung bereitgestellt). | `https://dcs.adobedc.net/collection/your-adobe-endpoint-id` |

{style="table-layout:auto"}

Konfigurieren Sie als Nächstes die folgenden Optionen für Ihre [!DNL webhook].

| Feld | Beschreibung | Wert |
| ---| --- | --- | 
| Anfrage-Header | Die benutzerdefinierten Kopfzeilen für die [!DNL webhook]. Stellen Sie sicher, dass Sie die `x-adobe-flow-id` einschließen. Sie können diesen Wert abrufen, nachdem Ihr [Datenfluss erstellt wurde](../../tutorials/ui/create/consent-and-preferences/didomi.md#retrieve-the-streaming-endpoint-url). | `{"Content-Type": "application/json", "Cache-Control": "no-cache", "x-adobe-flow-id": "{DATAFLOW_ID}"}` |
| abflachen | Diese Eigenschaft muss überprüft werden, da sie sicherstellt, dass die [!DNL webhook] Daten als flaches Objekt gesendet werden. | Aktiviert |
| Ereignistypen | Wählen Sie die spezifische Gruppe von [!DNL Didomi]-Ereignissen (`event.*` oder `user.*`) aus, die den Trigger der [!DNL webhook] bilden sollen. Verwenden Sie `event.*`, um Änderungen des Einverständnisses oder der Voreinstellungen zu verfolgen, und verwenden Sie `user.*`, um Aktualisierungen von Benutzerprofilen zu verfolgen. Diese Auswahl ist erforderlich, um sicherzustellen, dass nur kompatible Ereignisse an Adobe gesendet werden. Adobe unterstützt nur ein Schema pro Datenfluss. Daher kann die Auswahl beider Ereignistypen zu Aufnahmefehlern führen. | Die Liste der unterstützten Ereignistypen ist: <ul><li>`Event.created`</li><li>`Event.updated`</li><li>`Event.deleted`</li><li>`User.created`</li><li>`User.updated`</li><li>`User.deleted`</li></ul> |

### Payload-Beispieldatei herunterladen {#download-the-sample-payload-file}

Laden Sie basierend auf Ihrer ausgewählten Ereignisgruppe die entsprechende **Beispiel-Payload-Datei** direkt von der [!DNL Didomi]-Konsole herunter. Diese Datei stellt die Datenstruktur dar und wird während der Schema- und Zuordnungsschritte in Adobe verwendet.

| **Ereignisgruppe** | **Beispieldatei zum Herunterladen** | **Filteroption** |
| --- | ---| --- |
| `event.*` | Beispiel für `event.created` herunterladen | Nur nach `event.*` Ereignissen filtern |
| `user.*` | Beispiel für `user.created` herunterladen | Nur nach `user.*` Ereignissen filtern |

## Verbinden Ihres [!DNL Didomi] mit Experience Platform

Lesen Sie das Handbuch unter [Verbinden [!DNL Didomi] mit Experience Platform](../../tutorials/ui/create/consent-and-preferences/didomi.md), um zu erfahren, wie Sie eine Quellverbindung erstellen und Einverständnis- und Voreinstellungsdaten aus [!DNL Didomi] in Experience Platform aufnehmen.
