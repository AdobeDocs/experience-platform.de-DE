---
keywords: Experience Platform;Startseite;beliebte Themen;PSQL;psqlconnect to query service;Abfrage-Service;Abfrage-Service;
solution: Experience Platform
title: PSQL mit Query Service verbinden
description: PSQL ist eine Befehlszeilenschnittstelle, die bei der Installation von PostgreSQL auf Ihrem Computer zur Verfügung steht. Sie können es installieren, indem Sie die nachfolgenden Anweisungen befolgen.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 11%

---

# PSQL mit Query Service verbinden

PSQL ist eine Befehlszeilenschnittstelle, die bei der Installation von [!DNL PostgreSQL] auf Ihrem Computer installiert wird. In diesem Dokument werden die Schritte zum Verbinden von PSQL mit Adobe Experience Platform [!DNL Query Service] beschrieben.

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL PSQL] haben und mit dessen Verwendung vertraut sind. Weitere Informationen zu [!DNL PSQL] finden Sie in der [offiziellen [!DNL PSQL] Dokumentation](https://www.postgresql.org/docs/current/app-psql.html).

Nachdem Sie PSQL auf Ihrem Computer installiert haben, können Sie PSQL mit dem Abfrage-Service verbinden. Kehren Sie zur [!DNL Experience Platform]-Benutzeroberfläche zurück und wählen Sie **[!UICONTROL Abfragen]** gefolgt von **[!UICONTROL Anmeldeinformationen]** aus.

Wählen Sie im Abschnitt **[!UICONTROL PSQL]** Befehl das Symbol **[!UICONTROL In Zwischenablage kopieren]** (![Kopiersymbol](/help/images/icons/copy.png)) aus, um die Befehlszeichenfolge zu kopieren.

![Die Registerkarte „Anmeldeinformationen“ des Abfragen-Dashboards mit hervorgehobenem Kopiersymbol.](../images/clients/psql/connect-bi.png)

Fügen Sie die Befehlszeichenfolge in ein Terminal- oder Befehlszeilenfenster ein und drücken Sie die **Eingabetaste** auf der Tastatur.

>[!IMPORTANT]
>
>Wenn Sie sich auf einem PC befinden, verwenden Sie einen Texteditor, um die Zeilenumbrüche in der Befehlszeichenfolge zu entfernen, und kopieren Sie dann die Zeichenfolge. Wenn Sie Version 12.0 oder höher verwenden, müssen Sie `PGGSSENCMODE=disable` zu Ihrer Verbindungszeichenfolge hinzufügen. Wenn Sie nicht ablaufende Zugangsdaten verwenden, ersetzen Sie außerdem das Feld „Kennwort“ durch das nicht ablaufende Zugangsdaten-Kennwort. Weitere Informationen zu nicht ablaufenden Anmeldedaten finden Sie im [Handbuch zu Anmeldedaten](../ui/credentials.md).

Die Ausgabe sollte in folgt lauten:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Wird für die Versionsnummer nicht mindestens 10.5 angegeben, müssen Sie Version 10.5 oder höher herunterladen.

## Nächste Schritte

Nachdem Sie sich mit [!DNL Query Service] verbunden haben, können Sie PSQL zum Schreiben von Abfragen verwenden. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Handbuch unter [Ausführen von Abfragen](../best-practices/writing-queries.md).
