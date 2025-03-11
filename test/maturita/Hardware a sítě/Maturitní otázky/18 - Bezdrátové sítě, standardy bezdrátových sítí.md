#### 1) Současné technologie bezdrátových sítí

##### Způsoby bezdrátového přenosu
- Zvukový přenos (hustotní vlny šířící se vzdušným či vodním prostředím)
- Optický přenos (světelné vlny šířící se průhledným prostředím)
- Přenos pomocí magnetického pole (střídavé magnetické pole na kratší vzdálenost)
- Rádiový přenos (vysokofrekvenční elektromagnetické vlny ve vzdušném prostředí nebo vakuu)

##### Bezdrátové sítě Bluetooth
- Standard IEEE 802.15.1 (již společností nespravovaný)
- Bluetooth trademark patří Bluetooth SIG
- Frekvence od 2,4 do 2,48 GHz (ISM pásmo - Industrial, Scientific, Medical)
- Určen pro PAN (Personal Area Network)
	- Až 7 zařízení ve společné síti, role master/slave
- Dosah až 100 m

##### Bezdrátové sitě WLAN (Wi-Fi)
- Standard IEEE 802.11
	- 802.11b (až 11 Mb/s)
	- 802.11g (až 54 Mb/s)
	- 802.11n (až 600 Mb/s)
	- 802.11ac (až 1,69 Gb/s)
- Wi-Fi trademark asociace Wi-Fi Alliance (Wi-Fi Certified pouze pro certifikovaná zařízení)
- Frekvenční pásma 2,45 GHz a 5 GHz
	- ISM pásma (Industrial, Scientific and Medical)
	- U-NII pásma (Unlicensed National Information Infrastructure)
- Dva možné režimy provozu: Infratrukturní režim a ad-hoc režim
- Název bezdrátové sítě je dán Service Set ID (SSID)
- Zabezpečení:
	- WEP (Wired Equivalent Privacy)
		- Zranitelné, nepoužívá se
	- Wi-Fi Protected Access (WPA, WPA2, WPA3)
		- V režimu PSK se volí SSID a heslo
		- V režimu Enterpise autentizace probíhá přes RADIUS server
	- Wi-fi Protected Setup (WPS)

##### Celluar
- Komunikace probíhá pomocí radiových vln na nejlbližší mobilní věž
- 3G/4G/5G a LTE

##### Satelit
- Typicky používané v oblastech kde není dostupné kabelové a DSL připojení
- K přístupu k Internetu uživatelé potřebují satelitní disk, dva modemy (uplink, downlink) a koaxialní kabel mezi diskem a modemem
- Router se připojí k satelitnímu disku, který je namířen k satelitu, který se nachází ve vesmíru
#### 2) Přístupová metoda CSMA/CA v bezdrátových sítích

##### Carrier Sence Multiple Access with Collision Avoidance (CSMA/CA)
- Uzel před zahájením vysílání nejprve alokuje kanál
- Násobný přístup ke sdílenému médiu s redukcí kolizí (Wi-Fi)
- Zlepšuje přenosové vlastnosti metody CSMA, potlačení kolizí zvyšuje dostupnost média
- Při detekci cizího vysílání čeká na náhodný čas, poté opět zjišťuje dostupnost média
- Během vysílání neprovádí detekci kolizí, rámec se odešle bez ohledu na stav média
- Pokud se na médiu nenachází žádný datový signál a médium je tedy volné, uzel vyšle po médiu upozornění, že hodlá médium využít
	- Jakmile obdrží oznámení, že může vysílat, začne posílat data
- Tato metoda se používá u WLAN technologií standardu 802.11
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
















