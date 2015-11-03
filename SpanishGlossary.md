#summary Spanish translation glossary and terminology
#labels Phase-Implementation

# Introduction #

This page is used by the Spanish translators to coordinate on terminology and terms to use while translating Tryton, thus, from this point, it's in Spanish only.

# Referencias externas #

  * Guía de traducción de GNOME: http://www.es.gnome.org/Documentacion/Guias/TraduccionDeAplicaciones?action=AttachFile&do=get&target=GNOME_l10n_es.pdf
  * http://www.allbusiness.com/glossaries/projected-benefit-obligation/4945200-1.html
  * http://code.google.com/p/tinyerp-community/wiki/Traduccion_es_ES
  * http://www.spanish-translator-services.com/espanol/diccionarios/

Es fundamental que podamos consensuar los términos a utilizar en las traducciones. Que cada cual utilice una traducción personalizada porque se encuentra más cómodo con los términos que se manejan en esta nos traerá problemas a la larga y dificultará el desarrollo de documentación localizada en el futuro. Por estos motivos esta página pretende ser un lugar donde comentar y proponer alternativas en relación a los términos utilizados en la traducción de Tryton.

# Normativa general #

  * Siempre que sea posible, hay que intentar usar un término lo más neutro posible de forma que se entienda en todos los países de habla española sin necesidad de aclaraciones extras. Un buen ejemplo de este tipo de traducciones es el proyecto GNOME y por eso apuntamos a su guía de traducción ya que cubre muchos trucos para conseguir dicha traducción neutra.
  * Se ha utilizado acentos, tanto en mayúsculas como en minúsculas. Esto no acarrea ningún tipo de problema codificando en UTF-8 el fichero de la traducción. Además de ser normativa ortográfica, permite automatizar la traducción a otros idiomas latinos como catalán y gallego.
  * Sólo se utilizan mayúsculas al inicio de la frase/texto o cuando es nombre propio. El uso de mayúsculas en la primera letra de cada palabra está aceptado en inglés pero no en castellano. Además los textos quedan ligeramente más cortos y se facilita la lectura. Se hace una excepción con la abreviaciones (p.e. LdM).
  * Las acciones son verbos en infinitivo (p.e. Cancelar). Los estados son verbos en participio (p.e. Cancelado).
  * En las ayudas o sugerencias se usa la forma verbal de usted, sin poner nunca la palabra usted. Por ejemplo: Marque esta opción para poder cancelar asientos en este diario. Seleccione Bajo pedido para ...
  * Los mensaje de error y los textos de ayuda se terminan en punto (el original en inglés no siempre lo tiene).
  * Se ha intentado mantener la longitud de los textos originales, aunque es imposible pues en la mayoría de casos las traducciones al castellano son más largas. Se ha testeado la mayoría de menús, vistas, formularios e informes para comprobar que no aparezcan textos demasiado largos.
  * Tryton está orientado a la empresa, por tanto, hay que evitar juegos de palabras que puedan inducir a error a futuros usuarios, por ejemplo, traducir términos en masculino y femenino usando la letra «@».


# Glosario de términos comunes #

En esta sección se pueden ver varias tablas de terminología específica de Tryton/ERPs ordenada alfabéticamente para decidir un consenso en cuanto al término a utilizar. Algunas veces dicho consenso no se podrá adoptar, dado que la terminología es muy distinta en cada país. En dichos casos se necesitará una traducción específica para cada país. Cuando una expresión se ha traducido de dos o más formas diferentes se han separado con la barra inclinada /.

## Contabilidad ##

| Inglés          | España       | Colombia | México | Comentario |
|:----------------|:-------------|:---------|:-------|:-----------|
| account         | cuenta       |          |        |            |
| account chart   | plan contable|          |        |            |
| account journal | diario contable | libro diario |        |            |
| account move    | asiento      |          |        |            |
| account move line| apunte       | movimiento |        |            |
| aged balance    | saldo vencido|          |        |            |
| amount          | importe      |          |        |            |
| balance         | balance o saldo (según contexto) |          |        |            |
| balance         | saldo pendiente (en formas de pago) |          |        |            |
| balance sheet   | balance general / balance de situación |          |        |            |
| bank account    | cuenta bancaria |          |        |            |
| bank statement  | extracto bancario |          |        |            |
| chart code      |              | lista de códigos |        | Si hay una mejor traducción reportarla |
| chart of account| plan contable| plan de cuentas |        |            |
| credit          | haber        |          |        |            |
| credit balance  | saldo acreedor |          |        |            |
| credit note     | abono        |          |        |            |
| debit           | debe         |          |        |            |
| debit balance   | saldo deudor |          |        |            |
| default         | por defecto  |          | predeterminado |            |
| deferral        | cierre       |          |        |            |
| fiscal year     | ejercicio fiscal |          |        |            |
| general ledger  | libro mayor  |          |        |            |
| general journal | libro diario |          |        |            |
| income statement| estado de pérdidas y ganancias | declaración de renta |        |            |
| move line       | apunte       | movimiento |        |            |
| payable         | a pagar      |          |        |            |
| payment terms   | plazos de pago | formas de pago |        | esCO: antigüo Términos de Pago |
| receivable      | a cobrar     |          |        |            |
| tax             | impuesto     |          |        |            |
| term            | plazo de pago|          |        |            |
| total           | total        |          |        |            |
| trial balance   | balance de sumas y saldos |          |        |            |
| untaxed amount  | base imponible |          |        | también: gravable |
| VAT             | IVA          |          |        |            |
| VAT number      | NIF          |          | RFC    |            |
| write-off       | desajuste    | ajuste   | ajuste |            |

