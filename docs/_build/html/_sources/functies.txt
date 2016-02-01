########
Functies
########

Voor de meeste functies was eenvoudig te achterhalen welke informatie uit de gef-bestanden moest worden opgehaald. Als uit de uitgevoerde test in 'betrouwbaarheid' vervolgens een 100% match bleek is naar de betreffende functie verder (nog) niet inhoudelijk gekeken.

Functies waar wel meer in detail naar is gekeken zijn hieronder opgenomen.

============
gbr_is_gbr()
============
`Programmers documentation <http://localhost/rdddiv/gef2prog_3.pdf>`_::

	int  gbr_is_gbr();
	Output:
	True if the file contains a reportcode: GEF-BORE-Report

Bovenstaande klopt met de inhoud van Gef2Open.py. Bij een test waarbij de test Gbr_Is_Gbr() van Gef2.dll is uitgevoerd hadden alle gef-bestanden dezelfde uitkomst voor Gef2.dll en Gef2Open.py. **ToDo**: 'PROCEDURECODE' uit functie halen

============
gcr_is_gcr()
============
`Programmers documentation <http://localhost/rdddiv/gef2prog_3.pdf>`_::

	int gcr_is_legal();
	This functions returns a true if the file is a legal (approved by the CUR) CPT Report file.
	int gcr_is_gcr();
	This functions is an alias for gcr_is_legal(); since there is a gbr_is_gbr(); as well
Bovenstaande is een andere meer omvattende beschrijving dan Gbr_Is_Gbr(). De functie in Gef2Open.py is analoog aan de beschrijving in Gbr_Is_Gbr() gebouwd. Dus uitkomst 'True' als de file een reportcode met waarde 'GEF-CPT-Report' bevat. In de uitgevoerde test had 1 van de 2000 gef-bestanden een andere uitkomst voor Gef2Open.py (True) in vergelijking met Gef2.dll (False). Het betreffende bestand had de volgende relevante regels::

	#PROCEDURECODE= GEF-CPT-Report, 1, 1, 0, -
	#REPORTCODE= GEF-DISS-Report, 1, 0, 0, -
In Gef2Open.py geeft een 'True' als 'GEF-CPT-Report' in ofwel 'PROCEDURECODE' ofwel 'REPORTCODE' voorkomt. Dit is een andere benadering dan hierboven beschreven en kennelijk kijkt Gef2.dll alleen in 'REPORTCODE' en niet in 'PROCEDURECODE'. **ToDo**: 'PROCEDURECODE' uit functie halen



==============
get_nr_scans()
==============
`Programmers documentation <http://localhost/rdddiv/gef2prog_3.pdf>`_::

	long get_nr_scans():

	This function retrieves the actual number of scans, present in the data block.
	This number may differ from the value as given in the keyword LASTSCAN.
	When data is written, converted,processed, this property reflects the actual 
	number of scans being accessed.
	Output:
	The actual number of scans, as present in the data block.

Bij een test waarbij de test Get_Nr_Scans() van Gef2.dll is uitgevoerd hadden 10 van 2000 gef-bestanden een andere uitkomst (1990 waren dus gelijk). In Gef2Open is echter simpelweg de waarde achter 'LASTSCAN' in de header overgenomen. Uit de beschrijving hierboven blijkt dat dit niet de bedoeling is. **ToDo**: uitzoeken hoe Get_Nr_Scans() werkt! 

========================
get_procedurecode_flag()
========================
`Programmers documentation <http://localhost/rdddiv/gef2prog_3.pdf>`_::

	#Procedurecode= Code, Release, Version, Update[, Reference]

	Setting:
	void set_procedurecode( char *Code, int Release, int Version, int Update, char *Reference );
	Getting:
	int get_procedurecode_flag();

	==================================   =================================
	Preferred names                      Alias
	==================================   =================================
        char* get_procedurecode_Code()       char* get_procedurecode_code(); 
	int get_procedurecode_Release()      int   get_procedurecode_release();
        int get_procedurecode_Version()      int   get_procedurecode_versie();
	int get_procedurecode_Update()       int   get_procedurecode_update();
        char* get_procedurecode_Reference()  char* get_procedurecode_isoref();
	==================================   =================================

	Deleting:
	int del_procedurecode ();

	Code		Text stating the code of the procedure.
	Release		A number which gives the release of the procedure.
	Version		A number which gives the version of the procedure.
	Update		A number which gives the update of the procedure.
	Reference	Reference document or ISO-9000 standard. Maximum 80 characters.

	Example: #Procedurecode=GEF-CPT-Report, 1,0,0.

**Gef2Open.py**::

	def Get_ProcedureCode_Flag():
		fp = open("tmpheaderdict.pkl")
		headerdict=ast.literal_eval(pickle.load(fp))
		if ('PROCEDURECODE' in headerdict and len(headerdict['PROCEDURECODE'])>0):
			out=True
		else:
			out=False
		try:
			return out
		except:
			return None

Bij een vergelijking tussen de uitkomsten van de functie in Gef2.dll en Gef2Open.py gaf 1 van 2000 gef-bestanden een verschillende uitkomst. Gef2.dll: False / Gef2Open.py: True. De relevante regel in het gef-bestand is::

	#PROCEDURECODE= GEF-CPT-Report, 1, 1, 0, -
Het is onduidelijk / onlogisch waarom Gef2.dll hier een False afgeeft. Ik ga er daarom vanuit dat Gef2Open.py goed is. 

========================
get_procedurecode_code()
========================
`Programmers documentation <http://localhost/rdddiv/gef2prog_3.pdf>`_:
zie onder **Get_ProcedureCode_Code()**

