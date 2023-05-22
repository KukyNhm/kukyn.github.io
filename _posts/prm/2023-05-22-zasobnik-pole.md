---
title: Zásobník realizovaný v poli
date: 2023-04-05 12:29:30 -200
layout: post
categories: [Informační technologie, Programovací metody]
tags: [prm, zasobnik]
---

```java
package it3a_20230405_StackInArray;

public class StackInArray {

    //atributy
    private int array[];
    private int top;

    //konstruktor prazdneho zasobniku
    public StackInArray(int capacity) {
        //kontrola
        if(capacity < 2) {
            throw new IllegalArgumentException("Velikost alespon 2 prvky");
        }
        //kapacita je ok -> pridelime pamet
        array = new int[capacity];
        //vytvorime prazdny zasobnik -> top ukazuje na volny prvek a to je 0.
        top = 0;
    }

    //test na prazdnost
    public boolean isEmpty() {
        if(top == 0) {
            return true;
        } else {
            return false;
        }
    }

    //geter na kapacitu
    public int getCapacity() {
        return array.length;
    }

    //test na plnost
    public boolean isFull() {
        if(top == getCapacity()) {
            return true;
        } else {
            return false;
        }
    }

    //pridani prvku na vrchol zasobniku
    public void push(int value) {
        //kontrola na plnost - toto by nikdy nemelo nastat
        /*
        if(isFull()) {
            //zasobnik je plny
            throw new ArrayIndexOutOfBoundsException("Zasobnik je plny");
        }
        */
        //pokud neni zasobnik plny -> muzeme pridat
        //vlozime novou hodnotu na akt. volnou pozici (top)
        array[top] = value;
        //vrchol posuneme nahoru
        top++;
        //kontrola jestli neni potreba zvetsit
        if(isFull()) {
            //jestlize je po pridani plno -> tak zvetsujeme
            enlarge();
        }
    }

    //odebrani prvku z vrcholu zasobniku
    public int pop() {
        //kontrola na prazdnost
        if(isEmpty()) {
            //zasobnik je prazdny
            throw new ArrayIndexOutOfBoundsException("Zasobnik je prazdny");
        }
        //pokud neni zasobnik prazdny -> muzeme odebrat
        //vrchol posuneme dolu
        top--;

        //pozalohujeme si odebirany prvek
        int pom = array[top];

        //kontrola jestli neni potreba zmensit
        if((top <= getCapacity() / 2) && (getCapacity() >= 2)) {
            schrink();
        }

        //vratime prvek na vrcholu
        return pom;
    }

    //getter na top prvek
    public int getTop() {
        //kontrola
        if(isEmpty()) {
            //zasobnik je prazdny
            throw new ArrayIndexOutOfBoundsException("Zasobnik je prazdny");
        }
        //zasobnik neni prazdny
        return array[top - 1];
    }

    //prohledani zasobniku
    public boolean contains(int value) {
        for(int i = 0; i < top; i++) {
            if(array[i] == value) {
                return true;
            }
        }
        return false;
    }

    //zvetsi zasobnik 2x
    public void enlarge() {
        //vyrobime 2x vetsi pole nez bylo
        int newArray[] = new int[2 * getCapacity()];
        //prekopirujeme prvky ze stareho pole do noveho
        for(int i = 0; i < top; i++) {
            newArray[i] = array[i];
        }
        //prepojime reference
        array = newArray;
    }

    //zmenseni zasobniku na 1/2
    public void schrink() {
        //kontrola jestli povolime zmensovani
        if((top <= getCapacity() / 2) && (getCapacity() >= 2)) {
            //vyrobime polovicni pole nez bylo
            int newArray[] = new int[getCapacity() / 2];
            //prekopirujeme prvky ze stareho do noveho
            for(int i = 0; i < top; i++) {
                newArray[i] = array[i];
            }
            //prepojime reference
            array = newArray;
        } else {
            throw new ArrayIndexOutOfBoundsException("Nelze zmensit");
        }
    }

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        //konstruktor
        StackInArray sa = new StackInArray(5);
        //test na prazdnost
        System.out.println(sa.isEmpty());
        //test na plnost
        System.out.println(sa.isFull());

        //pridame prvek
        sa.push(10);
        //test na prazdnost
        System.out.println(sa.isEmpty());
        //test na plnost
        System.out.println(sa.isFull());
        //kontrola vrcholu
        System.out.println(sa.getTop());

        //zaplnime zasobnik
        for(int i = 0; i < 4; i++) {
            sa.push(i);
        }

        //test na prazdnost
        System.out.println(sa.isEmpty());
        //test na plnost
        System.out.println(sa.isFull());
        //kontrola vrcholu
        System.out.println(sa.getTop());

        //test vyhledavani
        System.out.println(sa.contains(10));
        System.out.println(sa.contains(3));
        System.out.println(sa.contains(4));

        //vysypeme zasobnik
        while(!sa.isEmpty()) {
            System.out.println(sa.pop());
        }

        //obebrani z prazdneho zasobniku
        //sa.pop();

        //zaplnovani
        for(int i = 1 ; i <= 100; i++) {
            System.out.println("Pridavam " + i);
            sa.push(i);
            System.out.println("Na vrchu je: " + sa.getTop());
            System.out.println("Akt. kapacita: " + sa.getCapacity());
        }

        //vysypeme
        while(!sa.isEmpty()) {
            System.out.println("Na vrchu je: " + sa.getTop());
            System.out.println("Odebiram: " + sa.pop());
            System.out.println("Akt. kapacita: " + sa.getCapacity());
        }

        //zaplnovani
        for(int i = 1 ; i <= 100; i++) {
            System.out.println("Pridavam " + i);
            sa.push(i);
            System.out.println("Na vrchu je: " + sa.getTop());
            System.out.println("Akt. kapacita: " + sa.getCapacity());
        }

        //vysypeme
        while(!sa.isEmpty()) {
            System.out.println("Na vrchu je: " + sa.getTop());
            System.out.println("Odebiram: " + sa.pop());
            System.out.println("Akt. kapacita: " + sa.getCapacity());
        }

    }
}
```
