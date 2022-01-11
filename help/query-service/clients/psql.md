---
keywords: Experience Platform; Startseite; beliebte Themen; PSQL; psqlconnect zu Query Service; Query Service; Query Service;
solution: Experience Platform
title: PSQL mit Query Service verbinden
topic-legacy: connect
description: PSQL ist eine Befehlszeilenschnittstelle, die bei der Installation von PostgreSQL auf Ihrem Computer bereitgestellt wird. Sie können es installieren, indem Sie die nachfolgenden Anweisungen befolgen.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 06d3a8aa6f2f73c2d5392a76fb5b36b18691cf0d
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 20%

---

# PSQL mit Query Service verbinden

PSQL ist eine Befehlszeilenschnittstelle, die bei der Installation installiert wird [!DNL PostgreSQL] auf Ihrem Computer. In diesem Dokument werden die Schritte zum Verbinden von PSQL mit Adobe Experience Platform beschrieben. [!DNL Query Service].

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL PSQL] und sind mit der Verwendung vertraut. Weitere Informationen [!DNL PSQL] finden Sie im Abschnitt [offiziell [!DNL PSQL] Dokumentation](https://www.postgresql.org/docs/current/app-psql.html).

Nach der Installation von PSQL auf Ihrem Computer können Sie PSQL mit Query Service verbinden. Kehren Sie zu [!DNL Platform] Benutzeroberfläche, wählen Sie **[!UICONTROL Abfragen]**, gefolgt von **[!UICONTROL Anmeldeinformationen]**.

![Bild](../images/clients/psql/connect-bi.png)

Wählen Sie das Symbol aus, um den Abschnitt mit der Bezeichnung **[!UICONTROL PSQL-Befehl]** und fügen Sie dann die Befehlszeichenfolge in ein Terminal- oder Befehlszeilenfenster ein, bevor Sie die Eingabetaste drücken.

>[!IMPORTANT]
>
>Verwenden Sie auf einem PC einen Texteditor, um in der Zeichenfolge des Befehls die Zeilenumbrüche zu entfernen, und kopieren Sie dann die Zeichenfolge. Wenn Sie Version 12.0 oder höher verwenden, müssen Sie `PGGSSENCMODE=disable` zu Ihrer Verbindungszeichenfolge hinzufügen. Wenn Sie nicht ablaufende Anmeldedaten verwenden, müssen Sie außerdem das Kennwortfeld durch das Passwort ersetzen, das nicht abläuft. Weitere Informationen zu nicht ablaufenden Anmeldedaten finden Sie im Abschnitt [Handbuch zu Anmeldeinformationen](../ui/credentials.md).

Die Ausgabe sollte in folgt lauten:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Wird für die Versionsnummer nicht mindestens 10.5 angegeben, müssen Sie Version 10.5 oder höher herunterladen.

## Nächste Schritte

Jetzt, da Sie mit [!DNL Query Service], können Sie PSQL zum Schreiben von Abfragen verwenden. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Handbuch unter [Ausführen von Abfragen](../best-practices/writing-queries.md).
