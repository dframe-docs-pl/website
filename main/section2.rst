.. center::
 Postawowa Struktura plików

.. div:: row
 .. div:: col-sm-6
  **Bootstrap.php** - znajdują się globalny dostępne zmienne. Jest to podstawowa klasa która jest dostępna w całym projekcje i jest ładowana na starcie. Dostęp poprzez zmienną $this->baseClass. W przykładowym projecie znajduje się tu przedewyszystkim ładowanie sesji, tokenów i załadowanie bazy danych.
  
  **Config** - folder zawiera pliki konfiguracyjne w postaci 
  
  .. code-block:: php
   return array(
       'klucz' -> 'Wartość',
       'innyKlucz' => 'Inna Wartość'
   );
  W naszym przypadku znaduje się jeszcze **router.php** gdyż przykładowa aplikacja używa Dframe\Router oraz folder **view** z plikiem **smarty.php** bo w przykładzie użyliśmy silnik **S.M.A.R.T.Y** jednak do renderowania html można użyć dowolnego systemu np: **Twig, Mustache** ewenualnie czysty php
  
  **Controller** - kluczowym plikiem jest tutaj **Controller.php** Łączy on ze sobą Router i wymieniony wcześniej |baseClass|

  Uwaga!

  - Każde klasy które są w tym folderze muszą dziedziczyły tą klase bądź klase która się do niej odwołuje 
  |extentionController|
  - Zamiast |__construct()| używamy metody |init()| działa ona w takim sam sposób

  **View** - folder ten odpowiada za warstwę widoku niedostępną bezpośrednio z adresu.

  - **index.php** można dowolnie modyfikować i dopisywać metody które będą dostępne w szablonie przykładem takiego dopisania może być np jakaś klasa autoryzacji. Używając |auth()| W łatwy sposób można np określać wyświetlane treści. W templatce na przykładzie używanego silnika przestawia się sposób |isLogin()|
  - **config.php** ogólna konfiguracja ewentualnie dostępy do debugowania, nazwa i wersja aplikacji oraz adres pod jakim się znajduje dla dev oraz produkcji
 .. div:: col-sm-6
  .. code-block:: bash
   |   composer.json
   |   composer.lock
   |   LICENSE
   |         
   +---app
   |   |   Bootstrap.php
   |   |   
   |   +---Config
   |   |   |   router.php
   |   |   |   
   |   |   \---view
   |   |           smarty.php
   |   |           
   |   +---Controller
   |   |       Controller.php
   |   |       Page.php
   |   |       
   |   \---View
   |       |   Index.php
   |       |   View.php
   |       |   
   |       +---templates
   |           |   footer.html.php
   |           |   header.html.php
   |           |   index.html.php
   |           |        
   |           +---errors
   |           |       404.html.php
   |           |       
   |           +---page
   |                 test.html.php
   | 
   +---vendor
   \---web
       |   config.php
       |   index.php
       |   
       +---assets


.. |baseClass| cCode:: $this->baseClass
.. |extentionController| cCode:: extention Controller\Controller
.. |__construct()| cCode:: __construct()
.. |init()| cCode:: init()
.. |auth()| cCode:: $this->assign('auth', new auth());
.. |isLogin()| cCode:: {if $auth->isLogin()} Treść Tylko dla zalogowanej osoby {/if}
