# Közösségek (Community) a Mátrix protokoll szerint

## Bevezető

- https://medium.com/@RiotChat/communities-aka-groups-are-here-announcing-riot-web-0-13-riot-ios-0-6-and-riot-android-0-7-4-933cb193a28e

## Használati esetek

Több használati esetét is látom:

- Alap felhasználásra ha sok szobában vagyunk, tudunk kattintásra váltani a perspektívák között
- Az egyes közösségekhez tartozó új üzenetek száma is a közösség ikonján van összegezve, így nem kell végiggörgetni a szobalistán annak ellenőrzéséhez, hogy van-e valami fontos
- Egy konkrét nagyobb projektnek lehet egy olyan közössége ahol elkülönítik a fejlesztői, automatizációba bekötött, hibabejelentésre szolgáló vagy az off topic szobáikat

További használati eset ha ezen kívül egy felhasználó a beállításainál engedélyezi a `flair` mutatását 1-1 közösséghez (és az adott szoba is mutatja az adott flairt):

- Segít másokkal megismertetni magunkat azzal, hogy tudják milyen érdeklődéssel rendelkezünk (például ha egy társalgó csatornán sokan vannak és mindenkinek minden flairje látszik).
- Büszkék lehessünk a közösségekre amihez tartozunk
- A legfontosabb pedig a promóció ("manuális ajánlói rendszer"): ezzel segít a szoba többi résztvevőjének megismertetni az adott szobához kapcsolódó egyéb releváns szobákat a hozzá tartozó közösségen belül illetve hogy látszódjék: egy olyan ember aki ebben a közösségben benne van milyen más, kapcsolódó közösségben lehet benne és ez érdekelheti-e őket is

## Példák

A mátrix magyar szelete egyelőre még nagyon kicsi. Ha valaki újonnan regisztrál a mátrixra, honnan tudja, hogy mik a magyar szobák amikre érdemes csatlakozni? Pont erre van a `+magyarul:matrix.org` És honnan tudja, hogy van ilyen közösség? Elképzelhető, hogy aki meghívta mátrixra ezt is elmondta neki, de lehet, hogy ő csak 1 szoba miatt hívta meg és nem tartotta fontosnak. Nem lehet mindenki gondolatolvasó. Viszont az első olyan szobán keresztül ahol látszik ez a flair máris kap egy linket a többire.

Egy másik fontos példa a `+linuxhu:matrix.org` csatornák a különféle Linuxokra vagy a `+programozas:matrix.org` ahol a magyar programozás vonatkozásai vannak összegyűjtve, de külföldön számtalan más jellegű téma is van. 

Mondjuk ha a "Magyar Wikimédisták" helyett egy "Magyar Szabad Tartalomgyártók", "Magyar Techwriterek" vagy ilyesmi közösségre fókuszálnánk, abba beleillene például a már meglévő `#openscope:grin.hu` is, illetve később más (akár oktatási célú) CC könyv/podcast/videó gyártással foglalkozó közösségek akikkel szintén létezhet kooperáció illetve működésbeli vagy érdeklődésbeli hasonlóság.

Egy extrém példa a sokrétű kapcsolódásra, ha valaki fejleszt egy szótár alkalmazást és ehhez feldolgozza egyszerre a Wiktionary, a FreeDict és az OpenScope szótárait is egyben (a licenc kérdéstől most tekintsünk el), de ennél lazább kapcsolódás esetén is érzem a relevanciát.

## Mennyit mutassunk

Igazából még mi is csak barátkozunk az ötlettel, de egyelőre a legtöbb használati esetre praktikusnak számítana ha minden szoba mutatná szinte az összes flairt - a normál tagok úgysem szoktak több mint 2-3 közösséghez tartozni.

