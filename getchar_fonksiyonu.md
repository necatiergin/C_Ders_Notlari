getchar formatsız giriş işlemi _(unformatted input)_ gerçekleştiren standart bir C fonksiyonu.

_stdio.h_ başlık dosyasındaki bildirimi şöyle:

```
int getchar(void);
```

Fonksiyon standart giriş akımının tamponundan bir byte okuyor, okuduğu byte'ı standart giriş akımının tamponundan çıkartıyor. _(extract ediyor)_.<br>
Fonksiyonun geri dönüş değeri okunan _byte_'ın tamsayı değeri.<br>
Eğer fonksiyon çağrıldığında standart giriş akımının tamponu boş ise kullanıcının bir giriş yapması gerekiyor. <bt>
__getchar__ echo veren bir giriş fonksiyonu. Yani girişi yapılan karakterleri konsol ekranında görüyoruz. <br>
__getchar__ satır tamponlu bir giriş fonksiyonu. Yani giriş işleminin sonlandırılması için standart giriş akımının tamponuna '\n' karakterinin gelmesi gerekiyor.
__getchar__ fonksiyonu çağrıldığında standart giriş akımının tamponu boş bırakılırsa _(Windows sistemlerinde ctrl-Z enter)_ getchar hata kodu olarak _-1_ değeri döndürüyor. Kodun kolay okunabilmesi için bu hata kodu karşılığı _stdio.h_ başlık dosyasında tanımlanan _EOF_ makrosu kullanılmalı:
```
#define   EOF   (-1)
```

__getchar__ fonksiyonu ile _scanf_ fonksiyonu aynı buffer'ı kullanıyorlar.

