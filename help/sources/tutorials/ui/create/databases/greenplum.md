---
keywords: Experience Platform; Startseite; beliebte Themen; Greenplum; Greenplum
solution: Experience Platform
title: Erstellen einer GreenPlum-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine GreenPlum-Quellverbindung erstellen.
exl-id: e6c6a495-25ce-4497-b20e-91374c7bb548
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 12%

---

# Erstellen einer [!DNL GreenPlum]-Quellverbindung in der Benutzeroberfläche

Quell-Connectoren in Adobe Experience Platform bieten die Möglichkeit, extern bezogene Daten auf geplanter Basis zu erfassen. Dieses Tutorial enthält Schritte zum Erstellen eines Quell-Connectors [!DNL GreenPlum] mithilfe der [!DNL Platform]-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) zum Schema Editor: Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL GreenPlum]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Konfigurieren eines Datenflusses [fortfahren.](../../dataflow/databases.md)

### Erforderliche Anmeldedaten sammeln

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine Verbindung zu [!DNL GreenPlum] herstellen zu können.

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die Verbindungszeichenfolge, die für die Verbindung mit Ihrer [!DNL GreenPlum]-Instanz verwendet wird. Das Verbindungszeichenfolgenmuster für [!DNL GreenPlum] ist `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem GreenPlum-Dokument](https://gpdb.docs.pivotal.io/580/security-guide/topics/Authenticate.html#topic_fzv_wb2_jr__config_ssl_client_conn).

## Ihr [!DNL GreenPlum]-Konto verbinden

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL GreenPlum]-Konto mit [!DNL Platform] zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** aus der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** enthält eine Vielzahl von Quellen, für die Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Datenbanken]** die Option **[!UICONTROL GreenPlum]** aus. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]** aus. Klicken Sie andernfalls auf **[!UICONTROL Daten hinzufügen]** , um einen neuen [!DNL GreenPlum]-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/greenplum/catalog.png)

Die Seite **[!UICONTROL Verbindung zu GreenPlum]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldedaten verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Namen, eine optionale Beschreibung und Ihre [!DNL GreenPlum]-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![connect](../../../../images/tutorials/create/greenplum/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL GreenPlum]-Konto aus, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann in der oberen rechten Ecke auf **[!UICONTROL Weiter]** , um fortzufahren.

![vorhandene](../../../../images/tutorials/create/greenplum/existing.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL GreenPlum]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in [!DNL Platform]](../../dataflow/databases.md) zu übertragen.
