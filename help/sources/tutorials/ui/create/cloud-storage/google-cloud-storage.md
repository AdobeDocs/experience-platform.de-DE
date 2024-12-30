---
title: Erstellen einer Google Cloud Storage-Source-Verbindung über die Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Benutzeroberfläche von Adobe Experience Platform eine Google Cloud Storage-Quellverbindung erstellen.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 46%

---

# Erstellen eines Quell-Connectors für [!DNL Google Cloud Storage] in der Benutzeroberfläche

In diesem Tutorial finden Sie die Schritte zum Erstellen einer [!DNL Google Cloud Storage]-Quellverbindung mithilfe der Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Google Cloud Storage]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/batch/cloud-storage.md) fortfahren.

### Unterstützte Dateiformate

[!DNL Experience Platform] unterstützt die folgenden Dateiformate, die aus externen Speichern aufgenommen werden können:

* Durch Trennzeichen getrennte Werte (DSV): Jeder einzelne Zeichenwert kann als Trennzeichen für DSV-formatierte Datendateien verwendet werden.
* JavaScript Object Notation (JSON): JSON-formatierte Datendateien müssen XDM-kompatibel sein.
* Apache Parquet: Dateien im Parquet-Format müssen XDM-kompatibel sein.

### Sammeln erforderlicher Anmeldedaten

Um auf Ihre [!DNL Google Cloud Storage] in Platform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| Zugriffsschlüssel-ID | Eine 61-stellige alphanumerische Zeichenfolge, die zur Authentifizierung Ihres [!DNL Google Cloud Storage]-Kontos bei Platform verwendet wird. |
| Geheimer Zugriffsschlüssel | Eine mit Base-64 verschlüsselte Zeichenfolge mit 40 Zeichen, die zum Authentifizieren Ihres [!DNL Google Cloud Storage] bei Platform verwendet wird. |
| Behältername | Der Name Ihres [!DNL Google Cloud Storage]. Sie müssen einen Behälternamen angeben, wenn Sie Zugriff auf einen bestimmten Unterordner in Ihrem Cloud-Speicher gewähren möchten. |
| Ordnerpfad | Der Pfad zum Ordner, auf den Sie Zugriff gewähren möchten. |

Weitere Informationen zu diesen Werten finden Sie im Handbuch [HMAC-Schlüssel für Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Anweisungen zum Generieren Ihrer eigenen Zugriffsschlüssel-ID und Ihres geheimen Zugriffsschlüssels finden Sie in der [[!DNL Google Cloud Storage] Übersicht](../../../../connectors/cloud-storage/google-cloud-storage.md).

Nachdem Sie die erforderlichen Anmeldedaten zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL Google Cloud Storage]-Konto mit Platform zu verknüpfen.

## Verbinden Ihres [!DNL Google Cloud Storage]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud] die Option **[!UICONTROL Google Cloud-Speicher]** und dann **[!UICONTROL Daten hinzufügen]** aus.

![Der Bildschirm der Platform-Benutzeroberfläche mit der Seite „Quellkatalog“.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

Die **[!UICONTROL Verbindung zum Google Cloud-Speicher herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Google Cloud Storage] Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![Der Bildschirm der Platform-Benutzeroberfläche mit der bestehenden Kontoseite für eine Google Cloud-Speicherquelle](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### Neues Konto

Wenn Sie neue Anmeldedaten verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Eingabeformular einen Namen, eine optionale Beschreibung und Ihre [!DNL Google Cloud Storage] Anmeldeinformationen ein. In diesem Schritt können Sie auch die Unterordner festlegen, auf die Ihr Konto Zugriff haben soll, indem Sie den Namen des Pfads zum Unterordner definieren.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Der Bildschirm der Platform-Benutzeroberfläche mit der neuen Kontoseite für eine Google Cloud-Speicherquelle.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Google Cloud Storage]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten aus Ihrem Cloud-Speicher in Platform zu übertragen](../../dataflow/batch/cloud-storage.md).
