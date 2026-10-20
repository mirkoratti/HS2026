## Intuizioni e spiegazioni chiave

**Demodulazione coerente (sincrona)**: moltiplico $x_{AM}(t)$ per $x_{LO}(t)=\cos(\omega_c t)$ e ottengo un termine in banda base e uno spostato a $2\omega_c$. Il passa-basso tiene solo la banda base. $A_c$ e $\mu$ compaiono solo come offset e come fattore di scala, quindi la forma di $m(t)$ resta intatta.

**Perché la demodulazione coerente funziona anche con $\mu>100\%$**: nel calcolo non si usa mai $1+\mu m(t)>0$. Il segno viene conservato.

**Rivelatore di inviluppo (diodo + $RC$)**: il diodo conduce solo se l'ingresso supera $v(t)$ sul condensatore. Altrimenti $C$ si scarica in modo esponenziale attraverso $R$. Se la scarica è più lenta dell'inviluppo, $v(t)$ resta sopra, il diodo resta bloccato e l'uscita non segue più l'inviluppo (*diagonal clipping*).

**Perché si confrontano le pendenze in $t_0$**: la scarica dura circa un periodo di portante, poi il diodo riaggancia con un nuovo $t_0$. Su un intervallo così breve le curve sono quasi rette che partono dallo stesso punto $E(t_0)$. Siccome $t_0$ scorre su tutto il periodo, la condizione deve valere per ogni $t_0$.

**Supereterodina**: il filtro FI resta fisso e si sposta il segnale. La manopola cambia $f_{LO}$, quindi ogni posizione porta una sola stazione su $f_{FI}$.

**Due scelte per $f_{LO}$**: il coseno è pari, quindi conta solo $|f_{LO}-f_c|$. Una "frequenza negativa" non è fisica: $-455\ \text{kHz}$ e $+455\ \text{kHz}$ sono lo stesso coseno.

## Formule e risultati importanti

$$x_{AM}(t)=A_c\bigl(1+\mu m(t)\bigr)\cos(\omega_c t)$$

$$x_{AM}\cdot\cos(\omega_c t)=\frac{A_c}{2}\bigl(1+\mu m(t)\bigr)+\frac{A_c}{2}\bigl(1+\mu m(t)\bigr)\cos(2\omega_c t)$$
Dopo il passa-basso resta $y(t)=\frac{A_c}{2}+\frac{A_c\mu}{2}m(t)$.

$$\cos\alpha\cos\beta=\tfrac12\cos(\alpha-\beta)+\tfrac12\cos(\alpha+\beta)$$
Il mixer produce la somma e la differenza delle due frequenze.

$$\frac{1}{RC}\ge\omega_m\cdot\frac{\mu\sin(\omega_m t_0)}{1+\mu\cos(\omega_m t_0)}\quad\forall t_0$$
È la condizione di inseguimento per $m(t)=\cos(\omega_m t)$ con $0<\mu<1$. Nel tratto in salita ($\sin<0$) è sempre soddisfatta.

$$RC\le\frac{1}{\omega_m}\cdot\frac{\sqrt{1-\mu^2}}{\mu}$$
È la stessa condizione nel caso peggiore, che si ha per $\cos\varphi^*=-\mu$. Inoltre $RC$ deve essere molto più grande di $1/\omega_c$, altrimenti c'è troppo ripple.

$$|f_{LO}-f_c|=f_{FI}\qquad f_{FI}=455\ \text{kHz}\ \text{(onde medie)}$$

## Esempi ed esercizi significativi

**Rivelatore di inviluppo, (a)**: si parte da $|v'(t_0)|\ge|E'(t_0)|$ con $v'(t_0)=-\frac{E(t_0)}{RC}$ e $E'(t_0)=-A_c\mu\omega_m\sin(\omega_m t_0)$. Si tolgono i valori assoluti nel tratto in discesa, si semplifica $A_c$ e si isola $\frac{1}{RC}$.

**Rivelatore di inviluppo, (b)**: si studia $f(\varphi)=\frac{\mu\sin\varphi}{1+\mu\cos\varphi}$, la cui derivata è $f'(\varphi)=\frac{\mu(\cos\varphi+\mu)}{(1+\mu\cos\varphi)^2}$. Il massimo è $f(\varphi^*)=\frac{\mu}{\sqrt{1-\mu^2}}$. Invertendo si ottiene la condizione su $RC$. Controllo numerico: con $\mu=0.7$ il limite è $RC\,\omega_m\approx1.02$.

**Supereterodina, onde medie** ($531$–$1602\ \text{kHz}$):
- (i) $f_{LO}$ sopra: $986\ \text{kHz}<f_{LO}<2057\ \text{kHz}$, rapporto $\approx2.1$
- (ii) $f_{LO}$ sotto: $76\ \text{kHz}<f_{LO}<1147\ \text{kHz}$, rapporto $\approx15.1$

Si sceglie (i). Con un oscillatore LC vale $\frac{C_{\max}}{C_{\min}}=\left(\frac{f_{\max}}{f_{\min}}\right)^2$, cioè $\approx4.4$ contro $\approx228$.

## Errori comuni e chiarimenti

- $\frac{1+\cos(2\omega_c t)}{2}=\frac12+\frac12\cos(2\omega_c t)$, non $\frac12+\cos(2\omega_c t)$.
- $\cos^2(\omega_c t)$ va scritto in modo chiaro, perché si confonde facilmente con $\cos(2\omega_c t)$.
- Un derivatore toglie l'offset ma restituisce $\frac{dm}{dt}$ e amplifica il rumore. Serve invece qualcosa che blocchi solo la componente a $0$ Hz.
- Dalla derivata: $\cos\varphi^*=-\mu$, non $\varphi^*=\pi$, perché $f(\pi)=0$.
- Prendendo l'inverso di entrambi i membri positivi, il verso della disuguaglianza si inverte.
- Unità: kHz, non Hz. Il valore è $531-455=76$, non $75$.

