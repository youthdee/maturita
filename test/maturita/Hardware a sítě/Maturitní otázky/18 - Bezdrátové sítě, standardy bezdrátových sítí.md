#### 1) Současné technologie bezdrátových sítí
##### Způsoby bezdrátového přenosu
1) **Zvukový přenos**:
	- Hustotní vlny šířící se vzdušným či vodním prostředím
2) **Optický přenos**:
	- Světelné vlny šířící se průhledným prostředím
3) **Přenos pomocí**:
	- Magnetického pole (střídavé magnetické pole na kratší vzdálenost
4) **Rádiový přenos**:
	-  Vysokofrekvenční elektromagnetické vlny ve vzdušném prostředí nebo vakuu
##### Bezdrátové sítě Bluetooth
- Standard `IEEE 802.15.1`
- Frekvence od `2,4` do `2,48 GHz`: 
	- `ISM` pásmo - Industrial, Scientific, Medical
- Určen pro `PAN` (Personal Area Network):
	- Až 7 zařízení ve společné síti, role `master`/`slave`
- Dosah až `100 m`
##### Bezdrátové sitě WLAN (Wi-Fi)
1) `Standard IEEE 802.11`
	1) `802.11b` (až 11 Mb/s)
	2) `802.11g` (až 54 Mb/s)
	3) `802.11n` (až 600 Mb/s)
	4) `802.11ac` (až 1,69 Gb/s)
2) **Frekvenční pásma** `2,45 GHz` a `5 GHz`
	- `ISM` pásma (Industrial, Scientific and Medical)
	- `U-NII` pásma (Unlicensed National Information Infrastructure)
3) Dva možné **režimy provozu**:
	- Infratrukturní režim
	- Ad-hoc režim
4) **Název** bezdrátové sítě je dán **Service Set ID** (`SSID`)
5) **Zabezpečení**:
	1) `WEP` (Wired Equivalent Privacy)
		- Zranitelné, nepoužívá se
	2) Wi-Fi Protected Access (`WPA`, `WPA2`, `WPA3`)
		- V režimu PSK se volí SSID a heslo
		- V režimu Enterpise autentizace probíhá přes RADIUS server
	3) Wi-fi Protected Setup (`WPS`)
##### NFC
- Standard `ISO/IEC 18000-3` a `ISO/IEC 14443`
- Frekvence `13,56 MHz` (HF pásmo)
- Dosah **maximálně 10 cm** (typicky 1-4 cm)
- Rychlost přenosu dat `106`, `212` nebo `424 kbit/s`
- Tři režimy provozu:
    1. `Čtecí/Zapisovací` režim (aktivní zařízení komunikuje s pasivním tagem)
    2. `Peer-to-Peer` režim (dvě aktivní zařízení komunikují spolu)
    3. `Emulace karty` (zařízení se chová jako pasivní tag)
- Využití:
    - Bezkontaktní platby
    - Přístupové systémy
    - Přenos kontaktů a adres
    - Bluetooth a Wi-Fi párování
##### Bezdrátová technologie RFID
- Radio Frequency Identification
- Frekvenční pásma:
    1. `LF` (nízká frekvence): `125-134 kHz`, dosah do `10 cm`
    2. `HF` (vysoká frekvence): `13,56 MHz`, dosah do `1 m`
    3. `UHF` (ultra vysoká frekvence): `860-960 MHz`, dosah `1-12 m`
    4. `Mikrovlnné` pásmo: `2,45 GHz` a `5,8 GHz`, dosah až `30 m`
- Typy tagů:
    - `Pasivní` (bez zdroje energie, napájené polem čtečky)
    - `Aktivní` (vlastní zdroj energie, větší dosah)
    - `Semi-pasivní` (baterie napájí čip, ale ne komunikaci)
- Využití:
    - Logistika a sledování zboží
    - Identifikace osob a zvířat
    - Elektronické cestovní doklady
    - Mýtné systémy
