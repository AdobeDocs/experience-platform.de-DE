---
title: Erste Schritte mit der Privacy Service-API
description: Erfahren Sie, wie Sie sich bei der Privacy Service-API authentifizieren und wie Sie Beispiel-API-Aufrufe in der Dokumentation interpretieren.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 59dc28a84971dc8c21d633741cfe2dc1b44ea1a6
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 19%

---

# Erste Schritte mit der Privacy Service-API

Dieses Handbuch bietet eine Einführung in die wichtigsten Konzepte, die Sie kennen müssen, bevor Sie Aufrufe an die Adobe Experience Platform Privacy Service-API durchführen.

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis der [Privacy Service](../home.md) und wie Sie damit Zugriffs- und Löschanfragen Ihrer Datensubjekte (Kunden) in allen Adobe Experience Cloud-Anwendungen verwalten können.

Um Zugriffsberechtigungen für die API zu erstellen, muss ein Administrator in Ihrem Unternehmen zuvor Produktprofile für den Privacy Service in Adobe Admin Console eingerichtet haben. Das Produktprofil, das Sie einer API-Integration zuweisen, bestimmt, welche Berechtigungen diese Integration beim Zugriff auf Privacy Service-Funktionen besitzt. Siehe Handbuch unter [Verwalten von Privacy Service-Berechtigungen](../permissions.md) für weitere Informationen.

## Sammeln von Werten für erforderliche Kopfzeilen

