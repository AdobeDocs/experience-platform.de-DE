---
keywords: Experience Platform;Home;beliebte Themen;Snowflake
title: Snowflake-Quellverbindung in der Benutzeroberfläche erstellen
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie eine Snowflake-Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche erstellen.
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 76b3e3e9bcb27eb2bd6981ae6eb109410ae16336
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 10%

---

# Erstellen Sie eine [!DNL Snowflake] Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
> Die [!DNL Snowflake] Stecker befindet sich in Beta. Siehe [Quellübersicht](../../../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-gekennzeichneten Steckverbindern.

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Snowflake] Quellanschluss über die Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu kennzeichnen und zu verbessern, indem Sie [!DNL Platform] Dienstleistungen.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Erforderliche Anmeldedaten sammeln

Um auf Ihr Snowflake-Konto zuzugreifen auf [!DNL Platform], müssen Sie den folgenden Authentifizierungswert angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| Konto | Der vollständige Kontoname, der Ihrem [!DNL Snowflake] Konto. Eine vollqualifizierte [!DNL Snowflake] Der Kontoname enthält Ihren Kontonamen, Ihre Region und Ihre Cloud-Plattform. Beispiel: `cj12345.east-us-2.azure`. Weitere Informationen zu Kontonamen finden Sie in dieser [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| Warehouse | Die [!DNL Snowflake] warehouse verwaltet den Ausführungsprozess der Abfrage für die Anwendung. Jeden [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss einzeln aufgerufen werden, wenn Daten an Platform übertragen werden. |
| Datenbank | Die [!DNL Snowflake] -Datenbank enthält die Daten, die Sie zur Übertragung der Plattform benötigen. |
| Benutzername | Der Benutzername für [!DNL Snowflake] Konto. |
| Passwort | Das Kennwort für die [!DNL Snowflake] Benutzerkonto. |
| Verbindungszeichenfolge | Die Verbindungszeichenfolge, die für die Verbindung mit Ihrem [!DNL Snowflake] Instanz. Das Muster der Verbindungszeichenfolge für [!DNL Snowflake] ist `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |

Weitere Informationen zu diesen Werten finden Sie unter [dieses Snowflake-Dokument](https://docs.snowflake.com/en/user-guide/oauth-custom.html).

## Snowflake-Konto verbinden

Wählen Sie in der Plattform-Benutzeroberfläche **[!UICONTROL Quellen]** von der linken Navigation aus, um auf [!UICONTROL Quellen] Arbeitsbereich. Die [!UICONTROL Katalog] zeigt eine Reihe von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie aus dem Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die Quelle finden, an der Sie arbeiten möchten, indem Sie die Suchleiste verwenden.

Im Rahmen der [!UICONTROL Datenbanken] Kategorie, auswählen **[!UICONTROL Snowflake]** und wählen Sie dann **[!UICONTROL Daten Hinzufügen]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

Die **[!UICONTROL Mit Snowflake verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein bestehendes Konto zu verbinden, wählen Sie das Snowflake, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Weiter]** um fortzufahren.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Neues Konto

Wenn Sie neue Anmeldedaten verwenden, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im angezeigten Eingabefeld einen Namen, eine optionale Beschreibung und Ihre Snowflake-Anmeldedaten ein. Wählen Sie nach Beendigung **[!UICONTROL Verbinden]** und dann etwas Zeit für die Einrichtung der neuen Verbindung.

![](../../../../images/tutorials/create/snowflake/new.png)

## Nächste Schritte

Durch Befolgen dieses Tutorials haben Sie eine Verbindung zu Ihrem Snowflake-Konto hergestellt. Sie können nun mit dem nächsten Tutorial fortfahren und [Dataflow konfigurieren, um Daten in [!DNL Platform]](../../dataflow/databases.md).
