---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; Query Service; Looker; Looker; Verbindung mit Query Service
solution: Experience Platform
title: Verbinden von Looker mit Query Service
description: In diesem Dokument werden die Schritte zum Verbinden von Looker mit dem Adobe Experience Platform Query Service beschrieben.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 5%

---

# Verbinden von [!DNL Looker] mit dem Abfrage-Service

In diesem Dokument werden die Schritte zum Verbinden von [!DNL Looker] mit Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL Looker] und sind mit dem Navigieren in der Benutzeroberfläche vertraut. Weitere Informationen [!DNL Looker] finden Sie im Abschnitt [offiziell [!DNL Looker] Dokumentation](https://docs.looker.com/).

## Neue Datenbankverbindung erstellen {#create-connection}

Nach der Anmeldung bei [!DNL Looker]auswählen **[!DNL Admin]**, gefolgt von **[!DNL Connections]**. Die [!DNL Connections] Seite geöffnet. Im [!DNL Connections] Seite, wählen Sie **[!DNL Add Connection]**.

Geben Sie hier die Details für die unten aufgeführten Verbindungsparameter ein. Siehe die offizielle Looker-Dokumentation für [Anweisungen zum Erstellen einer neuen Datenbankverbindung und Beschreibungen der verfügbaren Eigenschaften](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** Der Name Ihrer Verbindung.
- **[!DNL Dialect]:** Das für die SQL-Datenbank verwendete Dialogfeld. [!DNL Query Service] verwendet **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** Der Host-Endpunkt und sein Port für [!DNL Query Service].
- **[!DNL Database]:** Die zu verwendende Datenbank.
- **[!DNL Username and Password]:** Die Anmeldeinformationen, die verwendet werden. Der Benutzername lautet wie folgt: `ORG_ID@AdobeOrg`.
- **SSL**: Aktivieren Sie SSL, um eine sichere Verbindung im Netzwerk sicherzustellen.

Melden Sie sich bei der Platform-Benutzeroberfläche an und wählen Sie **[!UICONTROL Abfragen]** aus der linken Navigation, gefolgt von **[!UICONTROL Anmeldeinformationen]**. Weitere Informationen zum Auffinden Ihrer **Host**, **port**, **Datenbank**, **Benutzername** und **password** Anmeldeinformationen, lesen Sie bitte die [Handbuch zu Anmeldeinformationen](../ui/credentials.md).

![Auf der Seite &quot;Anmeldeinformationen&quot;im Arbeitsbereich &quot;Experience Platform-Abfragen&quot;werden Anmeldeinformationen und ablaufende Anmeldeinformationen hervorgehoben.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] bietet auch nicht ablaufende Anmeldeinformationen, um eine einmalige Einrichtung mit Drittanbieterclients zu ermöglichen. Weitere Informationen finden Sie in der Dokumentation für [Vollständige Anweisungen zum Generieren und Verwenden von nicht ablaufenden Anmeldedaten](../ui/credentials.md#non-expiring-credentials). Dieser Vorgang muss abgeschlossen werden, wenn Sie Looker als einmaliges Setup verbinden möchten. Die `credential` und `technicalAccountId` Die erworbenen Werte umfassen den Wert für den Looker `password` Parameter.

Weitere Informationen zur SSL-Unterstützung für Drittanbieterverbindungen in Adobe Experience Platform finden Sie unter [[!DNL Query Service] SSL-Dokumentation](./ssl-modes.md). In diesem Dokument erfahren Sie, wie Sie mithilfe von `verify-full` SSL-Modus.

Nachdem Sie Ihre Verbindungsdetails eingegeben haben, wählen Sie **[!DNL Test These Settings]** , um sicherzustellen, dass Ihre Anmeldeinformationen ordnungsgemäß funktionieren. Weitere Informationen über [Testen der Verbindungseinstellungen](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) werden in der offiziellen Looker-Dokumentation bereitgestellt. Bei erfolgreicher Verbindung wird auf dem Bildschirm eine Meldung angezeigt, die angibt, dass Sie eine Verbindung herstellen können. Nachdem die Verbindung erfolgreich hergestellt wurde, wählen Sie **[!DNL Add Connection]** , um Ihre Verbindung herzustellen.

## Nächste Schritte

Jetzt, da Sie mit [!DNL Query Service]können Sie [!DNL Looker] , um Abfragen zu schreiben. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
