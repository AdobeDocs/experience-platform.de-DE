---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: PayPal-Anschluss
topic: overview
translation-type: tm+mt
source-git-commit: 52a01c5f90a9643691a25e2d0a5f03a7f0334a7d
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 13%

---


# (Beta) [!DNL PayPal] -Anschluss

>[!NOTE]
>Der [!DNL PayPal] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../home.md#terms-and-conditions) Quellen.

Adobe Experience Platform allows data to be ingested from external sources while providing you with the ability to structure, label, and enhance incoming data using [!DNL Platform] services. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Experience Platform] unterstützt die Erfassung von Daten aus einem Drittanbieter-Zahlungsantrag. Die Unterstützung für Zahlungsdienstleister umfasst [!DNL PayPal].

## Zulassungsliste der IP-Adresse

Die folgenden IP-Adressen müssen einer Zulassungsliste hinzugefügt werden, bevor Sie mit Quellschnittstellen arbeiten können. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen.

### Ost-USA-Region

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### Westeuropa

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Australien Osten

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

Die nachstehende Dokumentation enthält Informationen zum Herstellen einer Verbindung [!DNL PayPal] mit [!DNL Platform] APIs oder der Benutzeroberfläche:

## Verbindung [!DNL PayPal] mit [!DNL Platform] APIs

- [Erstellen eines PayPal-Connectors mit der Flow Service API](../../tutorials/api/create/payments/paypal.md)
- [Durchsuchen einer Zahlungsanwendung mit der Flow Service API](../../tutorials/api/explore/payments.md)
- [Erfassen von Daten aus einer Zahlungsanwendung mithilfe der Flow Service API](../../tutorials/api/collect/payments.md)

## Verbindung [!DNL PayPal] mit der [!DNL Platform] Benutzeroberfläche

- [Erstellen eines Quell-Connectors für PayPal über die Benutzeroberfläche](../../tutorials/ui/create/payments/paypal.md)
- [Konfigurieren eines Datenflusses für einen Zahlungsanschluss in der Benutzeroberfläche](../../tutorials/ui/dataflow/payments.md)