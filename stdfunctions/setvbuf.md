

```
// C99 öncesi
int setvbuf( FILE* stream, char* buffer, int mode, size_t size ); 

// C99 ve sonrası
int setvbuf( FILE* restrict stream, char* buffer, int mode, size_t size); 
```
## Parametreler

+ __stream:__ tamponlama için düzenleme yapılacak dosyaya ilişkin handle	
+ __buffer:__	tampon olarak kullanılacak dizinin adresi. Eğer sadece tamponlama modu ya da buffer size değiştirilecek ise _NULL_ pointer geçilmeli
+ __mode	:__ Kullanılacak tamponlama modu _(enum int)_. Aşağıdaki değerlerden biri olmalı:

\_IOFBF	tam tamponlama için <br>
\_IOLBF	satır tabanlı tamponlama için <br>
\_IONBF	tamponlama yapılmaması için <br>
+ __size__	buffer olarak kullanılacak boyut

## Geri Dönüş Değeri
Başarı durumunda _0_ başarısızlık durumunda _0_'dan farklı bir değer.

## Notlar
+ 2. parametreye __NULL__ pointer geçilirse buffer boyutu size olarak değiştirilir.
+ normal olarak _BUFSIZ_ makrosuun değeri giriş çıkış işlemleri için en etkili buffer boyutu olarak düşünülmeli. 
Ancak __fstat__ _POSIX_ fonksiyonu daha iyi bir değer belirleyebilir.
+ Fonksiyon dosya açıldıktan sonra ancak dosya üstünde herhangi bir işlem yapılmadan önce çağrılmalı
+ size değeri gönderilen değerden daha küçük olan bir 2'nin kuvvetine, sayfa boyutu _(page size)_ katına vs  çekilebilir.
+ derleyicilerin çoğunda satır tabanlı tamponlama sadece terminal giriş akımı için sunulmaktadır.
+ _stdin_ ve _stdout_ için kullanılacak buffer dizilerinin hayatı programın sonuna kadar devam ediyor olmalı. (Aksi halde tanımsız davranış)
