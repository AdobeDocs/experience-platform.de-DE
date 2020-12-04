---
keywords: Experience Platform;home;popular topics;namespace;Namespace;Namespaces;namespaces;identity namespace;Identity namespace;identity;Identity;Identity service;identity service
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
description: 'Identitäts-Namespaces sind eine Komponente des Identity Service, die als Indikatoren für den Kontext dient, auf den sich eine Identität bezieht. Sie unterscheiden beispielsweise den Wert "name@email.com"als E-Mail-Adresse oder "443522"als numerische CRM-ID. '
translation-type: tm+mt
source-git-commit: dfb16c1808ac61e6c4f4d97c08ac3d1dcc8499a8
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 73%

---


# Übersicht über Identitäts-Namespaces

Identitäts-Namespaces sind eine Komponente des [[!DNL Identity Service]](./home.md), die als Indikatoren für den Kontext dient, auf den sich eine Identität bezieht. Sie unterscheiden beispielsweise den Wert von „name<span>@email.com“ als E-Mail-Adresse oder „443522“ als numerische CRM-ID.

## Erste Schritte

Das Verwenden von Identitäts-Namespaces setzt ein Verständnis der verschiedenen beteiligten Adobe Experience Platform-Dienste voraus. Bevor Sie Namespaces nutzen, lesen Sie bitte die Dokumentation für folgende Dienste:

- [[!DNL Real-time Customer Profile]](../profile/home.md): Bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Identity Service]](./home.md): Sorgt für eine bessere Darstellung einzelner Kunden und deren Verhalten, indem Identitäten zwischen Geräten und Systemen überbrückt werden.
- [[!DNL Privacy Service]](../privacy-service/home.md): Identitäts-Namespaces werden zur Einhaltung der Datenschutz-Grundverordnung (DSGVO) verwendet, laut der DSGVO-Anfragen für einen Namespace gestellt werden können.

## Identitäts-Namespaces verstehen

Eine vollqualifizierte Identität umfasst einen ID-Wert und einen Namespace. When matching record data across profile fragments, as when [!DNL Real-time Customer Profile] merges profile data, both the identity value and the namespace must match.

Zwei Profilfragmente können z. B. unterschiedliche primäre Kennungen enthalten, für den Namespace „E-Mail“ jedoch denselben Wert nutzen. So kann Platform erkennen, dass die Fragmente in Wahrheit zur gleichen Person gehören und die Daten im Identitätsdiagramm für diese Person zusammenführen.

![](images/identity-service-stitching.png)

### Identitätstypen

Daten können anhand verschiedener Identitätstypen identifiziert werden. Der Identitätstyp wird zum Zeitpunkt der Erstellung des Identitäts-Namespace angegeben und steuert, ob die Daten im Identitätsdiagramm persistiert werden oder nicht. Außerdem gibt es spezielle Anweisungen zum Umgang mit diesen Daten.

The following identity types are available within [!DNL Platform]:

| Identitätstyp | Beschreibung |
| --- | --- |
| Cookie | Diese Identitäten sind für Erweiterungen von entscheidender Bedeutung und bilden den Großteil des Identitätsdiagramms. Sie verfallen jedoch naturgemäß schnell und verlieren mit der Zeit ihren Wert. Das Löschen von Cookies wird im Identitätsdiagramm speziell behandelt. |
| Geräteübergreifend | This indicates that [!DNL Identity Service] should consider this to be a strong people identifier and hence preserve it forever. Beispiele dafür sind eine Anmelde-ID, CRM-ID, Loyalitäts-ID usw. |
| Gerät | Umfasst IDFA-, GAID- und andere IOT-IDs. Diese können von Menschen in einem Haushalt auch geteilt werden. |
| E-Mail | Identitäten dieser Art beinhalten personenbezogene Daten (PII). This is an indication to [!DNL Identity Service] to handle the value sensitively. |
| Mobile | Identitäten dieser Art umfassen PII. This is an indication to [!DNL Identity Service] to handle the value sensitively. |
| Nichtpersonen | Dient zum Speichern von Kennungen, die Namespaces benötigen, aber nicht an einen Personen-Cluster gebunden sind. Diese Kennungen werden dann aus dem Identitätsdiagramm herausgefiltert. Mögliche Anwendungsfälle sind Daten zu Produkten, Organisationen, Geschäften usw. (Zum Beispiel eine Produkt-SKU.) |
| Telefon | Identitäten dieser Art umfassen PII. This is indication to [!DNL Identity Service] to handle the value sensitively. |

### Standard-Namespaces {#standard}

Adobe Experience Platform bietet verschiedene Identitäts-Namespaces, die für alle Organisationen verfügbar sind. These are known as Standard namespaces and are visible using the [!DNL Identity Service] API or through the [!DNL Platform] UI.

Klicken Sie in der linken Leiste auf **[!UICONTROL Identitäten]** und dann auf den Tab **[!UICONTROL Durchsuchen]**, um in der Benutzeroberfläche die Standard-Namespaces anzuzeigen. All identity namespaces accessible to your organization will be shown, however those with &quot;[!UICONTROL Standard]&quot; as the &quot;[!UICONTROL Owner]&quot; are the Standard namespaces provided by Adobe.

Sie können dann auf einen der aufgeführten Namespaces klicken, um Details anzuzeigen.

![](./images/standard-namespace-detail.png)

## Verwalten von Namespaces für Ihre Organisation

Je nach den Daten und Anwendungsfällen in Ihrer Organisation benötigen Sie möglicherweise benutzerdefinierte Namespaces.

These are visible in the UI as those namespaces with &quot;[!UICONTROL Custom]&quot; as the &quot;[!UICONTROL Owner]&quot;. Custom namespaces can be created using the [!DNL Identity Service] API or through the user interface.

Um mithilfe der Benutzeroberfläche einen benutzerdefinierten Namespace zu erstellen, klicken Sie auf **[!UICONTROL Identitäts-Namespace erstellen]**, füllen Sie das Dialogfeld aus und klicken Sie auf **[!UICONTROL Erstellen]**.

Namespaces that you define are private to your organization and require a unique &quot;[!UICONTROL Identity Symbol]&quot; (or &quot;code&quot; if you are using the API) in order to be created successfully.

![](./images/create-identity-namespace.png)

Ähnlich wie bei Standard-Namespaces können Sie über den Tab **[!UICONTROL Durchsuchen]** auf einen benutzerdefinierten Namespace klicken, um dessen Details anzuzeigen. Bei einem benutzerdefinierten Namespace können Sie im Detailbereich jedoch auch dessen Anzeigenamen und die Beschreibung bearbeiten.

>[!NOTE]
>
>Nachdem ein Namespace erstellt wurde, kann er nicht mehr gelöscht werden; außerdem lassen sich sein „Identitätssymbol“ (oder „Code“ in der API) und „Typ“ nicht mehr ändern.

## Namespaces in Identitätsdaten

Die Angabe des Namespace für eine Identität hängt von der Methode ab, mit der Sie Identitätsdaten bereitstellen. Einzelheiten zur Bereitstellung von Identitätsdaten finden Sie im Abschnitt zum [Bereitstellen von Identitätsdaten](./home.md#supplying-identity-data-to-identity-service) in der Übersicht über den [!DNL Identity Service]
