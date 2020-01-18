Cloud Identity!
Bezpieczeństwo jest bardzo ważną cechą usług Google Cloud Platform, a GCP opracował specjalne narzędzia zapewniające bezpieczeństwo i tożsamość we wszystkich Twoich projektach. W tym zadaniu domowym, popracujesz z usługą GCP Identity and Access Management (IAM), która umożliwia tworzenie i zarządzanie uprawnieniami dla zasobów Google Cloud. Łączy kontrolę dostępu do usług w jeden system i przedstawia spójny zestaw operacji.

Wiesz już co to jest Cloud IAM i dlaczego jest tak ważną usługą. Zatem do dzieła!

Czas na zadanie!
Zadanie 1.
Klient poprosił cię o przygotowanie maszyny dla swoich pracowników, którzy będą mogli pobierać faktury z przygotowanego repozytorium ( w naszym przypadku jest to pojemnik Cloud Storage )

Twoim zadaniem będzie zapewnienie, że użytkownicy korzystający z maszyny, będą mogli odczytywać obiekty z danego pojemnika. Wykreuj instancję, która ma dostęp tylko do możliwości odczytywania obiektów znajdujących się w wytworzonym pojemniku Cloud Storage.

Wrzuć przykładowe dokumenty do swojego pojemnika, a następnie wyświetl jego zawartość z poziomu maszyny, którą przed chwilą skonfigurowałeś. Aby w pełni potwierdzić poprawność konfiguracji spróbuj wykonać usunięcie danego obiektu.

Jeśli masz problem z utworzeniem pojemnika w usłudze Cloud Storage to nie przejmuj się! Możesz cofnąć się do zadania domowego w Tygodniu 2, w którym tworzyliśmy pojemnik na potrzeby eksportu danych bilingowych do pliku. Możesz spojrzeć również do dokumentacji, którą znajdziesz pod tym linkiem - How to create Cloud Storage bucket

Zadanie 2.
Dany klient przetrzymuje bardzo ważne dokumenty. Zarząd zdecydował, że wprowadzą szyfrowanie krytycznych dokumentów, które będą mogły zostać odszyfrowane po stronie pracownika, który z danego dokumentu chce skorzystać.

Wykreuj instancję, której umożliwisz dostęp do pobierania dokumentów z pojemnika Cloud Storage. Oprócz uprawnień do pobierania obiektów musisz umożliwić użytkownikowi możliwość szyfrowania/odszyfrowywania danych za pomocą klucza znajdującego się w Cloud KMS.

Wytwórz klucz w usłudze Cloud KMS:

Może być to klucz symetryczny, którego użyjesz zarówno do zaszyfrowania jak i odszyfrowania dokumentu
Lub mogą być to dwa osobne klucze asymetryczne za pomocą, których zaszfrujesz oraz odszyfrujesz dokument.
Przetestuj poprawność konfiguracji za pomocą następujących kroków:

Umieść w pojemniku przykładowe dokumenty.
Na wykreowanej maszynie spróbuj pobrać przykładowy dokument.
Zaszyfruj dokument za pomocą klucza utworzonego wcześniej w Cloud KMS
Na sam koniec spróbuj odszyfrować dany plik, aby przywrócić do postaci pierwotnej.
Dla osób mających więcej czasu na zadanie zachęcamy, aby wykonać odszyfrowanie danych na innej maszynie niż ta, na której zostało wykonane szyfrowanie. To pozwoli lepiej przećwiczyć temat uprawnień do wykonywania różnych funkcji za pomocą różnych usług - w naszym przypadku Cloud Storage oraz Cloud KMS.

Zadanie 3.
3. Firma zdecydowała się już na ostatni krok ... zbudowanie niestandardowej roli za pomocą, której połączą możliwości szyfrowania oraz odszyfrowywania danych za pomocą KMS oraz dostępu do danych w Cloud Storage na poziomie READ

Wytwórz niestandardową rolę oraz przypisz odpowiednie uprawnienia, aby spełnić powyższe wymagania.
Zadanie wymagałoby stworzenia przykładowego użytkownika co wiąże się z założeniem nowego konta Google, dlatego w zamian za to proponujemy przejrzenie dokumentacji w jaki sposób jesteśmy w stanie wykreować niestandardową rolę: Creating custom roles - takich sposobów jest kilka.

Wszystkie wyniki swojej pracy umieść na naszym Facebooku! Wszelkie ciekawe wnioski oraz pytania również mile widziane!

Podsumowanie
Mamy nadzieję, że ten tydzień przyniósł ci bardzo dużą wiedzę na temat bezpieczeństwa i tożsamości w Google Cloud.

Miałeś okazję przećwiczyć jedne z najpopularniejszych tematów z egzaminu dotyczących Cloud Identity, dzięki czemu pytania na temat tej usługi nie powinny już sprawić ci problemu! 😉

Dziękujemy za rzetelną pracę w tym tygodniu!
Do zobaczenia!
