---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;verbinden;mit Abfrage-Service verbinden;aqua data studio;Aqua Data Studio;Looker;Looker;Postico;postico;Power BI;power bi;psql;rstudio;PSQL;RStudio;Tableau;tableau;
solution: Experience Platform
title: Verbinden von Clients mit dem Abfragedienst
description: In diesem Dokument wird erläutert, wie Sie eine Verbindung zum Abfrage-Service von einer Vielzahl von Desktop-Client-Anwendungen aus herstellen und diese Verbindungen überprüfen können.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 5e5a196074e844826579102fa6b36102c6481096
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 6%

---

# Clients mit dem Abfrage-Service verbinden

In diesem Abschnitt wird erläutert, wie Sie eine Verbindung zum Abfrage-Service von einer Vielzahl von Desktop-Client-Anwendungen aus herstellen und diese Verbindungen überprüfen. Der Abfrage-Service verwendet das PostgreSQL-Protokoll. Daher wird in den Anweisungen in diesem Abschnitt erläutert, wie Sie mit PostgreSQL-Tools und -Treibern Abfragen verbinden und schreiben können.

>[!IMPORTANT]
>
>Die TLS/SSL-Zertifikate in Produktionsumgebungen für die interaktive Postgres-API des Abfrage-Services wurden am Mittwoch, 24. Januar 2024 aktualisiert.<br>Dies ist zwar eine jährliche Anforderung, doch in diesem Fall hat sich auch das Stammzertifikat in der Kette geändert, da der TLS/SSL-Zertifikatanbieter von Adobe seine Zertifikatshierarchie aktualisiert hat. Dies kann sich auf bestimmte Postgres-Clients auswirken, wenn in ihrer Liste der Zertifizierungsstellen das Stammzertifikat fehlt. Beispielsweise müssen einem PSQL-CLI-Client die Stammzertifikate möglicherweise zu einer expliziten `~/postgresql/root.crt` hinzugefügt werden. Andernfalls kann dies zu einem Fehler führen, z. B. `psql: error: SSL error: certificate verify failed`. Weitere Informationen zu [ Problem finden Sie in ](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) offiziellen PostgreSQL-Dokumentation .<br>Das hinzuzufügende Stammzertifikat kann von [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem heruntergeladen ](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

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
>Als Power BI- und Tableau-Anwender können Sie Customer Journey Analytics mithilfe der auf der Registerkarte „Anmeldeinformationen für den Abfrage-Service“ bereitgestellten Anmeldeinformationen mit Ihren BI-Tools verbinden. Anleitungen zum Verbinden Ihrer BI-Tools mit Customer Journey Analytics finden [ in der Dokumentation zu Anmeldeinformationen ](../ui/credentials.md#connect-to-customer-journey-analytics).