Ha egy-egy szoba minél kevesebb flairt akarna megjeleníteni, extrém esetben csak egyetlen egyet - pont azt amiben az egyetlen említett szoba van, és kölcsönösségi elven máshol sem jelenítik meg ezt a flairt, tehát ki-ki a saját flairjét, az kevésbé informatív. Innen is látszik, hogy csak akkor hasznos, ha van egy kis "áthallás", egy kis "perturbáció" is a különböző szobák között.

Ellenben az olyan közösség amibe (szinte) csak egyetlen szoba illik bele az tényleg kakukktojás.

## Alternatív mátrix megoldások

Mivel a Matrix community-k felfedezhetősége nem valami jó (nincs hozzá kereső mint a szobákhoz), ennek a megoldása vagy a flair mutatása, vagy az, hogy a résztvevők manuálisan begépelik valamilyen időközönként a community ID-t és ezzel ajánlgatják másoknak is, hogy lépjenek be, de ez elég zavaró lehet a résztvevőknek. Persze lehetne még manuális community invite is a szobákhoz hasonlóan de az nem skálázódik és nincs is ilyen funkció a felületen kiajánlva.

Alternatíva lenne ha minden magyar szoba fejlécébe minden másik magyar csatorna linkjét beraknánk, de ez se nem skálázható, se nem áttekinthető.

Esetleg minden magyar szoba fejlécébe egy osztott dokumentumot ahol fel van sorolva az összes többi. Felmerült még egy olyan gyűjtőszoba belinkelése ide ahová mindenki bedobhatja és pinnelheti a szobaajánlásait.

## Más rendszerekben

A publikus felhasználói profilokon keresztüli információközlés előnyben részesítése valóban egy ismert vélemény amit más rendszer is követ, de az nem reális, hogy egy cset szobában minden résztvevő profilját egyenként végigkattintgatja valaki, és ezt rendszeresen megismétli (mivel emberek beléphetnek-kiléphetnek közösségekből). Eddig ez csak akkor fordult elő velem ha valakinek vicces vagy ismerős volt a profilképe és megnéztem volna nagyobban.

Slacken még céges, szabályozott környezetben is azokat a mezőket amik nem bukkannak fel a cset szobában az egér alatt, az vagy ki lesz töltve vagy nem, esetleg nem lesz aktuális vagy annak tartalma nem lesz hasznos.

A Meetup.com inline-olja mindenki bemutatkozását egy-egy csoport `members` oldalán, az `event attendees` oldalán pedig kiemeli az 1-1 résztvevővel közös csoportokat.

Sok fórummotoron az üzeneteink mellett a nevünkön és képünkön kívül tipikusan szintén sokféle információt mutathatunk: ország, aláírás, hivatás, kedvenc oprendszer, kedvenc csapat, weblap, stb.

## Jövőbeli lehetséges fejlesztések

Ha flair nélkül akarnánk ezt csinálni, mondjuk egyes használati esetekre az is működne ha valahol a szoba tulajdonságai között (a tárgy mellett?) lenne egy statisztika szekció ahol mutatnák, hogy az itt lévő emberek közül hány ember milyen más szobákban/közösségekben vesz részt.

A többi használati esetre viszont nem volna elegendő a profilban való feltüntetés. Ha körbenézünk akár politikai vagy más mozgalmakkal kapcsolatos témakörökben, ott is sokszor beleírnak átmenetileg akár a display name-be hívószavakat, rövidítéseket a közösségi hálókon, ami nem túl elegáns dolog (és nem kattintható), de mindenesetre közismert, hogy az a figyelemfelhívás leghatékonyabb módja, ha az üzeneteink környéken szerepel ez az információ, nem pedig indirekcióval.

Szóval a flair nyilván egy úttörő kezdeményezés, egy kísérlet, és nem egy jól bevált recept, de ezért én még nem szólnám le - látok benne fantáziát. Nyilván a fórumokhoz képest a csetrendszeren a rövidebb üzeneteket figyelembe véve kompaktabb alternatívát kellett keresni és szerintem jó kompromisszumot képviselnek a nevünk melletti kis ikonok amik nem növelik az üzenet vertikális helyfoglalását sem.
