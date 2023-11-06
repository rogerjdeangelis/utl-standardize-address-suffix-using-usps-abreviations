# utl-standardize-address-suffix-using-usps-abreviations
Standardize address suffix using usps abreviations
    %let pgm=utl-standardize-address-suffix-using-usps-abreviations;

    Standardize address suffix using usps abreviations

    guthub
    https://tinyurl.com/3kwtf4f7
    https://github.com/rogerjdeangelis/utl-standardize-address-suffix-using-usps-abreviations

    USPS
    https://tinyurl.com/3yxh72af
    https://bcdcspatial.blogspot.com/2012/09/normalize-to-usps-street-abbreviations.html

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* REPLACE STREET SUFFIXES WITH USPS ABREVIATIONS                                                                         */
    /*                                                                                                                        */
    /* Obs   INPUT                              OUTPUT                       RULE                                             */
    /*                                                                                                                        */
    /*   1   3616 HAYGOOD BOULEVARD             3616 HAYGOOD BLVD            Normal case                                      */
    /*   2   3616 HAYGOOD BOULEVARD BOULEVARD   3616 HAYGOOD BOULEVARD BLVD  Only the suffix is changed (2 BOULEVARD strings) */
    /*   3   554 MANCHEST ROAD DRIVE            554 MANCHEST ROAD DR         Only the suffix is changed                       */
    /*   4   5 LANE                             5 LANE                       Must have a street name no change                */
    /*   5   5 ROAD                             5 ROAD                       Must have a street name no change                */
    /*   6   554 MANCHEST ROAD                  554 MANCHEST RD                                                               */
    /*   7   567 MANCHESTER DRIVE               567 MANCHESTER DR                                                             */
    /*   8   13 NEAL AVENUE                     13 NEAL AVE                                                                   */
    /*   9   918 SMITH MEADOW ROAD              918 SMITH MEADOW RD          Note only the suffix is changed                  */
    /*  10   916 SMITH RD                       916 SMITH RD                                                                  */
    /*  11   1345 CASTLE ROCK TURNPIKE          1345 CASTLE ROCK TPKE                                                         */
    /*  12   0 HAYGOOD UNDERPASS                0 HAYGOOD UPAS                                                                */
    /*  13   5 LANE                             5 LANE                                                                        */
    /*  14   6 ROAD                             6 ROAD                                                                        */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  MAPPING DATASET                                                                                                       */
    /*                                                                                                                        */
    /*  SD1.MAP total obs=362                                                                                                 */
    /*                                                                                                                        */
    /*  Obs    FRO          TOO                                                                                               */
    /*                                                                                                                        */
    /*    1    BOULEVARD    BLVD                                                                                              */
    /*    2    EXTNSN       EXT                                                                                               */
    /*    3    HOLLOWS      HOLW                                                                                              */
    /*    4    VSTA         VIS                                                                                               */
    /*    5    PLAINS       PLNS                                                                                              */
    /*    6    TRPK         TPKE                                                                                              */
    /*    7    FORGES       FRGS                                                                                              */
    /*    8    BYPAS        BYP                                                                                               */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */
    libname sd1 "d:/sd1";

    data sd1.map;
     informat map $24.;
     infile cards4 dsd delimiter=',';
     input map @@;
     if not missing(map);
     fro=scan(map,1,':');
     too=scan(map,2,':');
     drop map;
     if fro=too then delete;
    cards4;
    BOULEVARD:BLVD,EXTNSN:EXT,MDWS:MDWS,HOLLOWS:HOLW,VSTA:VIS,PLAINS:PLNS,
    TRPK:TPKE,FORGES:FRGS,BYPAS:BYP,MNR:MNR,VIADUCT:VIA,MNT:MT,
    LNDNG:LNDG,VILL:VLG,ALY:ALY,MILL:ML,PTS:PTS,CENTERS:CTRS,ROW:ROW,CNTER:CTR,
    HRBOR:HBR,TR:TRL,LNDG:LNDG,PASSAGE:PSGE,WALKS:WALK,FRKS:FRKS,CREST:CRST,MEADOWS:MDWS,
    FREEWY:FWY,GARDEN:GDN,BLUFFS:BLFS,VLG:VLG,VLY:VLY,FALL:FALL,TRK:TRAK,SQUARES:SQS,
    TRL:TRL,HARBOR:HBR,FRRY:FRY,DIV:DV,STRAVEN:STRA,CMP:CP,GRDNS:GDNS,VILLG:VLG,
    MEADOW:MDW,TRAILS:TRL,STREETS:STS,PRAIRIE:PR,HTS:HTS,CRESCENT:CRES,PASS:PASS,
    TER:TER,PORT:PRT,BLUF:BLF,AVNUE:AVE,LIGHTS:LGTS,RPDS:RPDS,HARBORS:HBRS,
    MEWS:MEWS,LODG:LDG,PLZ:PLZ,TRACKS:TRAK,PATH:PATH,PKWAY:PKWY,GLN:GLN,
    BOT:BTM,DRV:DR,RDG:RDG,FWY:FWY,HBR:HBR,VIA:VIA,DIVIDE:DV,INLT:INLT,
    FORDS:FRDS,AVENU:AVE,VIS:VIS,BRK:BRK,RIVR:RIV,OVAL:OVAL,GATEWAY:GTWY,
    STREAM:STRM,BAYOO:BYU,MSN:MSN,KNOLL:KNL,EXPRESSWAY:EXPY,SPRNG:SPG,
    FLAT:FLT,HOLW:HOLW,GRDEN:GDN,TRAIL:TRL,JCTNS:JCTS,RDGS:RDGS,
    TUNNEL:TUNL,ML:ML,FLS:FLS,FLT:FLT,LKS:LKS,MT:MT,GROVES:GRVS,
    VALLY:VLY,FERRY:FRY,PARKWAY:PKWY,RADIEL:RADL,STRVNUE:STRA,FLD:FLD,
    OVERPASS:OPAS,PLAZA:PLZ,ESTATE:EST,MNTN:MTN,LOCK:LCK,ORCHRD:ORCH,
    STRVN:STRA,LOCKS:LCKS,BEND:BND,KYS:KYS,JUNCTIONS:JCTS,MOUNTIN:MTN,
    BURGS:BGS,PINE:PNE,LDGE:LDG,CAUSWAY:CSWY,SPG:SPG,BEACH:BCH,FT:FT,
    CRSE:CRSE,MOTORWAY:MTWY,BLUFF:BLF,COURT:CT,GROV:GRV,SPRNGS:SPGS,
    OVL:OVAL,VILLAG:VLG,VDCT:VIA,NECK:NCK,ORCHARD:ORCH,LIGHT:LGT,
    SQ:SQ,PKWY:PKWY,SHORE:SHR,GREEN:GRN,STRM:STRM,ISLND:IS,
    TURNPIKE:TPKE,STRA:STRA,MISSION:MSN,SPNGS:SPGS,COURSE:CRSE,
    TRAFFICWAY:TRFY,TERRACE:TER,HWAY:HWY,AVENUE:AVE,GLEN:GLN,
    BOUL:BLVD,INLET:INLT,LA:LN,LN:LN,FRST:FRST,CLF:CLF,
    CRES:CRES,BROOK:BRK,LK:LK,BYP:BYP,SHOAR:SHR,BYPASS:BYP,
    MTIN:MTN,ALLY:ALY,FOREST:FRST,JUNCTION:JCT,VIEWS:VWS,WELLS:WLS,CEN:CTR,
    EXTS:EXTS,CRT:CT,CORNERS:CORS,TRAK:TRAK,FRWAY:FWY,PRARIE:PR,CROSSING:XING,
    EXTN:EXT,CLIFFS:CLFS,MANORS:MNRS,PORTS:PRTS,GATEWY:GTWY,SQUARE:SQ,HLS:HLS,
    HARB:HBR,LOOPS:LOOP,MDW:MDW,SMT:SMT,RD:RD,HILL:HL,BLF:BLF,
    HIGHWAY:HWY,WALK:WALK,CLFS:CLFS,BROOKS:BRKS,BRNCH:BR,AVEN:AVE,
    SHORES:SHRS,ISS:ISS,ROUTE:RTE,WLS:WLS,PLACE:PL,SUMIT:SMT,PINES:PNES,
    TRKS:TRAK,SHOAL:SHL,STRT:ST,FRWY:FWY,HEIGHTS:HTS,RANCHES:RNCH,
    STATION:STA,CIRCL:CIR,MNTNS:MTNS,PRTS:PRTS,SHLS:SHLS,VILLAGES:VLGS,
    PARK:PARK,NCK:NCK,RST:RST,HAVEN:HVN,TURNPK:TPKE,EXPY:EXPY,STA:STA,
    EXPR:EXPY,STN:STA,EXPW:EXPY,STREET:ST,STR:ST,SPURS:SPUR,CRECENT:CRES,
    RAD:RADL,RANCH:RNCH,WELL:WL,SHOALS:SHLS,ALLEY:ALY,PLZA:PLZ,MEDOWS:MDWS,
    ALLEE:ALY,KNLS:KNLS,ESTS:ESTS,ST:ST,ANX:ANX,HAVN:HVN,PATHS:PATH,BYPA:BYP,
    SPGS:SPGS,MILLS:MLS,PARKS:PARK,BYPS:BYP,FLTS:FLTS,TUNNELS:TUNL,CLUB:CLB,SQRS:SQS,
    HLLW:HOLW,MANOR:MNR,CENTRE:CTR,TRACK:TRAK,HGTS:HTS,RNCH:RNCH,CRCLE:CIR,FALLS:FLS,
    LANDING:LNDG,PLAINES:PLNS,VIADCT:VIA,GDNS:GDNS,GTWY:GTWY,GROVE:GRV,CAMP:CP,TPK:TPKE,
    DRIVE:DR,FREEWAY:FWY,EXT:EXT,POINTS:PTS,EXP:EXPY,KY:KY,COURTS:CTS,PKY:PKWY,CORNER:COR,
    CRSSING:XING,MNRS:MNRS,UNIONS:UNS,CYN:CYN,LODGE:LDG,TRFY:TRFY,CIRCLE:CIR,BRIDGE:BRG,
    DL:DL,DM:DM,EXPRESS:EXPY,TUNLS:TUNL,DV:DV,DR:DR,SHR:SHR,KNOLLS:KNLS,GREENS:GRNS,
    TUNEL:TUNL,FIELDS:FLDS,COMMON:CMN,ORCH:ORCH,CRK:CRK,RIVER:RIV,SHL:SHL,VIEW:VW,
    CRSENT:CRES,RNCHS:RNCH,CRSCNT:CRES,ARC:ARC,BTM:BTM,BLVD:BLVD,WAYS:WAYS,RADL:RADL,
    RDGE:RDG,CAUSEWAY:CSWY,PARKWY:PKWY,JUNCTON:JCT,STATN:STA,GARDN:GDN,MNTAIN:MTN,
    CRSSNG:XING,RAPID:RPD,KEY:KY,PLNS:PLNS,WY:WAY,COR:COR,RAMP:RAMP,THROUGHWAY:TRWY,
    ESTATES:ESTS,CK:CRK,LOAF:LF,HVN:HVN,WALL:WALL,HOLLOW:HOLW,CANYON:CYN,CLB:CLB,
    CSWY:CSWY,VILLAGE:VLG,CR:CRK,TRCE:TRCE,CP:CP,CV:CV,CT:CTS,PR:PR,FRG:FRG,
    JCTION:JCT,PT:PT,MSSN:MSN,FRK:FRK,BRDGE:BRG,CENT:CTR,SPUR:SPUR,FRT:FT,PK:PARK,
    FRY:FRY,PL:PL,LANES:LN,GTWAY:GTWY,PRK:PARK,VWS:VWS,STRAVENUE:STRA,LGT:LGT,
    HIWAY:HWY,CTR:CTR,PRT:PRT,VILLE:VL,PLAIN:PLN,MOUNT:MT,MLS:MLS,LOOP:LOOP,
    RIV:RIV,CENTR:CTR,IS:IS,PRR:PR,VL:VL,AVN:AVE,VW:VW,AVE:AVE,SPNG:SPG,
    HIWY:HWY,DAM:DM,ISLE:ISLE,CRCL:CIR,SQRE:SQ,JCT:JCT,JCTN:JCT,MOUNTAIN:MTN,
    KEYS:KYS,PARKWAYS:PKWY,DRIVES:DRS,TUNL:TUNL,JCTS:JCTS,KNL:KNL,CENTER:CTR,
    DRIV:DR,TPKE:TPKE,SUMITT:SMT,CANYN:CYN,LDG:LDG,HARBR:HBR,REST:RST,SHOARS:SHRS,
    VIST:VIS,GDN:GDN,ISLNDS:ISS,HILLS:HLS,CRESENT:CRES,POINT:PT,LAKE:LK,VLLY:VLY,
    STRAV:STRA,CROSSROAD:XRD,BND:BND,STRAVE:STRA,STRAVN:STRA,KNOL:KNL,VLGS:VLGS,
    FORGE:FRG,CNTR:CTR,CAPE:CPE,HEIGHT:HTS,LCK:LCK,HIGHWY:HWY,TRNPK:TPKE,RPD:RPD,
    BOULV:BLVD,CIRCLES:CIRS,VALLEYS:VLYS,VST:VIS,CREEK:CRK,MALL:MALL,SPRING:SPG,
    BRG:BRG,HOLWS:HOLW,LF:LF,EST:EST,XING:XING,TRACE:TRCE,BOTTOM:BTM,
    STREME:STRM,ISLES:ISLE,CIRC:CIR,FORKS:FRKS,BURG:BG,RUN:RUN,TRLS:TRL,
    RADIAL:RADL,LAKES:LKS,RUE:RUE,VLYS:VLYS,BR:BR,CORS:CORS,PLN:PLN,
    PIKE:PIKE,EXTENSION:EXT,ISLAND:IS,FRD:FRD,LCKS:LCKS,TERR:TER,
    UNION:UN,EXTENSIONS:EXTS,PKWYS:PKWY,ISLANDS:ISS,ROAD:RD,SHRS:SHRS,
    ROADS:RDS,GLENS:GLNS,SPRINGS:SPGS,MISSN:MSN,RIDGE:RDG,ARCADE:ARC,
    BAYOU:BYU,CRSNT:CRES,JUNCTN:JCT,WAY:WAY,VALLEY:VLY,FORK:FRK,
    MOUNTAINS:MTNS,BOTTM:BTM,FORG:FRG,HT:HTS,FORD:FRD,HL:HL,
    GRDN:GDN,FORT:FT,TRACES:TRCE,CNYN:CYN,CIR:CIR,UN:UN,MTN:MTN,
    FLATS:FLTS,ANEX:ANX,GATWAY:GTWY,RAPIDS:RPDS,VILLIAGE:VLG,FLDS:FLDS,
    COVES:CVS,RVR:RIV,AV:AVE,PIKES:PIKE,GRV:GRV,VISTA:VIS,PNES:PNES,
    FORESTS:FRST,FIELD:FLD,BRANCH:BR,GRN:GRN,DALE:DL,RDS:RDS,ANNEX:ANX,
    SQR:SQ,COVE:CV,SQU:SQ,SKYWAY:SKWY,RIDGES:RDGS,HWY:HWY,TUNNL:TUNL,
    UNDERPASS:UPAS,CLIFF:CLF,LANE:LN,LAND:LAND,BCH:BCH,DVD:DV,CURVE:CURV,
    CPE:CPE,SUMMIT:SMT,GARDENS:GDNS
    ;;;;
    run;quit;


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  SD1.MAP total obs=362                                                                                                 */
    /*                                                                                                                        */
    /*  Obs    FRO         TOO                                                                                                */
    /*                                                                                                                        */
    /*    1    TRPK        TPKE                                                                                               */
    /*    2    FORGES      FRGS                                                                                               */
    /*    3    BYPAS       BYP                                                                                                */
    /*    4    VIADUCT     VIA                                                                                                */
    /*    5    MNT         MT                                                                                                 */
    /*    6    LNDNG       LNDG                                                                                               */
    /*    7    VILL        VLG                                                                                                */
    /*    8    MILL        ML                                                                                                 */
    /*    9    CENTERS     CTRS                                                                                               */
    /*   10    CNTER       CTR                                                                                                */
    /*   ...                                                                                                                  */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    data sd1.have;
     input;
     adr=_infile_;
    cards4;
    3616 HAYGOOD BOULEVARD
    3616 HAYGOOD BOULEVARD BOULEVARD
    554 MANCHEST ROAD DRIVE
    5 LANE
    5 ROAD
    554 MANCHEST ROAD
    567 MANCHESTER DRIVE
    13 NEAL AVENUE
    918 SMITH MEADOW ROAD
    916 SMITH RD
    1345 CASTLE ROCK TURNPIKE
    0 HAYGOOD UNDERPASS
    5 LANE
    6 ROAD
    ;;;;
    run;quit;


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  Obs   INPUT                                                                                                           */
    /*                                                                                                                        */
    /*    1   3616 HAYGOOD BOULEVARD                                                                                          */
    /*    2   3616 HAYGOOD BOULEVARD BOULEVARD                                                                                */
    /*    3   554 MANCHEST ROAD DRIVE                                                                                         */
    /*    4   5 LANE                                                                                                          */
    /*    5   5 ROAD                                                                                                          */
    /*    6   554 MANCHEST ROAD                                                                                               */
    /*    7   567 MANCHESTER DRIVE                                                                                            */
    /*    8   13 NEAL AVENUE                                                                                                  */
    /*    9   918 SMITH MEADOW ROAD                                                                                           */
    /*   10   916 SMITH RD                                                                                                    */
    /*   11   1345 CASTLE ROCK TURNPIKE                                                                                       */
    /*   12   0 HAYGOOD UNDERPASS                                                                                             */
    /*   13   5 LANE                                                                                                          */
    /*   14   6 ROAD                                                                                                          */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    proc datasets lib=sd1 nolist nodetails;delete want; run;quit;

    %utl_submit_wps64x("

    libname sd1 'd:/sd1';

    data sd1.want;
      set sd1.have;
      if countw(adr) > 2 then do;
         len=length(strip(scan(adr,-1,' ')));
         sfx=strip(scan(adr,-1,' '));
         put sfx;
         select;
            when (strip(sfx)='BOULEVARD') substr(adr,length(adr)-len) =' BLVD';
            when (strip(sfx)='TRPK') substr(adr,length(adr)-len) =' TPKE';
            when (strip(sfx)='FORGES') substr(adr,length(adr)-len) =' FRGS';
            when (strip(sfx)='BYPAS') substr(adr,length(adr)-len) =' BYP';
            when (strip(sfx)='VIADUCT') substr(adr,length(adr)-len) =' VIA';
            when (strip(sfx)='MNT') substr(adr,length(adr)-len) =' MT';
            when (strip(sfx)='LNDNG') substr(adr,length(adr)-len) =' LNDG';
            when (strip(sfx)='VILL') substr(adr,length(adr)-len) =' VLG';
            when (strip(sfx)='MILL') substr(adr,length(adr)-len) =' ML';
            when (strip(sfx)='CENTERS') substr(adr,length(adr)-len) =' CTRS';
            when (strip(sfx)='CNTER') substr(adr,length(adr)-len) =' CTR';
            when (strip(sfx)='HRBOR') substr(adr,length(adr)-len) =' HBR';
            when (strip(sfx)='TR') substr(adr,length(adr)-len) =' TRL';
            when (strip(sfx)='PASSAGE') substr(adr,length(adr)-len) =' PSGE';
            when (strip(sfx)='WALKS') substr(adr,length(adr)-len) =' WALK';
            when (strip(sfx)='CREST') substr(adr,length(adr)-len) =' CRST';
            when (strip(sfx)='MEADOWS') substr(adr,length(adr)-len) =' MDWS';
            when (strip(sfx)='FREEWY') substr(adr,length(adr)-len) =' FWY';
            when (strip(sfx)='GARDEN') substr(adr,length(adr)-len) =' GDN';
            when (strip(sfx)='BLUFFS') substr(adr,length(adr)-len) =' BLFS';
            when (strip(sfx)='TRK') substr(adr,length(adr)-len) =' TRAK';
            when (strip(sfx)='SQUARES') substr(adr,length(adr)-len) =' SQS';
            when (strip(sfx)='HARBOR') substr(adr,length(adr)-len) =' HBR';
            when (strip(sfx)='FRRY') substr(adr,length(adr)-len) =' FRY';
            when (strip(sfx)='DIV') substr(adr,length(adr)-len) =' DV';
            when (strip(sfx)='STRAVEN') substr(adr,length(adr)-len) =' STRA';
            when (strip(sfx)='CMP') substr(adr,length(adr)-len) =' CP';
            when (strip(sfx)='GRDNS') substr(adr,length(adr)-len) =' GDNS';
            when (strip(sfx)='VILLG') substr(adr,length(adr)-len) =' VLG';
            when (strip(sfx)='MEADOW') substr(adr,length(adr)-len) =' MDW';
            when (strip(sfx)='TRAILS') substr(adr,length(adr)-len) =' TRL';
            when (strip(sfx)='STREETS') substr(adr,length(adr)-len) =' STS';
            when (strip(sfx)='PRAIRIE') substr(adr,length(adr)-len) =' PR';
            when (strip(sfx)='CRESCENT') substr(adr,length(adr)-len) =' CRES';
            when (strip(sfx)='PORT') substr(adr,length(adr)-len) =' PRT';
            when (strip(sfx)='BLUF') substr(adr,length(adr)-len) =' BLF';
            when (strip(sfx)='AVNUE') substr(adr,length(adr)-len) =' AVE';
            when (strip(sfx)='LIGHTS') substr(adr,length(adr)-len) =' LGTS';
            when (strip(sfx)='HARBORS') substr(adr,length(adr)-len) =' HBRS';
            when (strip(sfx)='LODG') substr(adr,length(adr)-len) =' LDG';
            when (strip(sfx)='TRACKS') substr(adr,length(adr)-len) =' TRAK';
            when (strip(sfx)='PKWAY') substr(adr,length(adr)-len) =' PKWY';
            when (strip(sfx)='BOT') substr(adr,length(adr)-len) =' BTM';
            when (strip(sfx)='DRV') substr(adr,length(adr)-len) =' DR';
            when (strip(sfx)='DIVIDE') substr(adr,length(adr)-len) =' DV';
            when (strip(sfx)='FORDS') substr(adr,length(adr)-len) =' FRDS';
            when (strip(sfx)='AVENU') substr(adr,length(adr)-len) =' AVE';
            when (strip(sfx)='RIVR') substr(adr,length(adr)-len) =' RIV';
            when (strip(sfx)='GATEWAY') substr(adr,length(adr)-len) =' GTWY';
            when (strip(sfx)='STREAM') substr(adr,length(adr)-len) =' STRM';
            when (strip(sfx)='BAYOO') substr(adr,length(adr)-len) =' BYU';
            when (strip(sfx)='KNOLL') substr(adr,length(adr)-len) =' KNL';
            when (strip(sfx)='EXPRESSWAY') substr(adr,length(adr)-len) =' EXPY';
            when (strip(sfx)='SPRNG') substr(adr,length(adr)-len) =' SPG';
            when (strip(sfx)='FLAT') substr(adr,length(adr)-len) =' FLT';
            when (strip(sfx)='GRDEN') substr(adr,length(adr)-len) =' GDN';
            when (strip(sfx)='TRAIL') substr(adr,length(adr)-len) =' TRL';
            when (strip(sfx)='JCTNS') substr(adr,length(adr)-len) =' JCTS';
            when (strip(sfx)='TUNNEL') substr(adr,length(adr)-len) =' TUNL';
            when (strip(sfx)='GROVES') substr(adr,length(adr)-len) =' GRVS';
            when (strip(sfx)='VALLY') substr(adr,length(adr)-len) =' VLY';
            when (strip(sfx)='FERRY') substr(adr,length(adr)-len) =' FRY';
            when (strip(sfx)='PARKWAY') substr(adr,length(adr)-len) =' PKWY';
            when (strip(sfx)='RADIEL') substr(adr,length(adr)-len) =' RADL';
            when (strip(sfx)='STRVNUE') substr(adr,length(adr)-len) =' STRA';
            when (strip(sfx)='OVERPASS') substr(adr,length(adr)-len) =' OPAS';
            when (strip(sfx)='PLAZA') substr(adr,length(adr)-len) =' PLZ';
            when (strip(sfx)='ESTATE') substr(adr,length(adr)-len) =' EST';
            when (strip(sfx)='MNTN') substr(adr,length(adr)-len) =' MTN';
            when (strip(sfx)='LOCK') substr(adr,length(adr)-len) =' LCK';
            when (strip(sfx)='ORCHRD') substr(adr,length(adr)-len) =' ORCH';
            when (strip(sfx)='STRVN') substr(adr,length(adr)-len) =' STRA';
            when (strip(sfx)='LOCKS') substr(adr,length(adr)-len) =' LCKS';
            when (strip(sfx)='BEND') substr(adr,length(adr)-len) =' BND';
            when (strip(sfx)='JUNCTIONS') substr(adr,length(adr)-len) =' JCTS';
            when (strip(sfx)='MOUNTIN') substr(adr,length(adr)-len) =' MTN';
            when (strip(sfx)='BURGS') substr(adr,length(adr)-len) =' BGS';
            when (strip(sfx)='PINE') substr(adr,length(adr)-len) =' PNE';
            when (strip(sfx)='LDGE') substr(adr,length(adr)-len) =' LDG';
            when (strip(sfx)='CAUSWAY') substr(adr,length(adr)-len) =' CSWY';
            when (strip(sfx)='BEACH') substr(adr,length(adr)-len) =' BCH';
            when (strip(sfx)='MOTORWAY') substr(adr,length(adr)-len) =' MTWY';
            when (strip(sfx)='BLUFF') substr(adr,length(adr)-len) =' BLF';
            when (strip(sfx)='COURT') substr(adr,length(adr)-len) =' CT';
            when (strip(sfx)='GROV') substr(adr,length(adr)-len) =' GRV';
            when (strip(sfx)='SPRNGS') substr(adr,length(adr)-len) =' SPGS';
            when (strip(sfx)='OVL') substr(adr,length(adr)-len) =' OVAL';
            when (strip(sfx)='VILLAG') substr(adr,length(adr)-len) =' VLG';
            when (strip(sfx)='VDCT') substr(adr,length(adr)-len) =' VIA';
            when (strip(sfx)='NECK') substr(adr,length(adr)-len) =' NCK';
            when (strip(sfx)='ORCHARD') substr(adr,length(adr)-len) =' ORCH';
            when (strip(sfx)='LIGHT') substr(adr,length(adr)-len) =' LGT';
            when (strip(sfx)='SHORE') substr(adr,length(adr)-len) =' SHR';
            when (strip(sfx)='GREEN') substr(adr,length(adr)-len) =' GRN';
            when (strip(sfx)='ISLND') substr(adr,length(adr)-len) =' IS';
            when (strip(sfx)='TURNPIKE') substr(adr,length(adr)-len) =' TPKE';
            when (strip(sfx)='MISSION') substr(adr,length(adr)-len) =' MSN';
            when (strip(sfx)='SPNGS') substr(adr,length(adr)-len) =' SPGS';
            when (strip(sfx)='COURSE') substr(adr,length(adr)-len) =' CRSE';
            when (strip(sfx)='TRAFFICWAY') substr(adr,length(adr)-len) =' TRFY';
            when (strip(sfx)='TERRACE') substr(adr,length(adr)-len) =' TER';
            when (strip(sfx)='HWAY') substr(adr,length(adr)-len) =' HWY';
            when (strip(sfx)='AVENUE') substr(adr,length(adr)-len) =' AVE';
            when (strip(sfx)='GLEN') substr(adr,length(adr)-len) =' GLN';
            when (strip(sfx)='BOUL') substr(adr,length(adr)-len) =' BLVD';
            when (strip(sfx)='INLET') substr(adr,length(adr)-len) =' INLT';
            when (strip(sfx)='LA') substr(adr,length(adr)-len) =' LN';
            when (strip(sfx)='BROOK') substr(adr,length(adr)-len) =' BRK';
            when (strip(sfx)='SHOAR') substr(adr,length(adr)-len) =' SHR';
            when (strip(sfx)='BYPASS') substr(adr,length(adr)-len) =' BYP';
            when (strip(sfx)='MTIN') substr(adr,length(adr)-len) =' MTN';
            when (strip(sfx)='ALLY') substr(adr,length(adr)-len) =' ALY';
            when (strip(sfx)='FOREST') substr(adr,length(adr)-len) =' FRST';
            when (strip(sfx)='JUNCTION') substr(adr,length(adr)-len) =' JCT';
            when (strip(sfx)='VIEWS') substr(adr,length(adr)-len) =' VWS';
            when (strip(sfx)='WELLS') substr(adr,length(adr)-len) =' WLS';
            when (strip(sfx)='CEN') substr(adr,length(adr)-len) =' CTR';
            when (strip(sfx)='CRT') substr(adr,length(adr)-len) =' CT';
            when (strip(sfx)='CORNERS') substr(adr,length(adr)-len) =' CORS';
            when (strip(sfx)='FRWAY') substr(adr,length(adr)-len) =' FWY';
            when (strip(sfx)='PRARIE') substr(adr,length(adr)-len) =' PR';
            when (strip(sfx)='CROSSING') substr(adr,length(adr)-len) =' XING';
            when (strip(sfx)='EXTN') substr(adr,length(adr)-len) =' EXT';
            when (strip(sfx)='CLIFFS') substr(adr,length(adr)-len) =' CLFS';
            when (strip(sfx)='MANORS') substr(adr,length(adr)-len) =' MNRS';
            when (strip(sfx)='PORTS') substr(adr,length(adr)-len) =' PRTS';
            when (strip(sfx)='GATEWY') substr(adr,length(adr)-len) =' GTWY';
            when (strip(sfx)='SQUARE') substr(adr,length(adr)-len) =' SQ';
            when (strip(sfx)='HARB') substr(adr,length(adr)-len) =' HBR';
            when (strip(sfx)='LOOPS') substr(adr,length(adr)-len) =' LOOP';
            when (strip(sfx)='HILL') substr(adr,length(adr)-len) =' HL';
            when (strip(sfx)='HIGHWAY') substr(adr,length(adr)-len) =' HWY';
            when (strip(sfx)='BROOKS') substr(adr,length(adr)-len) =' BRKS';
            when (strip(sfx)='BRNCH') substr(adr,length(adr)-len) =' BR';
            when (strip(sfx)='AVEN') substr(adr,length(adr)-len) =' AVE';
            when (strip(sfx)='SHORES') substr(adr,length(adr)-len) =' SHRS';
            when (strip(sfx)='ROUTE') substr(adr,length(adr)-len) =' RTE';
            when (strip(sfx)='PLACE') substr(adr,length(adr)-len) =' PL';
            when (strip(sfx)='SUMIT') substr(adr,length(adr)-len) =' SMT';
            when (strip(sfx)='PINES') substr(adr,length(adr)-len) =' PNES';
            when (strip(sfx)='TRKS') substr(adr,length(adr)-len) =' TRAK';
            when (strip(sfx)='SHOAL') substr(adr,length(adr)-len) =' SHL';
            when (strip(sfx)='STRT') substr(adr,length(adr)-len) =' ST';
            when (strip(sfx)='FRWY') substr(adr,length(adr)-len) =' FWY';
            when (strip(sfx)='HEIGHTS') substr(adr,length(adr)-len) =' HTS';
            when (strip(sfx)='RANCHES') substr(adr,length(adr)-len) =' RNCH';
            when (strip(sfx)='BOULEVARD') substr(adr,length(adr)-len) =' BLVD';
            when (strip(sfx)='EXTNSN') substr(adr,length(adr)-len) =' EXT';
            when (strip(sfx)='HOLLOWS') substr(adr,length(adr)-len) =' HOLW';
            when (strip(sfx)='VSTA') substr(adr,length(adr)-len) =' VIS';
            when (strip(sfx)='PLAINS') substr(adr,length(adr)-len) =' PLNS';
            when (strip(sfx)='STATION') substr(adr,length(adr)-len) =' STA';
            when (strip(sfx)='CIRCL') substr(adr,length(adr)-len) =' CIR';
            when (strip(sfx)='MNTNS') substr(adr,length(adr)-len) =' MTNS';
            when (strip(sfx)='VILLAGES') substr(adr,length(adr)-len) =' VLGS';
            when (strip(sfx)='HAVEN') substr(adr,length(adr)-len) =' HVN';
            when (strip(sfx)='TURNPK') substr(adr,length(adr)-len) =' TPKE';
            when (strip(sfx)='EXPR') substr(adr,length(adr)-len) =' EXPY';
            when (strip(sfx)='STN') substr(adr,length(adr)-len) =' STA';
            when (strip(sfx)='EXPW') substr(adr,length(adr)-len) =' EXPY';
            when (strip(sfx)='STREET') substr(adr,length(adr)-len) =' ST';
            when (strip(sfx)='STR') substr(adr,length(adr)-len) =' ST';
            when (strip(sfx)='SPURS') substr(adr,length(adr)-len) =' SPUR';
            when (strip(sfx)='CRECENT') substr(adr,length(adr)-len) =' CRES';
            when (strip(sfx)='RAD') substr(adr,length(adr)-len) =' RADL';
            when (strip(sfx)='RANCH') substr(adr,length(adr)-len) =' RNCH';
            when (strip(sfx)='WELL') substr(adr,length(adr)-len) =' WL';
            when (strip(sfx)='SHOALS') substr(adr,length(adr)-len) =' SHLS';
            when (strip(sfx)='ALLEY') substr(adr,length(adr)-len) =' ALY';
            when (strip(sfx)='PLZA') substr(adr,length(adr)-len) =' PLZ';
            when (strip(sfx)='MEDOWS') substr(adr,length(adr)-len) =' MDWS';
            when (strip(sfx)='ALLEE') substr(adr,length(adr)-len) =' ALY';
            when (strip(sfx)='HAVN') substr(adr,length(adr)-len) =' HVN';
            when (strip(sfx)='PATHS') substr(adr,length(adr)-len) =' PATH';
            when (strip(sfx)='BYPA') substr(adr,length(adr)-len) =' BYP';
            when (strip(sfx)='MILLS') substr(adr,length(adr)-len) =' MLS';
            when (strip(sfx)='PARKS') substr(adr,length(adr)-len) =' PARK';
            when (strip(sfx)='BYPS') substr(adr,length(adr)-len) =' BYP';
            when (strip(sfx)='TUNNELS') substr(adr,length(adr)-len) =' TUNL';
            when (strip(sfx)='CLUB') substr(adr,length(adr)-len) =' CLB';
            when (strip(sfx)='SQRS') substr(adr,length(adr)-len) =' SQS';
            when (strip(sfx)='HLLW') substr(adr,length(adr)-len) =' HOLW';
            when (strip(sfx)='MANOR') substr(adr,length(adr)-len) =' MNR';
            when (strip(sfx)='CENTRE') substr(adr,length(adr)-len) =' CTR';
            when (strip(sfx)='TRACK') substr(adr,length(adr)-len) =' TRAK';
            when (strip(sfx)='HGTS') substr(adr,length(adr)-len) =' HTS';
            when (strip(sfx)='CRCLE') substr(adr,length(adr)-len) =' CIR';
            when (strip(sfx)='FALLS') substr(adr,length(adr)-len) =' FLS';
            when (strip(sfx)='LANDING') substr(adr,length(adr)-len) =' LNDG';
            when (strip(sfx)='PLAINES') substr(adr,length(adr)-len) =' PLNS';
            when (strip(sfx)='VIADCT') substr(adr,length(adr)-len) =' VIA';
            when (strip(sfx)='GROVE') substr(adr,length(adr)-len) =' GRV';
            when (strip(sfx)='CAMP') substr(adr,length(adr)-len) =' CP';
            when (strip(sfx)='TPK') substr(adr,length(adr)-len) =' TPKE';
            when (strip(sfx)='DRIVE') substr(adr,length(adr)-len) =' DR';
            when (strip(sfx)='FREEWAY') substr(adr,length(adr)-len) =' FWY';
            when (strip(sfx)='POINTS') substr(adr,length(adr)-len) =' PTS';
            when (strip(sfx)='EXP') substr(adr,length(adr)-len) =' EXPY';
            when (strip(sfx)='COURTS') substr(adr,length(adr)-len) =' CTS';
            when (strip(sfx)='PKY') substr(adr,length(adr)-len) =' PKWY';
            when (strip(sfx)='CORNER') substr(adr,length(adr)-len) =' COR';
            when (strip(sfx)='CRSSING') substr(adr,length(adr)-len) =' XING';
            when (strip(sfx)='UNIONS') substr(adr,length(adr)-len) =' UNS';
            when (strip(sfx)='LODGE') substr(adr,length(adr)-len) =' LDG';
            when (strip(sfx)='CIRCLE') substr(adr,length(adr)-len) =' CIR';
            when (strip(sfx)='BRIDGE') substr(adr,length(adr)-len) =' BRG';
            when (strip(sfx)='EXPRESS') substr(adr,length(adr)-len) =' EXPY';
            when (strip(sfx)='TUNLS') substr(adr,length(adr)-len) =' TUNL';
            when (strip(sfx)='KNOLLS') substr(adr,length(adr)-len) =' KNLS';
            when (strip(sfx)='GREENS') substr(adr,length(adr)-len) =' GRNS';
            when (strip(sfx)='TUNEL') substr(adr,length(adr)-len) =' TUNL';
            when (strip(sfx)='FIELDS') substr(adr,length(adr)-len) =' FLDS';
            when (strip(sfx)='COMMON') substr(adr,length(adr)-len) =' CMN';
            when (strip(sfx)='RIVER') substr(adr,length(adr)-len) =' RIV';
            when (strip(sfx)='VIEW') substr(adr,length(adr)-len) =' VW';
            when (strip(sfx)='CRSENT') substr(adr,length(adr)-len) =' CRES';
            when (strip(sfx)='RNCHS') substr(adr,length(adr)-len) =' RNCH';
            when (strip(sfx)='CRSCNT') substr(adr,length(adr)-len) =' CRES';
            when (strip(sfx)='RDGE') substr(adr,length(adr)-len) =' RDG';
            when (strip(sfx)='CAUSEWAY') substr(adr,length(adr)-len) =' CSWY';
            when (strip(sfx)='PARKWY') substr(adr,length(adr)-len) =' PKWY';
            when (strip(sfx)='JUNCTON') substr(adr,length(adr)-len) =' JCT';
            when (strip(sfx)='STATN') substr(adr,length(adr)-len) =' STA';
            when (strip(sfx)='GARDN') substr(adr,length(adr)-len) =' GDN';
            when (strip(sfx)='MNTAIN') substr(adr,length(adr)-len) =' MTN';
            when (strip(sfx)='CRSSNG') substr(adr,length(adr)-len) =' XING';
            when (strip(sfx)='RAPID') substr(adr,length(adr)-len) =' RPD';
            when (strip(sfx)='KEY') substr(adr,length(adr)-len) =' KY';
            when (strip(sfx)='WY') substr(adr,length(adr)-len) =' WAY';
            when (strip(sfx)='THROUGHWAY') substr(adr,length(adr)-len) =' TRWY';
            when (strip(sfx)='ESTATES') substr(adr,length(adr)-len) =' ESTS';
            when (strip(sfx)='CK') substr(adr,length(adr)-len) =' CRK';
            when (strip(sfx)='LOAF') substr(adr,length(adr)-len) =' LF';
            when (strip(sfx)='HOLLOW') substr(adr,length(adr)-len) =' HOLW';
            when (strip(sfx)='CANYON') substr(adr,length(adr)-len) =' CYN';
            when (strip(sfx)='VILLAGE') substr(adr,length(adr)-len) =' VLG';
            when (strip(sfx)='CR') substr(adr,length(adr)-len) =' CRK';
            when (strip(sfx)='CT') substr(adr,length(adr)-len) =' CTS';
            when (strip(sfx)='JCTION') substr(adr,length(adr)-len) =' JCT';
            when (strip(sfx)='MSSN') substr(adr,length(adr)-len) =' MSN';
            when (strip(sfx)='BRDGE') substr(adr,length(adr)-len) =' BRG';
            when (strip(sfx)='CENT') substr(adr,length(adr)-len) =' CTR';
            when (strip(sfx)='FRT') substr(adr,length(adr)-len) =' FT';
            when (strip(sfx)='PK') substr(adr,length(adr)-len) =' PARK';
            when (strip(sfx)='LANES') substr(adr,length(adr)-len) =' LN';
            when (strip(sfx)='GTWAY') substr(adr,length(adr)-len) =' GTWY';
            when (strip(sfx)='PRK') substr(adr,length(adr)-len) =' PARK';
            when (strip(sfx)='STRAVENUE') substr(adr,length(adr)-len) =' STRA';
            when (strip(sfx)='HIWAY') substr(adr,length(adr)-len) =' HWY';
            when (strip(sfx)='VILLE') substr(adr,length(adr)-len) =' VL';
            when (strip(sfx)='PLAIN') substr(adr,length(adr)-len) =' PLN';
            when (strip(sfx)='MOUNT') substr(adr,length(adr)-len) =' MT';
            when (strip(sfx)='CENTR') substr(adr,length(adr)-len) =' CTR';
            when (strip(sfx)='PRR') substr(adr,length(adr)-len) =' PR';
            when (strip(sfx)='AVN') substr(adr,length(adr)-len) =' AVE';
            when (strip(sfx)='SPNG') substr(adr,length(adr)-len) =' SPG';
            when (strip(sfx)='HIWY') substr(adr,length(adr)-len) =' HWY';
            when (strip(sfx)='DAM') substr(adr,length(adr)-len) =' DM';
            when (strip(sfx)='CRCL') substr(adr,length(adr)-len) =' CIR';
            when (strip(sfx)='SQRE') substr(adr,length(adr)-len) =' SQ';
            when (strip(sfx)='JCTN') substr(adr,length(adr)-len) =' JCT';
            when (strip(sfx)='MOUNTAIN') substr(adr,length(adr)-len) =' MTN';
            when (strip(sfx)='KEYS') substr(adr,length(adr)-len) =' KYS';
            when (strip(sfx)='PARKWAYS') substr(adr,length(adr)-len) =' PKWY';
            when (strip(sfx)='DRIVES') substr(adr,length(adr)-len) =' DRS';
            when (strip(sfx)='CENTER') substr(adr,length(adr)-len) =' CTR';
            when (strip(sfx)='DRIV') substr(adr,length(adr)-len) =' DR';
            when (strip(sfx)='SUMITT') substr(adr,length(adr)-len) =' SMT';
            when (strip(sfx)='CANYN') substr(adr,length(adr)-len) =' CYN';
            when (strip(sfx)='HARBR') substr(adr,length(adr)-len) =' HBR';
            when (strip(sfx)='REST') substr(adr,length(adr)-len) =' RST';
            when (strip(sfx)='SHOARS') substr(adr,length(adr)-len) =' SHRS';
            when (strip(sfx)='VIST') substr(adr,length(adr)-len) =' VIS';
            when (strip(sfx)='ISLNDS') substr(adr,length(adr)-len) =' ISS';
            when (strip(sfx)='HILLS') substr(adr,length(adr)-len) =' HLS';
            when (strip(sfx)='CRESENT') substr(adr,length(adr)-len) =' CRES';
            when (strip(sfx)='POINT') substr(adr,length(adr)-len) =' PT';
            when (strip(sfx)='LAKE') substr(adr,length(adr)-len) =' LK';
            when (strip(sfx)='VLLY') substr(adr,length(adr)-len) =' VLY';
            when (strip(sfx)='STRAV') substr(adr,length(adr)-len) =' STRA';
            when (strip(sfx)='CROSSROAD') substr(adr,length(adr)-len) =' XRD';
            when (strip(sfx)='STRAVE') substr(adr,length(adr)-len) =' STRA';
            when (strip(sfx)='STRAVN') substr(adr,length(adr)-len) =' STRA';
            when (strip(sfx)='KNOL') substr(adr,length(adr)-len) =' KNL';
            when (strip(sfx)='FORGE') substr(adr,length(adr)-len) =' FRG';
            when (strip(sfx)='CNTR') substr(adr,length(adr)-len) =' CTR';
            when (strip(sfx)='CAPE') substr(adr,length(adr)-len) =' CPE';
            when (strip(sfx)='HEIGHT') substr(adr,length(adr)-len) =' HTS';
            when (strip(sfx)='HIGHWY') substr(adr,length(adr)-len) =' HWY';
            when (strip(sfx)='TRNPK') substr(adr,length(adr)-len) =' TPKE';
            when (strip(sfx)='BOULV') substr(adr,length(adr)-len) =' BLVD';
            when (strip(sfx)='CIRCLES') substr(adr,length(adr)-len) =' CIRS';
            when (strip(sfx)='VALLEYS') substr(adr,length(adr)-len) =' VLYS';
            when (strip(sfx)='VST') substr(adr,length(adr)-len) =' VIS';
            when (strip(sfx)='CREEK') substr(adr,length(adr)-len) =' CRK';
            when (strip(sfx)='SPRING') substr(adr,length(adr)-len) =' SPG';
            when (strip(sfx)='HOLWS') substr(adr,length(adr)-len) =' HOLW';
            when (strip(sfx)='TRACE') substr(adr,length(adr)-len) =' TRCE';
            when (strip(sfx)='BOTTOM') substr(adr,length(adr)-len) =' BTM';
            when (strip(sfx)='STREME') substr(adr,length(adr)-len) =' STRM';
            when (strip(sfx)='ISLES') substr(adr,length(adr)-len) =' ISLE';
            when (strip(sfx)='CIRC') substr(adr,length(adr)-len) =' CIR';
            when (strip(sfx)='FORKS') substr(adr,length(adr)-len) =' FRKS';
            when (strip(sfx)='BURG') substr(adr,length(adr)-len) =' BG';
            when (strip(sfx)='TRLS') substr(adr,length(adr)-len) =' TRL';
            when (strip(sfx)='RADIAL') substr(adr,length(adr)-len) =' RADL';
            when (strip(sfx)='LAKES') substr(adr,length(adr)-len) =' LKS';
            when (strip(sfx)='EXTENSION') substr(adr,length(adr)-len) =' EXT';
            when (strip(sfx)='ISLAND') substr(adr,length(adr)-len) =' IS';
            when (strip(sfx)='TERR') substr(adr,length(adr)-len) =' TER';
            when (strip(sfx)='UNION') substr(adr,length(adr)-len) =' UN';
            when (strip(sfx)='EXTENSIONS') substr(adr,length(adr)-len) =' EXTS';
            when (strip(sfx)='PKWYS') substr(adr,length(adr)-len) =' PKWY';
            when (strip(sfx)='ISLANDS') substr(adr,length(adr)-len) =' ISS';
            when (strip(sfx)='ROAD') substr(adr,length(adr)-len) =' RD';
            when (strip(sfx)='ROADS') substr(adr,length(adr)-len) =' RDS';
            when (strip(sfx)='GLENS') substr(adr,length(adr)-len) =' GLNS';
            when (strip(sfx)='SPRINGS') substr(adr,length(adr)-len) =' SPGS';
            when (strip(sfx)='MISSN') substr(adr,length(adr)-len) =' MSN';
            when (strip(sfx)='RIDGE') substr(adr,length(adr)-len) =' RDG';
            when (strip(sfx)='ARCADE') substr(adr,length(adr)-len) =' ARC';
            when (strip(sfx)='BAYOU') substr(adr,length(adr)-len) =' BYU';
            when (strip(sfx)='CRSNT') substr(adr,length(adr)-len) =' CRES';
            when (strip(sfx)='JUNCTN') substr(adr,length(adr)-len) =' JCT';
            when (strip(sfx)='VALLEY') substr(adr,length(adr)-len) =' VLY';
            when (strip(sfx)='FORK') substr(adr,length(adr)-len) =' FRK';
            when (strip(sfx)='MOUNTAINS') substr(adr,length(adr)-len) =' MTNS';
            when (strip(sfx)='BOTTM') substr(adr,length(adr)-len) =' BTM';
            when (strip(sfx)='FORG') substr(adr,length(adr)-len) =' FRG';
            when (strip(sfx)='HT') substr(adr,length(adr)-len) =' HTS';
            when (strip(sfx)='FORD') substr(adr,length(adr)-len) =' FRD';
            when (strip(sfx)='GRDN') substr(adr,length(adr)-len) =' GDN';
            when (strip(sfx)='FORT') substr(adr,length(adr)-len) =' FT';
            when (strip(sfx)='TRACES') substr(adr,length(adr)-len) =' TRCE';
            when (strip(sfx)='CNYN') substr(adr,length(adr)-len) =' CYN';
            when (strip(sfx)='FLATS') substr(adr,length(adr)-len) =' FLTS';
            when (strip(sfx)='ANEX') substr(adr,length(adr)-len) =' ANX';
            when (strip(sfx)='GATWAY') substr(adr,length(adr)-len) =' GTWY';
            when (strip(sfx)='RAPIDS') substr(adr,length(adr)-len) =' RPDS';
            when (strip(sfx)='VILLIAGE') substr(adr,length(adr)-len) =' VLG';
            when (strip(sfx)='COVES') substr(adr,length(adr)-len) =' CVS';
            when (strip(sfx)='RVR') substr(adr,length(adr)-len) =' RIV';
            when (strip(sfx)='AV') substr(adr,length(adr)-len) =' AVE';
            when (strip(sfx)='PIKES') substr(adr,length(adr)-len) =' PIKE';
            when (strip(sfx)='VISTA') substr(adr,length(adr)-len) =' VIS';
            when (strip(sfx)='FORESTS') substr(adr,length(adr)-len) =' FRST';
            when (strip(sfx)='FIELD') substr(adr,length(adr)-len) =' FLD';
            when (strip(sfx)='BRANCH') substr(adr,length(adr)-len) =' BR';
            when (strip(sfx)='DALE') substr(adr,length(adr)-len) =' DL';
            when (strip(sfx)='ANNEX') substr(adr,length(adr)-len) =' ANX';
            when (strip(sfx)='SQR') substr(adr,length(adr)-len) =' SQ';
            when (strip(sfx)='COVE') substr(adr,length(adr)-len) =' CV';
            when (strip(sfx)='SQU') substr(adr,length(adr)-len) =' SQ';
            when (strip(sfx)='SKYWAY') substr(adr,length(adr)-len) =' SKWY';
            when (strip(sfx)='RIDGES') substr(adr,length(adr)-len) =' RDGS';
            when (strip(sfx)='TUNNL') substr(adr,length(adr)-len) =' TUNL';
            when (strip(sfx)='UNDERPASS') substr(adr,length(adr)-len) =' UPAS';
            when (strip(sfx)='CLIFF') substr(adr,length(adr)-len) =' CLF';
            when (strip(sfx)='LANE') substr(adr,length(adr)-len) =' LN';
            when (strip(sfx)='DVD') substr(adr,length(adr)-len) =' DV';
            when (strip(sfx)='CURVE') substr(adr,length(adr)-len) =' CURV';
            when (strip(sfx)='SUMMIT') substr(adr,length(adr)-len) =' SMT';
            when (strip(sfx)='GARDENS') substr(adr,length(adr)-len) =' GDNS};';
            otherwise;
         end;
      end;
    run;quit;
    ");

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  SD1.WANT total obs=10                                                                                                 */
    /*                                                                                                                        */
    /*  Obs    ADR                      SFX                                                                                   */
    /*                                                                                                                        */
    /*    1    5 FINCH LN               LANE                                                                                  */
    /*    2    554 MANCHEST RD          ROAD                                                                                  */
    /*    3    567 MANCHESTER DR        DRIVE                                                                                 */
    /*    4    13 NEAL AVE              AVENUE                                                                                */
    /*    5    3720 HAYGOOD RD          RD                                                                                    */
    /*    6    918 SMITH MDW            MEADOW                                                                                */
    /*    7    916 SMITH RD             RD                                                                                    */
    /*    8    1345 CASTLE ROCK TPKE    TURNPIKE                                                                              */
    /*    9    0 HAYGOOD UPAS           UNDERPASS                                                                             */
    /*   10    3616 HAYGOOD BLVD        BOULEVARD                                                                             */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