Um die Privacy Service-API aufrufen zu können, müssen Sie zunächst Ihre Zugriffsberechtigungen erfassen, damit sie in den erforderlichen Kopfzeilen verwendet werden können:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Diese Werte werden mithilfe von [Adobe Developer-Konsole](https://developer.adobe.com/console). Ihre `{ORG_ID}` und `{API_KEY}` muss nur einmal generiert werden und kann in zukünftigen API-Aufrufen wiederverwendet werden. Allerdings muss Ihre `{ACCESS_TOKEN}` ist temporär und muss alle 24 Stunden neu generiert werden.

Die Schritte zum Generieren dieser Werte werden im Folgenden detailliert beschrieben.

### Einmalige Einrichtung

Wechseln Sie zur [Adobe-Entwicklerkonsole](https://developer.adobe.com/console) und melden Sie sich mit Ihrer Adobe ID an. Führen Sie anschließend die im Tutorial [Erstellen eines leeren Projekts](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) in der Dokumentation zur Entwicklerkonsole beschriebenen Schritte aus.

Nachdem Sie ein neues Projekt erstellt haben, wählen Sie **[!UICONTROL Zum Projekt hinzufügen]** und wählen Sie **[!UICONTROL API]** aus dem Dropdown-Menü aus.

![Die API-Option, die im [!UICONTROL Zum Projekt hinzufügen] Dropdown-Liste auf der Seite mit den Projektdetails in der Developer Console](../images/api/getting-started/add-api-button.png)

#### Wählen Sie eine API aus und generieren Sie eine Tastatur. {#keypair}

Der Bildschirm **[!UICONTROL API hinzufügen]** wird angezeigt. Auswählen **[!UICONTROL Experience Cloud]** , um die Liste der verfügbaren APIs einzuschränken, wählen Sie dann die Karte für **[!UICONTROL Privacy Service-API]** vor der Auswahl **[!UICONTROL Nächste]**.

![Die aus der Liste der verfügbaren APIs ausgewählte Privacy Service-API-Karte](../images/api/getting-started/add-privacy-service-api.png)

Die **[!UICONTROL API konfigurieren]** angezeigt. Wählen Sie die zu **[!UICONTROL Generieren eines Schlüsselpaars]**, wählen Sie **[!UICONTROL Generieren von keypair]**.

![Die [!UICONTROL Generieren eines Schlüsselpaars] Option, die auf der [!UICONTROL API konfigurieren] Bildschirm](../images/api/getting-started/generate-key-pair.png)

Das Schlüsselpaar wird automatisch generiert und eine ZIP-Datei mit einem privaten Schlüssel und einem öffentlichen Zertifikat wird von Ihrem Browser heruntergeladen (um in einem späteren Schritt verwendet zu werden). Klicken Sie auf **[!UICONTROL Weiter]**, um fortzufahren.

![Die generierte Tastatur, die in der Benutzeroberfläche angezeigt wird, deren Werte automatisch vom Browser heruntergeladen werden](../images/api/getting-started/key-pair-generated.png)

#### Berechtigungen über Produktprofile zuweisen {#product-profiles}

Der letzte Konfigurationsschritt besteht darin, die Produktprofile auszuwählen, von denen diese Integration ihre Berechtigungen erbt. Wenn Sie mehr als ein Profil auswählen, werden die zugehörigen Berechtigungssätze für die Integration kombiniert.

>[!NOTE]
>
>Produktprofile und die granularen Berechtigungen, die sie bereitstellen, werden von Administratoren über Adobe Admin Console erstellt und verwaltet. Siehe Handbuch unter [Berechtigungen für Privacy Service](../permissions.md) für weitere Informationen.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Konfigurierte API speichern]**.

![Vor dem Speichern der Konfiguration wird ein einzelnes Produktprofil aus der Liste ausgewählt](../images/api/getting-started/select-product-profiles.png)

Nachdem die API zum Projekt hinzugefügt wurde, wird die Projektseite erneut auf der **Übersicht über die Privacy Service-API** Seite. Scrollen Sie von hier nach unten zum **[!UICONTROL Dienstkonto (JWT)]** -Abschnitt, der die folgenden Zugriffsberechtigungen bereitstellt, die für alle Aufrufe der Privacy Service-API erforderlich sind:

* **[!UICONTROL CLIENT-ID]**: Die Client-ID ist die erforderliche `{API_KEY}` , die im `x-api-key` -Kopfzeile.
* **[!UICONTROL ORGANISATIONS-ID]**: Die Organisations-ID ist der `{ORG_ID}`-Wert, der im `x-gw-ims-org-id`-Header verwendet werden muss.

![Die Werte für Client-ID und Organisations-ID , wie sie nach der Konfiguration der API auf der Übersichtsseite des Projekts angezeigt werden](../images/api/getting-started/jwt-credentials.png)

### Authentifizierung für jede Sitzung

Die letzte erforderliche Berechtigung, die Sie erfassen müssen, ist Ihre `{ACCESS_TOKEN}`, der in der Autorisierungskopfzeile verwendet wird. Im Gegensatz zu den Werten für `{API_KEY}` und `{ORG_ID}`muss ein neues Token alle 24 Stunden generiert werden, damit Sie die API weiterhin verwenden können.

Im Allgemeinen gibt es zwei Methoden zum Generieren eines Zugriffstokens:

* [Manuelles Generieren des Tokens](#manual-token) für Tests und Entwicklung.
* [Token-Generierung automatisieren](#auto-token) für API-Integrationen.

#### Manuelles Generieren eines Tokens {#manual-token}

So generieren Sie manuell eine neue `{ACCESS_TOKEN}`, öffnen Sie den zuvor heruntergeladenen privaten Schlüssel und fügen Sie seinen Inhalt in das Textfeld neben **[!UICONTROL Zugriffstoken generieren]** vor der Auswahl **[!UICONTROL Generate Token]**.

![Das zuvor generierte Zugriffstoken wird auf der Übersichtsseite des Projekts eingefügt, mit der [!UICONTROL Generate Token] Schaltfläche, die nach](../images/api/getting-started/paste-private-key.png)

Es wird ein neues Zugriffs-Token generiert und eine Schaltfläche zum Kopieren des Tokens in die Zwischenablage bereitgestellt. Dieser Wert wird für die erforderliche Autorisierungskopfzeile verwendet und muss im Format angegeben werden `Bearer {ACCESS_TOKEN}`.

![Das generierte Zugriffstoken, das aus der Benutzeroberfläche kopiert wird](../images/api/getting-started/generated-access-token.png)

#### Token-Generierung automatisieren {#auto-token}

Sie können neue Zugriffstoken für automatisierte Prozesse generieren, indem Sie ein JSON Web Token (JWT) über eine POST-Anfrage an Adobe Identity Management Service (IMS) senden. Weitere Informationen finden Sie im Dokument Developer Console unter [JWT-Authentifizierung](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) für detaillierte Schritte.

## Lesen von Beispiel-API-Aufrufen

Jedes Endpunkthandbuch enthält Beispiel-API-Aufrufe, die zeigen, wie Sie Ihre Anfragen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/api-guide.md#sample-api) in den Ersten Schritten für Platform-APIs.

## Nächste Schritte

Nachdem Sie nun wissen, welche Kopfzeilen zu verwenden sind, können Sie erste Aufrufe an die Privacy Service-API stellen. Wählen Sie eine der Endpunktleitfäden für die ersten Schritte aus:

* [Datenschutzaufträge](./privacy-jobs.md)
* [Einverständnis](./consent.md)
