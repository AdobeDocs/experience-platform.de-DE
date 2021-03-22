---
keywords: Experience Platform;Home;beliebte Themen;Google Cloud-Datenspeicherung;Google Cloud-Datenspeicherung;GCS;Gcs
solution: Experience Platform
title: Erstellen einer Google Cloud-Datenspeicherung-Quellverbindung in der Benutzeroberfläche
topic: Übersicht
type: Tutorial
description: Erfahren Sie, wie Sie eine Google Cloud-Datenspeicherung-Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche erstellen.
translation-type: tm+mt
source-git-commit: f6a63ca1e21b3c3f6a55574f31fdf04038b7e5c4
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 8%

---


# Erstellen einer [!DNL Google Cloud Storage]-Quellverbindung in der Benutzeroberfläche

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. In diesem Lernprogramm werden Schritte zum Erstellen eines [!DNL Google Cloud Storage] (im Folgenden &quot;GCS&quot; genannt) Quell-Connectors mithilfe der [!DNL Platform]-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über eine gültige GCS-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial [Konfigurieren eines Datenflusses](../../dataflow/batch/cloud-storage.md) fortfahren.

### Unterstützte Dateiformate

[!DNL Experience Platform] unterstützt die folgenden Dateiformate, die von externen Datenspeicherung erfasst werden:

* Trennzeichen-getrennte Werte (DSV): Die Unterstützung für DSV-formatierte Datendateien ist derzeit auf kommagetrennte Werte beschränkt. Der Wert von Feldkopfzeilen in DSV-formatierten Dateien darf nur aus alphanumerischen Zeichen und Unterstrichen bestehen. Die Unterstützung für allgemeine DSV-Dateien wird in Zukunft bereitgestellt.
* JavaScript Object Notation (JSON): JSON-formatierte Datendateien müssen XDM-kompatibel sein.
* Apache Parquet: Parquet-formatierte Datendateien müssen XDM-konform sein.

### Erforderliche Anmeldedaten sammeln

Um auf Ihre GCS-Daten auf [!DNL Platform] zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| Schlüssel-ID aufrufen | Eine 61-stellige, alphanumerische Zeichenfolge, mit der Ihr [!DNL Google Cloud Storage]-Konto für Platform authentifiziert wird. |
| Geheimer Zugriffsschlüssel | Eine 40-stellige Base-64-kodierte Zeichenfolge, mit der Ihr [!DNL Google Cloud Storage]-Konto für Platform authentifiziert wird. |

Weitere Informationen zu diesen Werten finden Sie im Handbuch [Google Cloud-Datenspeicherung HMAC-Schlüssel](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Anweisungen zum Generieren Ihrer eigenen Zugriffsschlüssel-ID und des geheimen Zugriffsschlüssels finden Sie im Abschnitt [[!DNL Google Cloud Storage] overview](../../../../connectors/cloud-storage/google-cloud-storage.md).

## Verbinden Sie Ihr [!DNL Google Cloud Storage]-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihr GCS-Konto mit [!DNL Platform] zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Reihe von Quellen an, für die Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Datenbanken]** **[!UICONTROL Google Cloud-Datenspeicherung]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen GCS-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

Die Seite **[!UICONTROL Mit Google Cloud-Datenspeicherung verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im eingeblendeten Eingabefeld einen Namen, eine optionale Beschreibung und Ihre GCS-Anmeldeinformationen ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbinden]** und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![connect](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das GCS-Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![existing](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem GCS-Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrer Cloud-Datenspeicherung in [!DNL Platform]](../../dataflow/batch/cloud-storage.md) zu übertragen.