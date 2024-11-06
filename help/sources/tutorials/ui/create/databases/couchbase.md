---
keywords: Experience Platform;home;popular topics;Couchbase;couchbase
solution: Experience Platform
title: Erstellen einer Couchbase Source-Verbindung in der Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung von Couchbase erstellen.
exl-id: 4270a48a-843c-4f1e-b280-35b620581d68
source-git-commit: 0781d04af12c4c11dfc917adfdec8673cf3be8de
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 50%

---

# Erstellen eines Quell-Connectors für [!DNL Couchbase] in der Benutzeroberfläche

>[!IMPORTANT]
>
>Die Quelle [!DNL Couchbase] wird Ende Mai 2025 nicht mehr unterstützt. Sie können die [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md) anstelle der [!DNL Couchbase]-Quelle verwenden.

Source-Connectoren in [!DNL Adobe Experience Platform] bieten die Möglichkeit, extern bezogene Daten planmäßig zu erfassen. In diesem Tutorial werden die Schritte zum Erstellen eines Quell-Connectors für [!DNL Couchbase] mithilfe der Benutzeroberfläche von [!DNL Platform] beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von [!DNL Platform] voraus.

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Couchbase]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/databases.md) fortfahren.

### Sammeln erforderlicher Anmeldedaten

Um den Quell-Connector [!DNL Couchbase] zu authentifizieren, müssen Sie Werte für die folgende Verbindungseigenschaft angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die Verbindungszeichenfolge, die für die Verbindung mit Ihrer [!DNL Couchbase]-Instanz verwendet wird. Das Verbindungszeichenfolgenmuster für [!DNL Couchbase] ist `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Weitere Informationen zum Erwerb einer Verbindungszeichenfolge finden Sie in der Dokumentation zu [[!DNL Couchbase] connection](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |

## Verbinden Ihres [!DNL Couchbase]-Kontos

Nachdem Sie die erforderlichen Anmeldedaten erfasst haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Couchbase]-Konto mit [!DNL Platform] zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste **[!UICONTROL Quellen]** aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Datenbanken]** die Option **[!UICONTROL Couchbase]** aus. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]** aus. Klicken Sie andernfalls auf **[!UICONTROL Daten hinzufügen]** , um einen neuen [!DNL Couchbase]-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/couchbase/catalog.png)

Die Seite **[!UICONTROL Mit Couchbase verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto

Wenn Sie neue Anmeldedaten verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Namen, eine optionale Beschreibung und Ihre [!DNL Couchbase]-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![connect](../../../../images/tutorials/create/couchbase/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das Konto [!DNL Couchbase] aus, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann oben rechts auf **[!UICONTROL Weiter]** , um fortzufahren.

![vorhanden](../../../../images/tutorials/create/couchbase/existing.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Couchbase]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen Datenfluss [konfigurieren, um Daten in  [!DNL Platform]](../../dataflow/databases.md) zu übertragen.
