---
keywords: Experience Platform; home; beliebte Themen; PSQL; psqlconnect zu Query Service; Query Service; Query Service
solution: Experience Platform
title: PSQL mit Query Service verbinden
description: PSQL ist eine Befehlszeilenschnittstelle, die bei der Installation von PostgreSQL auf Ihrem Computer bereitgestellt wird. Sie können es installieren, indem Sie die nachfolgenden Anweisungen befolgen.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 11%

---

# PSQL mit Query Service verbinden

PSQL ist eine Befehlszeilenschnittstelle, die installiert wird, wenn Sie [!DNL PostgreSQL] auf Ihrem Computer installieren. In diesem Dokument werden die Schritte zum Verbinden von PSQL mit Adobe Experience Platform [!DNL Query Service] beschrieben.

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL PSQL] haben und mit dessen Verwendung vertraut sind. Weitere Informationen zu [!DNL PSQL] finden Sie in der [offiziellen [!DNL PSQL] Dokumentation](https://www.postgresql.org/docs/current/app-psql.html).

Nach der Installation von PSQL auf Ihrem Computer können Sie PSQL mit Query Service verbinden. Kehren Sie zur Benutzeroberfläche [!DNL Platform] zurück, wählen Sie dann **[!UICONTROL Abfragen]** und dann **[!UICONTROL Anmeldeinformationen]** aus.

Wählen Sie unter dem Abschnitt **[!UICONTROL PSQL-Befehl]** das Symbol **[!UICONTROL In die Zwischenablage kopieren]** (![Symbol &quot;Kopieren&quot;](/help/images/icons/copy.png)), um die Befehlszeichenfolge zu kopieren.

![Die Registerkarte &quot;Dashboard-Anmeldedaten für Abfragen&quot;mit dem Kopiersymbol ist hervorgehoben.](../images/clients/psql/connect-bi.png)

Fügen Sie die Befehlszeichenfolge in ein Terminal- oder Befehlszeilenfenster ein und drücken Sie die **Eingabetaste** auf der Tastatur.

>[!IMPORTANT]
>
>Verwenden Sie auf einem PC einen Texteditor, um die Zeilenumbrüche in der Befehlszeichenfolge zu entfernen, und kopieren Sie dann die Zeichenfolge. Wenn Sie Version 12.0 oder höher verwenden, müssen Sie Ihrer Verbindungszeichenfolge `PGGSSENCMODE=disable` hinzufügen. Wenn Sie nicht ablaufende Anmeldedaten verwenden, müssen Sie außerdem das Kennwortfeld durch das Passwort ersetzen, das nicht abläuft. Weitere Informationen zu nicht ablaufenden Anmeldedaten finden Sie im [Benutzerhandbuch zu Anmeldedaten](../ui/credentials.md).

Die Ausgabe sollte in folgt lauten:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Wird für die Versionsnummer nicht mindestens 10.5 angegeben, müssen Sie Version 10.5 oder höher herunterladen.

## Nächste Schritte

Nachdem Sie sich mit [!DNL Query Service] angemeldet haben, können Sie PSQL zum Schreiben von Abfragen verwenden. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Handbuch zu [ausgeführten Abfragen](../best-practices/writing-queries.md).
