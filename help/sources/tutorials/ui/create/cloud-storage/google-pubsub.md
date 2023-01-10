---
keywords: Experience Platform;Startseite;beliebte Themen;Google PubSub;google pubsub
solution: Experience Platform
title: Erstellen eines Quell-Connectors für Google PubSub in der Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie einen Google PubSub-Quell-Connector in der Platform-Benutzeroberfläche erstellen.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 100%

---

# Erstellen eines Quell-Connectors für [!DNL Google PubSub] in der Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Google PubSub] (nachstehend „[!DNL PubSub]“ genannt) in der Benutzeroberfläche von Platform beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Wenn Sie bereits über eine gültige [!DNL PubSub]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/batch/cloud-storage.md) fortfahren.

### Sammeln erforderlicher Anmeldeinformationen

Um eine Verbindung von [!DNL PubSub] mit Platform herzustellen, müssen Sie einen gültigen Wert für die folgenden Anmeldeinformationen angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `projectId` | Die zum Authentifizieren von [!DNL PubSub] erforderliche Projekt-ID. |
| `credentials` | Die für die Authentifizierung von [!DNL PubSub] erforderliche Kennung der Anmeldeinformationen oder des privaten Schlüssels. |

Weitere Informationen zu diesen Werten finden Sie im folgenden Dokument [PubSub-Authentifizierung](https://cloud.google.com/pubsub/docs/authentication). Wenn Sie die auf dem Service-Account basierende Authentifizierung verwenden, lesen Sie das folgende [PubSub-Handbuch](https://cloud.google.com/docs/authentication/production#create_service_account), in dem die Schritte zum Generieren Ihrer Anmeldeinformationen beschrieben werden.

>[!TIP]
>
>Wenn Sie die auf Service-Konten basierende Authentifizierung verwenden, stellen Sie sicher, dass Sie einen ausreichenden Benutzerzugriff auf Ihr Service-Konto gewährt haben und dass in JSON keine zusätzlichen Leerzeichen vorhanden sind, wenn Sie Ihre Anmeldeinformationen kopieren und einfügen.

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL PubSub]-Konto mit Platform zu verknüpfen.

## Verbinden Sie Ihr [!DNL PubSub]-Konto

Wählen Sie in der [Platform-Benutzeroberfläche](https://platform.adobe.com) in der linken Navigationsleiste **[!UICONTROL Quellen]** aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud-Speicherplatz] die Option **[!UICONTROL Google PubSub]** und dann die Option **[!UICONTROL Daten hinzufügen]** aus.

![Katalog](../../../../images/tutorials/create/google-pubsub/catalog.png)

Die Seite **[!UICONTROL Verbinden mit Google PubSub]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL PubSub]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/google-pubsub/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** aus und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre [!DNL PubSub]-Anmeldeinformationen zur Authentifizierung für das Eingabeformular an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbindung mit Quelle herstellen]** und warten Sie dann einige Zeit, bis die neue Verbindung hergestellt ist.

![neu](../../../../images/tutorials/create/google-pubsub/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zwischen Ihrem [!DNL PubSub]-Konto und Platform hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Streaming-Daten aus Ihrem Cloud-Speicher in Platform zu übertragen](../../dataflow/streaming/cloud-storage-streaming.md).
