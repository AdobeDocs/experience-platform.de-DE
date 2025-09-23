---
title: Übersicht über Kapillarstreaming-Ereignisse
description: Erfahren Sie, wie Sie Daten von Capillary zu Experience Platform streamen.
hide: true
hidefromtoc: true
source-git-commit: 7b733831932c48240340b0a2136e15f5d2144635
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 6%

---

# [!DNL Capillary Streaming Events]

[!DNL Capillary Technologies] ist eine führende Treue- und Interaktionsplattform, der über 300 Marken auf der ganzen Welt vertrauen. Verwenden Sie die [!DNL Capillary Streaming Events], damit Ihr Unternehmen Kundenprofile, Treuedaten und Transaktionsereignisse nahtlos von [!DNL Capillary] in Adobe Experience Platform streamen kann. Verbinden Sie Ihre [!DNL Capillary], um Personalisierung in Echtzeit, erweiterte Zielgruppensegmentierung und Omni-Channel-Kampagnenorchestrierung zu ermöglichen.

Durch die Integration von [!DNL Capillary] mit Experience Platform können Sie:

* Synchronisieren **Treuepunkte, -stufen und -belohnungen** in Echtzeit
* Senden Sie **Transaktionsdaten** zur Analyse und Aktivierung an Experience Platform.
* Nutzen Sie Real-Time CDP, Experience Platform und Adobe Journey Optimizer für die Segmentierung, Journey-Orchestrierung und Personalisierung.

## Voraussetzungen

Bevor Sie [!DNL Capillary] mit Adobe Experience Platform verbinden, stellen Sie Folgendes sicher:

* Eine gültige **Adobe-Organisations-** und Zugriff auf eine aktivierte Experience Platform-Sandbox.
* **[!DNL Capillary]-Quellberechtigungen** (Client-ID und Client-Geheimnis).
* Die erforderlichen Berechtigungen in der Adobe Admin Console zum Erstellen von Quellen und Datenflüssen.

### Sammeln erforderlicher Anmeldedaten

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um Ihr [!DNL Capillary]-Konto mit Experience Platform zu verbinden:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Client-ID | Die Client-Kennung für die [!DNL Capillary]. | `321c8a8fee0d4a06838d46f9d3109e8a` |
| Client-Geheimnis | Das mit der Client-ID herausgegebene Client-Geheimnis | `xxxxxxxxxxxxxxxxxx` |
| Organisations-ID | Ihre Adobe-Organisations-ID | `0A7D42FC5DB9D3360A495FD3@AdobeOrg` |

Weitere Informationen zum Generieren von Zugriffs-Token finden Sie im [Authentifizierungshandbuch für Adobe](https://developer.adobe.com/developer-console/docs/guides/authentication/).

### Erstellen eines Zugriffs-Tokens

Verwenden Sie anschließend Ihre Client-ID und Ihren geheimen Client-Schlüssel, um ein Zugriffs-Token aus Adobe zu generieren.

**Anfrage**

```shell
curl -X POST 'https://ims-na1.adobelogin.com/ims/token' \
  -d 'client_id={CLIENT_ID}' \
  -d 'client_secret={CLIENT_SECRET}' \
  -d 'grant_type=client_credentials' \
  -d 'scope=openid AdobeID read_organizations additional_info.projectedProductContext session'
```

**Antwort**

```json
{
  "access_token": "eyJhbGciOi...",
  "token_type": "bearer",
  "expires_in": 86399994
}
```

## Nächste Schritte

Nachdem Sie die erforderliche Einrichtung für [!DNL Capillary] abgeschlossen haben, lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie Ihr -Konto verbinden und mit dem Streaming von Daten von [!DNL Capillary] an Experience Platform beginnen können.

* [Verbindung  [!DNL Capillary Streaming Events]  Experience Platform über die API herstellen](../../tutorials/api/create/loyalty/capillary.md)
* [Verbindung  [!DNL Capillary Streaming Events]  Experience Platform über die Benutzeroberfläche herstellen](../../tutorials/ui/create/loyalty/capillary.md)