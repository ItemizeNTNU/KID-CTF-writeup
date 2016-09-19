###Database AIDS

En syk database? Huff. Ifølge OWASP er SQL injections det mest normale man kan møte på sammen med XSS ute på det store internettet. 

Den enkleste sjekken man kanskje kan gjøre på en SQL spørring er å se om de har tatt høyde for å unnlate fnutter, og passet på hva slags input de får inn.

Det står rapportert at det finnes en admin bruker, og at han har et sikkert passord, så brute force er lite nødvendig her.

så om vi prøver  admin ' or 1='1'#;` i brukernavnfeltet gjør vi en hel remse med ting:

Vi sender inn et gyldig brukernavn, noe en typisk login funksjon trenger. Den vil sannsynligvis spørre om noe som `SELECT username FROM users WHERE username='' AND password='';`

så gjør vi det slik at vi hopper ut av fnuttene, og putter oss midt inne i SQL spørringen. Så sant phpen ikke tar høyde for `'` kan vi spørre om hva vi vil! Så med det som ble skrevet over, sender vi da inn `OR 1=1'1` som alltid er sant, så spørringen vår er gyldig. Så må vi sørge for å avslutte og kommentere bort resterende SQL kode som ellers ville spurt om passordet. `;#` avslutter i vårt tilfelle spørringen. Syntaksen på kommentarer kan variere med ulike databasetyper.

Og vi får flagget,

`ctf{41w4y5_35c4p3_y0ur_57ring5}`

--Anders Been Wilhelmsen
been.anders@gmail.com

PS: Denne oppgaven var litt ekstra vanskelig siden man ikke fikk sett selve spørringen om man skrev noe feil. 
