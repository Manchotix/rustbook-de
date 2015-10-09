#Speisende Philosphen

Für unser zweites Projekt, schauen wir uns ein klassisches Problem des gleichzeitigen Zugriffes an. Hierfür ist das Beispiel der "Speisenden Philosphen" bekannt.
Dieses Konzept war ursprünglich erdacht von Dijkstra aus dem Jahr 1965, aber wir werden eine leicht veränderte Version von Tony Hoare verwenden aus dem Jahr 1985 .

> In der Antike, hat ein reicher Philanthrop, an einer Universität fünf 
> bedeutende Philosphen untergebracht. Jeder dieser Philosphen hat seinen 
> eigenen Raum, um sich mit seinen Gedanken zu befassen. Zusätzlich haben die 
> Philosphen ein gemeinsames Esszimmer, mit fünf Stühlen die um einen runden 
> Tisch aufgestellt sind. Jeder Platz ist einem Philosphen zugewiesen und sie 
> setzen sich gegen den Uhrzeigersinn hin. Links von jedem Philosphen liegt 
> eine goldene Gabel, in der Mitte von dem Tisch steht ein wiederaufüllender 
> Topf mit Spaghetti.
> Ein Philosph ist die meiste Zeit mit seinen Gedanken beschäftigt, aber wenn
> er Hunger bekommt geht er ins Esszimmer, setzt sich auf seinen Stuhl, nimmt > von links seine Gabel und steckt sie in den Topf mit Spaghetti.
> Aber es liegt in der Natur der Spaghetti, dass man eine zweite Gabel 
> benötigt um sie zum Mund zu führen. Daher nimmt der Philosph eine weitere 
> Gabel zu seiner Rechten. Wenn er fertig ist mit seinem Essen, legt er beide > Gabeln wieder zurück, steht von seinem Platz auf und beschäftigt sich weiter > mit seinen Gedanken. Allerdings, kann nur ein Philosph die Gabeln zur 
> gleichen Zeit verwenden, falls andere Philosphen diese Gabeln zur gleichen 
> Zeit verwenden wollen, müssen sie warten.


