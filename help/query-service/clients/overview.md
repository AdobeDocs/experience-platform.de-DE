---
keywords: Experience Platform;home;popular topics;Query service;query service;connect;connect to query service;aqua data studio;Aqua Data Studio;Looker;looker;Postico;postico;Power BI;power bi;psql;rstudio;PSQL;RStudio;Tableau;tableau;
solution: Experience Platform
title: Verbinden von Clients mit dem Abfragedienst
description: In diesem Dokument wird beschrieben, wie Sie über verschiedene Desktop-Client-Anwendungen eine Verbindung zu Query Service herstellen und diese Verbindungen überprüfen können.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 5%

---

# Clients mit [!DNL Query Service] verbinden

In diesem Abschnitt wird beschrieben, wie Sie von verschiedenen Desktop-Client-Programmen aus eine Verbindung zu [!DNL Query Service] herstellen und diese Verbindungen überprüfen können. [!DNL Query Service] verwendet das Protokoll [!DNL PostgreSQL], daher wird in den Anweisungen in diesem Abschnitt erläutert, wie Sie mit den [!DNL PostgreSQL] -Tools und -Treibern eine Verbindung herstellen und Abfragen schreiben können.

>[!IMPORTANT]
>
>Die TLS/SSL-Zertifikate für Produktionsumgebungen für die Query Service Interactive Postgres API wurden am Mittwoch, 24. Januar 2024 aktualisiert.<br>Obwohl dies eine jährliche Anforderung ist, hat sich in diesem Fall auch das Stammzertifikat in der Kette geändert, da der Adobe TLS/SSL-Zertifikatanbieter seine Zertifikathierarchie aktualisiert hat. Dies kann sich auf bestimmte Postgres-Clients auswirken, wenn in ihrer Liste der Zertifizierungsstellen das Stammzertifikat fehlt. Beispielsweise muss einem PSQL-CLI-Client möglicherweise die Root-Zertifikate zu einer expliziten Datei `~/postgresql/root.crt` hinzugefügt werden, da dies andernfalls zu einem Fehler führen kann. Beispiel: `psql: error: SSL error: certificate verify failed`. Weitere Informationen zu diesem Problem finden Sie in der [offiziellen PostgreSQL-Dokumentation](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) .<br>Das Stammzertifikat, das hinzugefügt werden soll, kann von [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem) heruntergeladen werden.

Anweisungen werden für folgende Clients bereitgestellt:

- [[!DNL Aqua Data Studio]](./aqua-data-studio.md)
- [[!DNL DbVisualizer]](./dbvisulaizer.md)
- [[!DNL Looker]](./looker.md)
- [[!DNL Postico (Mac)]](./postico.md)
- [[!DNL Power BI (PC)]](./power-bi.md)
- [[!DNL PSQL]](./psql.md)
- [[!DNL RStudio]](./rstudio.md)
- [[!DNL Tableau]](./tableau.md)

>[!IMPORTANT]
>
>Als Power BI- und Tableau-Benutzer können Sie über die Registerkarte Query Service-Anmeldedaten eine Verbindung zu Ihren BI-Tools herstellen. Anweisungen zum Verbinden Ihrer BI-Tools mit Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics) finden Sie in der Dokumentation zu den Anmeldedaten .[
