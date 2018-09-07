---
title: Czym jest Git? Wstęp do pracy z systemem kontroli wersji.
date: 2018-09-07 09:00:00
tags: 
- git
- kontrola wersji
categories:
- programowanie
- kontrola wersji
- git
---

**Git, choć nie wymaga właściwie żadnych umiejętności programistycznych, wciąż pozostaje narzędziem typowo deweloperskim. A trochę szkoda, bo po przebrnięciu przez trudne początki pracy z Git-em, jego stosowanie może oszczędzić nam sporo pracy i nerwów. Czym zatem jest Git?**

Wyobraźmy sobie sytuację, w której musimy przygotować dokument tekstowy, przeznaczony do druku. Zanim jednak go wydrukujemy, chcemy, aby został sprawdzony pod względem poprawności językowej przez inną osobę. Nawet jeśli piszemy składnie i ortografia nam nie straszna, są spore szanse na to, że zostanie nam zwrócony dokument z poprawkami. Mamy więc teraz już dwa dokumenty. Niech do tego dojdą nasze osobiste poprawki, które bez zastanowienia dodaliśmy do kopii wersji jeszcze niesprawdzonej. W efekcie mamy trzy wersje dokumentu, żadna z nich nie jest nadającą się do druku wersją ostateczną. Przykład z życia wzięty, prawda?

**mój_plik-nowy.doc**

**mój_plik-nowszy.doc**

**mój_plik-nowy-korekta-wersja2.doc ... :'(**

Jak bardzo sprawa się skomplikuje, jeśli nad edycją dokumentu pracuje cały zespół osób? Bardzo. Pierwszy napotkany problem - w danym momencie nad jednym dokumentem może pracować **tylko jedna osoba**. Dodatkowo, po zakończonej edycji każdy musi pamiętać, aby poinformować o wprowadzeniu zmian kolejnego edytora dokumentu i przekazać mu aktualną wersję pliku. Nawet nie myślmy o tych wiecznie ginących pendrive’ach i plikach nazywanych w stylu super-hiper-wersja-finalna-pliku-xxx-do-druku.doc. Każdy błąd w komunikacji zespołu ma co najmniej jeden zły skutek - wiele niespójnych wersji, brak wersji finalnej. Na szczęście - jest Git.

Git - jak to działa?
---
Git likwiduje problem wielu wersji pliku w zarodku, zapewniając nam system do ich kontroli. Pracujemy z **repozytorium** (skrótowo **repo**) - lokalnym (tym na naszym komputerze) oraz zdalnym (postawionym na platformie wspierającej kontrolę wersji). **Repozytorium zdalne** jest miejscem, gdzie trzymane są wersje dokumentów oficjalnie uznawane za **aktualne**, wszystkie inne wersje są nieaktualne. Każdy członek projektu ma na własnym komputerze **repozytorium lokalne**, które jest podpięte do zdalnego. Zmiany dokonywane lokalnie nabierają znaczenia dopiero po opublikowaniu ich w repozytorium zdalnym. Prostymi słowami - to, co robimy z plikami na własnym komputerze nie ma znaczenia, dopóki nie publikujemy ich w repozytorium zdalnym. Jednocześnie wszystkie zmiany wprowadzone lokalnie mogą zostać opublikowane, jeśli tego chcemy.

Workflow
--
W projektach zarządzanych Git-em obowiązuje flow: pobierasz najnowszą wersję pliku ze zdalnego repozytorium, edytujesz, a kiedy uznasz, że zmiany przez Ciebie wprowadzone powinny być dodane do pliku na stałe - wysyłasz plik na zdalne repozytorium (to w skrócie). Tam wszyscy już będą mogli zobaczyć wyraźnie zaznaczone różnice w najnowszej wersji (tej wysłanej przez Ciebie), porównanej do tej przed Twoimi zmianami. Oczywiście ważna będzie tylko ta ostatnia, wysłana przez Ciebie (przynajmniej do momentu, aż ktoś ją nadpisze). Za sprawą śledzenia przez Git całej historii zdarzeń, wszystkie akcje przeprowadzane na Gicie (może poza reset hard-em ;]) można cofnąć, każdą wersję pliku można odzyskać.

