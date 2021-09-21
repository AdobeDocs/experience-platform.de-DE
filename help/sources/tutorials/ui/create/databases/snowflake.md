---
keywords: Experience Platform; Homepage; beliebte Themen; Snowflake
title: Erstellen einer Snowflake-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Snowflake-Quellverbindung erstellen.
source-git-commit: 2e717f33b487430220bd3bb7812558cde81d8852
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 10%

---

# Erstellen einer [!DNL Snowflake]-Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
> Der Connector [!DNL Snowflake] befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren finden Sie unter [Quellen - Übersicht](../../../../home.md#terms-and-conditions) .

In diesem Tutorial werden die Schritte zum Erstellen eines Quell-Connectors [!DNL Snowflake] mithilfe der Adobe Experience Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Platform voraus:

* [Quellen](../../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Erforderliche Anmeldedaten sammeln

Um auf Ihr Snowflake-Konto auf [!DNL Platform] zugreifen zu können, müssen Sie den folgenden Authentifizierungswert angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| Konto | Das [!DNL Snowflake]-Konto, das Sie mit Platform verbinden möchten. |
| Warehouse | Das [!DNL Snowflake]-Warehouse verwaltet den Abfrageausführungsprozess für die Anwendung. Jedes [!DNL Snowflake]-Warehouse ist unabhängig voneinander und muss einzeln aufgerufen werden, wenn Daten an Platform übermittelt werden. |
| Datenbank | [!DNL Snowflake] enthält die Daten, die Sie an die Plattform übermitteln möchten. |
| Benutzername | Der Benutzername für das [!DNL Snowflake]-Konto. |
| Passwort | Das Kennwort für das [!DNL Snowflake]-Benutzerkonto. |
| Verbindungszeichenfolge | Die Verbindungszeichenfolge, die für die Verbindung mit Ihrer [!DNL Snowflake]-Instanz verwendet wird. Das Verbindungszeichenfolgen-Muster für [!DNL Snowflake] ist `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |

Weitere Informationen zu diesen Werten finden Sie in [diesem Snowflake document](https://docs.snowflake.com/en/user-guide/oauth-custom.html).

## Snowflake-Konto verbinden

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Quellen]** aus dem linken Navigationsbereich aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] enthält eine Vielzahl von Quellen, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle über die Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Datenbanken] die Option **[!UICONTROL Snowflake]** und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

Die Seite **[!UICONTROL Mit Snowflake verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein bestehendes Snowflake zu verbinden, wählen Sie das Konto aus, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Neues Konto

Wenn Sie neue Anmeldedaten verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Namen, eine optionale Beschreibung und Ihre Snowflake-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![](../../../../images/tutorials/create/snowflake/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem Snowflake-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in [!DNL Platform]](../../dataflow/databases.md) zu übertragen.
