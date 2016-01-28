########
Algemeen
########

**************
Missing values
**************
In de resultaten van functies van UtlGef.py komen veelvuldig de waarden '**32767**' en '**32767-32767-32767**' voor. In de tests die zijn uitgevoerd matchen deze resultaten altijd met de uitkomst 'None' in de bijbehorende functie in UtlGefOpen.py. Hetzelfde geldt voor de uitkomst '**-1.79769313486e+308**' van functies in UtlGef.py, maar deze komt slechts weinig voor. 
Een paar keer leverde in de test een functie in UtlGefOpen.py een lege waarde op (''), terwijl dezelfde functie in UtlGef.py geen resultaat leverde.

Op grond hiervan neem ik aan dat de volgende waardes missing values zijn en gelijk kunnen worden gesteld aan 'None'::

	Missing values: '-1.79769313486e+308', '32767', '32767-32767-32767', ''

De aanroep van Gef2.dll functies in UtlGef.py leveren veelvuldig geen resultaat op. In alle gevallen was dit ook bij de bijbehorende functie in UtlGefOpen.py het geval.

***********
Afrondingen
***********
Getalmatige uitkomsten in UtlGef.py werden veelal afgerond op 3 decimalen achter de comma. Bij het vergelijken van de uitkomsten tussen Gef2.dll/UtlGef.py en UtlGefOpen.py is hiermee rekening gehouden.
