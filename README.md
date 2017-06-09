# Web testing using Python

*a workshop by Magdalena Kabátová for PyCon CZ 2017*

*Write and run automated tests of web applications in few hours and let it work for you since then. First brief introduction to web testing will be given. Then we will use pytest and Selenium frameworks to create automated tests of a demo web page.*

*Basic knowledge of Python is required (suitable for PyLadies). Basic knowledge of html and css (DOM and selectors) is advantage.*


## Potřebné technologie

Před zahájením workshopu potřebujete mít:

* nainstalovaný [Python 3](http://python.org) - postup instalace na [Nauč se Python!](http://naucse.python.cz/lessons/beginners/install/)
* nainstalovaný webový prohlížeč [Chrome](https://www.google.com/chrome/browser/desktop/index.html)
* nainstalovaný [git](https://git-scm.com/) - postup instalace na [Nauč se Python!](http://nau2cse.python.cz/lessons/git/install)
* účet na [github](https://github.com/)

Ostatní nainstalujeme během workshopu.


## Obsah workshopu

* Zahájení
* Úvod do testování SW
* Příprava na testování
* Automatické testování


## Úvod do testování SW

* [Přednáška](https://www.youtube.com/watch?v=3YekbncInhU) na PyCon CZ 2016


## Příprava na testování

* Testovací eshop: http://testshop.pyladies.cz

* Testovací scénáře: https://goo.gl/8bXLte

**Úkol:** Zaregistrujte se na [testovacím eshopu](http://testshop.pyladies.cz/accounts/login/). Email může být smyšlený, ale zapamatujte si ho.


## Automatické testování

### Použité technologie:

* [Python 3](http://python.org)
* [virtualenv](https://virtualenv.pypa.io/en/stable/) - nástroj pro tvorbu izolovaných Python prostředí
* [pytest](http://pytest.org/) - testovací framework pro Python (alternativou je Python unittest modul)
* [Selenium](http://www.seleniumhq.org/) - nástroj pro automatické testování webových aplikací
* [pytest-selenium](http://pytest-selenium.readthedocs.io) - selenium plugin pro pytest
* webový prohlížeč [Chrome](https://www.google.com/chrome/browser/desktop/index.html)
  Proč Chrome? [Proto!](http://www.zive.cz/clanky/valka-prohlizecu-v-roce-2016-ie-mizi-ze-sceny-a-vsechno-bere-chrome/sc-3-a-185443/default.aspx)
* [Google Chrome Driver](https://sites.google.com/a/chromium.org/chromedriver/downloads) - ovladač webového prohlížeče Chrome
* verzovací systém [git](https://git-scm.com/) a webová služba [github](https://github.com/)

### Instalace

1. Otevřete konzoli a vstupte do vámi zvolené složky:
  ```
  cd my_projects
  ```

2. Naklonujte si repozitář [`webtesting`](https://github.com/madlenkk/webtesting.git) z githubu a vstupte do složky `webtesting`:
  ```
  git clone https://github.com/madlenkk/webtesting.git
  cd webtesting
  ```

3. Vytvořte virtuální prostředí:
  ```
  virtualenv -p python3 venv-tests
  ```

4. Spusťte virtuální prostředí:

  * Windows:
  ```
  > venv-tests\Scripts\activate.bat
  ```
   *Pozn.: V případě potíží, restartujte bash.*

  * Linux/macOS:
  ```
  $ source venv-tests/bin/activate
  ```

5. Do vitruálního prostředí nainstalujte potřebné balíky uvedené v souboru [`requirements.txt`](requirements.txt) pomocí `pip`:
  ```
  pip install -r requirements.txt
  ```
  Úspěšnost této instalace můžete ověřit například pomocí příkazu:
  ```
  pytest --version
  ```

6. Proveďte instalaci a nastavení webového ovladače:

  * [Windows](installation/install_windows.md)
  * [Linux](installation/install_linux.md)
  * [macOS](installation/install_macos.md)

  Stáhněte a nainstalujte [Google Chrome Driver](https://sites.google.com/a/chromium.org/chromedriver/downloads).
  Přidejte `chromedriver` do adresáře `$PATH`:
    * Windows: Exportujte zip, uložte soubor chromedriver.exe a přidejte cestu k souboru do Environment Variables (PATH).
    * Linux: Exportujte zip do `/usr/local/bin/`.

7. Správné nastavení webdriveru ověřte spuštěním zkušební testu [`installation.py`](installation/test_installation.py), který se nachází ve složce `installation`:
  ```
  python installation/test_installation.py
  ```
  Pokud je vše v pořádku, spustí se prohlížeč, provede se test, prohlížeč se opět vypne a v konzoli se vypíše výsledek testu. 
  Sledujte, co se děje v prohlížeči a následně proveďte úkon, který test vypsal do vaší konzole.


### Spuštění testů

Všechny testy jsou uloženy ve složce [`tests`](tests) a rozděleny do podsložek podle testovacích scénářů (suites). 

Před spuštěním testů, je potřeba:
* mít aktivované virtuální prostředí `venv-tests`
* být ve složce `tests`

Vaše konzole by tedy měla vypisovat zhruba toto: `(venv-tests) username: ~/webtesting/tests $` (Linux).

Všechny testy ve složce `tests` můžete spustit pomocí příkazu:
```
pytest
```

Pytest spouští automaticky všechny soubory a funkce začínající slovem `test`, které najde v akutální složce a jejích podsložkách. I ty musejí začínat slovem `test`.

Pokud chcete spouštět testy jednotlivě, přidejte cestu k souboru s daným testem - např.:
```
pytest test_suite_02_login/test_case_02_invalid_login.py
```

Probíhající test můžete přerušit zavřením prohlížeče, ve kterém test probíhá, nebo v konzoli pomocí `CTRL + C` (Linux).


### Konfigurace testů

Rozmanitá konfigurace je uložena v souboru [`pytest.ini`](tests/pytest.ini), díky kterému není potřeba vypisovat parametry do konzole. Nicméně vypsáním parametrů do konzole lze výchozí konfiguraci přebýt nebo doplnit.
```
pytest --html=reports/another_report.html
```

Více o jednotlivých parametrech se dozvíte pomocí:
```
pytest --help
```

Nebo v dokumentaci: 


### Proměnné

V jednotlivých testech jsou použity proměnné, které jsou odděleny od kódu a najdete je v souboru [`variables.json`](tests/variables.json).

**Úkol:** Otevřete soubor `variables.json` v textovém editoru a přepište hodnoty proměnných na vaše vlastní - `username` a `password` se musí shodovat s údaji, které jste vyplnili při registraci do testovacího eshopu. 
Spusťte test pro **validní** přihlášení a html report nechte vypsat do souboru `reports/01_valid_login.html`.


### Psaní testů



### Logy a reporty



## Úkoly

1. Napište test na odhlášení z testovacího eshopu - podle testovacího scénáře (test suite 06_logout).
  * vytvořte složku pro test suite `test_suite_06_logout_**vase_jmeno**`
  * vytvořte soubor pro test case `test_case_01_logout.py`
  * využijte v něm už hotové funkce (test_case_01_valid_login.py)
  * uložte a spusťte test
  * pokud test prošel, pošlete vaši změnu na github
  ```git add test_suite_06_logout
     git commit -a -m"Adding test for logout
     git push
  ```
