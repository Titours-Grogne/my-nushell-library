# 🎉 **MY-NUSHELL-LIBRARY** 🎉

- [🎉 **MY-NUSHELL-LIBRARY** 🎉](#-my-nushell-library-)
  - [Objectifs 🚩](#objectifs-)
  - [Script de base `minimal.nu`](#script-de-base-minimalnu)
  - [Librairies](#librairies)
    - [`output-script.nu`](#output-scriptnu)
    - [`external-command.nu`](#external-commandnu)
    - [`get-settings.nu`](#get-settingsnu)

## Objectifs 🚩

- base d'exécution d'un script *Nushell*
- ensemble de « librairies » associé

## Script de base `minimal.nu`

Script de base pouvant s'adapter à deux modes de fonctionnenment :

- mode « développement » / usage local

  Le script d'exécution, son fichier de configuration et ses librairies sont localisés dans la même arborescence

  ```txt
  .
  ├── script-name.nu
  ├── nu_modules
  │  ├── module-<aaa>.nu
  │  ├── [...]
  │  └── module-<zzz>.nu
  └── settings.toml
  ```

- mode « production » / usage global

  Le script d'exécution, son fichier de configuration et ses librairies sont répartis dans l'arborescence `/usr/local`.  

  ```txt
  /usr/local
  ├── bin
  │  └── script-name.nu
  ├── etc
  │  └── script-name
  │     └── settings.toml
  └── lib
     └── script-name
        ├── module-<aaa>.nu
        ├── [...]
        └── module-<zzz>.nu
  ```

## Librairies

### `output-script.nu`

Librairie permettant de gérer l'affichage dans les scripts.

1. `__display-message`

    ```txt
    Generate a style log message to display and/or log
    
    Usage:
      > __display-message (level) (msg) 
    
    Flags:
      -h, --help: Display the help message for this command
    
    Parameters:
      level <string>: Message level : alert, debug, error, info, successful_script, successful_step (optional)
      msg <string>: Message to display (optional)
    
    Input/output types:
      ╭───┬───────┬────────╮
      │ # │ input │ output │
      ├───┼───────┼────────┤
      │ 0 │ any   │ any    │
      ╰───┴───────┴────────╯
    ```

1. `__line-separator`

    ```txt
    Generate a line separator

    Usage:
      > __line-separator (separator_character) 

    Flags:
      -h, --help: Display the help message for this command

    Parameters:
      separator_character <string>:  (optional, default: '-')

    Input/output types:
      ╭───┬───────┬────────╮
      │ # │ input │ output │
      ├───┼───────┼────────┤
      │ 0 │ any   │ any    │
      ╰───┴───────┴────────╯
    ```

### `external-command.nu`

Librairie permettant de l'exécution et le retour des commandes externes au shell *Nushell*.

```txt
External control of nu commands

Usage:
  > __external-command-control <external_command> (control_command) (shell) 

Flags:
  -h, --help: Display the help message for this command

Parameters:
  external_command <string>
  control_command <string>: Control option: continue (allows to continue script execution in case of error), debug or standard (optional, default: 'standard')
  shell <string>:  (optional, default: 'bash')

Input/output types:
  ╭───┬───────┬────────╮
  │ # │ input │ output │
  ├───┼───────┼────────┤
  │ 0 │ any   │ any    │
  ╰───┴───────┴────────╯
```

### `get-settings.nu`

Librairie permettant de charger une partie ou l'ensemble d'un fichier de configuration au format TOML.

```txt
Get parameters from a toml file

Usage:
  > __get-settings {flags} (table) 

Flags:
  --settings_file <path>: Configuration file in TOML format (default: '')
  -h, --help: Display the help message for this command

Parameters:
  table <string>: Extract collection of key/value pairs (optional)

Input/output types:
  ╭───┬───────┬────────╮
  │ # │ input │ output │
  ├───┼───────┼────────┤
  │ 0 │ any   │ any    │
  ╰───┴───────┴────────╯
```
