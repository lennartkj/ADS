11, 12, 20, 15, 60, 10, 18, 14, 5, 2, 1

Einfügen 11 
11 
Einfügen 12 
11 | 12 
Einfügen 20 
11 12 20 => 12
        11|20
Einfügen 15 
      (12)->((11),(15|20))
Einfügen 60
      (12)->((11),(15|60|20))
      (12|20)->((11),(15),(60))
Einfügen 10 
      (12|20)->((10|11),(15),(60))
Einfügen 18
      (12|20)->((10|11),(15|18),(60))
Einfügen 14
      (12|20)->((10|11),(14|15|18),(60))
       (12|15|20)->((10|11),(14|18),(60))
       (15) -> ((12) -> ((10|11),(14))    , (20) -> ((18),(60)) )
Einfügen 5
       (15) -> ((12) -> ((5|10|11),(14))    , (20) -> ((18),(60)) )
       (15) -> ((10|12) -> ((5),(11),(14))    , (20) -> ((18),(60)) )
Einfügen 2
       (15) -> ((10|12) -> ((2|5),(11),(14))    , (20) -> ((18),(60)) )
Einfügen 1
       (15) -> ((10|12) -> ((1|2|5),(11),(14))    , (20) -> ((18),(60)) )
       (15) -> ((2|10|12) -> ((1),(5),(11),(14))    , (20) -> ((18),(60)) )
       (10|15) -> ((2),(12)) -> ((1),(5),(11),(14))    , (20) -> ((18),(60)) )
           (10|15) -> ((2) -> ((1),(5))    , (12) -> ((11,(14))), (20) -> ((18),(60)) )



> **Nutzen**
>
> * Die Datei lässt sich direkt auf GitHub, GitLab, StackEdit, VS Code Preview usw. anzeigen.
> * Kein externes Bild nötig – Mermaid rendert den Baum automatisch.

```markdown
# B‑Baum Ordnung 1 · Einfügefolge 11 → … → 1

Jeder *details*‑Block enthält ein Mermaid‑Diagramm.  
Knoten sind Rechtecke mit dem/den Schlüssel(n); Pfeile zeigen Kind­zeiger.

---

## Legende

```

\[11]           … Baum mit einem Schlüssel
\[11 12]        … Knoten (Ordnung 1 erlaubt max. 2 Schlüssel)

````

---

<details>
<summary>Schritt 1 · insert(<strong>11</strong>)</summary>

```mermaid
graph TD
    N11["11"]
````

</details>

<details>
<summary>Schritt 2 · insert(<strong>12</strong>)</summary>

```mermaid
graph TD
    N["11 12"]
```

</details>

<details>
<summary>Schritt 3 · insert(<strong>20</strong>) → Split Wurzel</summary>

```mermaid
graph TD
    R12["12"]
    L11["11"]
    R20["20"]
    R12 --- L11
    R12 --- R20
```

</details>

<details>
<summary>Schritt 4 · insert(<strong>15</strong>)</summary>

```mermaid
graph TD
    R12["12"]
    L11["11"]
    R1520["15 20"]
    R12 --- L11
    R12 --- R1520
```

</details>

<details>
<summary>Schritt 5 · insert(<strong>60</strong>) → Split Blatt</summary>

```mermaid
graph TD
    R1220["12 20"]
    L11["11"]
    M15["15"]
    R60["60"]
    R1220 --- L11
    R1220 --- M15
    R1220 --- R60
```

</details>

<details>
<summary>Schritt 6 · insert(<strong>10</strong>)</summary>

```mermaid
graph TD
    R1220["12 20"]
    L1011["10 11"]
    M15["15"]
    R60["60"]
    R1220 --- L1011
    R1220 --- M15
    R1220 --- R60
```

</details>

<details>
<summary>Schritt 7 · insert(<strong>18</strong>)</summary>

```mermaid
graph TD
    R1220["12 20"]
    L1011["10 11"]
    M1518["15 18"]
    R60["60"]
    R1220 --- L1011
    R1220 --- M1518
    R1220 --- R60
```

</details>

<details>
<summary>Schritt 8 · insert(<strong>14</strong>) → Split Mitte, Root übervoll → neue Wurzel 15</summary>

```mermaid
graph TD
    Root15["15"]
    L12["12"]
    R20["20"]
    LL1011["10 11"]
    LM14["14"]
    RL18["18"]
    RR60["60"]

    Root15 --- L12
    Root15 --- R20

    %% Kinder L12
    L12 --- LL1011
    L12 --- LM14
    %% Kinder R20
    R20 --- RL18
    R20 --- RR60
```

</details>

<details>
<summary>Schritt 9 · insert(<strong>5</strong>)</summary>

```mermaid
graph TD
    Root15["15"]
    L12["12"]
    R20["20"]

    LL51011["5 10 11"]
    LM14["14"]
    RL18["18"]
    RR60["60"]

    Root15 --- L12
    Root15 --- R20

    L12 --- LL51011
    L12 --- LM14
    R20 --- RL18
    R20 --- RR60
```

</details>

<details>
<summary>Schritt 10 · insert(<strong>2</strong>)</summary>

```mermaid
graph TD
    Root15["15"]
    L12["12"]
    R20["20"]

    LL251011["2 5 10 11"] 
    LM14["14"]
    RL18["18"]
    RR60["60"]

    Root15 --- L12
    Root15 --- R20

    L12 --- LL251011
    L12 --- LM14
    R20 --- RL18
    R20 --- RR60
```

*Hinweis:* Das Blatt `2 5 10 11` enthält nun 4 Schlüssel; beim nächsten Schritt wird es gesplittet.

</details>

<details>
<summary>Schritt 11 · insert(<strong>1</strong>) → letzter Split &amp; Promotion</summary>

```mermaid
graph TD
    RRoot1015["10 15"]
    L2["2"]
    M12["12"]
    R20["20"]

    LL1["1"]
    LR5["5"]
    ML11["11"]
    MR14["14"]
    RL18["18"]
    RR60["60"]

    RRoot1015 --- L2
    RRoot1015 --- M12
    RRoot1015 --- R20

    L2 --- LL1
    L2 --- LR5

    M12 --- ML11
    M12 --- MR14

    R20 --- RL18
    R20 --- RR60
```

</details>

---

## Endbaum (alle 11 Schlüssel)

```mermaid
graph TD
    Root["10 15"]
    L2["2"]
    M12["12"]
    R20["20"]

    LL1["1"]
    LR5["5"]
    ML11["11"]
    MR14["14"]
    RL18["18"]
    RR60["60"]

    Root --- L2
    Root --- M12
    Root --- R20

    L2 --- LL1
    L2 --- LR5

    M12 --- ML11
    M12 --- MR14

    R20 --- RL18
    R20 --- RR60
```

> *Alle Knoten erfüllen Ordnung 1: max 2 Schlüssel pro Knoten, Wurzel ≤ 2;
> Such­baumeigenschaft erhalten, Blätter liegen auf gleicher Tiefe.*

```

> **Speichern** als `baum_ord1.md` und auf GitHub oder einem anderen Markdown‑Renderer mit Mermaid‑Support öffnen.  
> Du kannst einzelne Details ein- oder ausklappen; die Diagramme passen sich automatisch an.
```