Wszystko idzie gładko, dopóki zmiany w plikach zachodzą liniowo - jedne zmiany wchodzą po innych. Problem zaczyna się wtedy, kiedy dwóch edytorów wprowadzi zmiany w tej samej linijce, lub jeden usunie linię, którą inny edytuje (w tej samej wersji pliku). Powstają wtedy tzw. **konflikty**, które się rozwiązuje. Jest to temat na osobny artykuł, a na chwilę obecną niech wystarczy nam fakt, że nie jest to sytuacja bez wyjścia. Tak więc, pomimo, że Git nie rozwiązuje pewnych problemów sam, to i tak znacznie ułatwia ogarnięcie chaosu wokół tworzenia wszelkiego rodzaju dokumentów tekstowych. A teraz - przyjrzyjmy się na moment gdzie i co możemy przechowywać z pomocą Git-a. 

Korzyści z prowadzenia projektów na Git-cie
--
1. Spójność projektu.
2. Wiemy, kto i kiedy wprowadził zmiany. 
3. W przypadku plików tekstowych - wiemy dokładnie, jakie zmiany zostały wprowadzone.
4. Możemy odzyskać dowolną wersję dokumentu z historii Git-a.

Gdzie założyć repozytorium?
---
Najbardziej popularną platformą wspierającą kontrolę wersji jest **[Github](https://github.com/)**. Inny godny polecenia produkt to **[Bitbucket](https://bitbucket.org/)** Atlassian’a. Zaletą pierwszego z nich jest popularność - wszystkie projekty open source, z jakimi się do tej pory spotkałam, były tworzone na Githubie. Małym minusem jest to, że za prywatne repozytorium musimy tutaj zapłacić. Bitbucket mogę polecić ze względu na darmowe, choć z pewnymi ograniczeniami, prywatne repozytoria. Taka opcja jest bardzo korzystna, jeśli dopiero uczymy się korzystać z Git’a i zależy nam na prywatnym repo bez opłat. Tym, którzy nie boją się iść na całość, polecam darmowe, publiczne repo na Githubie.

Co przechowywać w repo?
---
W repozytorium możemy umieszczać pliki wszelkiego rodzaju, ale musimy pamiętać o jednym - Git jest w stanie śledzić zmiany tylko w plikach tekstowych. Dla wyjaśnienia - pliki tworzone w Microsoft Word (oraz jakiejkolwiek innej aplikacji do edycji tekstu, poza zwykłym notatnikiem) **nie są plikami tekstowymi** w tym kontekście i Git nie będzie mógł śledzić zmian w tego rodzaju plikach. Pliki **HTML** lub **markdown** (plik tekstowy bez formatowania) spełniają te wymagania. Jak to jest z grafikami? W przypadku map bitowych - grafik w formatach **.jpg/.png/.ttf** - wersjonowanie jest utrudnione. Git nie jest w stanie wykryć różnic między dwoma grafikami rastrowymi. Nie oznacza to jednak, że nie warto wykorzystywać repozytorium do przechowywania tego rodzaju plików. Każde uaktualnienie pliku rastrowego będzie po prostu widoczne jako nowe załadowanie tego pliku. I choć dokładne różnice nie będą wyszczególnione, to będzie wiadomo kto i kiedy dokonał zmian.
Omówiliśmy już pliki rastrowe, a co z wektorowymi? 

Grafika wektorowa (**.svg**) jest bardzo ciekawym przypadkiem grafiki, a jedną spośród wielu jej zalet jest to, że obraz wektorowy jest w zasadzie plikiem tekstowym. Dlatego też Git "widzi" różnice między dwoma plikami wektorowymi. Dla mnie jest to jeden z mocnych argumentów przemawiających za tym, aby stosować grafikę wektorową tam, gdzie tylko jest to możliwe. 

Kilka słów na koniec
---
1. System kontroli wersji to pojęcie szersze niż tylko Git. Jest kilka systemów wspierających wersjonowanie, a Git jednym z nich.
1. Prowadzenie projektu na Git-cie zapewnia nam dane: kto i kiedy tworzył zmiany w repozytorium, a w przypadku plików śledzonych przez Git zaznaczy dokładne zmiany (na zielono - co dodano, na czerwono - co usunięto, brak oznaczenia oznacza brak zmian).
1. Trzymanie projektu w repozyrorium publicznym oznacza, że **każdy** ma do nich dostęp. Jeśli chcemy chronić nasze pliki, to tylko w repo **prywatnym**.
1. Do używania Git-a potrzebny jest w zasadzie tylko Internet. Do pisania komend Git-owych można używać **wiersza polecenia** (**terminal**), ale można też stosować aplikacje pośredniczące (np. **[Sourcetree](https://www.sourcetreeapp.com/)**).
1. Więcej o systemie znajdziemy na oficjalnej stronie **[Git-a](https://git-scm.com/)**. Po instrukcje instalacji oraz stawiania pierwszego projektu zapraszam do kolejnego posta w tematyce Git.