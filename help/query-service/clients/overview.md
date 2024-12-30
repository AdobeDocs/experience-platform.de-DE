---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;verbinden;mit Abfrage-Service verbinden;aqua data studio;Aqua Data Studio;Looker;Looker;Postico;postico;Power BI;power bi;psql;rstudio;PSQL;RStudio;Tableau;tableau;
solution: Experience Platform
title: Verbinden von Clients mit dem Abfragedienst
description: In diesem Dokument wird erläutert, wie Sie eine Verbindung zum Abfrage-Service von einer Vielzahl von Desktop-Client-Anwendungen aus herstellen und diese Verbindungen überprüfen können.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 5%

---

# Clients mit [!DNL Query Service] verbinden

In diesem Abschnitt wird beschrieben, wie Sie eine Verbindung zu [!DNL Query Service] von einer Vielzahl von Desktop-Client-Anwendungen aus herstellen und diese Verbindungen überprüfen. [!DNL Query Service] verwendet das [!DNL PostgreSQL]. In den Anweisungen in diesem Abschnitt wird daher erläutert, wie Sie [!DNL PostgreSQL] Tools und Treiber verwenden können, um Abfragen zu verbinden und zu schreiben.

>[!IMPORTANT]
>
>Die TLS/SSL-Zertifikate in Produktionsumgebungen für die interaktive Postgres-API des Abfrage-Services wurden am Mittwoch, 24. Januar 2024 aktualisiert.<br>Obwohl dies eine jährliche Anforderung ist, hat sich in diesem Fall auch das Stammzertifikat in der Kette geändert, da die Zertifikatanbieter von Adobe TLS/SSL ihre Zertifikatshierarchie aktualisiert haben. Dies kann sich auf bestimmte Postgres-Clients auswirken, wenn in ihrer Liste der Zertifizierungsstellen das Stammzertifikat fehlt. Beispielsweise müssen einem PSQL-CLI-Client die Stammzertifikate möglicherweise zu einer expliziten `~/postgresql/root.crt` hinzugefügt werden, da dies sonst zu einem Fehler führen kann. Beispiel: `psql: error: SSL error: certificate verify failed`. Weitere Informationen zu [ Problem finden Sie in ](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) offiziellen PostgreSQL-Dokumentation .<br>Das hinzuzufügende Stammzertifikat kann von [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem heruntergeladen ](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

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
>Als Power BI- und Tableau-Anwender können Sie Customer Journey Analytics über die Registerkarte Anmeldeinformationen des Abfrage-Service mit Ihren BI-Tools verbinden. Anleitungen zum Verbinden (Verbinden [ BI-Tools mit dem Customer Journey Analytics) finden Sie in der Dokumentation ](../ui/credentials.md#connect-to-customer-journey-analytics) Anmeldedaten .
