---
keywords: Experience Platform; Homepage; beliebte Themen; Snowflake
title: Erstellen einer Snowflake-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Snowflake-Quellverbindung erstellen.
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: ac7910c971fbedf3afebd87633f814d597260cae
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 10%

---

# Erstellen Sie eine [!DNL Snowflake] Quellverbindung in der Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Snowflake] Quell-Connector über die Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu beschriften und zu erweitern, indem Sie [!DNL Platform] Dienste.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Erforderliche Anmeldedaten sammeln

Um auf Ihr Snowflake-Konto zuzugreifen, klicken Sie auf [!DNL Platform]müssen Sie den folgenden Authentifizierungswert angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| Konto | Der vollständige Kontoname, der mit Ihrem [!DNL Snowflake] -Konto. Eine vollqualifizierte [!DNL Snowflake] Der Kontoname enthält Ihren Kontonamen, Ihre Region und Ihre Cloud-Plattform. Beispiel: `cj12345.east-us-2.azure`. Weiterführende Informationen zu Kontonamen finden Sie in diesem [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| Warehouse | Die [!DNL Snowflake] Warehouse verwaltet den Prozess der Ausführung der Abfrage für die Anwendung. Jeder [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss einzeln aufgerufen werden, wenn Daten an Platform übermittelt werden. |
| Datenbank | Die [!DNL Snowflake] -Datenbank enthält die Daten, die Sie an Platform übermitteln möchten. |
| Benutzername | Der Benutzername für die [!DNL Snowflake] -Konto. |
| Passwort | Das Kennwort für die [!DNL Snowflake] Benutzerkonto. |
| Verbindungszeichenfolge | Die Verbindungszeichenfolge, über die die Verbindung zu Ihrem [!DNL Snowflake] -Instanz. Das Verbindungszeichenfolgenmuster für [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

Weitere Informationen zu diesen Werten finden Sie unter [Dieses Snowflake-Dokument](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

## Snowflake-Konto verbinden

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** über die linke Navigationsleiste auf [!UICONTROL Quellen] Arbeitsbereich. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle über die Suchleiste finden.

Unter dem [!UICONTROL Datenbanken] category, select **[!UICONTROL Snowflake]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

Die **[!UICONTROL Mit Snowflake verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein bestehendes Konto zu verbinden, wählen Sie das Snowflake-Konto aus, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Nächste]** um fortzufahren.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im angezeigten Formular einen Namen, eine optionale Beschreibung und Ihre Snowflake-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und dann etwas Zeit für die Einrichtung der neuen Verbindung.

![](../../../../images/tutorials/create/snowflake/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem Snowflake-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in [!DNL Platform]](../../dataflow/databases.md).
