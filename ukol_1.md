# Zadání úkolu 1

Tvým úkolem je vytvořit aplikaci pro zjednodušený výpočet daně z nemovitostí. Aplikace bude postavená na principech OOP. Tato daň se vztahuje na pozemky, bytové a komerční prostory. Výše daně se odvíjí od několika faktorů, např. typu nemovitosti, velikosti, lokalitě, kde se nemovitost nachází atd.

### Lokalita

V rámci aplikace nejprve vytvoř třídu `Locality`, která označuje lokalitu, kde se nemovitost nachází. Třída bude mít atributy `name` (název katastru/obce) a `locality_coefficient` (tzv. místní koeficient, který se používá k výpočtu daně).

### Nemovitosti

Vytvoř třídu `Property`, která bude reprezentovat nějakou nemovitost. Třída bude mít atribut `locality` (lokalita, kde se pozemek nachází, bude to objekt třídy `Locality`).

Dále vytvoř třídu `Estate`, která reprezentuje pozemek a je potomkem třídy `Property`. Třída bude mít atributy `locality`, `estate_type` (typ pozemku), `area` (plocha pozemku v metrech čtverečních). Dále přidej metodu `calculate_tax()`, která spočítá výši daně pro pozemek a vrátí hodnotu jak celé číslo (pro zaokrouhlení použij funkci `ceil` z modulu `math`). Daň vypočítej pomocí vzorce: plocha pozemku * koeficient dle typu pozemku (atribut `estate_type`) * místní koeficient. U atributu `estate_type` následující hodnoty a koeficienty:

- _land_ (zemědělský pozemek) má koeficient 0.85.
- _building site_ (stavební pozemek) má koeficient 9.
- _forrest_ (les) má koeficient 0.35,
- _garden_ (zahrada) má koeficient 2. 

Uvažujme tedy například lesní pozemek o ploše 500 metrů čtverečních v lokalitě s místním koeficientem 2. Potom je daň 500 * 0.35 * 2 = 350.

Jako druhou vytvoř třídu `Residence`, která reprezentuje byt, dům či jinou stavbu a je potomkem třídy `Property`. Třída bude mít atributy `locality`, `area` (podlahová plocha bytu nebo domu) a `commercial` (pravdivostní hodnota, která určuje, zda se jedná o nemovitost používanou k podnikání). Dále přidej metodu `calculate_tax()`, která spočítá výši daně pro byt a vrátí hodnotu jako číslo. Daň vypočítej pomocí vzorce: podlahová plocha * koeficient lokality * 15. Pokud je hodnota parametru `commercial` `True`, tj. pokud jde o komerční nemovitost, vynásob celou daň číslem 2.

### Příklady výpočtu

Uvažujme tedy například byt (určený k bydlení) o ploše 60 metrů čtverečních v lokalitě s koeficientem 3. Potom je daň 60 * 3 * 15 = 2700. Pokud by stejný byt byl používán k podnikání, daň by byla 60 * 3 * 15 * 2 = 5400.

Vyzkoušej svůj program pomocí následujících nemovitostí:

- Zemědělský pozemek o ploše 900 metrů čtverečních v lokalitě Manětín s koeficientem 0.8. Daň z této nemovitosti je 900 * 0.85 * 0.8 = 612.
- Dům s podlahovou plochou 120 metrů čtverečních v lokalitě Manětín s koeficientem 0.8. Daň z této nemovitosti je 120 * 0.8 * 15 = 1440.
- Kancelář (tj. komerční nemovitost) s podlahovou plochou 90 metrů čtverečních v lokalitě Brno s koeficientem 3. Daň z této nemovitosti je 90 * 3 * 15 * 2 = 8100.

### Bonusy

Tyto bonusy jsou nepovinné a záleží čistě na tobě, zda se do nich pustíš. Jednotlivé části jsou nezávislé, můžeš si tedy vybrat libovolné odrážky a ty vyřešit.

- Ke třídě `Estate` a `Residence` přidej výpisy informací do metody `__str__()`. Např.: _Zemědělský pozemek, lokalita Manětín (koeficient 1), 900 metrů čtverečních, daň 765 Kč._
- Přečti si [bonusový text o abstraktních třídách](https://kodim.cz/czechitas/python-oop/lekce/dedicnost/abstraktni-tridy) a uprav třídu `Locality` na abstraktní třídu. Tato třída totiž nereprezentuje žádnou konkrétní nemovitost, nemovitost totiž musí být pozemek nebo stavba.
- Přidej třídu `TaxReport`, která bude reprezentovat daňové přiznání. Třída bude mít atributy `name` (jméno osoby, která přiznání podává) a `property_list`, což je seznam nemovitostí, které jsou v přiznání uvedeny. Dále přidej metodu `add_property()`, která bude mít jako parametr objekt (nemovitost, která je součástí přiznání) a vloží ji do seznamu `property_list`. Dále přidej metodu `calculate_tax`, která vypočte daň ze všech nemovitostí v seznamu `property_list`.
- Podívej se na to, jak fungují tzv. enum třídy. Můžeš si přečíst například [tento text](https://www.geeksforgeeks.org/enum-in-python/). Zkus vytvořit třídu pro typy pozemků (zemědělský pozemek, stavební pozemek, les, zahrada) a použít ji ve třídě `Estate`. Použití této třída zabrání, aby byl vytvořen pozemek s neexistujícím typem.
