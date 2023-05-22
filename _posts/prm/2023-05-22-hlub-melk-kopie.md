---
title: Hluboká vs. mělká kopie
date: 2023-05-15 12:29:30 -200
layout: post
categories: [Informační technologie, Programovací metody]
tags: [prm, kopie]
---

```java
package it3a_20230515_copy;

class pokus {
    private int hodn;

    public void setHodn(int hodn) {
        this.hodn = hodn;
    }

    @Override
    public String toString() {
        return Integer.toString(hodn);
    }
}

public class copy {

    public static void main(String[] args) {
        //Kopirovani prim. promennych
        int a = 10;
        int b = a;
        //Vypis
        System.out.println("a: " + a);
        System.out.println("b: " + b);
        //Zmena b
        b = 20;
        //Vypis
        System.out.println("a: " + a);
        System.out.println("b: " + b);
        //Vse v poradku

        //Kopirovani poli
        int poleA[] = new int[5];
        //naplneniA
        for (int i = 0; i < poleA.length; i++) {
            poleA[i] = i;
        }
        //vypis A
        for (int i = 0; i < poleA.length; i++) {
            System.out.print(poleA[i] + ", ");
        }
        System.out.println(" -- Pole A");
        //Hluboka kopie A do B
        int poleB[] = new int[poleA.length];
        for (int i = 0; i < poleA.length; i++) {
            poleB[i] = poleA[i];
        }
        //vypis B
        for (int i = 0; i < poleB.length; i++) {
            System.out.print(poleB[i] + ", ");
        }
        System.out.println(" -- Pole B");

        //zmena v B
        poleB[0] = 100;
        //vypis B
        for (int i = 0; i < poleB.length; i++) {
            System.out.print(poleB[i] + ", ");
        }
        System.out.println(" -- Pole B po zmene");
        //vypis A
        for (int i = 0; i < poleA.length; i++) {
            System.out.print(poleA[i] + ", ");
        }
        //Pole A se nezmenilo protoze B vzniklo jako hluboka kopie A
        System.out.println(" -- Pole A");

        //Melka kopie
        int poleC[];
        poleC = poleA;
        //Vypis C
        for (int i = 0; i < poleC.length; i++) {
            System.out.print(poleC[i] + ", ");
        }
        System.out.println(" -- Pole C");

        //Zmena v C
        poleC[0] = 500;
        //Vypis C
        for (int i = 0; i < poleC.length; i++) {
            System.out.print(poleC[i] + ", ");
        }
        System.out.println(" -- Pole C po zmene");
        //Vypis A
        for (int i = 0; i < poleA.length; i++) {
            System.out.print(poleA[i] + ", ");
        }
        //Pole A se take zmenilo, protoze jsem zmenil C, ktere vzniklo jako melka kopie A
        System.out.println(" -- Pole A");

        //Tridy
        pokus instanceA = new pokus();
        instanceA.setHodn(10);
        System.out.println("instanceA: " + instanceA);
        //Melka kopie
        pokus instanceB = instanceA;
        System.out.println("instanceB: " + instanceB);
        //Zmena v B
        instanceB.setHodn(20);
        System.out.println("instanceB: " + instanceB);
        //Instance A se take zmenila, protoze B vznikla jako melka kopie
        System.out.println("instanceA: " + instanceA);
    }
}
```