## Términos específicos ##

| Inglés      | España     | Colombia  | México | Comentario |
|:------------|:-----------|:----------|:-------|:-----------|
| assignation | asignación |           |        |            |
| attendances | servicios  |           |        |            |
| BOM         | Lista de Materiales |           |        |            |
| case        | caso       |           |        |            |
| chart       | gráfico / resumen |           |        |            |
| company     | empresa    |           |        |            |
| custom      | personalizado |           |        |            |
| dashboard   | tablero    |           |        |            |
| deadline    | fecha límite |           |        |            |
| done        | realizado  |           |        |            |
| draft       | borrador   |           |        |            |
| email       | email      |           | correo |            |
| event       | evento     |           |        |            |
| file        | archivo    |           |        |            |
| follow-up   | seguimiento|           |        |            |
| goods       | bienes     |           |        |            |
| grid        | tabla      |           |        |            |
| history     | historial  |           |        |            |
| HR          | RRHH       |           |        |            |
| in progress | en proceso |           |        |            |
| item        | elemento   |           |        |            |
| location    | ubicación  |           |        |            |
| lot         | lote       |           |        |            |
| meeting     | reunión    |           |        |            |
| Ok          | Aceptar    |           |        |            |
| opened      | abierto    |           |        |            |
| order       | orden / pedido |           |        |            |
| packing list| albarán    |           |        |            |
| packing name| Nº albarán / Ref albarán |           |        |            |
| party       | tercero     |           | entidad | tercero    |
| procurement | abastecimiento |           |        |            |
| purchase    | compra     |           |        |            |
| purchase order | pedido de compra |           |        |            |
| quotation   | presupuesto|           | cotización |            |
| report      | informe    |           | reporte |            |
| request     | solicitud  | solicitud |        |            |
| role        | rol        |           |        |            |
| salesman    | comercial  |           | vendedor |            |
| sale        | venta      |           |        |            |
| sale order  | pedido de venta |           |        |            |
| scheduling  | planificación |           |        |            |
| sequence    | secuencia  |           |        |            |
| setup       | configuración |           |        |            |
| shorcut     | acceso rápido / abreviación |           |        |            |
| state of mind | grado de satisfacción |           |        |            |
| stock       | stock      |           | inventario |            |
| structure   | estructura / despiece |           |        |            |
| timesheet   | hoja de servicios / hoja de asistencia |           |        |            |
| tracking    | seguimiento|           |        |            |
| tree        | árbol      |           |        |            |
| UOM         | UdM        |           |        | Unit of Measure=Unidad de Medida, hay que mantenerlo abreviado |
| UOS         | UdV        |           |        | Unit of Sell=Unidad de Venta, hay que mantenerlo abreviado |
| wage        | salario    |           |        |            |
| wizard      | asistente  |           |        |            |
| workflow    | flujo      |           |        |            |
| zip         | C.P.       |           |        | Código Postal abreviado |

## Acciones (verbos en infinitivo) ##

| Inglés   | España            | Colombia | México | Comentario |
|:---------|:------------------|:---------|:-------|:-----------|
| asigne   | asignar           |          |        |            |
| cancel   | cancelar          |          |        |            |
| close    | cerrar            |          |        |            |
| compute  | calcular          |          |        |            |
| confirm  | confirmar         |          |        |            |
| create   | crear             |          |        |            |
| open     | abrir             |          |        |            |
| pack     | empaquetar        |          | empacar |            |
| pay      | pagar             |          |        |            |
| print    | imprimir          |          |        |            |
| run      | ejecutar          |          |        |            |
| select   | seleccionar       |          |        |            |
| send     | enviar            |          |        |            |
| sign in  | registrar entrada |          |        |            |
| sign out | registrar salida  |          |        |            |