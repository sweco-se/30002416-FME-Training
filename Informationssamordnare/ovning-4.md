---
description: Läs in Excel och jämför
---

# Övning 4

Du känner på dig att alla filer inte har levererats ännu och vill veta hur leveransfilerna och handlingsförteckningen stämmer överens. Din uppgift är att jämföra filerna i leveransmappen med handlingsförteckningen och skriva ut en excellfil som visar på hur statusen ser ut.\
I projektmappen finns en handlingsförteckning 1568-C1-21-06033 (C:\FMEData2025\Data\Informationssamordnare\03\_Dokument\00\_Förteckningar) i Excel- format



* Utgå från övning 3 och lägg till en Reader för att läsa in Excel-filen med\
  handlingsförteckningen.
* Matcha filnamnen i handlingsförteckningen med filen i katalogen.
  * Testa med en FeatureMerger eller testa med en FeatureJoiner
* Skriv en flik i Excel med filer som finns i handlingsförteckningen
* Skriv en flik i Excel med filer som saknas i handlingsförteckningen
* Skriv en flik i Excel med filer som saknas i mappen.

<details>

<summary>Bonus:</summary>

* Kan vi ta ut vilken tekniksystem filen hör till?
  * Lägg till en StringSearcher transformer efter din joiner
  * Searh In: vilket attribut innehåller informationen vi letar efter?
  * Contains Regular Expression: (?<=Systemhandling\\)(.\*?)(?=\\)
  * Matched Result: attributnamn (t.ex. tekniksystem)

</details>
