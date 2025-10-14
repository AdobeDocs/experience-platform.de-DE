---
keywords: Experience Platform;Startseite;beliebte Themen;PSQL;psqlconnect to query service;Abfrage-Service;Abfrage-Service;
solution: Experience Platform
title: PSQL mit Query Service verbinden
description: Erfahren Sie, wie Sie den PSQL-Client mit dem Adobe Experience Platform Query Service verbinden, einschließlich unterstützter PostgreSQL-Versionen und Einrichtungsanweisungen.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: f75ea97e8631984dcd1d4a7f8aff3c10cba7b11f
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 2%

---

# PSQL mit Query Service verbinden

PSQL ist eine Befehlszeilenschnittstelle, die neben PostgreSQL auf Ihrem Computer installiert ist. In diesem Dokument werden die Schritte zum Verbinden von PSQL mit dem Abfrage-Service von Adobe Experience Platform beschrieben.

>[!IMPORTANT]
>
>Query Service unterstützt nur die Verbindung mit PSQL Version 14.x. Versionen vor 14.x (z. B. 10.x bis 13.x) und neuere Versionen (15.x und höher) werden nicht offiziell unterstützt. Vergewissern Sie sich, dass Sie eine kompatible Client-Version installiert haben. Weitere Informationen finden Sie unter [Enddatum von PostgreSQL](https://endoflife.date/postgresql).

Bevor Sie beginnen, stellen Sie sicher, dass Sie Zugriff auf PSQL haben und über grundlegende Kenntnisse in der Verwendung des Clients verfügen. Weitere Informationen zu PSQL finden Sie in der [offiziellen PSQL-Dokumentation](https://www.postgresql.org/docs/current/app-psql.html).

>[!IMPORTANT]
>
>Stellen Sie beim Herunterladen von PostgreSQL sicher, dass Sie Version 14.x auswählen. Standardmäßig bietet die PostgreSQL-Website die neueste Version an, die möglicherweise nicht mit dem Abfrage-Service kompatibel ist.

Sobald PSQL installiert ist, können Sie es mit dem Abfrage-Service verbinden. Kehren Sie zur Experience Platform-Benutzeroberfläche zurück und wählen Sie **[!UICONTROL Abfragen]** gefolgt von **[!UICONTROL Anmeldeinformationen]** aus.

Wählen Sie im Abschnitt **[!UICONTROL PSQL]** Befehl das Symbol **[!UICONTROL In Zwischenablage kopieren]** (![Kopiersymbol](/help/images/icons/copy.png)) aus, um die Befehlszeichenfolge zu kopieren.

![Die Registerkarte „Anmeldeinformationen“ des Abfragen-Dashboards mit hervorgehobenem Kopiersymbol.](../images/clients/psql/copy-credentials.png)

Fügen Sie die Befehlszeichenfolge in Ihr Terminal ein und drücken Sie **Eingabetaste** auf Ihrer Tastatur.

>[!IMPORTANT]
>
>Wenn Sie sich auf einem PC befinden, verwenden Sie einen Texteditor, um die Zeilenumbrüche in der Befehlszeichenfolge zu entfernen, und kopieren Sie dann die Zeichenfolge. Wenn Sie Version 12.0 oder höher verwenden, müssen Sie `PGGSSENCMODE=disable` zu Ihrer Verbindungszeichenfolge hinzufügen. Diese Einstellung deaktiviert die GSSAPI-Verschlüsselung, die für Verbindungen mit dem Abfrage-Service nicht erforderlich ist und Verbindungsfehler verursachen kann.<br>Wenn Sie nicht ablaufende Zugangsdaten verwenden, ersetzen Sie außerdem das Feld „Kennwort“ durch das nicht ablaufende Passwort. Weitere Informationen zu nicht ablaufenden Anmeldedaten finden Sie im [Handbuch zu Anmeldedaten](../ui/credentials.md).

Die Ausgabe sollte in folgt lauten:

```shell
psql (14.4, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Wenn Sie Version 14.x nicht sehen, laden Sie eine unterstützte Version 14.x von PSQL von der [offiziellen PostgreSQL-Downloadseite](https://www.postgresql.org/download/) herunter und installieren Sie sie.

>[!NOTE]
>
>Befolgen Sie die Installationsanweisungen für Ihr Betriebssystem und überprüfen Sie dann Ihre installierte PSQL-Version, indem Sie `psql --version` auf Ihrem Terminal ausführen.

## Nächste Schritte

Nachdem Sie sich mit dem Abfrage-Service verbunden haben, können Sie PSQL zum Schreiben von Abfragen verwenden. Weitere Informationen finden Sie im Handbuch [&#x200B; Ausführen &#x200B;](../best-practices/writing-queries.md) Abfragen .