**Gef2Open.py**::

	def Get_ProcedureCode_Code():
		fp = open("tmpheaderdict.pkl")
		headerdict=ast.literal_eval(pickle.load(fp))
		if ('PROCEDURECODE' in headerdict and len(headerdict['PROCEDURECODE'])>0):
			out=headerdict['PROCEDURECODE'][0]
		try:
			return out
		except:
			return None

Bij een vergelijking tussen de uitkomsten van de functie in Gef2.dll en Gef2Open.py had slechts 1 van 2000 gef-betanden een andere uitkomsten. De reden hiervoor is dezelfde als bij Get_ProcedureCode_Flag().

====================
get_projectid_flag()
====================
`Programmers documentation <http://localhost/rdddiv/gef2prog_3.pdf>`_::

	#Projectid=Type, [Number, [Sub]]

	Setting:
	void	set_projectid(char* sTtype, char*sNumber, char* sSub );
	Getting:
	int	get_projectid_flag();

	============================   ==============================
	Preferred names                Alias
	============================   ==============================
	char* get_projectid_Type()     char*  get_projectid_type();
	char* get_projectid_Number()   char*  get_projectid_number();
	char* get_projectid_Sub()      char*  get_projectid_sub();
	============================   ==============================

	Deleting:
	int	del_projectid();

	Type	Order identification
	Number	The order number.
	Sub	The sub-project number

	Example:	#Projectid=CO, 342770, 624

**Gef2Open.py**::

	def get_projectid_flag():
		fp = open("tmpheaderdict.pkl")
		headerdict=ast.literal_eval(pickle.load(fp))
		if 'PROJECTID' in headerdict:
			if len(headerdict['PROJECTID'])>0:
				out = True
			else:
				out = False
		try:
			return out
		except:
			return None

In de test waarbij de uitkomsten voor de functie in Gef2.dll met die van Gef2Open.py met elkaar zijn vergeleken leverde voor alle 2000 vergeleken bestanden dezelfde uitkomst.

=======================
qn2column(i_iQtyNumber)
=======================

`Programmers documentation <http://localhost/rdddiv/gef2prog_3.pdf>`_::

	This function queries the header structure for the presence of a column in the data block, which
	contains specific information, as determined by a quantity number. The main advantage of
	quantity number is that it is a number, independent of language, spelling (errors) or description.
	A particular quantity can thus be easily located.
	int	qn2column(int quantitynumber);
	Input:
	int	quantitynumber      The number that characterizes the requested quantity.
	Output:
	The number of the column in which the requested quantity can be found. If the quantity is not
	present, the function returns 0.

**Gef2Open.py**::

	def Qn2Column(i_iQtyNumber):
		headerdict=ast.literal_eval(pickle.load(open("tmpheaderdict.pkl")))
		try:
			(...)
			return int(out)
		except:
			return None

De beschrijving in de Programmers documentation geeft geen info over HOE 'the requested quantity' wordt 'characterized'. De werking van deze functie kon dus alleen worden achterhaald door het analyseren van de uitkomsten van tests op 2000 gef-bestanden. Voorlopig is dit alleen gebeurt voor de waarden '1' en '11' van i_iQtyNumber.

--------------
i_iQtyNumber=1
--------------
Ik moest testen of 1 van de termen 'sondeerlengte','penetration length','diepte bovenkant' of 'laag van' achter keyworde COLUMNINFO aanwezig was en vervolgens het nummer vooraan teruggeven. Voorbeeld::

	#COLUMNINFO= 1, m, Sondeerlengte, 1

Op deze manier kreeg ik in de test voor 1960 van 2000 bestanden dezelfde uitkomst voor Gef2.dll en Gef2Open.py. Wat de logica hierachter is is mij onbekend.

**Gef2Open.py**::

	(...)
	if i_iQtyNumber==1:
		out = 0
		for i in headerdict['COLUMNINFO']:
			j = headerdict['COLUMNINFO'][i]
			if 'sondeerlengte' in str.lower(str(j)):
				out = j[0]
			if 'penetration length' in str.lower(str(j)):
				out = j[0]
			if 'diepte bovenkant' in str.lower(str(j)):
				out = j[0]
			if 'laag van' in str.lower(str(j)):
				out = j[0]
	(...)

---------------
i_iQtyNumber=11
---------------
Ik moest testen of de term 'gecorrigeerde diepte' achter het keyword 'COLUMNINFO' aanwezig was en 
vervolgens het nummer vooraan teruggeven. Dit leverde in de uiteindelijke test altijd een match op in de vergelijking tussen de uitkomsten van Gef2.dll en Gef2Open.py.

**Gef2Open.py**::

	(...)
	if i_iQtyNumber==11:	
		out = 0
		for i in headerdict['COLUMNINFO']:
			j = headerdict['COLUMNINFO'][i]
			if 'gecorrigeerde diepte' in str.lower(str(j)) :
				out = j[0]
	(...)

=============
is_plotable()
=============
`Programmers documentation <http://localhost/rdddiv/gef2prog_3.pdf>`_::

	int is_plotable(void):
	
	This function determines whetter the most basic information is 
	present in the file in order to produce a graph of the data.
	Output:
	A boolean which signals whether a plot can be made.

Bij een test waarbij de test Is_Plotable() van Gef2.dll is uitgevoerd hadden alle 2000 geteste gef-bestanden als uitslag 'True'. Hier zaten ook 3 gef-bestanden bij waarbij de test Test_Gef('DATA') de uitslag 'False' had.
