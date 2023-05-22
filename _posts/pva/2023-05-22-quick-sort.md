---
title: Quick Sort Algoritmus
date: 2022-11-22 12:29:30 -200
layout: post
categories: [Informační technologie, Programování a vývoj aplikací]
tags: [prm, quick sort]
---

```java
/* quick sort */

import java.util.Random;

public class QuickSort {

  public static final int KOLIK = 30;
  public static int pole[] = new int[KOLIK];


  public static void qs(int l, int r) {
    int pivot, tmp;
    int i, j;

    System.out.println(l + " " + r);
    pivot = pole[ l ]; // vyber pivota
    i = l;
    j = r;

    // prohazeni dle pivota
    do {
      while (pole[i] < pivot) i++;
      while (pole[j] > pivot) j--;

      if (i<=j) {
        tmp = pole[i];
        pole[i] = pole[j];
        pole[j] = tmp;

        i++;
        j--;
      }  // endif
    } while ( i<j );

    if ((j-l) > 0) qs(l,j);
    if ((r-i) > 0) qs(i,r);
  }



  public static void main(String args[]) {
    Random rnd = new Random(12);
    int i;

    for (i=0; i<KOLIK; i++) pole[i] = rnd.nextInt(2*KOLIK);

    System.out.format("%d%n", System.currentTimeMillis());

    for ( int pr : pole ) System.out.print( pr + " ");System.out.println();
    qs(0,KOLIK-1);
    for ( int pr : pole ) System.out.print( pr + " ");System.out.println();

    System.out.format("%d%n", System.currentTimeMillis());
//for (i=0; i<KOLIK; i++) System.out.format("%6d", pole[i]);
  }
}
```
