# Proměnné v OpenSCADu: Co jde a co ne

```cpp
// Jednotlivé bloky oddělené komentářem uvažujte v jiném souboru (tedy nezávisle na ostatních)


// tohle jde
variable = 5;



// tohle nejde
// respektive nebude to fungovat tak, jak byste si mohli myslet
variable = 5;
echo(variable);
variable = 6;
echo(variable);


// tohle jde
module foo(arg) {
    arg = 3;
}


// změněná hodnota arg bude platiti jen uvnitř těla ifu
module foo(a) {
    a = 5;
    echo(a); // a je 5

    if (a > 10) {
        a = 2;
        echo(a); // a je 2
    } else {
        a = 3;
        echo(a); // a je 3
    }
    echo(a); // a je 5
}


// tohle ale jde
module foo(arg) {
    arg = arg >= 0 ? arg : 0;
    // ... arg je změněný, pokud něco
}


// ale samozřejmě, arg je v celém modulu stejný
module foo(arg) {
    echo(arg); // vypíše změněný arg!
    arg = arg >= 0 ? arg : 0;
}


// jde to ale udělat jenom jednou
// tohle nejde
module foo(arg) {
    arg = 5;
    echo(arg); // 3
    arg = 3;
}


// ani tohle nejde
module foo(arg) {
    arg = arg >= 0 ? arg : 0;
    arg = arg <= 10 ? arg : 10;
}


// musí se to spojit do jednoho komplikovaného ternárního operátoru
// nebo si na to napsat funkci a udělat:
arg = xyz(arg);
```
