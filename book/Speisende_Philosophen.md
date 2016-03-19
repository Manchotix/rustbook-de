#Speisende Philosophen

Für unser zweites Projekt schauen wir uns ein klassisches Problem der Nebenläufigkeit an. Hierfür ist das Beispiel der "Speisenden Philosophen" bekannt. <br>Dieses Konzept war ursprünglich erdacht von Dijkstra aus dem Jahr 1965, aber wir werden eine leicht veränderte Version von Tony Hoare verwenden aus dem Jahr 1985.

> In der Antike, hat ein reicher Philanthrop, an einer Universität fünf 
> bedeutende Philosophen untergebracht. Jeder dieser Philosophen hat seinen 
> eigenen Raum, um sich mit seinen Gedanken zu befassen. Zusätzlich haben die 
> Philosophen ein gemeinsames Esszimmer, mit fünf Stühlen die um einen runden 
> Tisch aufgestellt sind. Jeder Platz ist einem Philosphen zugewiesen und sie 
> setzen sich gegen den Uhrzeigersinn hin. Links von jedem Philosophen liegt 
> eine goldene Gabel, in der Mitte von dem Tisch steht ein wiederaufüllender 
> Topf mit Spaghetti. Ein Philosoph ist die meiste Zeit mit seinen Gedanken 
> beschäftigt, aber wenn er Hunger bekommt geht er ins Esszimmer, setzt sich 
> auf seinen Stuhl, nimmt von links seine Gabel und steckt sie in den Topf mit Spaghetti. Aber es liegt in der Natur der Spaghetti, dass man eine zweite 
> Gabel benötigt um sie zum Mund zu führen. Daher nimmt der Philosoph eine 
> weitere Gabel zu seiner Rechten. Wenn er fertig ist mit seinem Essen, legt 
> er beide Gabeln wieder zurück, steht von seinem Platz auf und beschäftigt 
> sich weiter mit seinen Gedanken. Allerdings, kann nur ein Philosoph die 
> Gabeln zur gleichen Zeit verwenden, falls andere Philosophen diese Gabeln 
> zur gleichen Zeit verwenden wollen, müssen sie warten.

Dieses klassische Problem zeigt unterscheidliche elemente auf von der Nebenläufigkeit. Es ist aktuell nur kompliziert zu implemtieren: eine simple Implementierung ist die Blockierung. Als Beispiel, betrachten wir einen simplen Algorithmus der das Problem lösen würde:

1. Ein Philosoph nimmt die Gabel zu seiner linken.
2. Dann nimmt er die Gabel von seiner rechten.
3. Dann isst er.
4. Legt die Gabeln wieder zurück.

Jetzt stellen wir uns den Vorgang der Events vor:

1. Philosoph 1 startet mit dem Algorithmus, nimmt die Gabel zu seiner linken.
2. Philosoph 2 startet mit dem Algorithmus, nimmt die Gabel zu seiner linken.
3. Philosoph 3 startet mit dem Algorithmus, nimmt die Gabel zu seiner linken.
4. Philosoph 4 startet mit dem Algorithmus, nimmt die Gabel zu seiner linken.
5. Philosoph 5 startet mit dem Algorithmus, nimmt die Gabel zu seiner linken.
6. ...? Alle Gabel sind genommen, aber keiner kann essen.

Es gibt verschiedene wege dieses Problem zu lösen. Wir werden auch andere Lösungen für das Problem sehen in diesem Tutorial. Fürs erste fangen wir an das Problem zu modellieren. Wir fangen an mit den Philosophen:


```rust
struct Philosopher {
    name: String,
}

impl Philosopher {
    fn new(name: &str) -> Philosopher {
        Philosopher {
            name: name.to_string(),
        }
    }
}

fn main() {
    let p1 = Philosopher::new("Judith Butler");
    let p2 = Philosopher::new("Gilles Deleuze");
    let p3 = Philosopher::new("Karl Marx");
    let p4 = Philosopher::new("Emma Goldman");
    let p5 = Philosopher::new("Michel Foucault");
}
```
Hier erstellen wir ein Struct das ein Philosophen repräsentiert. Fürs erste reicht ein Name.
Wir wählen für denn Namen den Typ String, beziehungsweise `&str` . Generell ist es leichter mit Typen zu arbeiten die diese Daten enthält, als solche die mit einer Referenz arbeiten.

Lasst uns weiter machen.

```rust
impl Philosopher {
    fn new(name: &str) -> Philosopher {
        Philosopher {
            name: name.to_string(),
        }
    }
}
```
Der `impl` block lässt uns dinge definieren für denn `Philosopher` 'Struct'. In diesem Fall, erstellen wir eine 'associated function'('zugehörige Funktion') `new`. Die erste Zeile sieht wie folgt aus.

```rust
fn new(name: &str) -> Philosopher {
```
Wir nehemen als Funktions argument ein 'namen'(`name`) vom Typ `&str`. Das ist eine Referenz zu einem anderen 'String' und gibt eine Instance von `Philosopher` zurück.
```rust
Philosopher {
    name: name.to_string(),
}
```
Das erstellt uns ein neuen Philosopher und setzt denn namen(`name`) gleich unseren Argument `name`. Aber nicht dem Argument selber sondern wir werden ein `.to_string()` anwenden. Das erzeugt uns eine String Kopie von &str .. 