## Obnovování seznamu keší ##

Automaticky reaguje na změny polohy, při malé změně pouze znova setřídí seznam a překreslí ho s novými směry a vzdálenostmi. Při větší změně načte celý nový seznam. Hranice je polovina vzdálenosti nastavené ve filtru.
Vše se děje pouze pokud je referenční bod GPS, při pevném ručně zadaném bodu to nemá smysl.

Narozdíl pod PocketDrake tu není žádný pevný časový interval, vše se odehrává jen na základě změny polohy.

## Seznam čekajících logů ##
Zapsané logy se ukládají do databáze `_`adrake.db3 do tabulky geolog (stejná jako v GG)
Logy lze buď exportovat jako textový soubor Field Notes nebo odeslat on-line. Šablona pro log platí v obou případech, stejně jako počítání pořadí. Začátek je stejný - uživatel si v seznamu označí, které logy poslat a spustí akci:
  * Field Notes - vybrané logy se uloží do souboru, pokud je v nastavení zvoleno mazání po exportu, dojde k výmazu z tabulky a tím se končí - log ještě není na webu, takže z aDrake zmizí
  * Odeslání na web s okamžitou publikací - vybrané logy se přes Live API pošlou na web a pokud se to povede, přesunou se do standardní tabulky logů a z dočasné se vymažou. Log je na webu, tak se ukáže u keše mezi ostatními logy. Takto to funguje vždy.
  * Odeslání na web jako Field Notes - logu se přes Live API pošlou, ale nepuklikují se, jen se uloží do seznamu fieldnotes. Pokud se to povede, log z aD mizí.

## Výběr bodu z mapy ##
V menu vyberu
  1. keš => otevře se hlavní obrazovka, pokud chci na keš navigovat, mám tlačítko po ruce
  1. waypoint => vybraný waypoint se nastaví jako cíl, otevře se příslušná keš a ihned se přepne na kompas, který ukazuje na ten waypoint

## Kompas ##
V klidu se řídí magnetickým kompasem, při pohybu nad 1 m/s přepíná na GPS. Magnetický kompas často při chůzi zmateně poskakuje nebo vertikálně umístěný (např. v držáku auta) přestává fungovat úplně, GPS je v takové situaci lepší.

## Logy ##
Logy se zobrazují jako běžné ListView, klikem na jméno autora se ve webovém prohlížeči otevře jeho profil. Kvůli různým divočinám s diakritikou, kterou geocaching.com občas nepobere ani při URL encode se používá id logujícího, až v případě, že není k dispozici, použije se nickname.

Standardně se zobrazí právě seznam logů v databázi. Při aktualizaci logů z Gl Live se staré logy vymažou a následně se stáhne 10 posledních logů. Seznam je automaticky natahovací, tj. pokud uživatel sroluje na konec, načte se dalších 10. To funguje dokud nějaké další logy jsou.
Při opuštění keše a opětovném otevření se program vrátí do režimu zobrazení z databáze a další logy se už nenačítají.

## Obrázky ##
Galerie obrázků (od 1.11) se vytváří z těchto zdrojů:
  1. Obsah složky offline/inc/ patřící k dané keši
  1. Obsah složky spoilersync/ patřící k dané keši
  1. Tagy **gcimage** - pokud obrázek uložený v tomto tagu není v telefonu, automaticky se stáhne a uloží do offline/inc/
  1. soubory **.jpg z příloh (attach/...)**

Tag **gcimage** se přebírá z geogetu nebo importem přes Live API (úplná aktualizace keše)

Analogicky fungují obrázky v listingu - webové odkazy se převedou na lokální, obrázky se postahují a uloží do offline/sync

Při výmazu keše se maže i offline/inc a attach/... . Složka spoilersync/ se nemění, s té se jenom čte.

Od verze 2.0 se obrázky z listingu ukládají do databáze 