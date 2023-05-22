---
title: Fronta realizovaná v poli
date: 2023-05-10 12:29:30 -200
layout: post
categories: [Informační technologie, Programovací metody]
tags: [prm, fronta]
---

# Třída QueueInArray

```java
package it3a_20230510_QueueInArray;

public class QueueInArray {

    //atributy
    private int first;
    private int last;
    private int array[];

    //konstruktor prazdne fronty
    public QueueInArray(int capacity) {
        first = -1;
        last = -1;
        array = new int[capacity];
    }

    //test na prazdnost
    public boolean isEmpty() {
        if((first == -1) && (last == -1)) {
            return true;
        } else {
            return false;
        }
    }

    //test na plnost
    public boolean isFull() {
        if(((last + 1) % array.length) == first) {
            return true;
        } else {
            return false;
        }
    }

    //getter na first a last
    public int first() {
        if(isEmpty()) {
            throw new ArrayIndexOutOfBoundsException("Prazdna fronta");
        }
        return array[first];
    }

    public int last() {
        if(isEmpty()) {
            throw new ArrayIndexOutOfBoundsException("Prazdna fronta");
        }
        return array[last];
    }

    //pridavani prvku na konec
    public void add(int value) {
        if(isEmpty()) {
            //pridavame prvni prvek do prazdne fronty
            first = 0;
            last = 0;
            array[last] = value;
        } else {
            //do plne fronty nelze pridat
            if(isFull()) {
                throw new ArrayIndexOutOfBoundsException("Plna fronta");
            } else {
                //posun last o jedna vpred
                last = ((last + 1) % array.length);
                //na tuto pozici vloz prvek
                array[last] = value;
            }
        }
    }

    //odebrani prvku ze zacatku fronty
    public int remove() {
        //z prazdne fronty nelze odebirat
        if(isEmpty()) {
            throw new ArrayIndexOutOfBoundsException("Prazdna fronta");
        } else {
            //neni prazdna
            if(first == last) {
                //odebiram posledni prvek z fronty
                //ukaz si na prvni prvek
                int pom = array[first];
                //vyrob prazdnou frontu
                first = -1;
                last = -1;
                //vratim posledni prvek
                return pom;
            } else {
                //odebiram dalsi prvek
                //ukazu si pomocnym indexem na prvni prvek
                int pom = array[first];
                //posunu index prvniho o jedna dal
                first = (first + 1) % array.length;
                return pom;
            }
        }
    }

    //prohledavani fronty
    public boolean contains(int value) {
        if(!isEmpty()) {
            for(int i = first; i != last; i = ((i + 1) % array.length)) {
                if(array[i] == value) {
                    //nalezeno
                    return true;
                }
            }
            //test posledniho pokud neni prazdno

            if(array[last] == value) {
                return true;
            }
        }
        //nenalezeno
        return false;
    }
}
```

# Třída QueueInArrayTest

```java
package it3a_20230510_QueueInArray;

public class QueueInArray_Test {

    public static void main(String[] args) {
        //konstruktor
        QueueInArray qia = new QueueInArray(5);
        //testy na prazdnost i na plnost
        System.out.println("Prazdny: " + qia.isEmpty());
        System.out.println("Plny: " + qia.isFull());
        //vyhledavani
        System.out.println("Hledam 1: " + qia.contains(1));

        //pridame prvni prvek
        qia.add(1);
        //testy
        System.out.println("Prazdny: " + qia.isEmpty());
        System.out.println("Plny: " + qia.isFull());
        System.out.println("Prvni: " + qia.first());
        System.out.println("Posledni: " + qia.last());
        //vyhledavani
        System.out.println("Hledam 1: " + qia.contains(1));
        //odebrani
        qia.remove();
        //vyhledavani
        System.out.println("Hledam 1: " + qia.contains(1));
        //testy
        System.out.println("Prazdny: " + qia.isEmpty());
        System.out.println("Plny: " + qia.isFull());
        //(pre)naplneni
        qia.add(2);
        qia.add(3);
        qia.add(4);
        qia.add(5);
        qia.add(6);
        //qia.add(7);
        //testy
        System.out.println("Prazdny: " + qia.isEmpty());
        System.out.println("Plny: " + qia.isFull());
        //vyhledavani
        System.out.println("Hledam 1: " + qia.contains(1));
        System.out.println("Hledam 2: " + qia.contains(2));
        System.out.println("Hledam 3: " + qia.contains(3));
        System.out.println("Hledam 6: " + qia.contains(6));
        System.out.println("Hledam 7: " + qia.contains(7));
        //vyprazdneni fronty
        while(!qia.isEmpty()) {
            System.out.println("Odebiram: " + qia.remove());
        }
        //vyhledavani
        //vyhledavani
        System.out.println("Hledam 1: " + qia.contains(1));
        System.out.println("Hledam 2: " + qia.contains(2));
        System.out.println("Hledam 3: " + qia.contains(3));
        System.out.println("Hledam 6: " + qia.contains(6));
        System.out.println("Hledam 7: " + qia.contains(7));
    }
}
```
