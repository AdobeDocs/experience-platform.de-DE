---
product: experience-platform
audience: user
user-guide-title: Hilfe zum Experience-Datenmodell (XDM)-System
breadcrumb-title: Handbuch zum Erlebnisdatenmodell (XDM)
user-guide-description: Verwenden Sie Experience Data Model (XDM)-Klassen und -Mixins, um Erlebnisdaten zu standardisieren.
translation-type: tm+mt
source-git-commit: d96890fd79acaa09628dbba49ee6930ed4f9d0e6
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 58%

---


# Experience-Datenmodell (XDM)-System {#xdm}

* [XDM-System – Übersicht](home.md)
* Schemas {#schema}
   * [Grundlagen der Schemakomposition](schema/composition.md)
   * [Bewährte Verfahren für die Datenmodellierung](schema/best-practices.md)
   * [XDM-Feldtypeinschränkungen](schema/field-constraints.md)
   * [Wörterbuch der XDM-Felder](schema/field-dictionary.md)
   * Anwendungsfälle des Schemas {#use-cases}
      * [Datentyp &quot;Inhalt und Voreinstellungen&quot;](schema/privacy-consent.md)
* Klassen {#classes}
   * [XDM Individuelles Profil](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
* Mixins {#mixins}
   * Profil mixins {#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [Demografische Details](./mixins/profile/person-details.md)
      * [Persönliche Kontaktangaben](./mixins/profile/personal-details.md)
      * [Details zur Segmentmitgliedschaft](./mixins/profile/segmentation.md)
      * [Kontaktangaben bearbeiten](./mixins/profile/work-details.md)
   * Ereignis mixins {#event}
      * [Details zur Endbenutzer-ID](./mixins/event/enduserids.md)
      * [Umgebung](./mixins/event/environment-details.md)
   * [Aktualisierung von Mischnamen](./mixins/name-updates.md)
* Datentypen {#data-types}
   * [Beacon](./data-types/beacon.md)
   * [Browserdetails](./data-types/browser-details.md)
   * [Zustimmung und Voreinstellungen](./data-types/consents.md)
   * [Gerät](./data-types/device.md)
   * [E-Mail-Adresse](./data-types/email-address.md)
   * [Umgebung](./data-types/environment.md)
   * [Geo](./data-types/geo.md)
   * [Geo-Kreis](./data-types/geo-circle.md)
   * [Geo-Koordinaten](./data-types/geo-coordinates.md)
   * [Details zur Geo-Interaktion](./data-types/geo-interaction-details.md)
   * [Geo-Form](./data-types/geo-shape.md)
   * [Identität](./data-types/identity.md)
   * [Personenname](./data-types/person-name.md)
   * [Telefonnummer](./data-types/phone-number.md)
   * [Ortskontext](./data-types/place-context.md)
   * [POI-Details](./data-types/poi-details.md)
   * [POI-Interaktion](./data-types/poi-interaction.md)
   * [Postadresse](./data-types/postal-address.md)
* Schema Registry-API {#api}
   * [Übersicht](api/overview.md)
   * [Erste Schritte](api/getting-started.md)
   * [Schemas](api/schemas.md)
   * [Klassen](api/classes.md)
   * [Mixins](api/mixins.md)
   * [Datentypen](api/data-types.md)
   * [Deskriptoren](api/descriptors.md)
   * [Vereinigungen](api/unions.md)
   * [Ad-hoc-Schemata](api/ad-hoc.md)
   * [Anhang](api/appendix.md)
* Tutorials {#tutorials}
   * [Erstellen eines Schemas (API)](tutorials/create-schema-api.md)
   * [Erstellen eines Schemas (Benutzeroberfläche)](tutorials/create-schema-ui.md)
   * [Datentypen erstellen und bearbeiten (Benutzeroberfläche)](./tutorials/create-data-type.md)
   * [Definieren einer Beziehung zwischen zwei Schemata (API)](tutorials/relationship-api.md)
   * [Definieren einer Beziehung zwischen zwei Schemata (Benutzeroberfläche)](tutorials/relationship-ui.md)
   * [Erstellen eines Ad-hoc-Schemas (API)](tutorials/ad-hoc.md)
* [Handbuch zur Fehlerbehebung](troubleshooting-guide.md)
* [API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [Versionshinweise zur Plattform](https://docs.adobe.com/content/help/de-DE/experience-platform/release-notes/latest.html)