# 🌐 Core Protocols - Hinglish Notes

## Introduction to Core Protocols

Bhai, protocols basically **"Rules of Conversation"** hain. Jaise agar do log baat kar rahe hain, toh unhe ek common language (Hindi ya English) chahiye hoti hai taaki ek doosre ki baat samajh sakein. Waise hi, jab do computers internet pe connect hote hain, toh woh "Protocols" ka use karte hain. Agar tu pentesting kar raha hai aur tujhe protocol nahi pata, toh tujhe ye hi nahi pata chalega ki computer "bol" kya raha hai aur usme "jhoot" (exploit) kaise bolna hai.

---

## 🛠️ Detailed Concept Explanation

### 1. HTTP vs HTTPS (The Web Language)

- **HTTP (Port 80):** Ye purana tarika hai. Isme data "Plain Text" mein jata hai. Matlab agar tu apna password enter karega, toh raste mein koi bhi (attacker) usey padh sakta hai.
- **HTTPS (Port 443):** Ye HTTP ka upgraded version hai jisme **TLS (Transport Layer Security)** ki chadar lapeti gayi hai. Isme data encrypt ho jata hai.
- **Pentest Angle:** HTTP pe **Sniffing** (Wireshark se data dekhna) aasaan hai. HTTPS pe humein **SSL Stripping** jaise attacks try karne padte hain taaki server ko majboor kiya ja sake HTTP use karne ke liye.

---

### 2. TLS/SSL Handshake (The Secret Handshake)

Jab tu kisi HTTPS site pe jata hai, toh pehle ek "Secret Handshake" hota hai:

1. **ClientHello:** "Bhai, mere paas ye encryption tools hain."
2. **ServerHello:** "Theek hai, main ye wala select karta hoon, aur ye raha mera ID card (Certificate)."
3. **Key Exchange:** Dono milkar ek "Secret Key" banate hain.
4. **Finished:** Ab saari baat encrypted hogi.

---

### 3. FTP, SSH, & Telnet (Remote Access)

- **FTP (Port 21):** Files bhejne ke liye. Danger ye hai ki isme "Anonymous Login" aksar chhod diya jata hai, jahan koi bhi bina password ke ghus sakta hai.
- **Telnet (Port 23):** Ekdum khatarnaak! Sab kuch plain text mein dikhta hai.
- **SSH (Port 22):** Telnet ka baap. Sab kuch encrypted hai. Pentesting mein hum ispe **Brute Force** (Hydra tool se) try karte hain agar password weak ho.

---

### 4. TCP vs UDP (The Delivery Guys)

- **TCP:** Ye ek "Zimmedar" delivery guy hai. Pehle phone karke poochta hai (3-Way Handshake), phir saman deta hai, aur receipt (ACK) bhi leta hai.
- **UDP:** Ye "Rambo" hai. Bas packet phenk deta hai, usse farak nahi padta ki tu ghar pe hai ya nahi (Fast but unreliable). Use: Gaming, Video calls.

---

## 💡 The "Restaurant Order" Analogy

Maano tum ek restaurant mein ho:

- **TCP** wo waiter hai jo pehle aake "Hello" bolega, aap "Hi" bologe, phir wo menu dikhayega (**3-Way Handshake**). Order confirm hone ke baad hi khana layega.
- **UDP** wo fast-food counter hai jahan wo bas "Order Number 45!" chillata hai aur burger counter pe rakh deta hai. Aapne suna toh theek, nahi suna toh burger gaya!
- **HTTP** wo waiter hai jo bina uniform ke hai, koi bhi dekh sakta hai aap kya order kar rahe ho.
- **HTTPS** wo waiter hai jo ek black box mein khana lata hai, sirf aapke paas uski chabi hai.

---

## 📌 Key Important Points (Must Remember)

- **Port Numbers:** HTTP (80), HTTPS (443), SSH (22), FTP (21), Telnet (23). Inhe rat lo!
- **Status Codes:** 200 (Sab sahi hai), 403 (Entry mana hai), 404 (Kuch nahi mila), 500 (Server ki phat gayi).
- **3-Way Handshake:** SYN -> SYN-ACK -> ACK. Iske bina TCP connection nahi banta.
- **Plain Text Protocols:** Telnet, FTP, HTTP aur SMTP plain text hain. Inhe sniff karna sabse easy hai.

---

## 🧪 Practical Exercise (Apply the Learning)

Aapko apne system pe ye try karna hai (Learning by doing):

1. **Banner Grabbing:** Terminal kholo aur type karo `nc -nv <Target_IP> 22`. Dekho ki kya server apna version bata raha hai? (SSH version check karne ke liye).
2. **Wireshark Analysis:** Wireshark chalao, phir kisi HTTP (not HTTPS) website pe jao aur login try karo. Filter mein `http` dalo aur dekho kya aapko apna password dikh raha hai?
3. **Nmap Stealth Scan:** Try karo `nmap -sS <Target_IP>`. Ye SYN scan hai, check karo ki kya ye full scan se zyada fast hai.