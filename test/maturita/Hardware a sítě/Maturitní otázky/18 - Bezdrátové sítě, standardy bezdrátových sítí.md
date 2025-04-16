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
















