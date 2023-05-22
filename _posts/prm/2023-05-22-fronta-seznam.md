---
title: Fronta realizovaná spojovým seznamem
date: 2023-05-17 12:29:30 -200
layout: post
categories: [Informační technologie, Programovací metody]
tags: [prm, fronta]
---

# Třída Element

```java
package it3a_20230426_Stack_LL;

/**
 * Trida predstavujici jeden prvek spojoveho seznamu
 * @author johanovsky
 * @version 1.0
 */
public class Element {
    //atributy
    //nesena hodnota - co chci ukladat
    private int value;
    //odkaz na dalsiho
    private Element next;

    /**
     * Konstruktor prvku.
     * @param value Pri vytvareni prveku musime znat hodnotu.
     */
    public Element(int value) {
        this.value = value;
        this.next = null;
    }

    /**
     * Getter na hodnotu.
     * @return vraci aktualni hodnotu nesenou v prvku.
     */
    public int getValue() {
        return value;
    }

    /**
     * Getter na naslednika.
     * @return vraci odkaz na nasledujici prvek.
     */
    public Element getNext() {
        return next;
    }

    /**
     * Setter na hodnotu.
     * @param value nova hodnota nesena v prvku.
     */
    public void setValue(int value) {
        this.value = value;
    }

    /**
     * Setter na naslednika.
     * @param next novy odkaz na neslednika prvku.
     */
    public void setNext(Element next) {
        this.next = next;
    }

    /**
     * Textovy vypis prvku.
     */
    @Override
    public String toString() {
        return Integer.toString(value);
    }


    public static void main(String[] args) {
        Element e1 = new Element(1);
        System.out.println(e1);
        Element e2 = new Element(2);
        e1.setNext(e2);
        System.out.println(e1.getNext());
    }
}
```

# Třída Queue

```java
package it3a_20230517_Queue_LL;

import it3a_20230426_Stack_LL.Element;

public class Queue_LL {

    //atributy
    private Element first;
    private Element last;

    //konstruktor prazdne fronty
    public Queue_LL() {
        first = null;
        last = null;
    }

    //test prazdnosti
    public boolean isEmpty() {
        if((first == null) && (last == null)) {
            return true;
        } else {
            return false;
        }
    }

    //gettery
    public Element first() {
        if(isEmpty()) {
            throw new RuntimeException("Fronta je prazdna");
        }
        return first;
    }

    public Element last() {
        if(isEmpty()) {
            throw new RuntimeException("Fronta je prazdna");
        }
        return last;
    }

    //pridani prvku na konec fronty
    public void add(Element e) {
        //test na prazdnost
        if(isEmpty()) {
            //fronta je prazdna -> pridavam prvni prvek
            //1a. krok - aktualizuju odkaz na prvniho
            first = e;
        } else {
            //fornta neni prazdna -> pridavam dalsi prvek
            //1b. krok - poslednimu prvku nastavime noveho naslednika
            last.setNext(e);
        }
        //2. krok - aktualizuju odkaz na posledniho
        last = e;
    }

    //odebrani prvku ze zacatku fronty
    public Element remove() {
        //test na prazdnost
        if(isEmpty()) {
            //fronta je prazdna -> neni co odebrat
            throw new RuntimeException("Fronta je prazdna");
        } else {
            //fronta neni prazdna
            //1. krok - ukazu si pomocnou referenci na prvni prvek
            Element pom = first;
            //2. krok - prepojim prvniho na jeho naslednika
            first = first().getNext();
            //2,5 krok - volitelny, jestlize odebiras posledni prvek -> aktualizuj i last
            if(first() == null) {
                last = null;
            }
            //3. krok odpojim odebirany prvek od zbytku seznamu
            pom.setNext(null);
            //vratime odebirany prvek
            return pom;
        }
    }

    //prohledani fronty
    public boolean contains(int value) {
        for(Element pom = first; pom != null; pom = pom.getNext()) {
            if(pom.getValue() == value) {
                //nalezeno
                return true;
            }
        }
        //nenalezeno
        return false;
    }
}
```

# Třída QueueTest

```java
package it3a_20230517_Queue_LL;

import it3a_20230426_Stack_LL.Element;

public class Queue_LL_Test {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        //konstruktor
        Queue_LL qll = new Queue_LL();
        //test na prazdnost
        System.out.println("Prazdna: " + qll.isEmpty());
        //vyhledavani
        System.out.println("Hledam 1: " + qll.contains(1));
        //pridame prvni prvek
        qll.add(new Element(1));
        //test na prazdnost
        System.out.println("Prazdna: " + qll.isEmpty());
        //prvni / posledni
        System.out.println("Prvni: " + qll.first());
        System.out.println("Posledni: " + qll.last());
        //vyhledavani
        System.out.println("Hledam 1: " + qll.contains(1));
        //odebrani
        System.out.println("Odebiram: " + qll.remove());
        //test na prazdnost
        System.out.println("Prazdna: " + qll.isEmpty());
        //naplnime prvky
        for(int i = 1; i <= 10; i++) {
            System.out.println("Pridavam: " + i);
            qll.add(new Element(i));
            //prvni / posledni
            System.out.println("Prvni: " + qll.first());
            System.out.println("Posledni: " + qll.last());
        }
        //vyprazdnime frontu
        while(!qll.isEmpty()) {
            //prvni / posledni
            System.out.println("Prvni: " + qll.first());
            System.out.println("Posledni: " + qll.last());
            System.out.println("Odebiram: "+ qll.remove());
        }
    }
}
```
