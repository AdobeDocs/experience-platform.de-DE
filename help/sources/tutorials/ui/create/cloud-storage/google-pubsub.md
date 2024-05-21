---
title: Erstellen einer Google PubSub-Source-Verbindung in der Benutzeroberfläche
description: Erfahren Sie, wie Sie einen Google PubSub-Quell-Connector in der Platform-Benutzeroberfläche erstellen.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: fcac805e151d6142886eb8e05da0eb1babad2f69
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 36%

---

# Erstellen eines Quell-Connectors für [!DNL Google PubSub] in der Benutzeroberfläche

>[!IMPORTANT]
>
>Die [!DNL Google PubSub] -Quelle ist im Quellkatalog für Benutzer verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Google PubSub] (nachstehend „[!DNL PubSub]“ genannt) in der Benutzeroberfläche von Platform beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Wenn Sie bereits über eine gültige [!DNL PubSub]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/batch/cloud-storage.md) fortfahren.

### Sammeln erforderlicher Anmeldeinformationen

Sie müssen Werte für die unten beschriebenen Verbindungseigenschaften angeben, um Ihre [!DNL PubSub] -Konto auf Experience Platform. Weitere Informationen zur Authentifizierung und zur Einrichtung der Voraussetzungen finden Sie im Abschnitt [[!DNL PubSub source] Übersicht](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).


>[!BEGINTABS]

>[!TAB Projektbasierte Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| Projekt-ID | Die zur Authentifizierung von [!DNL PubSub] erforderliche Projekt-ID. |
| Anmeldeinformationen | Die zum Authentifizieren erforderliche Berechtigung [!DNL PubSub]. Sie müssen sicherstellen, dass Sie die vollständige JSON-Datei platzieren, nachdem Sie die Leerzeichen aus Ihren Anmeldedaten entfernt haben. |

>[!TAB Themen- und Abonnement-basierte Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| Anmeldeinformationen | Die zum Authentifizieren erforderliche Berechtigung [!DNL PubSub]. Sie müssen sicherstellen, dass Sie die vollständige JSON-Datei platzieren, nachdem Sie die Leerzeichen aus Ihren Anmeldedaten entfernt haben. |
| Themenname | Der Name Ihres [!DNL PubSub] Abonnement. In [!DNL PubSub], können Sie über Abonnements Nachrichten empfangen, indem Sie sich für das Thema anmelden, in dem Nachrichten veröffentlicht wurden. **Hinweis**: Eine einzelne [!DNL PubSub] Abonnements können nur für einen Datenfluss verwendet werden. Um mehrere Datenflüsse erstellen zu können, müssen Sie über mehrere Abonnements verfügen. |
| Abonnementname | Der Name Ihres [!DNL PubSub] Abonnement. In [!DNL PubSub], können Sie über Abonnements Nachrichten empfangen, indem Sie sich für das Thema anmelden, in dem Nachrichten veröffentlicht wurden. |

>[!ENDTABS]

Weitere Informationen zu diesen Werten finden Sie im folgenden Dokument [PubSub-Authentifizierung](https://cloud.google.com/pubsub/docs/authentication). Wenn Sie die auf dem Service-Account basierende Authentifizierung verwenden, lesen Sie das folgende [PubSub-Handbuch](https://cloud.google.com/docs/authentication/production#create_service_account), in dem die Schritte zum Generieren Ihrer Anmeldeinformationen beschrieben werden.

>[!TIP]
>
>Wenn Sie die auf Service-Konten basierende Authentifizierung verwenden, stellen Sie sicher, dass Sie einen ausreichenden Benutzerzugriff auf Ihr Service-Konto gewährt haben und dass in JSON keine zusätzlichen Leerzeichen vorhanden sind, wenn Sie Ihre Anmeldeinformationen kopieren und einfügen.

Nachdem Sie die erforderlichen Anmeldeinformationen zusammen haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL PubSub]-Konto mit Platform zu verknüpfen.

## Verbinden Sie Ihr [!DNL PubSub]-Konto

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud-Speicherplatz] die Option **[!UICONTROL Google PubSub]** und dann die Option **[!UICONTROL Daten hinzufügen]** aus.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche.](../../../../images/tutorials/create/google-pubsub/catalog.png)

