/*
Proyecto: GEIH 2023 - DANE
Objetivo: PEGADO AJUSTADO
Autor: 
Pablo Santiago Cárdenas Moreno 
Fecha: 12/07/2024
*/

/*=====================================================
		0:Pegado GEIH 2023
======================================================*/

foreach x of numlist 1 2 3 4 5 6 7 8 9 10 11 12 {

cd C:\Users\USUARIO\Downloads\2023_V2\mes_`x'\DTA

use "Características generales, seguridad social en salud y educación",clear
merge  1:1 DIRECTORIO  SECUENCIA_P ORDEN using  "Características generales, seguridad social en salud y educación",nogenerate
merge 1:1 DIRECTORIO  SECUENCIA_P ORDEN using  "Fuerza de trabajo",nogenerate
merge 1:1 DIRECTORIO  SECUENCIA_P ORDEN using  "Migración",nogenerate
merge 1:1 DIRECTORIO  SECUENCIA_P ORDEN using  "No ocupados",nogenerate
merge 1:1 DIRECTORIO  SECUENCIA_P ORDEN using  "Ocupados",nogenerate
merge 1:1 DIRECTORIO  SECUENCIA_P ORDEN using  "Otras formas de trabajo",nogenerate
merge 1:1 DIRECTORIO  SECUENCIA_P ORDEN using  "Otros ingresos e impuestos",nogenerate
merge 1:1 DIRECTORIO  SECUENCIA_P ORDEN using  "Tipo de investigación",nogenerate
merge m:1 DIRECTORIO  SECUENCIA_P  using  "Datos del hogar y la vivienda",nogenerate
gen MESS=`x'
label drop _all
cd "C:\Users\USUARIO\Downloads\2023_V2\2023"
save mes_`x', replace
clear
}

/*=====================================================
		1:Liviana GEIH 2023
======================================================*/

cd "C:\Users\USUARIO\Downloads\2023_V2\2023"
    foreach x of numlist 1 2 3 4 5 6 7 8 9 10 11 12{
         use mes_`x'.dta
	     export delimited using mes_`x', replace
}

csvconvert C:\Users\USUARIO\Downloads\2023_V2\2023, replace input_file(mes_1.csv mes_2.csv mes_3.csv mes_4.csv mes_5.csv mes_6.csv mes_7.csv mes_8.csv mes_9.csv mes_10.csv mes_11.csv mes_12.csv) output_file(2023.csv) output_dir(C:\Users\USUARIO\Downloads\2023_V2\2023)

csvconvert C:\Users\USUARIO\Downloads\2023_V2\2023, replace input_file(mes_1.csv mes_2.csv mes_3.csv mes_4.csv mes_5.csv mes_6.csv mes_7.csv mes_8.csv mes_9.csv mes_10.csv mes_11.csv mes_12.csv) output_file(2023.dta) output_dir(C:\Users\USUARIO\Downloads\2023_V2\2023)

