---
keywords: Experience Platform;Home;beliebte Themen;FTP;FTP
solution: Experience Platform
title: Erstellen einer FTP-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie eine FTP-Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche erstellen.
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 10%

---

# Erstellen einer FTP-Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
>Der FTP-Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../../../home.md#terms-and-conditions).

In diesem Lernprogramm werden Schritte zum Erstellen einer FTP-Quellverbindung mithilfe der Adobe Experience Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige FTP-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial [Konfigurieren eines Datenflusses](../../dataflow/batch/cloud-storage.md) fortfahren.

### Erforderliche Anmeldedaten sammeln

Um eine Verbindung mit FTP herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Der Name oder die IP-Adresse, die mit Ihrem FTP-Server verknüpft ist. |
| `username` | Der Benutzername mit Zugriff auf Ihren FTP-Server. |
| `password` | Das Kennwort für Ihren FTP-Server. |

## Verbindung zum FTP-Server herstellen

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues FTP-Konto für die Verbindung mit der Plattform zu erstellen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Reihe von Quellen an, für die Sie ein eingehendes Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud-Datenspeicherung] **[!UICONTROL FTP]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um eine neue FTP-Verbindung zu erstellen.

![Katalog](../../../../images/tutorials/create/ftp/catalog.png)

Die Seite **[!UICONTROL Verbindung mit FTP]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im eingeblendeten Eingabefeld einen Namen, eine optionale Beschreibung und Ihre Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![new](../../../../images/tutorials/create/ftp/new.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das FTP-Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![existing](../../../../images/tutorials/create/ftp/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem FTP-Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in Platform](../../dataflow/batch/cloud-storage.md) zu übertragen.
