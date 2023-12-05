---
title: Azure Event Hubs Source Connector - Überblick
description: Erfahren Sie, wie Sie Azure Event Hubs über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 12ddf87d594b7e25a0356cd419e990b262c1734e
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 20%

---

# [!DNL Azure Event Hubs] source

>[!IMPORTANT]
>
>Die [!DNL Azure Event Hubs] -Quelle ist im Quellkatalog für Benutzer verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform], und [!DNL Azure]. Sie können Ihre Daten aus diesen Systemen in Platform importieren.

Cloud-Speicher bieten eine Quelle, von der Sie Ihre Daten in Platform übertragen können, ohne diese herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON, XDM Parquet oder mit Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird in den Quell-Workflow integriert. Mit Platform können Sie Daten aus [!DNL Event Hubs] in Echtzeit importieren.

## Skalierung mit [!DNL Event Hubs]

Der Skalierungsfaktor Ihres [!DNL Event Hubs] -Instanz muss erhöht werden, wenn Sie Daten mit hohem Volumen aufnehmen, die Parallelität erhöhen oder die Geschwindigkeit der Aufnahmeplattform erhöhen müssen.

### Aufnehmen von Daten mit höherem Volumen

Derzeit ist das maximale Datenvolumen, das Sie aus Ihrem [!DNL Event Hubs] -Konto in Platform 2000 Datensätze pro Sekunde. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Daten mit höherem Datenvolumen zu skalieren und aufzunehmen.

### Erhöhen Sie den Parallelismus bei [!DNL Event Hubs] und Plattform

Parallelismus bezieht sich auf die gleichzeitige Ausführung der gleichen Aufgaben an mehreren Verarbeitungseinheiten, um die Geschwindigkeit und Leistung zu erhöhen. Sie können die Parallelität auf der [!DNL Event Hubs] , indem Sie die Partition vergrößern oder mehr Verarbeitungseinheiten für Ihre [!DNL Event Hubs] -Konto. Siehe dies [[!DNL Event Hubs] Dokument zur Skalierung](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) für weitere Informationen.

Um die Geschwindigkeit der Aufnahme auf Platform-Seite zu erhöhen, muss Platform die Anzahl der Aufgaben im Quell-Connector erhöhen, die von Ihrer [!DNL Event Hubs] Partitionen. Sobald Sie die Parallelität auf der [!DNL Event Hubs] wenden Sie sich bitte an Ihren Adobe-Kundenbetreuer, um Platform-Aufgaben basierend auf Ihrer neuen Partition zu skalieren. Derzeit ist dieser Prozess nicht automatisiert.

## Verwenden Sie ein virtuelles Netzwerk, um eine Verbindung herzustellen [!DNL Event Hubs] Platform

Sie können ein virtuelles Netzwerk für die Verbindung einrichten [!DNL Event Hubs] auf Platform zu setzen, während die Firewall-Maßnahmen aktiviert sind. Um ein virtuelles Netzwerk einzurichten, gehen Sie zu diesem [[!DNL Event Hubs] Netzwerkregelsatz-Dokument](https://learn.microsoft.com/en-us/azure/event-hubs/network-security) und führen Sie die folgenden Schritte aus:

* Auswählen **Testen** über das Bedienfeld REST-API;
* Authentifizieren Ihrer [!DNL Azure] Konto mit Ihren Anmeldedaten im selben Browser;
* Wählen Sie die [!DNL Event Hubs] Namespace, Ressourcengruppe und Abonnement, die Sie in Platform einbringen möchten, und wählen Sie dann **AUSFÜHREN**;
* Fügen Sie im angezeigten JSON-Textkörper das folgende Platform-Subnetz unter `virtualNetworkRules` inside `properties`:


>[!IMPORTANT]
>
>Sie müssen eine Sicherung des JSON-Hauptteils erstellen, den Sie erhalten, bevor Sie `virtualNetworkRules` mit dem Subnetz Plattform , da es Ihre vorhandenen IP-Filterregeln enthält. Andernfalls werden die Regeln nach dem Aufruf gelöscht.


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

Die nachstehende Liste zeigt verschiedene Regionen von Platform-Subnetzen:

### VA7: Nordamerika

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### NLD2: Europa

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
            "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_nld2_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2-vnet/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
        }, 
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### AUS5: Australien

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5-vnet/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

Siehe Folgendes [[!DNL Event Hubs] Dokument](https://learn.microsoft.com/en-us/azure/event-hubs/network-security) für weitere Informationen zu Netzwerkregelsätzen.

## Verbinden von [!DNL Event Hubs] mit Platform

Die folgende Dokumentation enthält Informationen dazu, wie Sie [!DNL Event Hubs] mithilfe von APIs oder der Benutzeroberfläche mit Platform verbinden können:

### Verwenden von APIs

* [Erstellen einer Quell-Verbindung für Ereignis-Hub mithilfe der Flow Service-API](../../tutorials/api/create/cloud-storage/eventhub.md)
* [Erfassen von Streaming-Daten mit der Flow Service-API](../../tutorials/api/collect/streaming.md)

### Verwenden der Benutzeroberfläche

* [Erstellen einer Quell-Verbindung für Ereignis-Hub in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [Konfigurieren eines Datenflusses für eine Cloud-Speicherverbindung über die Benutzeroberfläche](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
