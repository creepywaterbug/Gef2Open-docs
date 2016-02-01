###############
Betrouwbaarheid
###############

De betrouwbaarheid van de library Gef2Open.py is bepaald door het testen van alle functies op een groot (1000+) aantal gef-bestanden. De uitkomsten tussen de oorspronkelijke library Gef2.dll zijn vervolgens vergeleken met de uitkomsten van de onderhavige library Gef2Open.py.

Als alle diverse soorten 'ontbrekende waarden' gelijk aan elkaar gesteld werden dan hadden de meeste functies 100% overeenkomst en 3 functies 1 verschil en 2 functies tientallen verschillen.

Voor de functies test_gef() en is_plotable() zijn nog geen alternatieven gerealiseerd. Dit staat wel op het programma.

======================================	==============  ========
Functie					Gelijk ?        Aktie ?
======================================	==============  ========
def gbr_is_gbr()			ja		todo	
def gcr_is_gcr()			1van2000 niet   todo
def get_companyid_flag()		ja
def get_column()			ja
def get_column_flag()			ja
def get_companyid_name()		ja
def get_data(1, 1)			ja
def get_measurementtext_flag(1)		ja
def get_measurementtext_flag(15)	ja
def get_measurementvar_flag(1)		ja
def get_measurementvar_flag(15)		ja
def get_measurementtext_Tekst(1)	ja
def get_measurementtext_Tekst(15)	ja
def get_measurementvar_Value(1)		ja
def get_measurementvar_Value(15)	ja
def get_nr_scans()			17v2000 niet    todo 
def get_parent_flag()			ja
def get_parent_reference()		ja
def get_procedurecode_flag()		1v2000 niet     klaar
def get_procedurecode_Code()		1v2000 niet     klaar 
def get_projectid_flag()		ja	 	klaar
def get_projectid_number()		ja
def get_reportcode_flag()		ja
def get_reportcode_Code()		ja
def get_startdate_flag()		ja
def get_startdate_yyyy()		ja
def get_startdate_mm()			ja
def get_startdate_Dd()			ja
def get_xyid_flag()			ja
def get_xyid_x()			ja
def get_xyid_Y()			ja
def get_zid_flag()			ja
def get_zid_Z()				ja
def qn2column(1)			42v2000 niet	todo	
def qn2column(11)			ja		klaar
======================================	==============  ========

**Uitkomsten van 5 niet vergeleken test functies**

================================  ======  ====  =====
Functie                           Totaal  True  False
================================  ======  ====  =====
def test_gef('GEF-CPT-Report)	  2001    1017  984
def test_gef('HEADER')            2001    1937  64
def test_gef('GEF-BORE-Report')	  2001    570   1431
def test_gef('DATA')              2001    1998  3	
def is_plotable()                 2001    2001  0
================================  ======  ====  =====

*******************
Ontbrekende waarden
*******************
In de resultaten van functies van Gef2.dll komen veelvuldig de waarden '**32767**' , '**32767-32767-32767**' en '**3.40282346639e+38**' voor. In de tests die zijn uitgevoerd matchen deze resultaten altijd met de uitkomst 'None' in de bijbehorende functie in Gef2Open.py. Hetzelfde geldt voor de uitkomst '**-1.79769313486e+308**' van functies in Gef2.dll, maar deze komt slechts weinig voor. 
Een paar keer leverde in de test een functie in Gef2Open.py een lege waarde op (''), terwijl dezelfde functie in Gef2.dll geen resultaat leverde.

Op grond hiervan neem ik aan dat de volgende waardes missing values zijn en gelijk kunnen worden gesteld aan 'None'::

	Missing values: '3.40282346639e+38', '-1.79769313486e+308', '32767', '32767-32767-32767', ''

De aanroep van Gef2.dll functies leveren veelvuldig geen resultaat op. In alle gevallen was dit ook bij de bijbehorende functie in Gef2Open.py het geval.
