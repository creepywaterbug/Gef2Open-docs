###############
Gebruik Gef2Open.py
###############

De originele library wordt in windows systemen als volgt aangeroepen in python::

	>>> Gef2 = ctypes.windll.Gef2

De onderhavige library wordt op reguliere wijze geimporteerd in python::

	>>> import Gef2Open

In de originele gesloten library Gef2.dll moeten ter initialisatie de volgende functies worden aangeroepen::

	>>> init_gef()
	>>> free_gef()
	>>> read_gef(i_sBestandGef)

Het gef-bestand wordt dan in RAM geladen en is vervolgens voor andere functies beschikbaar

In de onderhavige open library Gef2.py hoeft alleen de functie read_gef() te worden aangeroepen::

	>>> read_gef(i_sBestandGef)

De functie converteert de informatie uit het gef-bestand naar een eenvoudig bevraagbare dictionary. Om de werking van Gef2.py vergelijkbaar te maken aan Gef2.dll wordt de dictionary vervolgens in een tijdelijk bestand weggeschreven.

Alle andere functies worden vervolgens op vergelijkbare wijze als bij Gef2.dll aangeroepen::

	Gef2Open.gbr_is_gbr()
	Gef2Open.gcr_is_gcr()
	Gef2Open.get_companyid_flag()
	Gef2Open.get_column()
	Gef2Open.get_column_flag()
	Gef2Open.get_companyid_Name()
	Gef2Open.get_data(i_Kol, iRij)
	Gef2Open.get_measurementtext_flag(i_Index)
	Gef2Open.get_measurementvar_flag(i_Index)
	Gef2Open.get_measurementtext_Tekst(i_Index)
	Gef2Open.get_measurementvar_Value(i_Index)
	Gef2Open.get_nr_scans()
	Gef2Open.get_parent_flag()
	Gef2Open.get_parent_reference()
	Gef2Open.get_procedurecode_flag()
	Gef2Open.get_procedurecode_Code()
	Gef2Open.get_projectid_flag()
	Gef2Open.get_projectid_Number()
	Gef2Open.get_reportCode_flag()
	Gef2Open.get_reportcode_Code()
	Gef2Open.get_startdate_flag()
	Gef2Open.get_startdate_Yyyy()
	Gef2Open.get_startdate_Mm()
	Gef2Open.get_startdate_Dd()
	Gef2Open.get_xyid_flag()
	Gef2Open.get_xyid_X()
	Gef2Open.get_xyid_Y()
	Gef2Open.get_zid_flag()
	Gef2Open.get_zid_Z()
	Gef2Open.qn2column(i_iQtyNumber)
	Gef2Open.is_plotable()
	Gef2Open.test_gef(i_sAspect)
