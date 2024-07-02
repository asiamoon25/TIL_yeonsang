```sql
CREATE TABLE HorseInfo (
    hrNo VARCHAR(6) PRIMARY KEY,
    hrNm VARCHAR(30),
    hrEngNm VARCHAR(30),
    birthDt CHAR(8),
    sex CHAR(2),
    color VARCHAR(10),
    age INT,
    prdCty VARCHAR(20),
    expCty VARCHAR(20),
    engOrgNm VARCHAR(30),
    breed VARCHAR(20),
    fhrNo VARCHAR(6),
    fhrNm VARCHAR(30),
    fhrCty CHAR(3),
    fhrYr CHAR(4),
    mhrNo VARCHAR(6),
    mhrNm VARCHAR(30),
    mhrCty CHAR(3),
    mhrYr CHAR(4),
    mhrFhrNo VARCHAR(6),
    mhrFhrNm VARCHAR(30),
    mhrFhrCty CHAR(3),
    mhrFhrYr CHAR(4),
    useNm VARCHAR(50),
    owNm VARCHAR(40),
    owNo VARCHAR(6),
    mgrNm VARCHAR(20),
    mgrNo VARCHAR(6),
    part CHAR(3),
    poNm VARCHAR(40),
    poNo VARCHAR(6),
    poArea VARCHAR(10),
    poGubun VARCHAR(10),
    brNm VARCHAR(40),
    brNo VARCHAR(6),
    brPoNm VARCHAR(40),
    brPoNo VARCHAR(6),
    brPoArea VARCHAR(10),
    brPoGubun VARCHAR(10),
    bldRegDt CHAR(8),
    bldOwNm VARCHAR(40),
    bldOwNo VARCHAR(6),
    bldCanDt CHAR(8),
    regDt CHAR(8),
    bhrOwNm VARCHAR(40),
    bhrOwNo VARCHAR(6),
    bhrPoNm VARCHAR(40),
    bhrPoNo VARCHAR(6),
    regDelDt CHAR(8),
    regOutDt CHAR(8),
    hrNmDt CHAR(8),
    hrNmChgDt CHAR(8),
    beforeHrNm VARCHAR(30),
    beforeHrEngNm VARCHAR(30),
    rhrRegDt1 CHAR(8),
    rhrOwNm VARCHAR(40),
    rhrOwNo VARCHAR(6),
    rhrMgrNm VARCHAR(20),
    rhrMgrNo VARCHAR(6),
    rhrPart CHAR(3),
    rhrRegDt2 CHAR(8),
    discardDt CHAR(8),
    discardUse VARCHAR(40),
    discardSellCls VARCHAR(20),
    discardRes VARCHAR(50),
    discardOwNm VARCHAR(40),
    discardOwNo VARCHAR(6),
    discardMgrNm VARCHAR(20),
    discardMgrNo VARCHAR(6),
    discardPart CHAR(3),
    discardMon DECIMAL(16, 2),
    FInDt CHAR(8),
    FMgrNm VARCHAR(20),
    FMgrNo VARCHAR(6),
    FPart CHAR(3),
    FInOwNm VARCHAR(40),
    FInOwNo VARCHAR(6),
    FInGubun VARCHAR(20),
    FInAge INT,
    FInSex CHAR(2),
    inDt CHAR(8),
    inMgrNm VARCHAR(20),
    inMgrNo VARCHAR(6),
    inPart CHAR(3),
    inOwNm VARCHAR(40),
    inOwNo VARCHAR(6),
    inRes VARCHAR(20),
    inCont VARCHAR(200),
    outDt CHAR(8),
    outMgrNm VARCHAR(20),
    outMgrNo VARCHAR(6),
    outPart CHAR(3),
    outOwNm VARCHAR(40),
    outOwNo VARCHAR(6),
    outRes VARCHAR(20),
    outCont VARCHAR(200),
    restDt CHAR(8),
    restOutDt CHAR(8),
    restAreaNm VARCHAR(50),
    restDt2 CHAR(8),
    restOutDt2 CHAR(8),
    trainIlja CHAR(8),
    FDebutDt CHAR(8),
    LChulDt CHAR(8),
    rcCnt INT,
    fstCnt INT,
    sndCnt INT,
    trdCnt INT,
    forthCnt INT,
    fifthCnt INT,
    outCnt INT,
    amt DECIMAL(16, 2),
    condAmt DECIMAL(16, 2),
    winRate DECIMAL(5, 2),
    quinRate DECIMAL(5, 2),
    avgWinDist INT,
    rankTop INT,
    rankLast INT,
    char1 VARCHAR(70),
    char2 VARCHAR(70),
    char3 VARCHAR(70),
    char4 VARCHAR(70),
    brand1 VARCHAR(50),
    brand2 VARCHAR(50),
    brand3 VARCHAR(50),
    auctionDt CHAR(8),
    auctionYear CHAR(4),
    inChasu CHAR(2),
    auctionMon DECIMAL(16, 2),
    auctionGubun VARCHAR(20),
    auctionResult VARCHAR(10),
    auctionMgr VARCHAR(20),
    auctionOwNo VARCHAR(6),
    auctionOwNm VARCHAR(40),
    auctionOwNmSebu VARCHAR(30),
    impDt CHAR(8),
    impUse VARCHAR(10),
    doipYr CHAR(4),
    doipNo CHAR(2),
    impMon DECIMAL(16, 2),
    impGubun CHAR(2),
    fgnSubsidy VARCHAR(20),
    fgnAuctAmt DECIMAL(16, 2),
    fgnRcCnt INT,
    fgnFstCnt INT,
    fgnSndCnt INT,
    fgnTrdCnt INT,
    getMon DECIMAL(16, 2),
    monCd VARCHAR(16),
    fgnAvgWinDist INT,
    chgDt CHAR(8),
    sexHis VARCHAR(40),
    sexMgrNm VARCHAR(10),
    sexMgrNo VARCHAR(6),
    sexPart CHAR(3),
    sexOwNm VARCHAR(40),
    sexOwNo VARCHAR(6),
    FOwNm VARCHAR(40),
    FOwNo VARCHAR(6),
    FKraInDt CHAR(8),
    FKraOutDt CHAR(8),
    FKraPoNo VARCHAR(6),
    FKraPoNm VARCHAR(40),
    kraInDt CHAR(10),
    kraOutDt CHAR(8),
    kraPoNo CHAR(2),
    kraPoNm CHAR(1),
    FUseNm VARCHAR(10),
    deadDt CHAR(8),
    stkFstCnt INT,
    stkFlag CHAR(1),
    breedGubun VARCHAR(10),
    rhrMon DECIMAL(16, 2),
    bhrMon DECIMAL(16, 2),
    bhrGubun VARCHAR(10),
    crossSubsidy VARCHAR(20),
    birthYr CHAR(4),
    bldRegYr CHAR(4),
    FInYr CHAR(4),
    rhrRegYr1 CHAR(4),
    discardYr CHAR(4),
    regYr CHAR(4),
    regOutYr CHAR(4),
    FDebutYr CHAR(4),
    FTrainYr CHAR(4),
    impYr CHAR(4),
    baljuDt CHAR(8),
    chefHrNo VARCHAR(6),
    chefHrNm VARCHAR(30),
    sanji VARCHAR(6),
    crossSupport CHAR(1),
    crossSupportPo CHAR(1),
    poip VARCHAR(10),
    discardResSebu VARCHAR(200),
    foalDiscardDt CHAR(8),
    foalDiscardRes VARCHAR(50),
    foalDiscardResSebu VARCHAR(200),
    foalDiscardUse VARCHAR(20),
    damPrdDusu INT,
    damInDusu INT,
    breedSerial INT,
    prdSerial INT,
    regOutOwNm VARCHAR(40),
    regOutOwNo VARCHAR(6),
    regOutPoNm VARCHAR(40),
    regOutPoNo VARCHAR(6),
    regOutPoArea VARCHAR(10),
    fgnCrossDate CHAR(8),
    FInMeet VARCHAR(20),
    FMeet CHAR(1),
    breedPoNm VARCHAR(40),
    breedPoArea VARCHAR(10),
    tameDate CHAR(8),
    tameCancelDate CHAR(8),
    rankGubun VARCHAR(20),
    tamePlace VARCHAR(20),
    tameTrainer VARCHAR(20),
    breedFarm VARCHAR(40)
);
```