## Punti ancora incerti

- (2b): la risposta finale sul blocco che toglie l'offset (passa-alto oppure condensatore in serie) non è stata formulata esplicitamente. Non è stato chiarito nemmeno come correggere il fattore $\frac{A_c\mu}{2}$.
- Il limite inferiore di $RC$ legato a $1/\omega_c$ è stato solo accennato, senza una derivazione.

## Intuizioni e spiegazioni chiave

**Portante (Träger).** Sinusoide ad alta frequenza $A_c\cos(\omega_c t)$ che da sola non porta informazione: è il "furgone", il messaggio è il "pacco". Permette antenne ragionevoli e il multiplex di frequenza (ogni stazione la sua portante).

**AM ordinaria.** L'offset "$1+$" tiene l'inviluppo $1+\mu m(t)$ sempre positivo, così basta un rivelatore d'inviluppo (diodo + $RC$). Quell'offset diventa una riga ferma a $f_c$ che non dipende dal messaggio: con $\mu=0$ le bande spariscono, la riga a $f_c$ resta.

**Due bande laterali.** Il prodotto di due coseni dà sempre somma e differenza delle frequenze. Equivalente: il coseno del messaggio ha righe a $\pm f_m$; la modulazione le sposta attorno a $f_c$ (teorema di modulazione). La banda inferiore è lo specchio della superiore: stessa informazione, banda occupata $2f_m$. La SSB ne trasmette una sola e dimezza la banda.

**DSB-SC.** Si toglie l'offset: resta solo il prodotto. Dove $m(t)<0$ la portante è capovolta (salto di 180°), l'inviluppo visibile è $|m(t)|$. Con un rettangolo $\pm1$ l'ampiezza è costante e il messaggio sta tutto nella fase (equivale a una BPSK).

**Demodulazione coerente.** Dividere per $\cos(\omega_c t)$ non si può (zeri). Si rimoltiplica per lo stesso coseno: $\cos^2$ ha valor medio $\tfrac12$ e "raddrizza" il segno; il passa-basso toglie la copia a $2f_c$.

## Formule e risultati importanti

$$x_{AM}(t)=A_c\bigl(1+\mu\,m_n(t)\bigr)\cos(\omega_c t),\qquad x_{DSB}(t)=A_c\,m_n(t)\cos(\omega_c t)$$
Con $|m_n(t)|\le 1$; $\mu$ = Modulationsgrad.

$$\mu=\frac{V_{max}-V_{min}}{V_{max}+V_{min}}$$
Dall'inviluppo all'oscilloscopio, vale solo per $\mu\le1$. Per $\mu>1$ con lobi esterno/interno: $\mu=\dfrac{V_{out}+V_{in}}{V_{out}-V_{in}}$.

$$\eta=\frac{(\mu/C)^2}{1+(\mu/C)^2}$$
Efficienza = potenza nelle bande / potenza totale; $C$ = fattore di cresta ($\sqrt2$ seno, $1$ rettangolo). DSB-SC: $\eta=100\,\%$.

$$y_m(t)=\tfrac12 A_c\,m(t)\cos\varphi$$
Uscita del demodulatore coerente con errore di fase $\varphi$; nulla a $\varphi=90°$, invertita a $180°$.

$$T_{max}=\frac{\sqrt{1-\mu^2}}{\mu\,\omega_m}$$
Limite di $T=RC$ del rivelatore d'inviluppo per un tono; serve anche $T\gg 1/f_c$.

## Esempi ed esercizi significativi

**AM a un tono** ($\mu=0.8$, $A_c=1$, $f_c=8$ kHz, $f_m=200$ Hz): $x_{AM}=\cos\omega_c t+0.4\cos(\omega_c\pm\omega_m)t$. Coefficienti $c_n$: $0.5$ a $\pm8$ kHz, $0.2$ a $\pm7.8$ e $\pm8.2$ kHz. Banda/portante $=20\log_{10}(\mu/2)=-7.96$ dB; $\eta=0.16/0.66=24.2\,\%$.

**AM con rettangolo** (duty $\tfrac12$, $\mu=0.8$): solo armoniche dispari, $\Delta L_n=20\log_{10}\bigl(\mu\tfrac{2}{n\pi}\bigr)$ → $-5.86$, $-15.40$, $-19.84$, $-22.76$ dB per $n=1,3,5,7$; $\eta\approx39\,\%$.

**Rivelatore d'inviluppo**: $1/f_c=0.125$ ms, $T_{max}\approx0.60$ ms → finestra circa $0.3\ldots0.6$ ms.

## Errori comuni e chiarimenti

- "Portante" ha due significati: l'onda $\cos(\omega_c t)$ e la riga a $f_c$ nello spettro AM. "Soppressa" in DSB-SC si riferisce alla riga.
- In DSB-SC il rivelatore d'inviluppo dà $|m(t)|$ (seno → fondamentale a $2f_m$); con rettangolo $\pm1$ dà una costante.
- Sovramodulazione con moltiplicatore lineare: niente nuove righe; l'inviluppo diventa $|1+\mu m_n|$ e il rivelatore d'inviluppo distorce, il coerente no.
- Nel PDF $f_c$ indica sia la portante sia il taglio del passa-basso (2 kHz).

## Punti ancora incerti

- Come il blocco di sincronizzazione a 8 kHz ricavi il LO in DSB-SC, dove non c'è riga a $f_c$.