---
title: Erstellen eines Quell-Connectors für Google PubSub in der Benutzeroberfläche
description: Erfahren Sie, wie Sie einen Google PubSub-Quell-Connector in der Platform-Benutzeroberfläche erstellen.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: f56cdc2dc67f2d4820d80d8e5bdec8306d852891
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 79%

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
| Projekt-ID | Die zur Authentifizierung von [!DNL PubSub] erforderliche Projekt-ID. |
| Anmeldeinformationen | Die für die Authentifizierung von [!DNL PubSub] erforderliche Kennung der Anmeldeinformationen oder des privaten Schlüssels. |
| Themen-ID | Die ID für die [!DNL PubSub] -Ressource, die einen Feed von Nachrichten darstellt. Sie müssen eine Themen-ID angeben, wenn Sie Zugriff auf einen bestimmten Datenstrom in Ihrer [!DNL Google PubSub] -Quelle. |

Weitere Informationen zu diesen Werten finden Sie im folgenden Dokument [PubSub-Authentifizierung](https://cloud.google.com/pubsub/docs/authentication). Wenn Sie die auf dem Service-Account basierende Authentifizierung verwenden, lesen Sie das folgende [PubSub-Handbuch](https://cloud.google.com/docs/authentication/production#create_service_account), in dem die Schritte zum Generieren Ihrer Anmeldeinformationen beschrieben werden.

>[!TIP]
>
>Wenn Sie die auf Service-Konten basierende Authentifizierung verwenden, stellen Sie sicher, dass Sie einen ausreichenden Benutzerzugriff auf Ihr Service-Konto gewährt haben und dass in JSON keine zusätzlichen Leerzeichen vorhanden sind, wenn Sie Ihre Anmeldeinformationen kopieren und einfügen.

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL PubSub]-Konto mit Platform zu verknüpfen.

## Verbinden Ihres [!DNL PubSub]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können..

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud-Speicherplatz] die Option **[!UICONTROL Google PubSub]** und dann die Option **[!UICONTROL Daten hinzufügen]** aus.

![Katalog](../../../../images/tutorials/create/google-pubsub/catalog.png)

Die Seite **[!UICONTROL Verbinden mit Google PubSub]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL PubSub]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/google-pubsub/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** aus und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre [!DNL PubSub]-Anmeldeinformationen zur Authentifizierung für das Eingabeformular an. In diesem Schritt können Sie die Daten definieren, auf die Ihr Konto Zugriff hat, indem Sie eine Themen-ID angeben. Nur die mit dieser Themen-ID verknüpften Abonnements sind verfügbar.

>[!NOTE]
>
>einem öffentlichen Projekt zugewiesene Prinzipale (Rollen) werden in allen Themen und Abonnements übernommen, die innerhalb eines [!DNL PubSub] Projekt. Wenn Sie einen Prinzipal (eine Rolle) hinzufügen möchten, um Zugriff auf ein bestimmtes Thema zu erhalten, muss dieser Prinzipal (die Rolle) auch zum entsprechenden Abonnement des Themas hinzugefügt werden. Weitere Informationen finden Sie im Abschnitt [[!DNL PubSub] Dokumentation zur Zugriffskontrolle](https://cloud.google.com/pubsub/docs/access-control).

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![neu](../../../../images/tutorials/create/google-pubsub/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zwischen Ihrem [!DNL PubSub]-Konto und Platform hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Streaming-Daten aus Ihrem Cloud-Speicher in Platform zu übertragen](../../dataflow/streaming/cloud-storage-streaming.md).
