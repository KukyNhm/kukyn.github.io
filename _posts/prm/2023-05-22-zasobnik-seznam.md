---
title: Zásobník realizovaný spojovým seznamem
date: 2023-04-26 12:29:30 -200
layout: post
categories: [Informační technologie, Programovací metody]
tags: [prm, zasobnik]
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

# Třída Stack

```java
papackage it3a_20230426_Stack_LL;

/**
 * Trida predstavuji zasobnik implementovany pomoci spojoveho seznamu.
 * @author johanovsky
 *
 */
public class Stack_LL {

    //atribut
    /**
     * Odkaz na prvni (vrchni) prvek v zasobniku
     */
    private Element top;

    /**
     * Konstruktor prazdneho zasobniku.
     */
    public Stack_LL() {
        this.top = null;
    }

    /**
     * Test na prazdnost zasobniku.
     * @return Vraci zda je zasobnik prazdny.
     */
    public boolean isEmpty() {
        //return(top == null);

        if(top == null) {
            return true;
        } else {
            return false;
        }
    }

    /**
     * Pridani prvku na vrchol zasobniku.
     * @param e Novy prvek, ktery ma prijit na vrchol.
     */
    public void push(Element e) {
        //1. novemu prvku nastavime jako naslednika toh co je doposud prvni
        e.setNext(top);
        //2. aktualizujeme vrchni prvek zasobniku
        top = e;
    }

    /**
     * Odebrani prvku z vrcholu zasobniku.
     * @return Vraci odebrany prvek z vrcholu zasobniku.
     * @throws RuntimeException Pri pokusu odebrat z prazdneho zasobniku.
     */
    public Element pop() {
        //kontrola prazdnosti
        if(isEmpty()) {
            //pokus odebrat z prazdneho zasobniku
            throw new RuntimeException("Prazdny zasobnik");
        } else {
            //je tam alespon jeden prvek
            //1. pomocnou referenci si ukazu na prvniho
            Element pom = top;
            //2. prepojime vrchol na nasledujici prvek
            top = top.getNext();
            //3. odpojime odebirany prvek z puv. seznamu
            pom.setNext(null);
            //vratime odebrany prvek
            return pom;
        }
    }

    /**
     * Getter na vrchni prvek.
     * @return Vraci prvek ktery je na vrcholu zasobniku, aniz by ho odebiral
     * @throws RuntimeException Pri pokusu podivat se na vrchol prazdneho zasobniku.
     */
    public Element getTop() {
        if(isEmpty()) {
            throw new RuntimeException("Prazdny zasobnik");
        }
        return top;
    }

    /**
     * Prohledani zasobniku.
     * @param value Hledana hodnota.
     * @return Vraci zda zasobnik obsahuje hledanou hodnotu, nebo ne.
     */
    public boolean contains(int value) {
        /*
         * varianta while
        Element pom = top;
        while(pom != null) {
            if(pom.getValue() == value) {
                //nalezeno
                return true;
            }
            //posuneme se na dalsi prvek
            pom = pom.getNext();
        }
        //nenalezeno
        return false;
        */
        //varianta for-cyklem
        for(Element pom = top; pom != null; pom = pom.getNext()) {
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

# Třída Stacktest

```java
package it3a_20230426_Stack_LL;

public class Stack_LL_Test {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        //konstruktor
        Stack_LL s1 = new Stack_LL();
        //test na prazdnost
        System.out.println(s1.isEmpty());
        //naplnime prvkama
        for(int i = 0; i < 10; i++) {
            //vytvorime Element
            Element e = new Element(i);
            //pak Element pripojime do zasobniku
            s1.push(e);
            //vypis
            System.out.println("Pridavam prvek: " + e);
            //vypis prvku na vrchu
            System.out.println("Na vrcholu je: " + s1.getTop());
            /*
            s1.push(new Element(i));
            */
        }
        //test na prazdnost
        System.out.println(s1.isEmpty());

        //test vyhledavani
        System.out.println("Hledam cislo 0: " + s1.contains(0));
        System.out.println("Hledam cislo 9: " + s1.contains(9));
        System.out.println("Hledam cislo 10: " + s1.contains(10));

        //vyprazdnime
        while(!s1.isEmpty()) {
            System.out.println("Odebiram: " + s1.pop());
        }

        //test vyhledavani
        System.out.println("Hledam cislo 0: " + s1.contains(0));
        System.out.println("Hledam cislo 9: " + s1.contains(9));
        System.out.println("Hledam cislo 10: " + s1.contains(10));
    }
}
```
