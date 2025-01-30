---
title : "C reference"
toc : true
---

# Preface
Jeg underviser dette semester i et fag der hedder Computer Architecture and Networking. Til en af de første afleveringer skal de lave noget c kode, så her er ett reference ark jeg har lavet.

- [Nyttige C funktioner](#org0cfaa6d)
  - [sizeof](#org447ae4d)
  - [Malloc](#org289f8e3)
- [C typer](#orgc6d4b13)
  - [Structs](#orge8b320d)
  - [Array Access](#orgb0d9939)
  - [Null pointer tjek](#org9b73886)
  - [Kommentare](#orge64ea64)



<a id="org0cfaa6d"></a>

# Nyttige C funktioner


<a id="org447ae4d"></a>

## sizeof

Denne funktion vil returnere størrelsen af en type i antal bytes. Exempel:

```c
sizeof(int)
```


<a id="org289f8e3"></a>

## Malloc

Denne funktion vil allokere en blok af bytes baseret på tallet den får givet, og returnere en pointer til denne blok. den vil returnere en null pointer hvis der ikke er plads Exempel:

```c
malloc(sizeof(int) * 8);
```

*Dette vil allokere 8 ints ved siden af hinanden, hvilket er et array*


<a id="orgc6d4b13"></a>

# C typer


<a id="orge8b320d"></a>

## Structs

En struct defineres på følgende måde:

```c
struct name_of_struct {
    type field_name;
    ...
}
```

Exempel:

```c
struct deck {
    int current_index;
    int *numbers;
}
```

*Denne struct indeholder et tal der er indexet for det øverste kort `current_index`, og så har den en pointer til et array af tal `numbers`*

**Bemærk**: `int *numbers` og `int* numbers` begge er pointers til ints

Man kan skabe et struct på følgende måder:

```c
struct Car {
    int door_numbers;
    int speed;
}

// Initialisering af struct
struct Car car1 = {4, 120};

// Modificering af værdier
car1.door_numbers = 23;
car1.speed = 23;
```

Dette laver structen direkte. Den anden måde er ved brug af `malloc`

```c
struct Car {
    int door_numbers;
    int speed;
}

// Allokering af plads til structen
struct Car *car1 = malloc(sizeof(struct Car));
// Modificering af værdierne
car1->door_numbers = 4;
car1->speed = 120;
```

Her bruger vi `->` istedet for `.`, da `malloc` returnerer en pointer til structen.


<a id="orgb0d9939"></a>

## Array Access

For at skabe et array af ints med størrelse 10 kan vi gøre følgende:

```c
int *new_array = (int*)malloc(sizeof(int) * 10);
```

Vi er nødt til at caste resultatet af `malloc` til en int pointer ellers får vi en fejl af compileren.

For at tilgå et element i arrayet bruger vi følgende syntax:

```c
new_array[4]
```

*Dette vil tilgå det femte element fra arrayet* **Bemærk**: c tjekker ikke efter om du kigger udenfor arrayet, så det skal du selv tjekke efter


<a id="org9b73886"></a>

## Null pointer tjek

Hvis vi kalder `malloc` og den ikke kan skabe nok plads til det vi beder den om, så vil den returnere en `null pointer`.

Dette kan man tjekke på følgende måde:

```c
int* x = (int*)malloc(sizeof(int) * 100);
// Vi beder om et array af størrelse 100
if (x) {
    ... //Kode til hvis x ikke er en null pointer
} else {
    ... // Kode til hvis x er en null pointer
}

// Alternativt
if (!x) {
    ... // Kode til hvis x er en null pointer
} else {
    ... // Kode til hvis x ikke er en null pointer
}
```

*`else` branchen er ikke obligatorisk, så man kan bruge `if (!x)` til evt at &rsquo;return fast&rsquo; som i SWEA*


<a id="orge64ea64"></a>

## Kommentare

I c har vi både oneline comments og block comments:

```c
// Jeg er en oneline comment

/*
  Jeg er en block
  comment. Jeg er gyldig
  indtil jeg slutter
*/
```
