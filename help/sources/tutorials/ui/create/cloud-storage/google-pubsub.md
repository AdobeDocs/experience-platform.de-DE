---
title: Erstellen einer Google PubSub-Source-Verbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Experience Platform-Benutzeroberfläche einen Quell-Connector für Google PubSub erstellen.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 24%

---

# Erstellen eines Quell-Connectors für [!DNL Google PubSub] in der Benutzeroberfläche

>[!IMPORTANT]
>
>Die [!DNL Google PubSub] ist im Quellkatalog für Benutzende verfügbar, die Real-Time Customer Data Platform Ultimate erworben haben.

In diesem Tutorial finden Sie die Schritte zum Erstellen eines [!DNL Google PubSub] (im Folgenden als &quot;[!DNL PubSub]&quot; bezeichnet) mithilfe der Benutzeroberfläche von Experience Platform.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Wenn Sie bereits über eine gültige [!DNL PubSub]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/batch/cloud-storage.md) fortfahren.

### Sammeln erforderlicher Anmeldedaten

Sie müssen Werte für die unten beschriebenen Verbindungseigenschaften angeben, um Ihr [!DNL PubSub]-Konto mit Experience Platform zu verbinden. Weitere Informationen zur Authentifizierung und zur Einrichtung vorausgesetzter Komponenten finden Sie unter [[!DNL PubSub source] Übersicht](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).


>[!BEGINTABS]

>[!TAB Projektbasierte Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| Projekt-ID | Die zur Authentifizierung von [!DNL PubSub] erforderliche Projekt-ID. |
| Anmeldedaten | Die zum Authentifizieren von [!DNL PubSub] erforderlichen Anmeldedaten. Sie müssen sicherstellen, dass Sie die vollständige JSON-Datei ablegen, nachdem Sie die Leerzeichen aus Ihren Anmeldeinformationen entfernt haben. |

>[!TAB Topic- und abonnementbasierte Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| Anmeldedaten | Die zum Authentifizieren von [!DNL PubSub] erforderlichen Anmeldedaten. Sie müssen sicherstellen, dass Sie die vollständige JSON-Datei ablegen, nachdem Sie die Leerzeichen aus Ihren Anmeldeinformationen entfernt haben. |
| Themenname | Der Name Ihres [!DNL PubSub]. In [!DNL PubSub] können Sie mit Abonnements Nachrichten empfangen, indem Sie das Thema abonnieren, in dem Nachrichten veröffentlicht wurden. **Hinweis**: Ein einzelnes [!DNL PubSub] kann nur für einen Datenfluss verwendet werden. Um mehrere Datenflüsse durchzuführen, müssen Sie über mehrere Abonnements verfügen. |
| Abonnementname | Der Name Ihres [!DNL PubSub]. In [!DNL PubSub] können Sie mit Abonnements Nachrichten empfangen, indem Sie das Thema abonnieren, in dem Nachrichten veröffentlicht wurden. |

>[!ENDTABS]

Weitere Informationen zu diesen Werten finden Sie im folgenden Dokument [PubSub-Authentifizierung](https://cloud.google.com/pubsub/docs/authentication). Wenn Sie die auf dem Service-Account basierende Authentifizierung verwenden, lesen Sie das folgende [PubSub-Handbuch](https://cloud.google.com/docs/authentication/production#create_service_account), in dem die Schritte zum Generieren Ihrer Anmeldedaten beschrieben werden.

>[!TIP]
>
>Wenn Sie die auf Service-Konten basierende Authentifizierung verwenden, stellen Sie sicher, dass Sie einen ausreichenden Benutzerzugriff auf Ihr Service-Konto gewährt haben und dass in JSON keine zusätzlichen Leerzeichen vorhanden sind, wenn Sie Ihre Anmeldedaten kopieren und einfügen.

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL PubSub]-Konto mit Experience Platform zu verknüpfen.

## Verbinden Ihres [!DNL PubSub]-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud-Speicherplatz] die Option **[!UICONTROL Google PubSub]** und dann die Option **[!UICONTROL Daten hinzufügen]** aus.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche.](../../../../images/tutorials/create/google-pubsub/catalog.png)

Die Seite **[!UICONTROL Verbinden mit Google PubSub]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL PubSub]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![Die Auswahl eines vorhandenen Kontos im Quell-Workflow.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Neues Konto

>[!TIP]
>
>* Beim Erstellen eines Kontos mit eingeschränktem Zugriff müssen Sie mindestens einen Themennamen oder einen Abonnementnamen angeben. Die Authentifizierung schlägt fehl, wenn beide Werte fehlen.
>* Nach der Erstellung können Sie den Authentifizierungstyp einer [!DNL Google PubSub] Basisverbindung nicht mehr ändern. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihr neues [!DNL PubSub]-Konto an.

![Die neue Kontoschnittstelle für die Google PubSub-Quelle im Quell-Workflow](../../../../images/tutorials/create/google-pubsub/new.png)

Mit der [!DNL PubSub] können Sie den Zugriffstyp angeben, den Sie während der Authentifizierung zulassen möchten. Sie können für Ihr Konto entweder eine projektbasierte Authentifizierung oder eine themen- und abonnementbasierte Authentifizierung einrichten. Mit der projektbasierten Authentifizierung können Sie Zugriff auf das Stammprojekt in Ihrem Konto gewähren, während Sie mit der themen- und abonnementbasierten Authentifizierung den Zugriff auf ein bestimmtes [!DNL PubSub] Thema und Abonnement einschränken können.

>[!BEGINTABS]

>[!TAB Projektbasierte Authentifizierung]

So erstellen Sie ein Konto mit Zugriff auf den Stammordner [!DNL PubSub] Projektordners. Wählen Sie **[!UICONTROL Anmeldedaten für die Google PubSub-]** als Authentifizierungstyp aus und geben Sie Ihre Projekt-ID und Ihre Anmeldedaten an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle für die Google PubSub-Quelle mit ausgewähltem Stammzugriff.](../../../../images/tutorials/create/google-pubsub/root.png)

>[!TAB Topic- und abonnementbasierte Authentifizierung]

Um ein Konto mit eingeschränktem Zugriff nur auf ein bestimmtes [!DNL PubSub] Thema und Abonnement zu erstellen, wählen Sie **[!UICONTROL Authentifizierungsdaten für Google PubSub-Bereich]** und geben Sie dann Ihre Anmeldeinformationen, Ihren Themennamen und/oder Ihren Abonnementnamen an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle für die Google PubSub-Quelle mit ausgewähltem Bereichszugriff.](../../../../images/tutorials/create/google-pubsub/scoped.png)

