---
keywords: Experience Platform;Home;beliebte Themen;Phoenix;Phoenix
solution: Experience Platform
title: Erstellen einer Phoenix-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie eine Phoenix-Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche erstellen.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 8%

---

# Erstellen einer [!DNL Phoenix]-Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
> Der [!DNL Phoenix]-Anschluss befindet sich in der Betaversion. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../../../home.md#terms-and-conditions).

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Erstellen eines [!DNL Phoenix]-Quellconnectors mithilfe der [!DNL Platform]-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Phoenix]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial [Konfigurieren eines Datenflusses](../../dataflow/databases.md) fortfahren

### Erforderliche Anmeldedaten sammeln

Um auf Ihr [!DNL Phoenix]-Konto bei [!DNL Platform] zuzugreifen, müssen Sie die folgenden Werte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Die IP-Adresse oder der Hostname des [!DNL Phoenix]-Servers. |
| `port` | Der TCP-Anschluss, den der [!DNL Phoenix]-Server verwendet, um auf Clientverbindungen zu warten. Wenn Sie eine Verbindung zu [!DNL Azure HDInsights] herstellen, geben Sie den Anschluss als 443 an. |
| `httpPath` | Die Teil-URL, die dem [!DNL Phoenix]-Server entspricht. Geben Sie /hbasephoenix0 an, wenn Sie den [!DNL Azure HDInsights]-Cluster verwenden. |
| `username` | Der Benutzername, mit dem Sie auf den [!DNL Phoenix]-Server zugreifen. |
| `password` | Das dem Benutzer zugeordnete Kennwort. |
| `enableSsl` | Ein Umschalter, der angibt, ob die Verbindungen zum Server mit SSL verschlüsselt werden. |

Weitere Informationen zum Einstieg finden Sie unter [this [!DNL Phoenix] Dokument](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

## Verbinden Sie Ihr [!DNL Phoenix]-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL Phoenix]-Konto für die Verbindung mit [!DNL Platform] zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Reihe von Quellen an, für die Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Datenbanken]** **[!UICONTROL Phoenix]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um ein neues [!DNL Phoenix]-Konto zu erstellen.

![Katalog](../../../../images/tutorials/create/phoenix/catalog.png)

Die Seite **[!UICONTROL Verbindung zu Phoenix]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im eingeblendeten Eingabeformular einen Namen, eine optionale Beschreibung und Ihre [!DNL Phoenix]-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![connect](../../../../images/tutorials/create/phoenix/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Phoenix]-Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![existing](../../../../images/tutorials/create/phoenix/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Phoenix]-Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und [einen Datendurchlauf konfigurieren, um Daten in [!DNL Platform]](../../dataflow/databases.md) zu übertragen.
