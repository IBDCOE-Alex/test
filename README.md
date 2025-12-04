
flowchart TD
  A[Access: Portugal WB - RENTECION.accdb] --> B{Botón}
  B -->|NuevasDenuncias| NL[Load DenunciasLocal]
  B -->|Proceso Masivo Campañas| C[Macro RW-PROCESO]
  B -->|Proceso Masivo Denuncias| D[Macro RW-PROCESODENUNCIAS]

  subgraph Campañas
    C --> C1[Queries 1: RW_PROCESO_1.dtsx]
    C1 --> POC[RW_POCALLBACK -> PWB.RW_POCALLBACK]
    C1 --> CCPP[CCPP -> PWB.CCPP]
    C1 --> CTF[COLECTIVO_TEXT_FACT -> PWB.COLECTIVO_TEXT_FACT]
    C1 --> IDTU[INT_DES_TELF_UNO -> PWB.INT_DES_TELF_UNO]
    C1 --> IDTD[INT_DES_TELF_DOS -> PWB.INT_DES_TELF_DOS]

    C --> C2[Queries 2: RW_PROCESO_2.dtsx]
    C2 --> FILES[Carga ficheros -> PWB.FICHEROS_EXTRACCIONES]
    C2 --> BCD[BENFICIO_CARGADO_DELTA -> PWB.BENFICIO_CARGADO_DELTA]
    C2 --> UBG[UBG -> PWB.UBG]
    C2 --> UBGCTO[UBG_CTO -> PWB.UBG_CTO]

    C --> C3[Queries 3: RW_PROCESO_3.dtsx]
    C3 --> EST2[ESTADOCTOCODCLENTE2 -> PWB.ESTADOCTOCODCLENTE2]
    C3 --> BV[BENEFVIGENTE -> PWB.BENEFVIGENTE]

    C --> BCS[RW_PROCESOBCS_1.dtsx]
    BCS --> OF1[OFERTAWB -> PWB.OfertaWB]
    BCS --> OF2[OFERTAWB2 -> PWB.OfertaWB2]
    C --> CL[Actualizaciones/Validaciones en Access]
  end

  subgraph Denuncias
    D --> D1[Queries 1: RW_PROCESODENUNCIAS_1.dtsx]
    D1 --> EST[ESTADOCTOCODCLENTE -> PWB.ESTADOCTOCODCLENTE]
    D1 --> ESTT[EstContratoTotal -> PWB.EstContratoTotal]

    D --> D2[Queries 2: RW_PROCESODENUNCIAS_2.dtsx]
    D2 --> IR[INTERACCIONRETENCION -> PWB.INTERACCIONRETENCION]
    D2 --> EFV[EFV -> PWB.EFV]
    D2 --> TLF[TLFCTO -> PWB.TLFCTO]
    D2 --> POT[Potencias -> PWB.Potencias]
    D2 --> PCTO[POT_CTO -> PWB.POT_CTO]
    D2 --> MPC[MAX_POT_CUPS -> PWB.MAX_POT_CUPS_TABLA]
    D2 --> UBG2[UBG/UBG_CTO -> PWB.UBG, PWB.UBG_CTO]
    D2 --> ORA[Volcado CTOS a Oracle]

    D --> D3[Queries 3: RW_PROCESODENUNCIAS_3.dtsx]
    D3 --> FILES2[Carga ficheros -> PWB.FICHEROS_EXTRACCIONES]
    D3 --> SOC[codSociedad -> PWB.codSociedad]
    D --> CL2[Actualizaciones/Validaciones en Access]
  end

  NL --> SOLH[SOL.HistoricoDenuncias]
