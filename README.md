# Smart Device

## TP

### Réponse aux questions

#### Schéma de mesure de résistance

1. **Vérification des fonctionnalités nominales**  
   - **Transitoire**  
     (Passage de 50nA à 100nA via un PULSE)  
     On voit bien que c’est de 5 mV à 10 mV à cause de la résistance de shunt de 100 kΩ.  
     En regardant sur la tension de l’ADC, on remarque que c’est bien multiplié par 101  
     (100 kΩ + 1 kΩ).  

2. **Analyse fréquentielle**  
   - Sur le diagramme de Bode ci-dessus, on observe un gain compris entre 140 et 150 dB.  
   - La fonction de transfert correspond à :  

     ```
     Vout = H = Vout / Iin = 10^(140/20) = 10^7
     ```

   - Avec 0,5V et Iin = 50 nA, on obtient :  

     ```
     0,5 / (50 * 10^-9) = 10^7
     ```

   - Le gain du diagramme de Bode est cohérent avec les données mises en entrée et obtenues en sortie.

3. **Recherche des fréquences de coupure**  
   - **Filtrage**

     | Numéro étage | Fc Théorique | Fc Mesurée (à -3dB) |
     |--------------|--------------|---------------------|
     | 1            | 15 Hz        |                     |
     | 2            | 1.6 Hz       |                     |
     | 3            | \( \frac{1}{2\pi R_6 C_2} = \frac{1}{2\pi \cdot 1000 \cdot 100 \cdot 10^{-9}} \approx 1591 \, \text{Hz} \) | 1.55 kHz |

     - **Étage 1**  
     - **Étage 2**  
     - **Étage 3**  

4. **Atténuation**
   - À 50 Hz : 100 dB, soit -40 dB d’atténuation (divisé par 100).  
   - À \( f_n = 7.5 \, \text{kHz} \) : 30 dB, soit -110 dB d’atténuation (divisé par 300 000).  

5. **Capteur sur LTSpice**  
   - Comportement d’un filtre passe-bas, le bruit est régulé car on est à 50 Hz.  
   - Avec la FFT de \( V_{adc} \), on voit le pic à 50 Hz.  
   - Si on divise la capacité du filtre 2 par 10, le pic augmente, ce qui montre que cette capacité sert à diminuer le bruit à 50 Hz.
