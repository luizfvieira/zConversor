# zConversor
Teste

REPORT  ZCONVERT3.

DATA: v_saida TYPE tdline.

SELECTION-SCREEN BEGIN OF BLOCK b1 WITH FRAME TITLE TEXT-001.

PARAMETERS: ARI_RO TYPE c RADIOBUTTON GROUP g1,
RO_ARI TYPE c RADIOBUTTON GROUP g1.

SELECTION-SCREEN END OF BLOCK b1.
SELECTION-SCREEN BEGIN OF BLOCK b2 WITH FRAME TITLE TEXT-002.

PARAMETERS: CONVERTA TYPE char30.

SELECTION-SCREEN END OF BLOCK b2.

CASE abap_true.
WHEN ARI_RO. " Arábico para romano

  DATA: r_numer TYPE tdlcount.

  r_numer = CONVERTA.

  IF r_numer LT 1
  OR r_numer GT 9999.
    MESSAGE 'Valor deve ser entre 1 e 9999' TYPE 'S' DISPLAY LIKE 'E'.
    LEAVE LIST-PROCESSING.
  ENDIF.

  CALL FUNCTION 'CONVERT_NUMBER'
    EXPORTING
      tdlcount   = r_numer
      tdnumberin = 'ROMAN'
      tdupper    = 'Y'
      tdnumfixc  = space
      tdnumoutl  = '0'
    IMPORTING
      string     = v_saida.
  WRITE v_saida.
ENDCASE.