>[!ENDTABS]

>[!NOTE]
>
>Einem [!DNL PubSub] Projekt zugewiesene Prinzipale (Rollen) werden in allen Themen und Abonnements übernommen, die in einem [!DNL PubSub] Projekt erstellt werden. Wenn Sie möchten, dass ein Prinzipal (eine Rolle) Zugriff auf ein bestimmtes Thema hat, muss dieser Prinzipal (diese Rolle) auch zum entsprechenden Abonnement des Themas hinzugefügt werden. Weitere Informationen finden Sie in der [[!DNL PubSub] Dokumentation zur Zugriffssteuerung](<https://cloud.google.com/pubsub/docs/access-control>).

## Daten auswählen

Bei einer erfolgreichen Authentifizierung gelangen Sie zum Schritt [!UICONTROL Daten auswählen], in dem Sie durch Ihre [!DNL PubSub] navigieren und die Daten auswählen können, die Sie an Experience Platform übermitteln möchten.

>[!BEGINTABS]

>[!TAB Projektbasierte Authentifizierung]

Wenn Sie sich mit projektbasiertem Zugriff authentifiziert haben, zeigt die [!UICONTROL Daten auswählen]-Schnittstelle alle Abonnements in Ihrem Projekt an, an die ein Thema angehängt ist.

![Der Schritt „Daten auswählen“ des Quell-Workflows mit projektbasierter Authentifizierung.](../../../../images/tutorials/create/google-pubsub/root-folders.png)

>[!TAB Topic- und abonnementbasierte Authentifizierung]

Wenn Sie sich mit einem Thema und einem abonnementbasierten Zugriff authentifiziert haben, kann die Anzeige der [!UICONTROL Daten auswählen] von den von Ihnen bereitgestellten Informationen abhängen.

* Wenn Sie nur den Themennamen angeben, zeigt die Benutzeroberfläche alle Themen-Abonnement-Paare an, die dem angegebenen Thema entsprechen.
* Wenn Sie nur den Abonnementnamen angeben, zeigt die Benutzeroberfläche alle Themen-Abonnementpaare an, die dem angegebenen Abonnementnamen entsprechen.
* Wenn sowohl Themen- als auch Abonnementnamen angegeben werden, zeigt die Schnittstelle das Themen-/Abonnementpaar an, das beiden angegebenen Werten entspricht.

![Der Schritt „Daten auswählen“ des Quell-Workflows mit themen- und abonnementbasierter Authentifizierung.](../../../../images/tutorials/create/google-pubsub/scoped-folders.png)

>[!ENDTABS]

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zwischen Ihrem [!DNL PubSub]-Konto und Experience Platform hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Streaming-Daten aus Ihrem Cloud-Speicher in Experience Platform zu übertragen](../../dataflow/streaming/cloud-storage-streaming.md).
