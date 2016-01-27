########
Functies
########
**Vergeleken functies**

======================================	==============  ========
Functie					Gelijk ?        Aktie ?
======================================	==============  ========
def Gbr_Is_Gbr()			Ja		Ja	
def Gcr_Is_Gcr()			1van2000 niet   Ja
def Get_CompanyID_Flag()		Ja
def Get_Column()			Ja
def Get_Column_Flag()			Ja
def Get_CompanyID_Name()		Ja
def Get_Data(i_Kol, iRij)		Ja
def Get_MeasurementText_Flag(i_Index)	??
def Get_MeasurementVar_Flag(i_Index)	??
def Get_MeasurementText_Tekst(i_Index)	??
def Get_MeasurementVar_Value(i_Index)	??
def Get_Nr_Scans()			10v2000 niet    Ja,hoe? 
def Get_Parent_Flag()			Ja
def Get_Parent_Reference()		Ja
def Get_ProcedureCode_Flag()		1v2000 niet     Nee,Klaar
def Get_ProcedureCode_Code()		helft niet      Ja
def Get_ProjectID_Flag()		500v2000 niet   Ja
def Get_ProjectID_Number()		Ja
def Get_ReportCode_Flag()		Ja
def Get_ReportCode_Code()		Ja
def Get_StartDate_Flag()		Ja
def Get_StartDate_Yyyy()		Ja
def Get_StartDate_Mm()			Ja
def Get_StartDate_Dd()			Ja
def Get_XYID_Flag()			10v2000 niet
def Get_XYID_X()			10v2000 niet
def Get_XYID_Y()			10v2000 niet
def Get_ZID_Flag()			Ja
def Get_ZID_Z()				Ja
def Qn2Column(i_iQtyNumber)		100v2000 niet
======================================	==============  ========

**Uitkomsten van 5 niet vergeleken test functies**

