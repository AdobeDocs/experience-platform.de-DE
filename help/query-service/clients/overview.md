---
keywords: Experience Platform;home;popular topics;Query service;query service;connect;connect to query service;aqua data studio;Aqua Data Studio;Looker;looker;Postico;postico;Power BI;power bi;psql;rstudio;PSQL;RStudio;Tableau;tableau;
solution: Experience Platform
title: Clients mit Query Service verbinden
description: In diesem Dokument wird beschrieben, wie Sie über verschiedene Desktop-Client-Anwendungen eine Verbindung zu Query Service herstellen und diese Verbindungen überprüfen können.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 778c65c6310ed4a627be0fd3ae076784cfc8495b
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 3%

---

# Clients mit verbinden [!DNL Query Service]

In diesem Abschnitt wird beschrieben, wie Sie eine Verbindung zu [!DNL Query Service] von verschiedenen Desktop-Client-Anwendungen und wie diese Verbindungen überprüft werden. [!DNL Query Service] verwendet die [!DNL PostgreSQL] -Protokoll verwenden. Daher wird in den Anweisungen in diesem Abschnitt die Verwendung von [!DNL PostgreSQL] Tools und Treiber zum Verbinden und Schreiben von Abfragen.

>[!IMPORTANT]
>
>Die TLS/SSL-Zertifikate für Produktionsumgebungen für die Query Service Interactive Postgres API wurden am Mittwoch, 24. Januar 2024 aktualisiert.<br>Obwohl dies eine Jahresanforderung ist, hat sich in diesem Fall auch das Stammzertifikat in der Kette geändert, da der Adobe TLS/SSL-Zertifikatanbieter seine Zertifikatshierarchie aktualisiert hat. Dies kann sich auf bestimmte Postgres-Clients auswirken, wenn in ihrer Liste der Zertifizierungsstellen das Stammzertifikat fehlt. Beispielsweise muss einem PSQL-CLI-Client möglicherweise die Root-Zertifikate zu einer expliziten Datei hinzugefügt werden. `~/postgresql/root.crt`, andernfalls kann dies zu einem Fehler führen. Beispiel: `psql: error: SSL error: certificate verify failed`. Siehe [offizielle PostgreSQL-Dokumentation](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) für weitere Informationen zu diesem Thema.<br>Das Stammzertifikat, das hinzugefügt werden soll, kann heruntergeladen werden von [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

Anweisungen werden für folgende Clients bereitgestellt:

- [[!DNL Aqua Data Studio]](./aqua-data-studio.md)
- [[!DNL DbVisualizer]](./dbvisulaizer.md)
- [[!DNL Looker]](./looker.md)
- [[!DNL Postico (Mac)]](./postico.md)
- [[!DNL Power BI (PC)]](./power-bi.md)
- [[!DNL PSQL]](./psql.md)
- [[!DNL RStudio]](./rstudio.md)
- [[!DNL Tableau]](./tableau.md)
