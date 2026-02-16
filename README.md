# ATM-Banking-Operations-Simulator
Sviluppo di un simulatore funzionale di uno sportello ATM (Bancomat) in linguaggio C. Il progetto gestisce la logica delle transazioni bancarie fondamentali tramite un'interfaccia a riga di comando (CLI).

#include <stdio.h>

int main() {
    // Variabili base
    float saldo = 1000.00; // Partiamo con mille euro finti
    float importo;
    int scelta;
    int pin_inserito;
    const int PIN_CORRETTO = 1234; // Il PIN è fisso per ora
    
    // 1. Fase di Login Semplice
    printf("--- BENVENUTO IN UNICAL BANK ---\n");
    printf("Inserisci il PIN per accedere: ");
    scanf("%d", &pin_inserito);
    
    // Se il pin è sbagliato, chiude tutto (return 0)
    if (pin_inserito != PIN_CORRETTO) {
        printf("ERRORE: PIN non valido. Accesso negato.\n");
        return 0; 
    }

    printf("Accesso effettuato!\n");

    // 2. Il Menu che gira all'infinito finché non scegli "Esci"
    while(1) {
        printf("\n\n--- MENU OPERAZIONI ---\n");
        printf("1. Visualizza Saldo\n");
        printf("2. Preleva Contanti\n");
        printf("3. Versa Contanti\n");
        printf("4. Esci\n");
        printf("Scegli un'opzione (1-4): ");
        scanf("%d", &scelta);

        // Gestione delle scelte con if o switch
        if (scelta == 1) {
            // MOSTRA SALDO
            printf("\n>> Il tuo saldo attuale e': %.2f Euro\n", saldo);
        
        } else if (scelta == 2) {
            // PRELIEVO
            printf("\nQuanto vuoi prelevare? ");
            scanf("%f", &importo);
            
            // Controllo fondamentale: hai i soldi?
            if (importo > saldo) {
                printf(">> ERRORE: Fondi insufficienti! Hai solo %.2f Euro.\n", saldo);
            } else if (importo <= 0) {
                printf(">> ERRORE: Inserisci un importo valido.\n");
            } else {
                saldo = saldo - importo; // Tolgo i soldi
                printf(">> Prelievo riuscito! Nuovo saldo: %.2f Euro\n", saldo);
            }

        } else if (scelta == 3) {
            // VERSAMENTO
            printf("\nQuanto vuoi versare? ");
            scanf("%f", &importo);

            if (importo <= 0) {
                printf(">> ERRORE: Non puoi versare numeri negativi.\n");
            } else {
                saldo = saldo + importo; // Aggiungo i soldi
                printf(">> Versamento riuscito! Nuovo saldo: %.2f Euro\n", saldo);
            }

        } else if (scelta == 4) {
            // USCITA
            printf("\nGrazie per aver usato Unical Bank. Arrivederci!\n");
            break; // Questo comando rompe il ciclo while e finisce il programma
        
        } else {
            printf("\n>> Scelta non valida. Riprova.\n");
        }
    }

    return 0;
}