================================  ======  ====  =====
Functie                           Totaal  True  False
================================  ======  ====  =====
def Test_Gef('GEF-CPT-Report)	  2001    1017  984
def Test_Gef('HEADER')            2001    1937  64
def Test_Gef('GEF-BORE-Report')	  2001    570   1431
def Test_Gef('DATA')              2001    1998  3	
def Is_Plotable()                 2001    2001  0
================================  ======  ====  =====



***********
Lange lijst
***********

=============
Is_Plotable()
=============
`Programmers documentation <http://localhost/rdddiv/gef2prog_3.pdf>`_::

	int is_plotable(void):
	
	This function determines whetter the most basic information is 
	present in the file in order to produce a graph of the data.
	Output:
	A boolean which signals whether a plot can be made.

Bij een test waarbij de test Is_Plotable() van Gef2.dll is uitgevoerd hadden alle 2000 geteste gef-bestanden als uitslag 'True'. Hier zaten ook 3 gef-bestanden bij waarbij de test Test_Gef('DATA') de uitslag 'False' had.

==============
Get_Nr_Scans()
==============
`Programmers documentation <http://localhost/rdddiv/gef2prog_3.pdf>`_::

	long get_nr_scans():

	This function retrieves the actual number of scans, present in the data block.
	This number may differ from the value as given in the keyword LASTSCAN.
	When data is written, converted,processed, this property reflects the actual 
	number of scans being accessed.
	Output:
	The actual number of scans, as present in the data block.

Bij een test waarbij de test Get_Nr_Scans() van Gef2.dll is uitgevoerd hadden 10 van 2000 gef-bestanden een andere uitkomst (1990 waren dus gelijk). In UtlGefOpen is echter simpelweg de waarde achter 'LASTSCAN' in de header overgenomen. Uit de beschrijving hierboven blijkt dat dit niet de bedoeling is. **ToDo**: uitzoeken hoe Get_Nr_Scans() werkt! 

========================
Get_Procedurecode_Flag()
========================
`Programmers documentation <http://localhost/rdddiv/gef2prog_3.pdf>`_::

	Procedurecode= Code, Release, Version, Update[, Reference]

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

	Code		Reference Text stating the code of the procedure.
	Release		A number which gives the release of the procedure.
	Version		A number which gives the version of the procedure.
	Update		A number which gives the update of the procedure.
	Reference	Reference document or ISO-9000 standard. Maximum 80 characters.

	Example: #Procedurecode=GEF-CPT-Report, 1,0,0.
============
Gbr_Is_Gbr()
============
`Programmers documentation <http://localhost/rdddiv/gef2prog_3.pdf>`_::

	int  gbr_is_gbr();
	Output:
	True if the file contains a reportcode: GEF-BORE-Report

Bovenstaande klopt met de inhoud van UtlGefOpen.py. Bij een test waarbij de test Gbr_Is_Gbr() van Gef2.dll is uitgevoerd hadden alle gef-bestanden dezelfde uitkomst voor Gef2.dll en UtlGefOpen.py. **ToDo**: 'PROCEDURECODE' uit functie halen

============
Gcr_Is_Gcr()
============
`Programmers documentation <http://localhost/rdddiv/gef2prog_3.pdf>`_::

	int gcr_is_legal();
	This functions returns a true if the file is a legal (approved by the CUR) CPT Report file.
	int gcr_is_gcr();
	This functions is an alias for gcr_is_legal(); since there is a gbr_is_gbr(); as well
Bovenstaande is een andere meer omvattende beschrijving dan Gbr_Is_Gbr(). De functie in UtlGefOpen.py is analoog aan de beschrijving in Gbr_Is_Gbr() gebouwd. Dus uitkomst 'True' als de file een reportcode met waarde 'GEF-CPT-Report' bevat. In de uitgevoerde test had 1 van de 2000 gef-bestanden een andere uitkomst voor UtlGefOpen.py (True) in vergelijking met Gef2.dll (False). Het betreffende bestand had de volgende relevante regels::

	#PROCEDURECODE= GEF-CPT-Report, 1, 1, 0, -
	#REPORTCODE= GEF-DISS-Report, 1, 0, 0, -
In UtlGefOpen.py geeft een 'True' als 'GEF-CPT-Report' in ofwel 'PROCEDURECODE' ofwel 'REPORTCODE' voorkomt. Dit is een andere benadering dan hierboven beschreven en kennelijk kijkt Gef2.dll alleen in 'REPORTCODE' en niet in 'PROCEDURECODE'. **ToDo**: 'PROCEDURECODE' uit functie halen


========================
Get_ProcedureCode_Flag()
========================
`Programmers documentation <http://localhost/rdddiv/gef2prog_3.pdf>`_::

	=================================   ================================
	Preferred names                     Alias
	=================================   ================================
        char* get_procedurecode_Code()      char* get_procedurecode_code();
        int get_procedurecode_Release()     int get_procedurecode_release();
        int get_procedurecode_Version()     int get_procedurecode_versie();
        int get_procedurecode_Update()      int get_procedurecode_update();
        int get_procedurecode_Reference()   int get_procedurecode_isoref();
	=================================   ================================

	#Procedurecode= Code, Release, Version, Update[, Reference]
	Setting:
	void	set_procedurecode(char *Code, int Release, int Version, int Update, char *Reference);
	Getting:
	int	get_procedurecode_flag();


	Deleting:
	int	del_procedurecode()

	Code		Text stating the code of the procedure
	Release		A number which gives the release of the procedure
	Version		A number which gives the version of the procedure
	Update		A number whic gives the update of the procedure
	Reference	Reference document of ISO-9000 standard. Maximum 80 characters
	Example:	#Procedurecode=GEF-CPT-Report, 1,0,0.

Bij een vergelijking tussen de uitkomsten van de functie in Gef2.dll en UtlGefOpen gaf 1 van 2000 gef-bestanden een verschillende uitkomst. Gef2.dll: False / UtlGefOpen: True. De relevante regel in het gef-bestand is::

	#PROCEDURECODE= GEF-CPT-Report, 1, 1, 0, -
Het is onduidelijk / onlogisch waarom Gef2.dll hier een False afgeeft. Ik ga er daarom vanuit dat UtlGefOpen.py goed is. 

========================
Get_ProcedureCode_Code()
========================
`Programmers documentation <http://localhost/rdddiv/gef2prog_3.pdf>`_:
zie onder **Get_ProcedureCode_Code()**

Bij een vergelijking tussen de uitkomsten van de functie in Gef2.dll en UtlGefOpen had circa de helft van de gef-bestanden een andere uitkomst. Op 1 gef-bestand na was de uitkomst van gef2.dll een geforceerde 'None' uitkomst als gevolg van een non-response van Gef2.dll. UtlGefOpen.py gaf in die gevalllen een False omdat het keyword 'PROCEDURECODE' afwezig was of geen bijbehorende waarde had. 

**ToDo**: Hoewel de Programmers docs geen uitsluitsel geeft vind ik de uitkomst None een betere dan False. Dus ga deze vervangen.

====================
Get_ProjectID_Flag()
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

**UtlGefOpen.py**::

	def Get_ProjectID_Flag():
		fp = open("tmpheaderdict.pkl")
		headerdict=ast.literal_eval(pickle.load(fp))
		if ('PROJECTID' in headerdict and len(headerdict['PROJECTID'])>1):
			out = True
		else:
			out = False
		try:
			return out
		except:
			return None

In de test waarbij de uitkomsten van de functie in Gef2.dll en UtlGefOpen.py met elkaar zijn vergeleken bleken alle 2000 bestanden voor Gef2.dll de uitkomst 'True' te hebben, terwijl circa 1500 daarvan in UtlGefOpen.py dezelfde uitkomst hadden (True) maar 500 een andere uitkomst hadden (False). Ik heb 1 gef-bestand (DKMP29-152KR_000_DIS_02) bekeken en zag daar de volgende relevante regel::

	#PROJECTID= 1204-0058-011
Dit hoort een 'True' op te leveren. Dit gaat fout vanwege 'len(headerdic...>1', moet zijn 'len(headerdic ....>0'

**ToDo**: Aanpassen!

