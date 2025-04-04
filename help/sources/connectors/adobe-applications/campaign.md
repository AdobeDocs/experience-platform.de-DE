---
keywords: Experience Platform;Startseite;beliebte Themen;Adobe Campaign Managed Cloud Services;Kampagne;Campaign Managed Services
title: Adobe Campaign Managed Cloud Services
description: Erfahren Sie, wie Sie Campaign Managed Cloud Services über die Benutzeroberfläche mit Experience Platform verbinden
exl-id: 8f18bf73-ebf1-4b4e-a12b-964faa0e24cc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 5%

---

# Adobe Campaign Managed Cloud Services

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Adobe Campaign Managed Cloud Services bietet eine Managed Services-Plattform für die Gestaltung kanalübergreifender Kundenerlebnisse und stellt dazu eine Umgebung für die visuelle Kampagnenorchestrierung, die Echtzeit-Interaktionsverwaltung und die kanalübergreifende Ausführung bereit. Weitere Informationen finden Sie in der Dokumentation ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaign-home.html?lang=de) Adobe Campaign v8 .[

Mit der Adobe Campaign Managed Cloud Services-Quelle können Sie Adobe Campaign v8-Versandlogs und -Trackinglog-Daten an Adobe Experience Platform übertragen.

## Voraussetzungen

Bevor Sie eine Quellverbindung erstellen können, um Ihre Campaign v8-Version nach Experience Platform zu bringen, müssen Sie zunächst die folgenden Voraussetzungen erfüllen:

* [Einrichten des Ereignisprotokollimports mithilfe der Adobe Campaign-Client-Konsole](#view-delivery-and-tracking-log-data)
* [Erstellen eines XDM-ExperienceEvent-Schemas](#create-a-schema)
* [Erstellen eines Datensatzes](#create-a-dataset)

### Versand- und Trackinglog-Daten anzeigen {#view-delivery-and-tracking-log-data}

>[!IMPORTANT]
>
>Sie müssen Zugriff auf die Client-Konsole von Adobe Campaign v8 haben, um Ihre Protokolldaten in Campaign anzeigen zu können. In der [Campaign v8-Dokumentation](https://experienceleague.adobe.com/docs/campaign/campaign-v8/deploy/connect.html) finden Sie Informationen zum Herunterladen und Installieren der Client-Konsole.

Melden Sie sich über die Client-Konsole bei Ihrer Campaign v8-Instanz an. Wählen Sie auf der Registerkarte [!DNL Explorer] die Option [!DNL Administration] und dann [!DNL Configuration] aus. Wählen Sie als Nächstes [!DNL Data schemas] aus und wenden Sie dann den `broadLog` auf Namen oder Titel an. Wählen Sie in der angezeigten Liste das Quellschema der Empfänger-Versandlogs mit dem Namen `broadLogRcp` aus.

![Die Adobe Campaign v8-Client-Konsole mit der ausgewählten Registerkarte „Explorer“, erweiterten die Knoten „Administration“, „Konfiguration“ und „Datenschemata“ und setzten die Filterung auf „Umfassend“.](./images/campaign/explorer.png)

Wählen Sie als Nächstes die **Daten** aus.

![Die Client-Konsole von Adobe Campaign v8 mit ausgewählter Registerkarte „Daten“.](./images/campaign/data.png)

Klicken/klicken Sie mit der rechten Maustaste im Datenbedienfeld, um das Kontextmenü zu öffnen. Wählen Sie hier **Liste konfigurieren…**

![Die Client-Konsole von Adobe Campaign v8 mit dem Kontextmenü wird geöffnet und die Option Liste konfigurieren ist ausgewählt.](./images/campaign/configure.png)

Das Listenkonfigurationsfenster wird angezeigt und bietet eine Oberfläche, über die Sie beliebige Felder zu der bereits vorhandenen Liste hinzufügen können, um die Daten im Datenbereich anzuzeigen.

![Eine Liste der Konfigurationen für Empfänger-Versandlogs, die zur Anzeige hinzugefügt werden können.](./images/campaign/list-configuration.png)

Jetzt können Sie die Versand-Logs Ihrer Empfänger einschließlich der im vorherigen Schritt hinzugefügten Konfigurationsfelder anzeigen.

>[!TIP]
>
>Sie können dieselben Schritte wiederholen, aber nach `tracking` filtern, um Ihre Trackinglog-Daten anzuzeigen.

![Die Versand-Logs der Empfänger werden mit Informationen zu ihrem zuletzt geänderten Namen, ihrem Versandkanal, ihrem internen Versandnamen und ihrer Bezeichnung angezeigt.](./images/campaign/recipient-delivery-logs.png)

### Erstellen eines Schemas {#create-a-schema}

Als Nächstes erstellen Sie ein XDM ExperienceEvent-Schema für Versandlogs und Trackinglogs. Sie müssen die Feldergruppe Versandlogs in Campaign auf Ihr Versandlog-Schema und die Feldergruppe Tracking-Logs in Campaign auf Ihr Trackinglog-Schema anwenden. Sie müssen auch das Feld `externalID` als primäre Identität Ihres Schemas definieren.

>[!NOTE]
>
>Ihr XDM ExperienceEvent-Schema muss Profil-aktiviert sein, damit Sie Ihre Campaign-Daten in [!DNL Real-Time Customer Profile] aufnehmen können.

Detaillierte Anweisungen zum Erstellen eines Schemas finden Sie im Handbuch unter [Erstellen eines XDM-Schemas in der Benutzeroberfläche](../../../xdm/tutorials/create-schema-ui.md).

### Erstellen eines Datensatzes {#create-a-dataset}

Schließlich müssen Sie einen Datensatz für Ihre Schemata erstellen. Detaillierte Anweisungen zum Erstellen eines Datensatzes finden Sie im Handbuch unter [Erstellen eines Datensatzes in der Benutzeroberfläche](../../../catalog/datasets/user-guide.md).

## Erstellen einer Adobe Campaign Managed Cloud Services-Quellverbindung mithilfe der Experience Platform-Benutzeroberfläche

Nachdem Sie nun auf Ihre Datenprotokolle in der Client-Konsole von Campaign zugegriffen, ein Schema erstellt und einen Datensatz erstellt haben, können Sie jetzt mit dem Erstellen einer Quellverbindung fortfahren, um Ihre Campaign Managed Services-Daten in Experience Platform zu übertragen.

Detaillierte Anweisungen zum Übertragen Ihrer Versand-Logs und Trackinglog-Daten von Campaign v8 auf Experience Platform finden Sie im Handbuch unter [Erstellen einer Managed Services-Quellverbindung in der Benutzeroberfläche von Campaign](../../tutorials/ui/create/adobe-applications/campaign.md).

>[!IMPORTANT]
>
>Es gibt einen Sonderfall, bei dem die Interaktion eines kürzlich entfernten E-Mail-Empfängers mit einer E-Mail personenbezogene Daten erneut in Experience Platform aufnehmen könnte. In einigen Fällen kann dies das Marketing für diesen Benutzer wieder aktivieren.
>
>* Dieses Szenario ist nur zwischen der Ausführung einer Datenschutzanfrage in Experience Platform und der Ausführung in Adobe Campaign Classic aktiv. Nachdem die Anfrage in Campaign ausgeführt wurde, gibt es eine Prüfung, um sicherzustellen, dass der Datensatz nicht in Campaign exportiert wird. Bitte stellen Sie nach 72 Stunden der Ausführung eine DSGVO-Anfrage erneut, um das Problem zu beheben.