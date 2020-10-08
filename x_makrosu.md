## X MAKROSU

Elimizde bir liste var ve bu listeyi kaynak dosyalarımızda bir çok yerde kullanıyoruz. Bu listeyle ilgili mantıksal bir ilişkisi olan kodlarımız, örneğin, dizilerimiz, numaralandırma sabitlerimiz, `switch` deyimlerimiz var. Listeye bir öğe eklendiğinde bu listeyle mantıksal ilişkisi olan bu kodlarımızın değiştirilmesi gerekiyor. `X makrosu` olarak bilinen idiyom hem işimizi kolaylaştırıyor hem de kodlama hatalarına karşı bizi koruyor. Peki nedir bu `X makrosu`?
Örnek olarak listemizde birden fazla yerde kullanacağımız renk ifade eden değerlerimiz olsun. Başlangıçta renklerimizin `WHITE, YELLOW, GRAY ve MAGENTA` olduğunu düşünelim. Aşağıdaki koda bakalım:

```
#define  XCOLORS \
X(WHITE) \
X(YELLOW) \
X(GRAY) \
X(MAGENTA)
```

Makromuzu tek satır halinde de yazabilirdik. Ancak okunması daha kolay olsun diye listenin her bir öğesini ayrı bir satıra yazmayı tercih ettik. Makromuzun alt satırdan devam edebilmesi için ters bölü `(\)` karakterinin kullanılması gerektiğini biliyorsunuz. Listemizdeki her bir ismin `X`'i izleyen bir parantez içine alındığını görüyorsunuz. Şimdi bu isimlerle bir numaralandırma `(enum)` türü oluşturuyoruz:

```
#define  XCOLORS \
X(WHITE) \
X(YELLOW) \
X(GRAY) \
X(MAGENTA)

enum Color {
#define  X(a)  a,
	XCOLORS
#undef X
};
```

Önişlemci programı `XCOLORS` makrosunu açınca ne olacak?

```
enum Color {
#define  X(a)  a,
	X(WHITE) X(YELLOW) X(GRAY) X(MAGENTA)
#undef X
};
```

Şimdi de önişlemci programımız `X` isimli işlevsel makroyu açacak. Makro açılım listesinde `a`'nın geçtiği yerlerde bizim renklerimiz kullanılacak, değil mi?

```
enum Color {
	WHITE, YELLOW, GRAY, MAGENTA,
};
```
En son numaralandırma sabitinden sonra yer alan virgül `(trailing comma)` bir sentaks hatasına neden olmuyor. Burada `X makrosunun`

```
#undef X
```
önişlemci komutuyla tanımının ortadan kaldırılması son derece önemli. Zira başka yerlerde bu makroyu faklı biçimlerde tanımlayacağız. `X` makrosununun tanımını ortadan kaldırmasaydık tanımsız davranışa `(undefined behavior)` neden olurduk. Şimdi de başka bir yerde bu kez bir gösterici dizisi tanımlayalım:

```
#define X(a)  #a,
const char *pcolors[] = {XCOLORS};
#undef X
```

Standart makro işleci `#`'in `(stringizing / stringification)` terimi olan yazıyı çift tırnak içine aldığını hatırlayalım.
Sırada bir `switch` deyimi var:

```
#include <stdio.h>

void func(Color c)
{
	switch (c) {
#define  X(a)   case a: printf("%s", #a); break;
		XCOLORS
#undef X
		default: printf("invalid color\n");
	}
}
```

Makromuzu kullanmasaydık, renk listemize yeni bir renk eklendiğinde ya da renk listemizde bir değişiklik yapıldığında birçok yerde değişiklik yapmamız gerekecekti. `XCOLORS` makrosunu değiştirip kodu yeniden derlediğimizde bu makronun geçtiği her yer değişmiş olacak, değil mi?

`XCOLORS` makrosunu ayrı bir dosyaya almak kodların bakımını kolaylaştıracak. `XCOLORS` makrosunun `"colors.def"` isimli dosyada bulunduğunu düşünelim:

```
enum Color {
#define  X(a)  a,
	#include "colors.def"
#undef X
};
```

`XCOLORS` makrosunu içeren başlık dosyasında koşullu derleme komutlarıyla renk listemiz duruma göre farklı şekilde biçimlendirilebilir:

```
//colors.def

#ifdef NO_YELLOW
#define XCOLORS \
X(WHITE) \
X(RED) \
X(GRAY) \
X(MAGENTA)
#else
#define XCOLORS \
X(WHITE) \
X(YELLOW) \
X(GRAY) \
X(MAGENTA)
#endif
```

`X makrosu` ilk olarak `1960`'lı yılların sonunda o zamanki bilgisayar kuşağı `DEC PDP`'lerin işletim sistemlerinin yazımında `assembly` dillerde etkin olarak kullanılmış. Zaman içinde unutulmaya yüz tutmuş bu faydalı tekniğin kullanımına siz de bir destek verin.
