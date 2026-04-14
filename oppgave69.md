# Oppgave 6 til 9 (Nice!)

## Oppgave 6

```java
public class Node {
    public int data;
    public Node neste;
    
    public Node(int data) {
        this.data = data;
        this.neste = null;
    }
    
    // b)
    public static void settInnBakerst(Node root, int value) {
        Node node = new Node(value);
        
        if(this.neste != null) this.neste.settInnBakerst(node);
        else this.neste = node;
    }
} 

public class Oppgave_6 {

    // a) 
    public static void main(String[] args) {
        Node forste = new Node(1);
        Node node2 = new Node(2); 
        Node node3 = new Node(3); 
        
        forste.neste = node2;
        node2.neste = node3; 
    }
}
```

## Oppgave 7

```java
public class Oppgave_7 {
    
    //a)
    public int antallMaater(int trinn) {
        if (trinn <= 1) return 1;
        if (trinn == 2) return 2;
        
        return antallMaater(trinn - 1) + antallMaater(trinn - 2);
    }

    //b)    ja, skal være i en egen fil og alt det der, 
    //      men dette er eksamen, ikke et realistisk scenario
    @Test
    public void testAntallMaater() {
        Trapp trapp = new Trapp();
        
        assertEquals(1, trapp.antallMaater(1));
        assertEquals(2, trapp.antallMaater(2));
        assertEquals(3, trapp.antallMaater(3));
        assertEquals(5, trapp.antallMaater(4));
        assertEquals(8, trapp.antallMaater(5));
    }
}
```

## Oppgave 8

### a)

```java
public class Oppgave_8 {
    public static <T extends Comparable<? super T>> void haugsortering(T[] a) {
        int n = a.length;
        MinHaug<T> haug = new MinHaug<T>(n);

        for (int i = 0; i < n; i++) {
            haug.leggTil(a[i]);
        }

        for (int i = 0; i < n; i++) {
            a[i] = haug.fjernMinste();
        }
    }
}
```

### b)

bruker manuelt insertion sort:

```json
i=0 -> [delfin, eple, fot, and, bok, cirka]
i=1 -> [delfin, eple, fot, and, bok, cirka]
i=2 -> [and, delfin, eple, fot, bok, cirka]
i=3 -> [and, bok, delfin, eple, fot, cirka]
i=4 -> [and, bok, cirka, delfin, eple, fot]
```

### c)

$O(n)$. Jeg må helt ærlig si at jeg bare pugger utenat disse algoritmene og
hvilke mønstre de fungerer på, men nå er jeg nysgjerrig nok å lære det før eksamen :p

### d)

manuelt binærsøk:

```json
Start: [delfin, eple, fot, and, bok, cirka] 

i=0 (eple) ->   [delfin, eple, fot, and, bok, cirka]
i=1 (fot)  ->   [delfin, eple, fot, and, bok, cirka]
i=2 (and)  ->   [and, delfin, eple, fot, bok, cirka]
i=3 (bok)  ->   [and, bok, delfin, eple, fot, cirka]
i=4 (cirka)->   [and, bok, cirka, delfin, eple, fot]
```

## Oppgave 9

```java
public class BS_Tre<T extends Comparable<? super T>> {
 private BinaerTreNode<T> rot;
 public BS_Tre(BinaerTreNode<T> rot) {
 this.rot = rot;
 }

 public T finnMinste() {
 // a) fyll inn – se nærmere beskrivelse i oppgaven
    if (rot == null) return null;
    BinaerTreNode<T> aktuell = rot;
    while (aktuell.venstre != null) {
        aktuell = aktuell.venstre;
    }
    return aktuell.element;
}

 private void visPreorden() {
 visPreorden(rot);
 }
 public void visPreorden(BinaerTreNode<T> p) {
 // b) fyll inn – se nærmere beskrivelse i oppgaven
    if (p != null) {
        System.out.println(p.element);
        visPreorden(p.venstre);
        visPreorden(p.hoyre);
    }
}

 public T finnStorste() {
 return finnStorste(rot);
 }

 private T finnStorste(BinaerTreNode<T> t) {
 // c) fyll inn – se nærmere beskrivelse i oppgaven
    if (t == null) return null;
    
    T maks = t.element;
    T vMaks = finnStorste(t.venstre);
    T hMaks = finnStorste(t.hoyre);
    
    if (vMaks != null && vMaks.compareTo(maks) > 0) maks = vMaks;
    if (hMaks != null && hMaks.compareTo(maks) > 0) maks = hMaks;
    
    return maks;
 }

 public BS_Tre<T> tabellTil_BSTre(T[] tab) {
 BinaerTreNode<T> r = tabellTil_BSTre(tab, 0, tab.length - 1);
 BS_Tre<T> tre = new BS_Tre<T>(r);
 }

 private BinaerTreNode<T> tabellTil_BSTre(T[] tab, int fra, int til) {
 // d) fyll inn – se nærmere beskrivelse i oppgaven
    if (fra > til) return null;
    
    int midt = (fra + til) / 2;
    BinaerTreNode<T> node = new BinaerTreNode<>(tab[midt]);
    
    node.venstre = tabellTil_BSTre(tab, fra, midt - 1);
    node.hoyre = tabellTil_BSTre(tab, midt + 1, til);
    
    return node;
 }
 
```
