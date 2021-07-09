

```
// C99 öncesi
int setvbuf( FILE* stream, char* buffer, int mode, size_t size ); 

// C99 ve sonrası
int setvbuf( FILE* restrict stream, char* buffer, int mode, size_t size); 
```
## Parametreler
Parameters
+ stream: tamponlama için düzenleme yapılacak dosyaya ilişkin handle	
+ buffer:	tampon olarak kullanılacak dizinin adresi. eğer sadece tamponlama modu ya da buffer size değiştirilecek ise NULL ointer geçilmeli
+ mode	: Kullanılacak tamponlama modu (enum int). Aşağıdaki değerlerden biri olmalı:

\_IOFBF	tam tamponlama için
\_IOLBF	satır tabanlı tamponlama için
\_IONBF	tamponlama yapılmaması için
+ size	buffer olarak kullanılacak boyut

## Notlar
+ 2. parametreye NULL pointer geçilirse buffer boyutu size olarak değiştirilir.