- **Horses** - 말의 기본 정보
- **Owners** - 소유자 정보
- **Trainers** - 조교사 정보
- **ParentHorses** - 부모 말 정보 (부마, 모마)
- **RaceHistory** - 경주 이력
- **Breeding** - 번식 정보
- **HorseHealth** - 건강 및 기타 특성
- **Auctions** - 경매 정보



```sql
CREATE TABLE horse (

hrNo VARCHAR(6) PRIMARY KEY,

hrNm VARCHAR(30),

hrEngNm VARCHAR(30),

birthDt CHAR(8),

sex CHAR(2),

color VARCHAR(10),

age INT,

prdCty VARCHAR(20),

expCty VARCHAR(20),

breed VARCHAR(20),

useNm VARCHAR(50)

);

  

  

CREATE TABLE owner (

owNo VARCHAR(6) PRIMARY KEY,

owNm VARCHAR(40)

);

  

CREATE TABLE trainer (

mgrNo VARCHAR(6) PRIMARY KEY,

mgrNm VARCHAR(20)

);

  

  

CREATE TABLE location (

poNo VARCHAR(6) PRIMARY KEY,

poNm VARCHAR(40),

poArea VARCHAR(10),

poGubun VARCHAR(10)

);

  

  

CREATE TABLE parentHorse (

hrNo VARCHAR(6),

parentType VARCHAR(4), -- 'sire' or 'dam'

parentNo VARCHAR(6),

parentNm VARCHAR(30),

parentCty CHAR(3),

parentYr CHAR(4),

PRIMARY KEY (hrNo, parentType),

FOREIGN KEY (hrNo) REFERENCES horse(hrNo)

);

  

  

  

CREATE TABLE breeding (

hrNo VARCHAR(6),

brNo VARCHAR(6),

brNm VARCHAR(40),

brPoNo VARCHAR(6),

brPoNm VARCHAR(40),

brPoArea VARCHAR(10),

brPoGubun VARCHAR(10),

bldRegDt CHAR(8),

bldOwNo VARCHAR(6),

bldOwNm VARCHAR(40),

bldCanDt CHAR(8),

regDt CHAR(8),

bhrOwNo VARCHAR(6),

bhrOwNm VARCHAR(40),

bhrPoNo VARCHAR(6),

bhrPoNm VARCHAR(40),

regDelDt CHAR(8),

regOutDt CHAR(8),

hrNmDt CHAR(8),

hrNmChgDt CHAR(8),

beforeHrNm VARCHAR(30),

beforeHrEngNm VARCHAR(30),

FOREIGN KEY (hrNo) REFERENCES horse(hrNo)

);

  

  

  

CREATE TABLE racing (

hrNo VARCHAR(6),

rhrRegDt1 CHAR(8),

rhrOwNo VARCHAR(6),

rhrOwNm VARCHAR(40),

rhrMgrNo VARCHAR(6),

rhrMgrNm VARCHAR(20),

rhrPart CHAR(3),

rhrRegDt2 CHAR(8),

discardDt CHAR(8),

discardUse VARCHAR(40),

discardSellCls VARCHAR(20),

discardRes VARCHAR(50),

discardOwNo VARCHAR(6),

discardOwNm VARCHAR(40),

discardMgrNo VARCHAR(6),

discardMgrNm VARCHAR(20),

discardPart CHAR(3),

discardMon DECIMAL(16, 2),

FInDt CHAR(8),

FMgrNo VARCHAR(6),

FMgrNm VARCHAR(20),

FPart CHAR(3),

FInOwNo VARCHAR(6),

FInOwNm VARCHAR(40),

FInGubun VARCHAR(20),

FInAge INT,

FInSex CHAR(2),

inDt CHAR(8),

inMgrNo VARCHAR(6),

inMgrNm VARCHAR(20),

inPart CHAR(3),

inOwNo VARCHAR(6),

inOwNm VARCHAR(40),

inRes VARCHAR(20),

inCont VARCHAR(200),

outDt CHAR(8),

outMgrNo VARCHAR(6),

outMgrNm VARCHAR(20),

outPart CHAR(3),

outOwNo VARCHAR(6),

outOwNm VARCHAR(40),

outRes VARCHAR(20),

outCont VARCHAR(200),

restDt CHAR(8),

restOutDt CHAR(8),

restAreaNm VARCHAR(50),

restDt2 CHAR(8),

restOutDt2 CHAR(8),

trainIlja CHAR(8),

FDebutDt CHAR(8),

LChulDt CHAR(8),

rcCnt INT,

fstCnt INT,

sndCnt INT,

trdCnt INT,

forthCnt INT,

fifthCnt INT,

outCnt INT,

amt DECIMAL(16, 2),

condAmt DECIMAL(16, 2),

winRate DECIMAL(5, 2),

quinRate DECIMAL(5, 2),

avgWinDist INT,

rankTop INT,

rankLast INT,

char1 VARCHAR(70),

char2 VARCHAR(70),

char3 VARCHAR(70),

char4 VARCHAR(70),

brand1 VARCHAR(50),

brand2 VARCHAR(50),

brand3 VARCHAR(50),

FOREIGN KEY (hrNo) REFERENCES horse(hrNo),

FOREIGN KEY (rhrOwNo) REFERENCES owner(owNo),

FOREIGN KEY (rhrMgrNo) REFERENCES trainer(mgrNo)

);

  

  

  

CREATE TABLE auction (

hrNo VARCHAR(6),

auctionDt CHAR(8),

auctionYear CHAR(4),

inChasu CHAR(2),

auctionMon DECIMAL(16, 2),

auctionGubun VARCHAR(20),

auctionResult VARCHAR(10),

auctionMgr VARCHAR(20),

auctionOwNo VARCHAR(6),

auctionOwNm VARCHAR(40),

auctionOwNmSebu VARCHAR(30),

FOREIGN KEY (hrNo) REFERENCES horse(hrNo)

);

  

  

CREATE TABLE imports (

hrNo VARCHAR(6),

impDt CHAR(8),

impUse VARCHAR(10),

doipYr CHAR(4),

doipNo CHAR(2),

impMon DECIMAL(16, 2),

impGubun CHAR(2),

fgnSubsidy VARCHAR(20),

fgnAuctAmt DECIMAL(16, 2),

fgnRcCnt INT,

fgnFstCnt INT,

fgnSndCnt INT,

fgnTrdCnt INT,

getMon DECIMAL(16, 2),

monCd VARCHAR(16),

fgnAvgWinDist INT,

chgDt CHAR(8),

sexHis VARCHAR(40),

sexMgrNo VARCHAR(6),

sexMgrNm VARCHAR(10),

sexPart CHAR(3),

sexOwNo VARCHAR(6),

sexOwNm VARCHAR(40),

FOwNo VARCHAR(6),

FOwNm VARCHAR(40),

FKraInDt CHAR(8),

FKraOutDt CHAR(8),

FKraPoNo VARCHAR(6),

FKraPoNm VARCHAR(40),

kraInDt CHAR(10),

kraOutDt CHAR(8),

kraPoNo CHAR(2),

kraPoNm CHAR(1),

FUseNm VARCHAR(10),

deadDt CHAR(8),

stkFstCnt INT,

stkFlag CHAR(1),

breedGubun VARCHAR(10),

rhrMon DECIMAL(16, 2),

bhrMon DECIMAL(16, 2),

bhrGubun VARCHAR(10),

crossSubsidy VARCHAR(20),

birthYr CHAR(4),

bldRegYr CHAR(4),

FInYr CHAR(4),

rhrRegYr1 CHAR(4),

discardYr CHAR(4),

regYr CHAR(4),

regOutYr CHAR(4),

FDebutYr CHAR(4),

FTrainYr CHAR(4),

impYr CHAR(4),

baljuDt CHAR(8),

chefHrNo VARCHAR(6),

chefHrNm VARCHAR(30),

sanji VARCHAR(6),

crossSupport CHAR(1),

crossSupportPo CHAR(1),

poip VARCHAR(10),

discardResSebu VARCHAR(200),

foalDiscardDt CHAR(8),

foalDiscardRes VARCHAR(50),

foalDiscardResSebu VARCHAR(200),

foalDiscardUse VARCHAR(20),

damPrdDusu INT,

damInDusu INT,

breedSerial INT,

prdSerial INT,

regOutOwNm VARCHAR(40),

regOutOwNo VARCHAR(6),

regOutPoNm VARCHAR(40),

regOutPoNo VARCHAR(6),

regOutPoArea VARCHAR(10),

fgnCrossDate CHAR(8),

FInMeet VARCHAR(20),

FMeet CHAR(1),

breedPoNm VARCHAR(40),

breedPoArea VARCHAR(10),

tameDate CHAR(8),

tameCancelDate CHAR(8),

rankGubun VARCHAR(20),

tamePlace VARCHAR(20),

tameTrainer VARCHAR(20),

breedFarm VARCHAR(40),

FOREIGN KEY (hrNo) REFERENCES horse(hrNo),

FOREIGN KEY (sexMgrNo) REFERENCES trainer(mgrNo),

FOREIGN KEY (sexOwNo) REFERENCES owner(owNo),

FOREIGN KEY (FOwNo) REFERENCES owner(owNo),

FOREIGN KEY (chefHrNo) REFERENCES horse(hrNo)

);
```


