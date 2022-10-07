# Esercizio di gruppo

1. Si formino gruppi di tre persone. Nel proseguo delle guida, i tre studenti saranno Pippo, Pluto, e Paperino.
2. Si scelga in modo casuale un project manager all'interno del gruppo. In questa guida, si suppone che Paperino sia stato scelto come project manager.
3. Paperino (anche aiutato dagli altri membri del gruppo) crei un nuovo repository su GitHub
4. Paperino (anche aiutato dagli altri membri del gruppo) dia agli altri membri del gruppo permessi per fare push su quel repository
5. Pippo crei un nuovo repository (con `git init`)
6. Pippo crei il seguente file `ComplexNumber.java`

```java
class ComplexNumber {
    private final double real;
    private final double imaginary;

    public ComplexNumber(final double real, final double imaginary) {
        this.real = real;
        this.imaginary = imaginary;
    }

    public double getImaginary() {
        return 0;
    }

    public double getReal() {
        return 0;
    }
    
    public ComplexNumber plus(final ComplexNumber other) {
        return null;
    }
    
    public ComplexNumber sub(final ComplexNumber other) {
        return null;
    }

    public ComplexNumber times(final ComplexNumber other) {
        return null;
    }

    public ComplexNumber div(final ComplexNumber other) {
        final double commonDenominator = other.getReal() * other.getReal() + other.getImaginary() * other.getImaginary();
        final double realNumerator = this.getReal() * other.getReal() + this.getImaginary() * other.getImaginary();
        final double imaginaryNumerator = other.getReal() * this.getImaginary() - this.getReal() * other.getImaginary();
        return new ComplexNumber(realNumerator / commonDenominator, imaginaryNumerator / commonDenominator);
    }
}
```

7. Pippo aggiunga `ComplexNumber.java` allo stage ed effettui un commit
8. Pippo configuri un nuovo remote `origin` che punta al repository creato da Paperino
9. Pippo effettui la push del suo branch verso origin

Da questo momento, si proceda in modo indipendente, e lavorando *in parallelo*.
Tutti gli sviluppatori si assicurino sempre che il file `ComplexNumber.java` compili prima di fare commit.

### Task di Pluto

Deve sviluppare, facendo un commit ed una push per ognuno di questi step:
* il getter `getImaginary()`
* il getter `getReal()`
* il metodo `plus(ComplexNumber)`
* il metodo `sub(ComplexNumber)`
* il metodo `times(ComplexNumber)`
* aggiungere a `main` un test che verifica che la divisione di complessi funziona

### Task di Paperino

Deve sviluppare, facendo un commit ed una push per ognuno di questi step:
* un metodo `main` inizialmente vuoto
* aggiungere a `main` la stampa del numero complesso 4+8i
* aggiungere a `main` un test che verifica che la somma di complessi funziona
* aggiungere a `main` un test che verifica che la sottrazione di complessi funziona

### Task di Pippo

Deve sviluppare, facendo un commit ed una push per ognuno di questi step:
* aggiungere un metodo `toString a ComplexNumber`
* aggiungere a `main` un test che verifica che la moltiplicazione di complessi funzioni
