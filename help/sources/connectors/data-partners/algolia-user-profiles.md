---
title: Übersicht über Algolia-Benutzerprofile in Source
description: Erfahren Sie mehr über die Algolia-Benutzerprofilquelle in der Adobe Experience Platform
hide: true
hidefromtoc: true
source-git-commit: 1bde4b831f1b79de1a8292ad5f221f522e871d08
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# [!DNL Algolia User Profiles]

[[!DNL Algolia]](https://www.algolia.com/) ist eine leistungsstarke Such- und Discovery-API-Plattform, mit der Unternehmen schnelle, relevante und anpassbare Sucherlebnisse bereitstellen können. Es bietet Funktionen für die Echtzeit-Suche mit Tippfehler-Toleranz, Filterung, Facettierung und KI-gestützter Relevanzabstimmung. [!DNL Algolia] unterstützt Unternehmen dabei, die Benutzerinteraktion, die Konversionsraten und das Kundenerlebnis insgesamt zu verbessern, indem es leistungsstarke Suchlösungen für Websites, E-Commerce-Plattformen und Anwendungen bereitstellt.

Zu den wichtigsten Vorteilen von [!DNL Algolia] gehören:

* Blitzschnelle Suche mit sofortigen Ergebnissen.
* Hochrelevante Empfehlungen mit KI-Unterstützung.
* Anpassbare Rangfolge zur Priorisierung der Geschäftsanforderungen.
* Skalierbarkeit zur mühelosen Handhabung hoher Traffic-Lasten.

Weitere Informationen finden Sie in der [[!DNL Algolia] Produktdokumentation](https://resources.algolia.com/).

## Architektur

Selbstbedienungsquellen (Batch-SDK) bieten alle erforderlichen Funktionen wie Authentifizierung, Paginierung oder sowohl vollständigen als auch teilweisen Daten-Pull. Die [!DNL Algolia User Profiles]-Quelle verwendet diese Funktionen, um die Integration abzuschließen.

![Architektur der Integration von Algolia und Experience Platform](../../images/tutorials/create/algolia/user-profiles/algolia-aep-user-profiles-arch.png)

## Voraussetzungen {#prerequisites}

Sie müssen die folgenden Schritte ausführen, bevor Sie Ihr [!DNL Algolia]-Konto mit Experience Platform verbinden können.

1. Verwenden Sie das [[!DNL Algolia] Dashboard](https://dashboard.algolia.com/users/sign_up), um sich bei Ihrem [!DNL Algolia]-Konto anzumelden oder ein neues Konto zu erstellen.
2. [Index vorbereiten](https://www.algolia.com/doc/guides/sending-and-managing-data/prepare-your-data/in-depth/prepare-data-in-depth/).
3. [Richten Sie Ihre Facetten ](https://www.algolia.com/doc/guides/managing-results/refine-results/faceting/).
4. [Benutzerereignisse senden](https://www.algolia.com/doc/guides/sending-events/getting-started/).
5. [Personalisieren Sie Ihren Index](https://www.algolia.com/doc/guides/personalization/advanced-personalization/configure/setup/indices/).

### Konfigurieren von Berechtigungen für Experience Platform

Sie müssen sowohl **[!UICONTROL Quellen anzeigen]** als auch **[!UICONTROL Quellen verwalten]** für Ihr Konto aktiviert haben, um Ihr [!DNL Algolia]-Konto mit Experience Platform zu verbinden. Wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten. Weitere Informationen finden Sie im [Handbuch zur Benutzeroberfläche der Zugriffssteuerung](../../../access-control/abac/ui/permissions.md).

### Zulassungsliste von IP-Adressen

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Auf die Zulassungsliste setzen Weitere Informationen finden Sie [ Seite ](../../ip-address-allow-list.md)IP-Adresse“.

## Verbinden Ihres [!DNL Algolia] mit Experience Platform

Nachdem Sie die Voraussetzungen erfüllt haben, können Sie mit dem nächsten Schritt fortfahren und [Ihr Konto mit  [!DNL Algolia]  Experience Platform verbinden](../../tutorials/ui/create/data-partners/algolia-user-profiles.md).