##### Bezdrátová technologie ZigBee
- Standard `IEEE 802.15.4`
- Frekvence:
    - `868 MHz` (Evropa, 1 kanál)
    - `915 MHz` (Amerika, 10 kanálů)
    - `2,4 GHz` (celosvětově, 16 kanálů)
- Rychlost přenosu dat:
    - `20 kbit/s` (pásmo 868 MHz)
    - `40 kbit/s` (pásmo 915 MHz)
    - `250 kbit/s` (pásmo 2,4 GHz)
- Dosah `10-100 m` podle prostředí
- Topologie sítě:
    - `Hvězda` (star)
    - `Strom` (tree)
    - `Mesh` (plně propojená síť)
- Typy uzlů:
    - `Koordinátor` (řídí celou síť, pouze jeden)
    - `Router` (směruje data v síti)
    - `Koncové zařízení` (end device, komunikuje jen s rodičem)
- Výhody: `nízká spotřeba energie`, `vysoká spolehlivost` díky mesh topologii
- Využití: automatizace domácnosti, průmyslové řízení, IoT
##### Celluar
- Komunikace probíhá pomocí radiových vln na nejbližší mobilní věž
- `3G`/`4G`/`5G` a `LTE`
##### Satelit
- K přístupu k Internetu uživatelé potřebují **satelitní disk**, **dva modemy** (`uplink`, `downlink`) a **koaxialní kabel** mezi diskem a modemem
- Router se připojí k **satelitnímu disku**, který je namířen k satelitu, který se nachází ve vesmíru
#### 2) Přístupová metoda CSMA/CA v bezdrátových sítích
##### CMSA/CA (Carrier sense multiple access with collision avoidance)
- Metoda **vícenásobného přístupu** s detekcí **nosné** a **předcházením kolize**
- Pokud se na médiu nenachází žádný datový signál a médium je tedy volné, uzel vyšle po médiu upozornění, že hodlá médium použít
- Jakmile obdrží oznámení, že může vysílat, začne posílat data
- Během vysílání neprovádí detekci kolizí, rámec se odešle bez ohledu na stav média
#### 3) Standardy bezdrátových sítí (802.11)

| Standard               | Frekvence       | Max. rychlost | Šířka kanálu | Poznámky                            |
| ---------------------- | --------------- | ------------- | ------------ | ----------------------------------- |
| **802.11**             | 2,4 GHz         | 2 Mbps        | 22 MHz       | První standard, dnes nepoužívaný    |
| **802.11a**            | 5 GHz           | 54 Mbps       | 20 MHz       | Vyšší rychlost, ale menší dosah     |
| **802.11b**            | 2,4 GHz         | 11 Mbps       | 22 MHz       | První masově rozšířená Wi-Fi        |
| **802.11g**            | 2,4 GHz         | 54 Mbps       | 20 MHz       | Zpětná kompatibilita s 802.11b      |
| **802.11n**            | 2,4 / 5 GHz     | 600 Mbps      | 20/40 MHz    | Zavedení MIMO (více antén)          |
| **802.11ac**           | 5 GHz           | 6,93 Gbps     | 20-160 MHz   | MU-MIMO, vyšší propustnost          |
| **802.11ax (Wi-Fi 6)** | 2,4 / 5 GHz     | 9,6 Gbps      | 20-160 MHz   | OFDMA, lepší efektivita             |
| **802.11be (Wi-Fi 7)** | 2,4 / 5 / 6 GHz | 46 Gbps       | 20-320 MHz   | Extrémní rychlosti, snížení latence |

##### MIMO (Multiple Input Multiple Output)
- Použití více antén pro zvýšení přenosové rychlosti
##### MU-MIMO (Multi-User Multiple Input Multiple Output)
- Umožňuje komunikaci s více zařízeními současně
##### OFDMA (Orthogonal Frequency Multiple Access)
- Efektivnější rozdělení frekvence mezi uživatele
















