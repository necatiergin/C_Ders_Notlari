

```
// C99 öncesi
int setvbuf( FILE* stream, char* buffer, int mode, size_t size ); 

// C99 ve sonrası
int setvbuf( FILE* restrict stream, char* buffer, int mode, size_t size); 
```

## Notlar
+ 2. parametreye NULL pointer geçilirse buffer boyutu size olarak değiştirilir.
