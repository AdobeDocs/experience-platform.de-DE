---
keywords: Experience Platform;Home;beliebte Themen;PSQL;psqlconnect to Abfrage Service;Abfrage-Dienst;Abfrage-Dienst
solution: Experience Platform
title: PSQL mit dem Abfrage-Dienst verbinden
topic-legacy: connect
description: PSQL ist eine Befehlszeilenschnittstelle, die bei der Installation von PostgreSQL auf Ihrem Computer verwendet wird. Sie können es installieren, indem Sie die nachfolgenden Anweisungen befolgen.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 23%

---

# PSQL mit dem Abfrage-Dienst verbinden

PSQL ist eine Befehlszeilenschnittstelle, die installiert wird, wenn Sie [!DNL PostgreSQL] auf Ihrem Computer installieren. Dieses Dokument beschreibt die Schritte zum Verbinden von PSQL mit Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Dieses Handbuch setzt voraus, dass Sie bereits Zugriff auf [!DNL PSQL] haben und mit dessen Verwendung vertraut sind. Weitere Informationen zu [!DNL PSQL] finden Sie in der [offiziellen [!DNL PSQL] Dokumentation](https://www.postgresql.org/docs/current/app-psql.html.

Nachdem Sie PSQL auf Ihrem Computer installiert haben, können Sie PSQL mit dem Abfrage Service verbinden. Kehren Sie zur Benutzeroberfläche [!DNL Platform] zurück und wählen Sie **[!UICONTROL Abfragen]**, gefolgt von **[!UICONTROL Anmeldeinformationen]**.

![Bild](../images/clients/psql/connect-bi.png)

Wählen Sie das Symbol aus, um den Abschnitt mit der Bezeichnung **[!UICONTROL PSQL-Befehl]** zu kopieren, und fügen Sie dann die Befehlszeichenfolge in ein Terminal- oder Befehlszeilenfenster ein, bevor Sie die Eingabetaste drücken.

>[!IMPORTANT]
>
>Verwenden Sie auf einem PC einen Texteditor, um in der Zeichenfolge des Befehls die Zeilenumbrüche zu entfernen, und kopieren Sie dann die Zeichenfolge. Wenn Sie außerdem Version 12.0 oder höher verwenden, müssen Sie `PGGSSENCMODE=disable` zu Ihrer Verbindungszeichenfolge hinzufügen.

Die Ausgabe sollte in folgt lauten:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Wird für die Versionsnummer nicht mindestens 10.5 angegeben, müssen Sie Version 10.5 oder höher herunterladen.

## Nächste Schritte

Nachdem Sie eine Verbindung mit [!DNL Query Service] hergestellt haben, können Sie PSQL verwenden, um Abfragen zu schreiben. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Leitfaden zu [laufenden Abfragen](../best-practices/writing-queries.md).
