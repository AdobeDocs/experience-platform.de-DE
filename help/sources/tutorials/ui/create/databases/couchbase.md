---
keywords: Experience Platform;Home;beliebte Themen;Couchbase;Couchbase
solution: Experience Platform
title: Erstellen einer Couchbase-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie eine Quellverbindung für Couchbase mithilfe der Adobe Experience Platform-Benutzeroberfläche erstellen.
exl-id: 4270a48a-843c-4f1e-b280-35b620581d68
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 6%

---

# Erstellen einer [!DNL Couchbase]-Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
> Der [!DNL Couchbase]-Anschluss befindet sich in der Betaversion. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../../../home.md#terms-and-conditions).

Quellschnittstellen in [!DNL Adobe Experience Platform] bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Erstellen eines [!DNL Couchbase]-Quellconnectors mithilfe der [!DNL Platform]-Benutzeroberfläche.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten von [!DNL Platform]:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Couchbase]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial [Konfigurieren eines Datenniedrig](../../dataflow/databases.md) fortfahren.

### Erforderliche Anmeldedaten sammeln

Um den [!DNL Couchbase]-Quellanschluss zu authentifizieren, müssen Sie Werte für die folgende Verbindungseigenschaft angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die Verbindungszeichenfolge, mit der eine Verbindung zu Ihrer [!DNL Couchbase]-Instanz hergestellt wird. Das Verbindungszeichenfolgen-Muster für [!DNL Couchbase] ist `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Weitere Informationen zum Abrufen einer Verbindungszeichenfolge finden Sie in der Dokumentation zu [[!DNL Couchbase] connection](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |

## Verbinden Sie Ihr [!DNL Couchbase]-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL Couchbase]-Konto mit [!DNL Platform] zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Reihe von Quellen an, für die Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Datenbanken]** **[!UICONTROL Couchbase]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen [!DNL Couchbase]-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/couchbase/catalog.png)

Die Seite **[!UICONTROL Mit Couchbase verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im eingeblendeten Eingabeformular einen Namen, eine optionale Beschreibung und Ihre [!DNL Couchbase]-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und lassen Sie dann etwas Zeit für die Einrichtung der neuen Verbindung zu.

![connect](../../../../images/tutorials/create/couchbase/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Couchbase]-Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann in der oberen rechten Ecke auf **[!UICONTROL Weiter]**, um fortzufahren.

![existing](../../../../images/tutorials/create/couchbase/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Couchbase]-Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und [einen Datendurchlauf konfigurieren, um Daten in [!DNL Platform]](../../dataflow/databases.md) zu übertragen.
