getchar standart bir C fonksiyonu.

stdio.h başlık dosyasındaki bildirimi şöyle:

```
int getchar(void);
```

Fonksiyon standart giriş akımının tamponundan bir byte okuyor, okuduğu byte'ı standart giriş akımının tamponundan çıkartıyor. _(extract ediyor)_.<br>
Fonksiyonun geri dönüş değeri okunan byte'ın tamsayı değeri.<br>
Eğer fonksiyon çağrıldığında standart giriş akımının tamponu boş ise kullanıcının bir giriş yapması gerekiyor. <bt>
getchar echo veren bir giriş fonksiyonu. Yani girişi yapılan karakterleri konsol ekranında görüyoruz. <br>
getchar satır tamponlu bir giriş fonksiyonu. Yani giriş işleminin sonlandırılması için standart giriş akımının tamponuna '\n' karakterinin gelmesi gerekiyor.
getchar fonksiyonu çağrıldığında standart giriş akımının tamponu boş bırakılırsa _(Windows sistemlerinde ctrl-Z enter)_ getchar hata kodu olarak _-1_ değeri döndürüyor. Kodun kolay okunabilmesi için bu hata kodu karşılığı stdio.h başlık dosyasında tanımlanan _EOF_ makrosu kullanılmalı:
```
#define   EOF   (-1)
```

