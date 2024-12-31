---
title: Übersicht über den Source-Connector für Azure Event Hubs
description: Erfahren Sie, wie Sie Azure Event Hubs über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 12ddf87d594b7e25a0356cd419e990b262c1734e
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 20%

---

# [!DNL Azure Event Hubs]

>[!IMPORTANT]
>
>Die [!DNL Azure Event Hubs] ist im Quellkatalog für Benutzende verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure]. Sie können Ihre Daten aus diesen Systemen in Platform importieren.

Cloud-Speicher bieten eine Quelle, von der Sie Ihre Daten in Platform übertragen können, ohne diese herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON, XDM Parquet oder mit Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird in den Quell-Workflow integriert. Mit Platform können Sie Daten aus [!DNL Event Hubs] in Echtzeit importieren.

## Skalierung mit [!DNL Event Hubs]

Der Skalierungsfaktor Ihrer [!DNL Event Hubs] muss erhöht werden, wenn Sie Daten mit hohem Datenvolumen aufnehmen, die Parallelität erhöhen oder die Geschwindigkeit der Aufnahmeplattform erhöhen müssen.

### Höheres Datenvolumen aufnehmen

Derzeit beträgt das maximale Datenvolumen, das Sie von Ihrem [!DNL Event Hubs]-Konto an Platform übermitteln können, 2.000 Datensätze pro Sekunde. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Daten mit einem größeren Datenvolumen zu skalieren und aufzunehmen.

### Steigerung der Parallelität auf [!DNL Event Hubs] und Platform

Parallelität bezieht sich auf die gleichzeitige Ausführung derselben Aufgaben auf mehreren Verarbeitungseinheiten, um Geschwindigkeit und Leistung zu erhöhen. Sie können die Parallelität auf der [!DNL Event Hubs] Seite erhöhen, indem Sie die Partition erhöhen oder mehr Verarbeitungseinheiten für Ihr [!DNL Event Hubs]-Konto erwerben. Weitere Informationen finden Sie [[!DNL Event Hubs]  diesem Dokument ](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) Skalierung .

Um die Aufnahmegeschwindigkeit auf der Platform-Seite zu erhöhen, muss Platform die Anzahl der Aufgaben im Quell-Connector erhöhen, die von Ihren [!DNL Event Hubs]-Partitionen gelesen werden. Sobald Sie die Parallelität auf der [!DNL Event Hubs] erhöht haben, wenden Sie sich bitte an Ihren Adobe-Support-Mitarbeiter, um die Plattformaufgaben auf der Grundlage Ihrer neuen Partition zu skalieren. Derzeit ist dieser Prozess nicht automatisiert.

## Verwenden eines virtuellen Netzwerks zur Verbindung von [!DNL Event Hubs] mit Platform

Sie können ein virtuelles Netzwerk einrichten, um [!DNL Event Hubs] mit Platform zu verbinden, während Ihre Firewall-Maßnahmen aktiviert sind. Um ein virtuelles Netzwerk einzurichten, gehen Sie zu diesem [[!DNL Event Hubs] Dokument zu Netzwerkregelsätzen](https://learn.microsoft.com/en-us/azure/event-hubs/network-security) und führen Sie die unten aufgeführten Schritte aus:

* Wählen **im REST** API-Bedienfeld aus.
* Authentifizieren Sie Ihr [!DNL Azure]-Konto mit Ihren Anmeldedaten im selben Browser.
* Wählen Sie den [!DNL Event Hubs] Namespace, die Ressourcengruppe und das Abonnement aus, die Sie in Platform importieren möchten, und wählen Sie dann **AUSFÜHREN**.
* Fügen Sie im angezeigten JSON-Text das folgende Platform-Subnetz unter `virtualNetworkRules` in `properties` hinzu:


>[!IMPORTANT]
>
>Sie müssen einen Backup des JSON-Bodys erstellen, den Sie erhalten, bevor Sie `virtualNetworkRules` mit dem Platform-Subnetz aktualisieren, da es Ihre vorhandenen IP-Filterregeln enthält. Andernfalls werden die Regeln nach dem Aufruf gelöscht.


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

In der folgenden Liste finden Sie die verschiedenen Regionen von Platform-Subnetzen:

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

Weitere Informationen [[!DNL Event Hubs]  Netzwerkregelsätze finden Sie ](https://learn.microsoft.com/en-us/azure/event-hubs/network-security) folgenden Dokument.

## Verbinden von [!DNL Event Hubs] mit Platform

Die folgende Dokumentation enthält Informationen dazu, wie Sie [!DNL Event Hubs] mithilfe von APIs oder der Benutzeroberfläche mit Platform verbinden können:

### Verwenden von APIs

* [Erstellen einer Event Hubs-Quellverbindung mithilfe der Flow Service-API](../../tutorials/api/create/cloud-storage/eventhub.md)
* [Erfassen von Streaming-Daten mit der Flow Service-API](../../tutorials/api/collect/streaming.md)

### Verwenden der Benutzeroberfläche

* [Erstellen einer Event Hubs-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [Konfigurieren eines Datenflusses für eine Cloud-Speicherverbindung über die Benutzeroberfläche](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
