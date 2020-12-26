## Değişken boyutlu diziler (Variable Length Arrays)

`C99` Standartları öncesinde dizi tanımlamalarında dizi boyutunun sabit ifadeleriyle `(constant expressions)` belirtilmesi zorunluydu. C99 standartları ile dizi boyutlarının değişken ifadeleriyle belirtilmesi olanağı getirildi. Bir dizinin boyutu sabit ifadesi ile belirtilmemiş ise ise bu bir değişken boyutlu dizidir `(Variable Length Array)`

Aşağıdaki kodu derleyip (C99) çalıştırın:

```
#include <string.h>
#include <stdlib.h>
#include <stdio.h>

int dcmp(const void* vp1, const void* vp2)
{
    typedef const double* Cdptr;
    return *(Cdptr)vp2 < *(Cdptr)vp1 ? 1 :
        *(Cdptr)vp1 < *(Cdptr)vp2 ? -1 : 0;
}

double median(const double* pa, size_t size)
{
    double cpa[size];
    memcpy(cpa, pa, sizeof(*pa) * size);
    qsort(cpa, size, sizeof(*cpa), dcmp);
    return cpa[size / 2];
}

int main()
{
    double a[] = { 0.1, 8.7, 9.4, 1.2, 4.3, 0.4, 12.4, 1.9, 2.7 };

    printf("%f\n", median(a, 9));
}
```
Yukarıdaki kodda ismi `median` olan fonksiyonda tanımlanan `cpa` değişken boyutlu bir dizi. Bu dizinin boyutu programın çalışma zamanında `median` fonksiyonu çağrıldığında belli olacak. Fonksiyon her çağrıldığında bu dizinin boyutu farklı olabilir.

`C99` standartları öncesinde `sizeof` operatörünün ürettiği değer bir derleme zamanı sabitiydi `(constant expression)` Ancak C99 standartları ile birlikte `sizeof` operatörünün operand olarak değişken boyutta bir diziyi alması durumunda ürettiği değer programın çalışma zamanında belli oluyor. Aşağıdaki kodu derleyip çalıştırın:

```
#include <stdio.h>

void func(int n)
{
	int a[n];

	printf("boyut = %zu\n", sizeof(a) / sizeof(*a));
	//...
}

int main()
{
	for (int i = 1; i <= 10; ++i) {
		func(i);
	}
}
```

Değişken boyutlu dizilere ilk değer verilemez. Aşağıdaki kodda `a` dizisinin tanımı geçersizdir.
```
#include <stddef.h>

void func(size_t size)
{
    int a[size] = {1, 5, 7, 9}; //geçersiz
    //...
}
```
Değişken boyutta diziler ve bunların türevi olan türlere (gösterici, dizi vs.) Değişkene bağlı türler `(Variably - modified types)` deniyor.  Değişkene boyutlu bir diziyi gösteren bir gösterici değişken tanımlayalım:
```

void func(int n)
{
	int a[n];
	int (*p)[n] = &a;

	for (int i = 0; i < n; ++i) {
		(*p)[n] = i;
	}
}
```

Dinamik matrislerin bellekte ardışık olarak oluşturulmasında değişken boyutlu bir matrisi gösteren gösterici değişkenin kullanılması diziyi dolaşan kodların daha kolay ve daha doğal yazılmasını sağlar.

```
#include <stdlib.h>
#include <stdio.h>
#include <time.h>

int main()
{
	size_t row, col;
        srand((unsigned)time(NULL));

	printf("satir ve sutun sayisi: ");
	scanf("%zu%zu", &row, &col);
	int(*p)[row][col] = malloc(sizeof(*p));
        //int *pd = malloc(row * col * sizeof(int));
	if (!p) {
		fprintf(stderr, "bellek yetersiz\n");
		return 1;
	}

	for (size_t i = 0; i < row; ++i) {
		for (size_t k = 0; k < col; ++k) {
                        //pd[i * col + k] = rand() % 10;
			(*p)[i][k] = rand() % 10;
		}
	}

    //...
    
    for (size_t i = 0; i < row; ++i) {
		for (size_t k = 0; k < col; ++k) {
			printf("%d", (*p)[i][k]);
		}
        printf("\n");
	}
	
    free(p);
}
```

Değişkene bağlı türler `(Variably - modified types)` yapıların `(structures)` ya da birliklerin öğeleri olamazlar.

```
int n = 10;

struct Nec {
    int m_a[n];   //Geçersiz
    int(*m_p)[n]; //Geçersiz
};
```
Yukarıdaki kodda yapılan `struct Nec` yapısı bildirimi geçersizdir. 

Değişken boyutlu dizilere destek C11 standartları ile derleyicilerin seçimine bırakıldı. Yani standart C derleyicileri değişken boyutlu dizilere destek vermek zorunda değil.

///eksik



