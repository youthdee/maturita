#### 1) Azure Active Directory, Azure Active Directory Domain Services
##### Azure Active Directory - Entra ID
- **Adresářová služba** Microsoft Entra ID, která umožňuje **přihlášení** do cloudových aplikacích přímo **Microsoftu** nebo **vlastních**.
- Pomáhá s nasazením a správou **stávající on-premise** Active Directory.
- Microsoft Entra ID lze propojit s on-premise **Active Directory** pomocí **Microsoft Entra Connect.**
##### Microsoft Entra ID je vhodná pro:
1) **Správce IT**
	- Řízení přístupu k prostředkům a aplikacím
2) **Vývojáře aplikací**
	- Zajištění SSO, přihlášení pod existujícími přihlašovacími údajema
3) **Uživatele**
	- Správa identity, provádění operace s účtem - reset hesla
4) **Zákazníky online služeb**
	- Ověření přístupu ke službám, MS 365, Azure...
##### Služby poskytované Microsoft Entra ID:
1) **Ověřování**
	- Identity pro přístup, reset hesla, vícefaktor, seznam zcizených hesel, chytré odemykání
2) **SSO**
	- Možnost přístupu k více aplikacím pod jedním loginem
3) **Správa aplikací v cloudu i on-premise**
	- Application Proxy, aplikace SaaS, portál My Apps
4) **Správa zařízení**
	- Registrace a následná správa zařízení - Microsoft Intune, definice zásad podmíněného nebo omezeného přístupu pouze pro známá zařízení
##### Microsoft Entra Domain Services
 - Služba, která poskytuje **spravované doménové služby**:
	 - Přidání do domény, zásady skupiny, LDAP 
	 - Bez nutnosti spravovat či nasazovat a aktualizovat řadiče domény
- Integrace do **existujícího tenanta Microsoft Entra**, což umožní uživatelům se přihlásit ke službám a aplikacím připojeným ke spravované doméně.
- Při **vytvoření** se **automaticky vytvoří namespace** (**jedinečný jmenný prostor**) a do vybrané oblasti se **nasadí dva řadiče domény** (**replica set**).
- Microsoft pak **zajišťuje jejich správu**, **zálohování** a **šifrování**. (Azure Disk Encryption)
-  doména **automaticky provádí jednosměrnou synchronizaci** z **Microsoft Entra ID** do **Microsoft Entra Domain Services**.
#### 2) Možnosti ověřování ve službě Azure
##### Ověřování definice
- Ověřování je proces prokázání identity osoby, služby nebo zařízení prostřednictvím ověřovacích mechanismů.
##### Single-Sign-On - SSO
- uživatel se **přihlásí pouze jednou** a **automaticky získá přístup k více prostředkům** či **aplikacím** od různých poskytovatelů.
	- Za předpokladu, že poskytovatelé tomuto ověření důvěřují.
- Snadná **zapamatovatelnost pro uživatele**, **zjednodušení modelu zabezpečení**, **méně uživatelských účtů**, **snadná správa identit**.
##### MultiFactor Authentication - MFA
- Během ověřování je **po uživateli požadováno více různých druhů ověření**. (kontrolní otázka, kód, biometrické údaje)
- V Azure tuto službu zajišťuje **Microsoft Entra Multi-Factor Authentication.**
##### Ověřování bez použití hesla
- Ověřování probíhá **pomocí metod využívajících prostředků**, které uživatel **vlastní** nebo které ho **identifikují** nebo které **uživatel** **zná**.
- Například ověření na **schváleném** **počítači** pomocí **biometrických** **údajů**.
##### Microsoft Entra ID podporuje ověřování pomocí:
- **Windows Hello for Business** (**PIN**, **Biometrie** na schváleném zařízení)
- Aplikace **Microsoft Authenticator** (vygenerování **Jednorázového**, **časově** **omezeného** přístupového kódu)
- Bezpečnostní klíče **FIDO2** (fast identity online)
	- USB, Bluetooth, NFC 
#### 3) Podmíněný přístup, přístup na základě rolí
##### Podmíněný přistup
 - Funkce pro **povolení** nebo **zamítnutí** **přístupu** na **základě identity uživatele**, **místa přihlašování** a **zařízení** použitého k přihlášení.
- **Sofistikovanější** přístup k **vícefaktorovému ověřování**, které se vyžaduje pouze při **nestandartních** **podmínkách** (neobvyklá lokace)
- Při přihlašování uživatele se **vyhodnocují různé signály** a na jejich základě se buď **povolí** nebo **zamítne** přistup, popřípadě se vynutí vícefaktorové ověření.
##### Přistup na základě rolí (Role-Based-Access-Control)
- Přístup na **základě rolí uživatele** (**předdefinované** nebo **vlastní**)
- Každá **role** má přiřazena **přistupová** **oprávnění**
- Přistup typu **RBAC** se **aplikuje na obor** (**scope**) - **prostředek** nebo **obor prostředků** (Skupina pro správu, předplatné, skupina prostředků...)
- Každému **oboru** se přiřazuje **určitá** **role** (**Reader**, **Contributor**, **Owner**)
- Přístup typu **RBAC** se vynucuje pomocí **ARM** (**Azure Resource Manager**)
	- Služba pro správu a zabezpečení cloudových prostředků.
- RBAC funguje na **principu dědičnosti** a **povolování přístupu**.
