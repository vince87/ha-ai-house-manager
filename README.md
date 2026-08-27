# AI Home Manager Blueprint

Blueprint per Home Assistant che organizza la gestione della casa in ambiti indipendenti, risolve automaticamente le entità tramite friendly name e usa un agente Conversation per pianificare azioni strutturate e verificabili.

## Caratteristiche

- Risoluzione deterministica dei friendly name contro il catalogo reale di Home Assistant.
- Nessuna selezione manuale delle entità nel blueprint.
- Pianificazione separata per ambito con priorità configurabili.
- Espansione automatica dei gruppi Home Assistant.
- Validazione di entità, servizi e parametri prima dell'esecuzione.
- Eliminazione delle azioni già soddisfatte.
- Esecuzione sequenziale e verifica dello stato raggiunto.
- Modalità simulazione `dry_run`.
- Diagnostica separata per riferimenti assenti, ambigui o azioni respinte.

## Requisiti

- Home Assistant 2025.4.0 o successivo.
- Un agente Conversation configurato in Home Assistant.
- L'agente deve restituire JSON valido secondo le istruzioni incluse nel blueprint.

## Installazione

[![Apri Home Assistant e importa il blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fvince87%2Fha-ai-house-manager%2Fblob%2Fmain%2Fblueprints%2Fautomation%2Fvincenzo%2Fai_controllo_casa.yaml)

In alternativa, copia `blueprints/automation/vincenzo/ai_controllo_casa.yaml` nella stessa posizione della configurazione Home Assistant e ricarica i blueprint delle automazioni.

## Come scrivere gli ambiti

Racchiudi tra backtick esclusivamente friendly name o `entity_id`:

```text
Controlla `Antifurto Casa`, `Portoncino Casa` e il gruppo `Tapparelle`.
```

Scrivi stati, modalità e altri valori tra virgolette normali:

```text
Considera l'antifurto attivo negli stati "armed_away", "armed_home" e "armed_night".
```

Ogni friendly name deve corrispondere a una sola entità. I nomi assenti o duplicati vengono segnalati e non utilizzati.

## Prima esecuzione

1. Crea un'automazione dal blueprint.
2. Configura trigger, agente Conversation e ambiti.
3. Imposta `Solo simulazione`.
4. Controlla notifiche e traccia dell'automazione.
5. Passa all'esecuzione reale soltanto dopo aver verificato entità e azioni.

## Sicurezza

Il blueprint limita i servizi utilizzabili, valida i parametri, impedisce all'AI di inventare entità ed elimina le azioni già soddisfatte. Le regole definite negli ambiti restano comunque responsabilità dell'utente.

## Licenza

MIT