Die Seite **[!UICONTROL Verbinden mit Google PubSub]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL PubSub]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![Die vorhandene Kontoauswahl im Ursprungs-Workflow.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Neues Konto

>[!TIP]
>
>* Beim Erstellen eines Kontos mit eingeschränktem Zugriff müssen Sie mindestens einen Namen für Ihr Thema oder Ihren Abonnementnamen angeben. Die Authentifizierung schlägt fehl, wenn beide Werte fehlen.
>* Nach der Erstellung können Sie den Authentifizierungstyp eines [!DNL Google PubSub] Basisverbindung. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihre neue [!DNL PubSub] -Konto.

![Die neue Kontoschnittstelle für die Google PubSub-Quelle im Quellen-Workflow](../../../../images/tutorials/create/google-pubsub/new.png)

Die [!DNL PubSub] -Quelle können Sie den Zugriffstyp angeben, den Sie während der Authentifizierung zulassen möchten. Sie können Ihr Konto so einrichten, dass es entweder über eine projektbasierte Authentifizierung oder über Themen- und Abonnement-basierte Authentifizierung verfügt. Projektbasierte Authentifizierung ermöglicht es Ihnen, Zugriff auf das Projekt auf der Stammebene in Ihrem Konto zu gewähren, während die Themen- und Abonnementbasierte Authentifizierung den Zugriff auf eine bestimmte [!DNL PubSub] Thema und Abonnement.

>[!BEGINTABS]

>[!TAB Projektbasierte Authentifizierung]

So erstellen Sie ein Konto mit Zugriff auf Ihren Stammordner [!DNL PubSub] Projektordner. Auswählen **[!UICONTROL Google PubSub-Authentifizierungsberechtigungen]** als Authentifizierungstyp verwenden und Ihre Projekt-ID und Anmeldeinformationen angeben. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle für die Google PubSub-Quelle mit ausgewähltem Stammzugriff.](../../../../images/tutorials/create/google-pubsub/root.png)

>[!TAB Themen- und Abonnement-basierte Authentifizierung]

So erstellen Sie ein Konto mit eingeschränktem Zugriff auf eine bestimmte [!DNL PubSub] Thema und Abonnement, wählen Sie **[!UICONTROL Google PubSub Scoped-Authentifizierungsberechtigungen]** Geben Sie dann Ihre Anmeldeinformationen, den Themennamen und/oder den Abonnementnamen ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle für die Google PubSub-Quelle mit aktiviertem Scoped-Zugriff.](../../../../images/tutorials/create/google-pubsub/scoped.png)

>[!ENDTABS]

>[!NOTE]
>
>Prinzipal (Rollen), das einem [!DNL PubSub] -Projekt wird in allen Themen und Abonnements übernommen, die innerhalb eines [!DNL PubSub] Projekt. Wenn Sie möchten, dass ein Prinzipal (eine Rolle) Zugriff auf ein bestimmtes Thema hat, muss dieser Prinzipal (die Rolle) auch zum entsprechenden Abonnement des Themas hinzugefügt werden. Weitere Informationen finden Sie im Abschnitt [[!DNL PubSub] Dokumentation zur Zugriffskontrolle](<https://cloud.google.com/pubsub/docs/access-control>).

## Daten auswählen

Eine erfolgreiche Authentifizierung bringt Sie zu [!UICONTROL Daten auswählen] Schritt, in dem Sie durch Ihre [!DNL PubSub] die Datenhierarchie und wählen Sie die Daten aus, die Sie zum Experience Platform bringen möchten.

>[!BEGINTABS]

>[!TAB Projektbasierte Authentifizierung]

Wenn Sie sich beim projektbasierten Zugriff authentifiziert haben, wird die [!UICONTROL Daten auswählen] -Oberfläche zeigt alle Abonnements in Ihrem Projekt an, denen ein Thema angehängt ist.

![Der Schritt Datenauswahl des Ursprungs-Workflows mit projektbasierter Authentifizierung.](../../../../images/tutorials/create/google-pubsub/root-folders.png)

>[!TAB Themen- und Abonnement-basierte Authentifizierung]

Wenn Sie sich mit einem Thema und Abonnementzugriff authentifiziert haben, wird die [!UICONTROL Daten auswählen] Die Anzeige der Benutzeroberfläche kann je nach den von Ihnen bereitgestellten Informationen variieren.

* Wenn Sie nur den Themennamen angeben, zeigt die Benutzeroberfläche alle Themen-Abonnementpaare an, die dem angegebenen Thema entsprechen.
* Wenn Sie nur den Abonnementnamen angeben, zeigt die Benutzeroberfläche alle Themen-Abonnementpaare an, die dem angegebenen Abonnementnamen entsprechen.
* Wenn sowohl Themen- als auch Abonnementnamen angegeben sind, zeigt die Benutzeroberfläche das Thema-Abonnement-Paar an, das beiden bereitgestellten Werten entspricht.

![Der Schritt &quot;Daten auswählen&quot;des Ursprungs-Workflows mit Themen- und Abonnement-basierter Authentifizierung.](../../../../images/tutorials/create/google-pubsub/scoped-folders.png)

>[!ENDTABS]

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zwischen Ihrer [!DNL PubSub] -Konto und -Plattform. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Streaming-Daten aus Ihrem Cloud-Speicher in Platform zu übertragen](../../dataflow/streaming/cloud-storage-streaming.md).
