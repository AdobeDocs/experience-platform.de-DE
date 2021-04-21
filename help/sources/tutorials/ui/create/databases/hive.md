---
keywords: Experience Platform;Home;beliebte Themen;Apache-Hive;Azurblaue HDInsights;Azure-Hdinsights
solution: Experience Platform
title: Erstellen eines Apache Hive auf der Azurblauen HDInsights-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie eine Apache Hive auf Azurblaus HDInsights-Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche erstellen.
exl-id: 3eb3cb02-9867-451a-b847-ab895310eedf
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 9%

---

# Erstellen einer [!DNL Apache Hive]-Quellverbindung in der Benutzeroberfläche[!DNL Azure HDInsights]

>[!NOTE]
>
> Der [!DNL Apache Hive] auf [!DNL Azure HDInsights] Connector befindet sich in der Beta-Version. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../../../home.md#terms-and-conditions).

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Erstellen eines [!DNL Apache Hive] auf [!DNL Azure HDInsights]-Quellanschluss mithilfe der [!DNL Platform]-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Hive]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial [Konfigurieren eines Datenflusses](../../dataflow/databases.md) fortfahren

### Erforderliche Anmeldedaten sammeln

Um auf Ihr [!DNL Hive]-Konto bei [!DNL Platform] zuzugreifen, müssen Sie die folgenden Werte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Die IP-Adresse oder der Hostname des [!DNL Hive]-Servers. |
| `username` | Der Benutzername, mit dem Sie auf den [!DNL Hive]-Server zugreifen. |
| `password` | Das dem Benutzer zugeordnete Kennwort. |

Weitere Informationen zum Einstieg finden Sie unter [this [!DNL Hive] Dokument](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted).

## Verbinden Sie Ihr [!DNL Hive]-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL Hive]-Konto mit [!DNL Platform] zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Reihe von Quellen an, für die Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Datenbanken]** **[!UICONTROL Ausblenden]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen [!DNL Hive]-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/hive/catalog.png)

Die Seite **[!UICONTROL Mit Hive]** verbinden wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im eingeblendeten Eingabeformular einen Namen, eine optionale Beschreibung und Ihre [!DNL Hive]-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![connect](../../../../images/tutorials/create/hive/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Hive]-Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![existing](../../../../images/tutorials/create/hive/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Hive]-Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und [einen Datendurchlauf konfigurieren, um Daten in [!DNL Platform]](../../dataflow/databases.md) zu übertragen.
