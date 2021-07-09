

```
// C99 öncesi
int setvbuf( FILE* stream, char* buffer, int mode, size_t size ); 

// C99 ve sonrası
int setvbuf( FILE* restrict stream, char* buffer, int mode, size_t size); 
```
## Parametreler
Parameters
+ __stream:__ tamponlama için düzenleme yapılacak dosyaya ilişkin handle	
+ __buffer:__	tampon olarak kullanılacak dizinin adresi. Eğer sadece tamponlama modu ya da buffer size değiştirilecek ise NULL ointer geçilmeli
+ __mode	:__ Kullanılacak tamponlama modu _(enum int)_. Aşağıdaki değerlerden biri olmalı:

\_IOFBF	tam tamponlama için <br<
\_IOLBF	satır tabanlı tamponlama için<br>
\_IONBF	tamponlama yapılmaması için <br>
+ __size__	buffer olarak kullanılacak boyut

## Geri Dönüş Değeri
Başarı durumunda _0_ başarısızlık durumunda _0_'dan farklı bir değer.

## Notlar
+ 2. parametreye __NULL__ pointer geçilirse buffer boyutu size olarak değiştirilir.
