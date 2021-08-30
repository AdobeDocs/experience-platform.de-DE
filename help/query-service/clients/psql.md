---
keywords: Experience Platform; Startseite; beliebte Themen; PSQL; psqlconnect zu Query Service; Query Service; Query Service;
solution: Experience Platform
title: PSQL mit Query Service verbinden
topic-legacy: connect
description: PSQL ist eine Befehlszeilenschnittstelle, die bei der Installation von PostgreSQL auf Ihrem Computer bereitgestellt wird. Sie können es installieren, indem Sie die nachfolgenden Anweisungen befolgen.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 20%

---

# PSQL mit Query Service verbinden

PSQL ist eine Befehlszeilenschnittstelle, die installiert wird, wenn Sie [!DNL PostgreSQL] auf Ihrem Computer installieren. In diesem Dokument werden die Schritte zum Verbinden von PSQL mit Adobe Experience Platform [!DNL Query Service] beschrieben.

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL PSQL] haben und mit dessen Verwendung vertraut sind. Weitere Informationen zu [!DNL PSQL] finden Sie in der [offiziellen [!DNL PSQL] Dokumentation](https://www.postgresql.org/docs/current/app-psql.html.

Nach der Installation von PSQL auf Ihrem Computer können Sie PSQL mit Query Service verbinden. Kehren Sie zur Benutzeroberfläche [!DNL Platform] zurück und wählen Sie **[!UICONTROL Abfragen]**, gefolgt von **[!UICONTROL Anmeldedaten]**.

![Bild](../images/clients/psql/connect-bi.png)

Wählen Sie das Symbol aus, um den Abschnitt **[!UICONTROL PSQL-Befehl]** zu kopieren. Fügen Sie dann die Befehlszeichenfolge in ein Terminal- oder Befehlszeilenfenster ein, bevor Sie die Eingabetaste drücken.

>[!IMPORTANT]
>
>Verwenden Sie auf einem PC einen Texteditor, um in der Zeichenfolge des Befehls die Zeilenumbrüche zu entfernen, und kopieren Sie dann die Zeichenfolge. Wenn Sie Version 12.0 oder höher verwenden, müssen Sie `PGGSSENCMODE=disable` zu Ihrer Verbindungszeichenfolge hinzufügen. Wenn Sie nicht ablaufende Anmeldedaten verwenden, müssen Sie außerdem das Kennwortfeld durch das Passwort ersetzen, das nicht abläuft. Weiterführende Informationen zu nicht ablaufenden Anmeldedaten finden Sie im [Berechtigungshandbuch](../ui/credentials.md).

Die Ausgabe sollte in folgt lauten:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Wird für die Versionsnummer nicht mindestens 10.5 angegeben, müssen Sie Version 10.5 oder höher herunterladen.

## Nächste Schritte

Nachdem Sie sich mit [!DNL Query Service] angemeldet haben, können Sie PSQL zum Schreiben von Abfragen verwenden. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Handbuch zu [laufenden Abfragen](../best-practices/writing-queries.md).
